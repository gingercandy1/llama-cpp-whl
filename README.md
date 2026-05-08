I recently tested a model using Qwen 3.5, but found that my previous llama-cpp version didn't support the latest model, resulting in errors when running it. Therefore, I pulled the latest llama-cpp source code and rebuilt a whl file that supports the new model. Here's a record of the compilation steps:

### Compilation Steps

1. First, you need to install the CUDA installation package according to your version. The installation links are as follows:
  > Install CUDA 13.2
    https://developer.nvidia.com/cuda-13-2-0-download-archive

  > Install CUDA 12.8
    https://developer.nvidia.com/cuda-12-8-0-download-archive
  

2. Download UV and set the environment variables according to your system version:
  > Install uv https://github.com/astral-sh/uv/releases


3. Download and install Visual Studio The 2022 version can be downloaded from the following two links:
  > install visual studio https://learn.microsoft.com/en-us/visualstudio/releases/2022/release-history
  >  Community Edition: https://aka.ms/vs/17/release/vs_community.exe

4. Install CMake
  > Cmake download https://cmake.org/download/

5. Install Git
  > git download https://gitforwindows.org/

6. Download and compile the source code

```
# clone repository
git clone https://github.com/abetlen/llama-cpp-python.git

# Create a virtual environment
cd llama-cpp-python
uv venv build_env --python 3.12
build_env\Scripts\activate

# Install build dependencies
uv pip install --upgrade pip
uv pip install build wheel setuptools cmake scikit-build-core

# Start compiling
set CMAKE_ARGS=-DGGML_CUDA=ON -DCMAKE_CUDA_ARCHITECTURES="120" -DGGML_NATIVE=OFF -DGGML_CUDA_FA_ALL_QUANTS=ON -DCMAKE_BUILD_TYPE=Release
python -m build --wheel --no-isolation

```

7. Finally, you can find the compiled whl file in the dist directory.

### Usage Method 

* Download the corresponding CUDA whl file, which can be found in the Release directory.

```
pip install XXX.whl
```
