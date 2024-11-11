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

## License
This guide is open-source and available for personal or educational use.
