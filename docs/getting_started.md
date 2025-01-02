# Getting started

## Downloading and installing APCEMM

Currently the only way to acquire APCEMM is to download it from the APCEMM [GitHub repository](https://github.com/MIT-LAE/APCEMM).

### Dependencies 

These are all managed using the `vcpkg` tool (see below) so do not need to be installed explicitly.

- netcdf-c (requires HDF5 and zlib)
- netcdf-cxx4
- Catch2
- FFTW3
- OpenMP
- Boost libraries
- yaml-cpp
- Eigen3

### Installation instructions

APCEMM can be built using CMake and requires GCC >= 11.2. Previously, the dependency structure and compile instructions were specified using manually generated Makefiles. CMake generates these Makefiles automatically, and should lead to a more pleasant software build experience. Dependencies on external libraries are managed using the [vcpkg](https://vcpkg.io/en/) tool, which is installed as a Git submodule. (This means that you just need to run the `git submodule update` command below to set it up.)

CMake will generate a single executable `APCEMM` that can receive an input file `input.yaml`. To compile this executable, you can call CMake as follows:

```
git submodule update --init --recursive
mkdir build
cd build
cmake ../Code.v05-00
cmake --build .
```

The `git submodule update` command installs the `vcpkg` dependency management tool, and the first time that you run CMake, all of the C++ dependencies will be installed. This will take some time, but subsequent runs of CMake will use cached binary builds of the dependencies, so will be much quicker.

The above commands will generate the `APCEMM` executable in the `build` directory (an "out-of-source" build). It is also possible to perform a build directly in the `Code.v05-00` directory, but this is not preferred. You can perform an "out-of-source" build anywhere that it's convenient, simply by calling CMake from within a different directory. For example,
```
cd APCEMM/rundirs/SampleRunDir/
cmake ../../Code.v05-00
cmake --build .
```
will generate the executable in the `rundirs/SampleRunDir/` directory. 

## Running APCEMM

To start a run from the aforementioned `rundirs/SampleRunDir`, simply call:
```
./../../Code.v05-00 input.yaml
```
Three examples and their accompanying jupyter notebooks for postprocessing tutorials are provided in the `examples` folder. The first example is one where the contrail doesn't persists, and only focuses on analyzing the output of the early plume model (EPM) module of APCEMM. The second example is a persistent contrail simulation where the ice supersaturated layer depth is specified. The third example features using a meteorological input file.

The input file options are explained via comments in the file `rundirs/SampleRunDir/input.yaml`

Advanced simulation parameters hidden in the input files (e.g. Aerosol bin size ratios, minimum/max bin aerosol sizes, etc) can be modified in `Code.v05-00/src/include/Parameters.hpp`. 

## Debugging

APCEMM can be compiled in debug mode to ensure reproducible results during testing. This fixes the seed of the random number generator and enforces single threaded computation. It can be enabled by passing the ```-DDEBUG=ON``` flag to CMake:

```
cmake ../Code.v05-00 -DDEBUG=ON
```

To debug APCEMM using gdb and the VSCode debugger the binary can be compiled with debug instructions by adding the ```-DCMAKE_BUILD_TYPE="Debug"``` flag. This comes at a significant cost in performance.

 ```
cmake ../Code.v05-00 -DCMAKE_BUILD_TYPE="Debug"
 ```
 
 Here's an example configuration of the VSCode debugger in ```APCEMM/.vscode/launch.json```:

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch APCEMM debug",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/rundirs/debug/APCEMM",
            "cwd": "${workspaceFolder}/rundirs/debug/test_rundir/",
            "args": ["${workspaceFolder}/examples/issl_rhi140/input.yaml"],
            "environment": [
                {
                    "name": "LD_LIBRARY_PATH",
                    "value": "${workspaceFolder}/build/lib"
                },
            ],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        },
    ]
}
```

This configuration runs the APCEMM binary located in ```"${workspaceFolder}/rundirs/debug/``` using the input file located in ```${workspaceFolder}/examples/issl_rhi140/input.yaml``` and the working directory ``` ${workspaceFolder}/rundirs/debug/test_rundir/```. Paths can be changed to suit the case to debug.
