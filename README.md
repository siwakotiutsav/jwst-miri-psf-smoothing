# jwst-miri-psf-smoothing

This repository contains the code I developed to smooth MIRI line files and full spectral cubes using JWST simulated PSFs, rather than relying on a Gaussian kernel. The goal is to perform physically motivated PSF matching across wavelengths using the official JWST PSF models.

## Project Status
 
The **V2** version represents the final, stable implementation.

## Overview

This repository includes two main workflows:

---

## 1. PSF Smoothing for Line Files (CASA‑processed)

These line files are produced using CASA. If you want to run CASA from Python, see my companion repository:  
https://github.com/siwakotiutsav/casatools

Because the line files do not contain an error (`ERR`) header, this workflow is simpler.

### Key Features

- Computes the JWST PSF at the native pixel scale of the line file  
- Smooths the line file to the PSF corresponding to a longer wavelength  
- Regrids the data to the **MIRI Channel 3** footprint  
- Applies a mask to match the **Channel 1** footprint  

---

## 2. PSF Smoothing for Full Spectral Cubes

This workflow handles full MIRI cubes and includes full error propagation, which required substantial effort to implement correctly.

### Highlights

- Convolves both the **data** and the **ERR header** with the appropriate JWST PSF  
- Ensures correct variance propagation through convolution  
- Includes diagnostic print statements throughout the code (some commented out) to help with debugging and verification  

The error‑header propagation alone took about 10 days to get right — but it now works correctly.

---

## Notes

- The PSF estimation uses JWST simulated PSFs at the appropriate wavelengths and pixel scales  
- This method is more physically accurate than Gaussian smoothing and is recommended for scientific analyses requiring precise PSF matching  

---

## Citations

If you use or adapt this code, please cite the relevant JWST PSF papers.  
I would also appreciate a citation to:

**Siwakoti et al. 2026, in preparation**

---

## Acknowledgments

Thanks for checking out this repository! I hope it helps streamline your JWST MIRI data analysis.
