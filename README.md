[![Linux GCC](https://github.com/sintef-ocean/conan-fmilibrary/workflows/Linux%20GCC/badge.svg)](https://github.com/sintef-ocean/conan-fmilibrary/actions?query=workflow%3A"Linux+GCC")
[![Windows MSVC](https://github.com/sintef-ocean/conan-fmilibrary/workflows/Windows%20MSVC/badge.svg)](https://github.com/sintef-ocean/conan-fmilibrary/actions?query=workflow%3A"Windows+MSVC")

[Conan.io](https://conan.io) recipe for [fmi-library](https://github.com/modelon-community/fmi-library).

## How to use this package

1. Add remote to conan's package [remotes](https://docs.conan.io/2/reference/commands/remote.html)

   ```bash
   $ conan remote add sintef https://artifactory.smd.sintef.no/artifactory/api/conan/conan-local
   ```

2. Using [*conanfile.txt*](https://docs.conan.io/2/reference/conanfile_txt.html) and *cmake* in your project.

   Add *conanfile.txt*:
   ```
   [requires]
   fmilib/2.4.1@sintef/stable

   [options]
   fmilib:with_fmus=True

   [tool_requires]
   cmake/[>=3.25.0]

   [layout]
   cmake_layout

   [generators]
   CMakeDeps
   CMakeToolchain
   VirtualBuildEnv

   ```
   Insert into your *CMakeLists.txt* something like the following lines:
   ```cmake
   cmake_minimum_required(VERSION 3.15)
   project(TheProject CXX)

   find_package(fmilib REQUIRED)

   add_executable(the_executor code.cpp)
   target_link_libraries(the_executor fmilibrary::fmilibrary)
   ```
   Install and build e.g. a Release configuration (linux):
   ```bash
   $ conan install . -s build_type=Release -pr:b=default
   $ source build/Release/generators/conanbuild.sh
   $ cmake --preset conan-release
   $ cmake --build build/Release
   $ source build/Release/generators/deactivate_conanbuild.sh
   ```

## Package options

| Option    | Allowed values | Default |
|-----------|----------------|---------|
| shared    | [True, False]  | False   |
| fPIC      | [True, False]  | True    |
| with_fmus | [True, False]  | False   |

## Known recipe issues
