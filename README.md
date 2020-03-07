# dlib-19.5.0-cp37-wheel-for-win64

dlib-19.5.0 Python 3.7 wheel for Windows x64

## How to build

Tested Environment:

- Windows 10 x64
- Microsoft Visual Studio 2019 Community (MSVC-14.2)
- Python 3.7.0 64 bit

1. Install Boost 1.70.0. Prebuilt msvc-14.2 binaries are [here](https://sourceforge.net/projects/boost/files/boost-binaries/1.70.0/boost_1_70_0-unsupported-msvc-14.2-64.exe/download).

2. Install [cuDNN](https://developer.nvidia.com/rdp/cudnn-download).

3. Download [dlib-19.5.0](https://pypi.org/project/dlib/19.5.0/#files) from PyPI.

4. Patch `dist/dlib-19.5.0/dlib/cmake_utils/add_python_module` file.

   ```diff
   --- add_python_module   2020-03-08 00:57:32.544454900 +0900
   +++ add_python_module   2020-03-08 00:56:41.635194300 +0900
   @@ -63,6 +63,9 @@
            FIND_PACKAGE(Boost 1.41.0 COMPONENTS python-py35)
        endif()
        if (NOT Boost_FOUND)
   +        FIND_PACKAGE(Boost 1.41.0 COMPONENTS python37)
   +    endif()
   +    if (NOT Boost_FOUND)
            FIND_PACKAGE(Boost 1.41.0 COMPONENTS python3)
        endif()
        if (NOT Boost_FOUND)
   ```

   Add `python37` component

5. Build.

   ```bat
   " Set Boost, cuDNN directory to environment variable
   dlib-19.5.0> SET BOOST_ROOT=C:\local\boost_1_70_0
   dlib-19.5.0> SET BOOST_LIBRARYDIR=C:\local\boost_1_70_0\lib64-msvc-14.2
   dlib-19.5.0> SET CMAKE_PREFIX_PATH=C:\cudnn-10.2-windows10-x64-v7.6.5.32\cuda\

   " Install dependency
   dlib-19.5.0> pip install wheel

   " Build wheel
   dlib-19.5.0> python setup.py bdist_wheel
   ```
