# Algorithmic Unfolding for Image Reconstruction and Localization

Silvia Bonettini, Luca Calatroni, Danilo Pezzi, Marco Prato  
*Algorithmic Unfolding for Image Reconstruction and Localization Problems in Single-Molecule Fluorescence Microscopy*  
IMA Journal of Applied Mathematics, Volume 90, Issue 5, October 2025, Pages 465–487  
https://doi.org/10.1093/imamat/hxaf025

This repository contains the MATLAB implementation of the algorithm described in the paper above.

The code trains an **unfolded projected gradient descent algorithm** for the **super-resolution and deblurring of microscopy images**. Sample `main.m` files and configuration files are provided for the different datasets used in the paper, together with a simple **toy overfitting example on a single sample**.

---

# Code Overview

### Configuration

All parameters are defined in **JSON configuration files**.  
Two configuration files are used:

- one for the **unfolding model**
- one for the **outer optimization algorithm**

---

### Outer Optimization

The training procedure uses the **Scaled Gradient Projection (SGP)** method as the outer optimizer.

Different step sizes are used for different parameter blocks, in the following order:

1. `rho`
2. `delta`
3. `alpha`

---

### Loss Function and Unfolding

In the provided examples, right before the call to `SGP`, the function loss_norm1_bin_FISTApi is initialized.

This function:

- performs the unfolding procedure for all training samples
- computes the binarized reconstruction
- evaluates the loss function
- computes the gradient with respect to the parameters to be learned via **backpropagation**

---

### Regularization

The regularization term in the energy function can be modified directly in the `main.m` file.

The code requires a struct `reg` containing three function handles:

- `.f` — regularizer function  
- `.g` — gradient of the regularizer with respect to the image  
- `.hz` — function computing the **Hessian–vector product** for a given input vector

---

### Validation

After training, the `validation` function applies the learned unfolded scheme to the full image stack and computes the **Jaccard index** for the binarized reconstruction.

---

### Logging and Verbosity

To disable **on-screen printing**, set verbose=false in the SGP JSON configuration file.

To disable logging to the dedicated logfile, set logfile = [] in the main.m file

# Citation

If you use this code in your research, please cite:

@article{algorithm_unfolding_smlm,
	author = {Bonettini, Silvia and Calatroni, Luca and Pezzi, Danilo and Prato, Marco},
	doi = {10.1093/imamat/hxaf025},
	issn = {0272-4960},
	journal = {IMA Journal of Applied Mathematics},
	month = {01},
	number = {5},
	pages = {465-487},
	title = {Algorithmic unfolding for image reconstruction and localization problems in single-molecule fluorescence microscopy},
	volume = {90},
	year = {2026},
	bdsk-url-1 = {https://doi.org/10.1093/imamat/hxaf025}}