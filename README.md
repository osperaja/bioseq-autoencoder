# Autoencoder for Denoising *k*-mers in Genomic Sequences

This project implements a neural autoencoder to denoise genomic *k*-mers extracted from the _Escherichia coli K-12 MG1655_ genome.
The autoencoder learns to reconstruct clean *k*-mers from noisy input sequences, aiming to improve the quality of sequence data for downstream applications such as genome assembly by De-Bruijn graphs and variant detection.

## Key Features
- Downloads and parses _E. coli_ genome data from NCBI.
- Extracts *k*-mers and introduces synthetic salt-and-pepper-ish noise.
- Converts *k*-mers to one-hot encoded tensors.
- Defines and trains a neural autoencoder using PyTorch.
- Evaluates performance with Hamming distance.

## Usage
1. Install dependencies:
```bash
pip install torch torchvision scikit-learn biopython matplotlib
```

2. Run the provided script to:
   - Download genome data
   - Prepare noisy and clean *k*-mers
   - Train the autoencoder for several epochs
   - Observe training and validation metrics

## Notes
- Uses CUDA if available for acceleration (definitely should).
- You should check which CUDA version you'll need.
- .. good luck finding out what to do if you're using another GPU (probably _ROCm_ for AMD GPU and _oneAPI_ for Intel GPUs, both of which are not integrated in PyTorch's main API).
- Also you may need to get yourself some few additional RAM banks or explicitly decrease the `subset_fraction`, since the current `subset_fraction` yields an amount of *k*-mers of a little above _3.7e6_ (*(k=31) in nucleotides) -- 32GB DDR4/DDR5 should suffice for a clean runthrough of the *k*-mers construction. Of course you can try wiht 16GB RAM but expect some small level of storage degradation if you run this a few million times.
- Suitable for experimentation with sequence denoising techniques.
- .. and I just started writing this so i still have to figure out the right architecture tweaks.

## What's next?
- Incorporate _Escherichia coli K-12 MG1655_ variants, focusing heavily on subclonal and rare variants, to conclude the proof of concept.
- To explore broader applicability, extend the repository to more complex organisms that can inherit and maintain low-frequency variants — such as somatic mutations in multicellular eukaryotes.
- .. and add like 5 more RAM banks, because holy shit.

## Previous training progress
The plots below show the decrease in validation Hamming distance of the model trained using binary cross-entropy with logits loss.
The drop indicates the model learning to reconstruct the clean sequence from the corrupted input (by SNP-insertion).
Since this experiment used only the gold-standard _Escherichia coli K-12 MG1655_ reference genome, most of the improvement may be attributed to strong overlaps in *k*-mers between the training and validation sets.
