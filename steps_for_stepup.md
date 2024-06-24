
# Env step-up steps for training using autotrain-advanced (Huggingface)

To refine the instructions with the specified Python version (3.10.12), CUDA version (11.8), and to create a Conda environment in a local directory, follow these updated steps. These instructions will ensure you're setting up your development environment according to the specific requirements.

### 1. Install Miniconda or Anaconda (If Not Already Installed)

First, ensure you have either Miniconda or Anaconda installed. These tools manage your Conda environments and packages. If you haven't installed one of these, download and install from their respective websites.

### 2. Create a New Conda Environment

You'll start by creating a new Conda environment named `myenv` (you can choose any name you prefer) with Python 3.10.12. Here, we also specify the directory for the local environment with the `--prefix` option, replacing `/path/to/myenv` with your desired directory path:

```bash
conda create --prefix /path/to/myenv python=3.10.12 -y
```

Activate your newly created environment:

```bash
conda activate /path/to/myenv
```

### 3. Ensure Correct CUDA Version

Since you need CUDA 11.8, verify that your system has CUDA 11.8 installed by running `nvcc --version` or `nvidia-smi` in your terminal. The PyTorch installation step will ensure compatibility with CUDA 11.8.

### 4. Install libpq-dev

Before installing Python packages, ensure your system packages are up to date and install `libpq-dev`:

```bash
sudo apt-get update
sudo apt-get install --reinstall libpq-dev -y
```

### 5. Install psycopg2 and Related Packages

Within your activated Conda environment, install `psycopg2`, `psycopg2-binary`, and `sentencepiece`:

```bash
pip install psycopg2 psycopg2-binary sentencepiece
```

### 6. Install HDBSCAN

Still within the environment, install `hdbscan` using Conda from the `conda-forge` channel:

```bash
conda install -c conda-forge hdbscan -y
```

### 7. Install PyTorch, torchvision, and torchaudio with CUDA Support

To install PyTorch and its related libraries with support for CUDA 11.8, use the following command. This ensures that your PyTorch installation will utilize the specified CUDA version for GPU acceleration:

```bash
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia -y
```

### 8. Install autotrain-advanced

Finally, install `autotrain-advanced`. Make sure this package name is correct and available in your Python package repository:

```bash
pip install autotrain-advanced
```

### Post-Installation Checks

After installation, you can verify the successful setup by checking the versions of the installed packages and running simple tests to ensure everything is working as expected.

### Tips

- Always activate your Conda environment before installing new packages or running your projects.
- Use `conda list` and `pip list` to check installed packages in your environment.
- Regularly update your Conda and packages to keep them in sync with the latest versions and security patches.

These steps will help you set up a local development environment tailored to your specific requirements for Python, CUDA, and the necessary libraries.