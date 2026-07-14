# ChronoProject_FinalGA

Genetic Algorithm project for structural optimization built with [Project Chrono](https://projectchrono.org/).

The executable target is `ChronoProject_FinalGA`. The application currently runs the genetic algorithm using the custom first individual path in `src/Main.cpp`, then displays the results with Chrono/Irrlicht.

## Prerequisites

Install or build Project Chrono before configuring this project. Chrono must be configured with the same optional modules used by `CMakeLists.txt`:

- `Irrlicht`
- `Postprocess`
- `Eigen` support

You also need:

- CMake 3.10 or newer
- A C++17-compatible compiler
- Irrlicht available to the Chrono build
- Eigen available to the Chrono build
- Visual Studio on Windows, or another supported CMake generator on macOS/Linux

When configuring this project, `Chrono_DIR` must point to the Chrono CMake package directory from a Chrono build or install that includes the required modules. Typical values look like:

- Windows build tree: `C:/path/to/chrono-build/cmake`
- Windows install tree: `C:/path/to/chrono-install/lib/cmake/Chrono`
- macOS/Linux install tree: `/path/to/chrono-install/lib/cmake/Chrono`

## Build From The Command Line

From the repository root:

```sh
cmake -S . -B build -DChrono_DIR=/path/to/chrono-build-or-install/cmake
cmake --build build --config Release
```

For multi-configuration generators such as Visual Studio, the executable is generated under `build/Release/`. For single-configuration generators such as Ninja or Unix Makefiles, it is generated under `build/`.

On macOS, also pass `CHRONO_LIB_PATH` so the post-build step can copy Chrono dynamic libraries next to the application:

```sh
cmake -S . -B build \
  -DChrono_DIR=/path/to/chrono-install/lib/cmake/Chrono \
  -DCHRONO_LIB_PATH=/path/to/chrono-install/lib
cmake --build build --config Release
```

## Build With CMake GUI

1. Open CMake GUI.
2. Set "Where is the source code" to this repository folder.
3. Set "Where to build the binaries" to a `build` folder inside this repository.
4. Click "Configure".
5. If CMake cannot find Chrono, set `Chrono_DIR` to the Chrono CMake package directory.
6. On macOS, set `CHRONO_LIB_PATH` to the directory containing the Chrono `.dylib` files.
7. Click "Configure" again, then "Generate".
8. Open the generated project or solution and build `ChronoProject_FinalGA`.

On Windows with Visual Studio, set `ChronoProject_FinalGA` as the startup project before running. The CMake script copies the Chrono and Irrlicht DLLs from the Chrono build or install path into the matching `Debug` or `Release` output folder when possible.

## Run

After building, run the generated executable:

```sh
./build/ChronoProject_FinalGA
```

For Visual Studio Release builds on Windows:

```bat
build\Release\ChronoProject_FinalGA.exe
```

For macOS app bundle builds, run the executable inside the generated bundle:

```sh
./build/ChronoProject_FinalGA.app/Contents/MacOS/ChronoProject_FinalGA
```

If the application cannot find Chrono or Irrlicht dynamic libraries at runtime, make sure the required DLLs, `.dylib` files, or shared libraries are available next to the executable or in your platform's library search path.

## Configuration Files

Example genetic algorithm input files are stored in:

- `configuration/example/`
- `configuration/real_bridge/`

The active run mode is selected in `src/Main.cpp`. By default, it calls:

```cpp
GeneticAlgorithmService::RunWithCustomFirstIndividual();
GeneticAlgorithmService::ShowResults();
```

Switch to `GeneticAlgorithmService::RunWithConfigValues();` in `src/Main.cpp` if you want to run from configuration values only.
