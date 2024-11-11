# Setting Up TensorFlow with GPU Support on MacBook Air M1

This guide provides step-by-step instructions to install TensorFlow with GPU support on a MacBook Air M1, leveraging Apple’s Metal API for hardware acceleration.

## Prerequisites

- **macOS**: macOS 11.0 or later
- **Python**: Use Miniforge (recommended) to manage Python environments on M1 chips.

## Installation Steps

### 1. Install Miniforge
Miniforge is a conda-based package manager optimized for ARM architecture on M1 Macs.

- Open Terminal and download the Miniforge installer:

  ```bash
  /bin/bash -c "$(curl -fsSL https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh)"
  ```

- Follow the on-screen prompts to complete the installation.
- Restart your terminal to apply the changes.

### 2. Set Up a Conda Environment with Python 3.9
It’s recommended to use Python 3.9 for compatibility.

```bash
conda create -n tf_m1 python=3.9
conda activate tf_m1
```

### 3. Install TensorFlow Dependencies
Install the TensorFlow dependencies from the `apple` channel for optimal support on M1 hardware.

```bash
conda install -c apple tensorflow-deps
```

### 4. Install TensorFlow and TensorFlow-Metal
These packages enable TensorFlow to use Apple’s Metal API for GPU acceleration.

```bash
pip install tensorflow-macos
pip install tensorflow-metal
```

### 5. Verify Installation
To ensure TensorFlow is installed correctly with GPU support, open Python and run the following commands:

```python
import tensorflow as tf
print("TensorFlow version:", tf.__version__)
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))
```

If everything is set up correctly, you should see TensorFlow’s version number and a message indicating one GPU is available.

### 6. Test with a Sample Model
To confirm the setup, you can load a sample model (e.g., VGG16) and check if it runs without errors:

```python
from tensorflow.keras.applications import VGG16

# Load the VGG16 model
model = VGG16(weights="imagenet")
print("Model loaded successfully!")
```

## Notes
- The MacBook Air M1 has passive cooling, so prolonged tasks may cause throttling. For large models or datasets, consider using batch processing.
- This setup allows you to leverage GPU acceleration with TensorFlow on Apple Silicon for faster deep learning workflows.

## Troubleshooting
- If `conda` is not found, ensure that Miniforge is installed correctly and that your terminal is restarted.
- If the Metal API is not detected, double-check the versions of `tensorflow-macos` and `tensorflow-metal`.


========================================================================================================================================================
To use Python with Jupyter on your MacBook Air M1, let’s go through the steps to install Jupyter Notebook and set it up with your TensorFlow environment.

### 1. Install Jupyter Notebook in Your TensorFlow Environment

1. First, make sure you activate your TensorFlow environment:

   ```bash
   conda activate tf_m1
   ```

2. Then, install Jupyter Notebook:

   ```bash
   conda install -c conda-forge jupyter
   ```

### 2. Launch Jupyter Notebook

- Once installed, you can start Jupyter Notebook by running:

  ```bash
  jupyter notebook
  ```

- This command will open Jupyter in your default web browser.

### 3. Create a Notebook Using the TensorFlow Environment

- In Jupyter, you should see an option to select the kernel (Python environment) when you create a new notebook.
- If your `tf_m1` environment doesn’t appear, follow the steps below to register it.

### 4. (Optional) Register Your Conda Environment as a Kernel in Jupyter

If `tf_m1` doesn’t appear as a kernel option in Jupyter, you can add it manually:

1. First, install the `ipykernel` package in the `tf_m1` environment:

   ```bash
   conda activate tf_m1
   pip install ipykernel
   ```

2. Add the environment to Jupyter:

   ```bash
   python -m ipykernel install --user --name=tf_m1 --display-name "Python (tf_m1)"
   ```

- Now, when you open Jupyter Notebook, you should see **Python (tf_m1)** as an available kernel.

### 5. Verify TensorFlow in Jupyter

To confirm everything works, open a new notebook in Jupyter and run:

```python
import tensorflow as tf
print("TensorFlow version:", tf.__version__)
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))
```

## License
This guide is open-source and available for personal or educational use.
