# MeddySuperproject

The superproject for all Meddy repositories as well as their third-party dependencies.

Key benefits of this project structure I designed:
- Fulfills any CMake use case (namely, installation and local build use cases).
- Keeps dependencies isolated and accessible via `find_package` along with FetchContent or ExternalProject.
- Wrote automated tests with CTest, distributed products with CPack, and wrote reusable CMakePresets.

## Project Structure 📂

Meddy repositories
- [MeddyCLI](https://github.com/ChristianHinkle/MeddyCLI) (executable)
- [MeddySDK](https://github.com/ChristianHinkle/MeddySDK)
    - [MeddySDK_Meddyproject](https://github.com/ChristianHinkle/MeddySDK_Meddyproject) (library)
    - [MeddySDK_Meddydata](https://github.com/ChristianHinkle/MeddySDK_Meddydata) (library)
    - [MeddySDK_DAM](https://github.com/ChristianHinkle/MeddySDK_DAM) (library)

Third-party repositories
- [CppUtils](https://github.com/ChristianHinkle/CppUtils)
    - Written by us. This is where we write our general C++ utilities.
    - [CppUtils_Core](https://github.com/ChristianHinkle/CppUtils_Core) (library)
    - [CppUtils_Misc](https://github.com/ChristianHinkle/CppUtils_Misc) (library)
    - [CppUtils_StdReimpl](https://github.com/ChristianHinkle/CppUtils_StdReimpl) (library)
    - Etc.
- [The Boost C++ Libraries](https://github.com/boostorg/boost)
    - A popular open source repository that provides many C++ libraries.
- [RapidJSON](https://github.com/Tencent/rapidjson)
    - A popular json serializer library known for being fast and memory efficient, often used in games.

These projects are built together using `FetchContent` in CMake. This means they configure together (all from the same invocation of CMake), which makes debugging and development easier with the subprojects.

There is also a "superbuild" version of this project structure which uses `ExternalProject` in CMake to configure each project in isolation, before they get built together. See: [MeddySuperbuild](https://github.com/ChristianHinkle/MeddySuperbuild).

## Build System ⌨

Built with CMake - cross-platform, standardized, and IDE-friendly.

We provide CMake presets, which handle feeding arguments to CMake for you.

### IDE Support

Most IDEs provide built-in CMake integration.

#### VS Code

Has the "CMake Tools" and "C/C++" extensions, both developed by Microsoft.

#### Visual Studio

Has very nice integration, but they seem behind when it comes to supporting the latest CMake features. I've had experiences where I have to switch to VS Code because of this.

## Build Instructions 🔨

### 1. Invoke CMake on the Project (the Configure Step)

Command line: `cmake --preset="win-debug-default"`.

IDE: Choose the `win-debug-default` configure preset, and "configure" the CMake project.

### 2. Invoke a Build Command

Command line: `cmake --build --preset="win-debug"`.

IDE: Choose the `win-debug` build preset, and "build" it.

## Package Instructions 📦

Here's how to package the build into a distributable product.

### 1. Build the Project

See "Build Instructions" above.

### 2. Invoke CPack

Command line: `cpack --preset="meddycli-win-debug-nsis"`.

IDE: Choose the `meddycli-win-debug-nsis` package preset, and "package" it.

## Test Instructions 🧪

Here's how to run automated tests, to verify that our code behaves as intended.

### 1. Build the Project

See "Build Instructions" above.

### 2. Invoke CTest

Command line: `ctest --preset="meddysdk-win-debug"`.

IDE: Choose the `meddysdk-win-debug` test preset, and "run tests".
