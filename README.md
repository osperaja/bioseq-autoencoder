# Autoencoder for Denoising *k*-mers in Genomic Sequences

This project implements a neural autoencoder to denoise genomic *k*-mers extracted from the _Escherichia coli K-12_ genome.
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
- .. good luck finding out what to do if you're using an AMD GPU (probably ROCm).
- Also you may need to get yourself some few additional RAM banks or explicitly decrease the `subset_fraction`, since the current `subset_fraction` yields an amount of *k*-mers equal to 
- Suitable for experimentation with sequence denoising techniques.
- .. and I just started writing this so i still have to figure out the right architecture tweaks.
