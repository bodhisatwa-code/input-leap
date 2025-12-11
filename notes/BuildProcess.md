# Input Leap Build Process

This document describes how to build Input Leap from source on various platforms.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Build System Overview](#build-system-overview)
3. [CMake Configuration Options](#cmake-configuration-options)
4. [Building on Linux](#building-on-linux)
5. [Building on macOS](#building-on-macos)
6. [Building on Windows](#building-on-windows)
7. [Building on FreeBSD](#building-on-freebsd)
8. [Build Targets](#build-targets)
9. [Running Tests](#running-tests)
10. [Creating Packages](#creating-packages)

---

## Prerequisites

### All Platforms

- **CMake 3.21+** - Build system generator
- **C++ Compiler** - C++14 (Qt5) or C++17 (Qt6) support required
- **Git** - For cloning and submodule management
- **OpenSSL 1.1.1+** - SSL/TLS support

### Compiler Requirements

| Platform | Compiler |
|----------|----------|
| Linux | GCC 7+ or Clang 6+ |
| macOS | Xcode Command Line Tools |
| Windows | Visual Studio 2019 or 2022 |
| FreeBSD | Clang (system) |

---

## Build System Overview

Input Leap uses CMake as its build system generator. The build process follows these steps:

```
1. Clone repository with submodules
        |
        v
2. Install platform dependencies
        |
        v
3. Configure with CMake (generate build files)
        |
        v
4. Build using native build tool (make/ninja/VS/Xcode)
        |
        v
5. (Optional) Run tests
        |
        v
6. (Optional) Install or package
```

### Directory Structure After Build

```
build/
├── bin/                  # Executables
│   ├── input-leap        # GUI application
│   ├── input-leapc       # Client CLI
│   └── input-leaps       # Server CLI
├── lib/                  # Static libraries
├── bundle/               # macOS app bundle (macOS only)
├── installer-inno/       # Inno Setup files (Windows)
├── installer-wix/        # WiX installer files (Windows)
└── rpm/                  # RPM spec files (Linux)
```

---

## CMake Configuration Options

### Core Options

| Option | Default | Description |
|--------|---------|-------------|
| `CMAKE_BUILD_TYPE` | - | Build type: `Debug`, `Release`, `RelWithDebInfo` |
| `CMAKE_INSTALL_PREFIX` | system default | Installation directory |
| `INPUTLEAP_BUILD_GUI` | ON | Build the Qt GUI application |
| `INPUTLEAP_BUILD_TESTS` | ON | Build the test suite |
| `QT_DEFAULT_MAJOR_VERSION` | 6 | Qt major version (5 or 6) |

### Platform Options (Linux)

| Option | Default | Description |
|--------|---------|-------------|
| `INPUTLEAP_BUILD_X11` | ON | Build with X11 support |
| `INPUTLEAP_BUILD_LIBEI` | OFF | Build with libei/Wayland support |

### Advanced Options

| Option | Default | Description |
|--------|---------|-------------|
| `INPUTLEAP_USE_EXTERNAL_GTEST` | OFF | Use system-installed Google Test |
| `INPUTLEAP_BUILD_GULRAK_FILESYSTEM` | OFF | Use bundled filesystem library |
| `CMAKE_UNITY_BUILD` | - | Enable unity (jumbo) builds for faster compilation |

### Example Configuration Commands

```bash
# Debug build with default options
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug

# Release build with Qt5
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DQT_DEFAULT_MAJOR_VERSION=5

# Build with Wayland support (Linux)
cmake -S . -B build -DINPUTLEAP_BUILD_LIBEI=ON

# Build without GUI
cmake -S . -B build -DINPUTLEAP_BUILD_GUI=OFF

# Build without tests
cmake -S . -B build -DINPUTLEAP_BUILD_TESTS=OFF

# Fast unity build with Ninja
cmake -S . -B build -G Ninja -DCMAKE_UNITY_BUILD=1
```

---

## Building on Linux

### Ubuntu/Debian Dependencies

```bash
# Core build tools
sudo apt install cmake g++ git ninja-build

# Required libraries
sudo apt install \
    libssl-dev \
    libavahi-compat-libdnssd-dev \
    libice-dev \
    libsm-dev \
    libxinerama-dev \
    libxrandr-dev \
    libxtst-dev \
    libxkbcommon-dev \
    libglib2.0-dev

# Qt 6 (recommended for Ubuntu 22.04+)
sudo apt install \
    qt6-base-dev \
    qt6-tools-dev \
    qt6-tools-dev-tools \
    qt6-l10n-tools

# OR Qt 5 (for older systems)
sudo apt install \
    qtdeclarative5-dev \
    qttools5-dev

# For testing
sudo apt install \
    libgtest-dev \
    libgmock-dev

# For Wayland/libei support (Ubuntu 24.04+)
sudo apt install \
    libei-dev \
    libportal-dev
```

### Fedora Dependencies

```bash
sudo dnf install \
    cmake \
    gcc-c++ \
    git \
    ninja-build \
    openssl-devel \
    avahi-compat-libdns_sd-devel \
    libICE-devel \
    libSM-devel \
    libXinerama-devel \
    libXrandr-devel \
    libXtst-devel \
    libxkbcommon-devel \
    glib2-devel \
    qt6-qtbase-devel \
    qt6-qttools-devel \
    gtest-devel \
    gmock-devel
```

### openSUSE Dependencies

```bash
sudo zypper install \
    cmake \
    gcc-c++ \
    git \
    ninja \
    libopenssl-devel \
    avahi-compat-mDNSResponder-devel \
    libICE-devel \
    libSM-devel \
    libXinerama-devel \
    libXrandr-devel \
    libXtst-devel \
    libxkbcommon-devel \
    glib2-devel \
    qt6-base-devel \
    qt6-tools-devel \
    gtest
```

### Linux Build Steps

```bash
# Clone with submodules
git clone --recurse-submodules https://github.com/input-leap/input-leap.git
cd input-leap

# Create build directory
mkdir build && cd build

# Configure (Qt6, Release)
cmake -DCMAKE_BUILD_TYPE=Release \
      -DQT_DEFAULT_MAJOR_VERSION=6 \
      ..

# Build (use -j for parallel jobs)
cmake --build . --parallel

# Run tests (optional)
ctest --verbose

# Install (optional)
sudo cmake --install .
```

### Using Ninja (Faster Builds)

```bash
cmake -G Ninja -DCMAKE_BUILD_TYPE=Release ..
ninja
```

---

## Building on macOS

### Dependencies

```bash
# Install Xcode Command Line Tools
xcode-select --install

# Install Homebrew packages
brew install cmake ninja qt@6
```

### macOS Build Steps

```bash
# Clone with submodules
git clone --recurse-submodules https://github.com/input-leap/input-leap.git
cd input-leap

# Create build directory
mkdir build && cd build

# Configure
cmake -G Ninja \
      -DCMAKE_BUILD_TYPE=Release \
      -DQT_DEFAULT_MAJOR_VERSION=6 \
      -DCMAKE_OSX_DEPLOYMENT_TARGET=11 \
      ..

# Build
ninja

# The app bundle is created at: build/bundle/InputLeap.app
```

### Building Universal Binary (Apple Silicon + Intel)

```bash
cmake -G Ninja \
      -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_OSX_ARCHITECTURES="arm64;x86_64" \
      -DCMAKE_OSX_DEPLOYMENT_TARGET=11 \
      ..
```

### Building for Older macOS

For Qt5 and older macOS support:

```bash
brew install qt@5

cmake -G Ninja \
      -DCMAKE_BUILD_TYPE=Release \
      -DQT_DEFAULT_MAJOR_VERSION=5 \
      -DCMAKE_OSX_DEPLOYMENT_TARGET=10.9 \
      -DINPUTLEAP_BUILD_GULRAK_FILESYSTEM=ON \
      ..
```

---

## Building on Windows

### Prerequisites

1. **Visual Studio 2019 or 2022** with C++ workload
2. **CMake 3.21+** (can use VS integrated CMake)
3. **Qt 5.15+ or 6.2+** ([download](https://www.qt.io/download-qt-installer))
4. **Bonjour SDK** or compatible ([mDNSResponder](https://github.com/nicemicro/mDNSResponder))
5. **OpenSSL** (static build recommended)

### Environment Setup

Set environment variables:

```cmd
set Qt6_DIR=C:\Qt\6.6.0\msvc2022_64
set BONJOUR_SDK_HOME=C:\path\to\bonjour\sdk
set OPENSSL_ROOT_DIR=C:\path\to\openssl
```

### Windows Build Steps

```cmd
:: Clone repository
git clone --recurse-submodules https://github.com/input-leap/input-leap.git
cd input-leap

:: Create build directory
mkdir build
cd build

:: Configure (Visual Studio 2022, 64-bit)
cmake -G "Visual Studio 17 2022" -A x64 ^
      -DCMAKE_BUILD_TYPE=Release ^
      -DQT_DEFAULT_MAJOR_VERSION=6 ^
      ..

:: Build
cmake --build . --config Release --parallel

:: Or open in Visual Studio
start InputLeap.sln
```

### Using Qt5 on Windows

```cmd
set Qt5_DIR=C:\Qt\5.15.2\msvc2019_64
cmake -G "Visual Studio 16 2019" -A x64 ^
      -DQT_DEFAULT_MAJOR_VERSION=5 ^
      -DINPUTLEAP_BUILD_GULRAK_FILESYSTEM=ON ^
      ..
```

---

## Building on FreeBSD

### Dependencies

```bash
sudo pkg install \
    cmake \
    pkgconf \
    git \
    avahi-libdns \
    libsm \
    libxinerama \
    libxrandr \
    libxtst \
    libxkbcommon \
    glib \
    ninja \
    qt6-base \
    qt6-tools \
    qt6-declarative
```

### FreeBSD Build Steps

```bash
git clone --recurse-submodules https://github.com/input-leap/input-leap.git
cd input-leap
mkdir build && cd build

cmake -G Ninja \
      -DCMAKE_BUILD_TYPE=Release \
      -DQT_DEFAULT_MAJOR_VERSION=6 \
      ..

ninja
```

---

## Build Targets

### Main Executables

| Target | Description |
|--------|-------------|
| `input-leap` | GUI application |
| `input-leaps` | Server CLI |
| `input-leapc` | Client CLI |
| `input-leapd` | Windows daemon (Windows only) |

### Test Targets

| Target | Description |
|--------|-------------|
| `unittests` | Unit test executable |
| `integtests` | Integration test executable |
| `guiunittests` | GUI unit tests |

### Build Specific Target

```bash
# Build only the server
cmake --build . --target input-leaps

# Build only the client
cmake --build . --target input-leapc

# Build only the GUI
cmake --build . --target input-leap
```

---

## Running Tests

### Using CTest

```bash
# Run all tests
ctest --test-dir build --verbose

# Run specific test
ctest --test-dir build -R unittests --verbose

# Run with output on failure
ctest --test-dir build --output-on-failure
```

### Running Test Executables Directly

```bash
# Unit tests
./build/bin/unittests

# Integration tests
./build/bin/integtests

# GUI tests
./build/bin/guiunittests
```

---

## Creating Packages

### Linux - Debian Package

```bash
cd input-leap
cp -r dist/debian debian

# Modify debian/rules if needed (Qt version, libei, etc.)

debuild -us -uc
# Package created in parent directory
```

### Linux - RPM Package

```bash
cmake -S . -B build -DINPUTLEAP_USE_EXTERNAL_GTEST=True
cmake --build build --target package_source

rpmbuild -D "_sourcedir $PWD/build" \
         -D "_rpmdir $PWD/rpms" \
         -bb build/rpm/input-leap.spec
```

### Linux - Flatpak

```bash
flatpak-builder --force-clean build-flatpak dist/flatpak/io.github.input_leap.input-leap.yaml
```

### macOS - DMG Installer

The DMG is automatically created as part of the macOS build:

```bash
cmake --build build
# DMG created at: build/bundle/InputLeap-X.Y.Z.dmg
```

### Windows - Inno Setup Installer

```cmd
cmake --build build --config Release

:: Run Inno Setup compiler
"%ProgramFiles(x86)%\Inno Setup 6\ISCC.exe" /Qp build\installer-inno\input-leap.iss
:: Installer created in build\installer-inno\bin\
```

### Windows - WiX Installer

```cmd
cmake --build build --config Release
cd build\installer-wix
candle input-leap.wxs
light input-leap.wixobj
```

---

## Troubleshooting

### CMake Version Too Old

On older systems (e.g., Ubuntu 20.04), install CMake from Kitware:

```bash
wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc | sudo gpg --dearmor -o /usr/share/keyrings/kitware-archive-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ focal main' | sudo tee /etc/apt/sources.list.d/kitware.list
sudo apt update && sudo apt install cmake
```

### Qt Not Found

Ensure Qt is in your PATH or set the appropriate CMake variable:

```bash
# Linux
export PATH="/path/to/qt/bin:$PATH"

# Or use CMake variable
cmake -DQt6_DIR=/path/to/qt/lib/cmake/Qt6 ..
```

### OpenSSL Not Found

```bash
# Linux
sudo apt install libssl-dev

# macOS
brew install openssl
cmake -DOpenSSL_ROOT=/usr/local/opt/openssl ..

# Windows
cmake -DOPENSSL_ROOT_DIR=C:/path/to/openssl ..
```

### Submodules Not Initialized

```bash
git submodule update --init --recursive
```

### Unity Build Failures

If unity builds fail, try disabling:

```bash
cmake -DCMAKE_UNITY_BUILD=OFF ..
```

---

## CI/CD Reference

The project uses GitHub Actions for continuous integration. See `.github/workflows/builds.yml` for the complete CI configuration including:

- Ubuntu 20.04, 22.04, 24.04
- Debian 12
- Fedora 40
- openSUSE Tumbleweed
- macOS (x86_64, Apple Silicon, Universal)
- Windows (VS2019, VS2022)
- FreeBSD 14.1
- Flatpak

This can serve as a reference for build commands and dependency installation on each platform.
