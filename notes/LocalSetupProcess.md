# Input Leap Local Development Setup

This guide covers setting up a local development environment for contributing to Input Leap.

---

## Table of Contents

1. [Development Environment Setup](#development-environment-setup)
2. [IDE Configuration](#ide-configuration)
3. [Development Workflow](#development-workflow)
4. [Debugging](#debugging)
5. [Testing](#testing)
6. [Code Style and Guidelines](#code-style-and-guidelines)
7. [Contributing](#contributing)
8. [Common Development Tasks](#common-development-tasks)

---

## Development Environment Setup

### Step 1: Fork and Clone

```bash
# Fork the repository on GitHub first, then:
git clone --recurse-submodules https://github.com/YOUR_USERNAME/input-leap.git
cd input-leap

# Add upstream remote
git remote add upstream https://github.com/input-leap/input-leap.git
```

### Step 2: Install Dependencies

#### Linux (Ubuntu/Debian)

```bash
# Development tools
sudo apt install \
    cmake \
    g++ \
    clang \
    git \
    ninja-build \
    gdb \
    valgrind

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
    libglib2.0-dev \
    libgl-dev

# Qt 6 development
sudo apt install \
    qt6-base-dev \
    qt6-tools-dev \
    qt6-tools-dev-tools \
    qt6-l10n-tools

# Testing frameworks
sudo apt install \
    libgtest-dev \
    libgmock-dev

# Optional: Wayland/libei (Ubuntu 24.04+)
sudo apt install \
    libei-dev \
    libportal-dev

# Optional: Documentation tools
sudo apt install \
    doxygen \
    graphviz
```

#### Linux (Fedora)

```bash
sudo dnf install \
    cmake \
    gcc-c++ \
    clang \
    git \
    ninja-build \
    gdb \
    valgrind \
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

#### macOS

```bash
# Install Xcode Command Line Tools
xcode-select --install

# Install Homebrew packages
brew install \
    cmake \
    ninja \
    qt@6 \
    openssl \
    llvm  # for clang-format, clang-tidy
```

#### Windows

1. Install **Visual Studio 2022** with:
   - "Desktop development with C++" workload
   - CMake tools for Windows
   - Git for Windows

2. Install **Qt 6** from [qt.io](https://www.qt.io/download-qt-installer)

3. Download **Bonjour SDK** compatible library:
   - [mDNSResponder releases](https://github.com/nelsonjchen/mDNSResponder/releases)

4. Install **OpenSSL**:
   - [Shining Light Productions](https://slproweb.com/products/Win32OpenSSL.html) (recommended)

### Step 3: Configure Build for Development

```bash
# Create debug build directory
mkdir build-debug && cd build-debug

# Configure with debug symbols and all features
cmake -G Ninja \
    -DCMAKE_BUILD_TYPE=Debug \
    -DCMAKE_EXPORT_COMPILE_COMMANDS=ON \
    -DINPUTLEAP_BUILD_TESTS=ON \
    -DQT_DEFAULT_MAJOR_VERSION=6 \
    ..

# Build
ninja

# Verify build
./bin/input-leaps --version
./bin/input-leapc --version
```

### Step 4: Verify Setup

```bash
# Run unit tests
ctest --verbose

# Run a quick sanity check
./bin/input-leaps --help
./bin/input-leapc --help
```

---

## IDE Configuration

### Visual Studio Code

#### Recommended Extensions

- **C/C++** (Microsoft)
- **CMake** (twxs)
- **CMake Tools** (Microsoft)
- **clangd** (LLVM) - Alternative to Microsoft C++ IntelliSense

#### `.vscode/settings.json`

```json
{
    "cmake.buildDirectory": "${workspaceFolder}/build-debug",
    "cmake.configureArgs": [
        "-DCMAKE_BUILD_TYPE=Debug",
        "-DCMAKE_EXPORT_COMPILE_COMMANDS=ON",
        "-DINPUTLEAP_BUILD_TESTS=ON"
    ],
    "cmake.generator": "Ninja",
    "C_Cpp.default.configurationProvider": "ms-vscode.cmake-tools",
    "files.associations": {
        "*.h": "cpp",
        "*.cpp": "cpp"
    },
    "editor.formatOnSave": false,
    "clangd.arguments": [
        "--compile-commands-dir=${workspaceFolder}/build-debug"
    ]
}
```

#### `.vscode/launch.json` (Linux)

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug Server",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build-debug/bin/input-leaps",
            "args": ["-f", "--debug", "DEBUG", "-c", "/path/to/config.conf"],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb"
        },
        {
            "name": "Debug Client",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build-debug/bin/input-leapc",
            "args": ["-f", "--debug", "DEBUG", "server-hostname"],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb"
        },
        {
            "name": "Debug GUI",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build-debug/bin/input-leap",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb"
        },
        {
            "name": "Debug Unit Tests",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build-debug/bin/unittests",
            "args": ["--gtest_filter=*"],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb"
        }
    ]
}
```

### CLion

1. Open the project folder (CLion auto-detects CMakeLists.txt)
2. Configure CMake profiles in **Settings > Build, Execution, Deployment > CMake**:
   - **Debug**: `-DCMAKE_BUILD_TYPE=Debug -DINPUTLEAP_BUILD_TESTS=ON`
   - **Release**: `-DCMAKE_BUILD_TYPE=Release`
3. Set the generator to **Ninja** for faster builds

### Qt Creator

1. **File > Open File or Project** and select `CMakeLists.txt`
2. Select kit (ensure Qt 6 is available)
3. Configure CMake arguments in **Projects > Build Settings**
4. Enable **compile_commands.json** for code completion

### Visual Studio (Windows)

1. **File > Open > CMake** and select the root `CMakeLists.txt`
2. Configure CMake settings via **CMakeSettings.json**:

```json
{
    "configurations": [
        {
            "name": "x64-Debug",
            "generator": "Ninja",
            "configurationType": "Debug",
            "buildRoot": "${projectDir}\\build-debug",
            "installRoot": "${projectDir}\\install",
            "cmakeCommandArgs": "-DINPUTLEAP_BUILD_TESTS=ON -DQT_DEFAULT_MAJOR_VERSION=6",
            "buildCommandArgs": "",
            "ctestCommandArgs": "",
            "inheritEnvironments": ["msvc_x64_x64"]
        }
    ]
}
```

---

## Development Workflow

### Branch Strategy

```bash
# Sync with upstream
git fetch upstream
git checkout master
git merge upstream/master

# Create feature branch
git checkout -b feature/my-feature

# Work on feature...
git add .
git commit -m "Add feature X"

# Push and create PR
git push origin feature/my-feature
```

### Incremental Builds

```bash
# Rebuild only changed files
ninja

# Rebuild specific target
ninja input-leaps

# Clean build
ninja clean

# Full rebuild
rm -rf build-debug && mkdir build-debug && cd build-debug
cmake -G Ninja -DCMAKE_BUILD_TYPE=Debug .. && ninja
```

### Running During Development

```bash
# Run server in foreground with debug logging
./bin/input-leaps -f --debug DEBUG -c /path/to/config.conf

# Run client in foreground with debug logging
./bin/input-leapc -f --debug DEBUG server-address

# Run GUI
./bin/input-leap
```

#### Command Line Options

| Option | Description |
|--------|-------------|
| `-f` | Run in foreground (don't daemonize) |
| `--debug <level>` | Set debug level: `ERROR`, `WARNING`, `NOTE`, `INFO`, `DEBUG`, `DEBUG1`, `DEBUG2` |
| `-c <file>` | Configuration file (server) |
| `--name <name>` | Override screen name |
| `-l <file>` | Log to file |

---

## Debugging

### GDB (Linux/macOS)

```bash
# Debug server
gdb --args ./bin/input-leaps -f --debug DEBUG -c config.conf

# GDB commands
(gdb) break Server::onMouseMove
(gdb) run
(gdb) bt  # backtrace
(gdb) p variable  # print variable
(gdb) c  # continue
```

### LLDB (macOS)

```bash
lldb -- ./bin/input-leaps -f --debug DEBUG -c config.conf

(lldb) b Server::onMouseMove
(lldb) run
(lldb) bt
(lldb) frame variable
```

### Visual Studio Debugger (Windows)

1. Set startup project to `input-leaps` or `input-leapc`
2. Configure command line arguments in **Project Properties > Debugging**
3. Set breakpoints and press F5

### Logging

The codebase uses a custom logging system. Key log levels:

```cpp
LOG((CLOG_ERR "Error message: %s", error.c_str()));
LOG((CLOG_WARN "Warning message"));
LOG((CLOG_NOTE "Note message"));
LOG((CLOG_INFO "Info message"));
LOG((CLOG_DEBUG "Debug message"));
LOG((CLOG_DEBUG1 "Detailed debug"));
LOG((CLOG_DEBUG2 "Very detailed debug"));
```

### Core Dumps (Linux)

```bash
# Enable core dumps
ulimit -c unlimited
echo "core.%p" | sudo tee /proc/sys/kernel/core_pattern

# Run and crash...
./bin/input-leaps ...

# Analyze core dump
gdb ./bin/input-leaps core.12345
```

### Valgrind (Linux)

```bash
# Memory leak detection
valgrind --leak-check=full ./bin/input-leaps -f --debug DEBUG -c config.conf

# Thread debugging
valgrind --tool=helgrind ./bin/input-leaps -f --debug DEBUG -c config.conf
```

---

## Testing

### Running All Tests

```bash
cd build-debug

# Using CTest
ctest --verbose

# Or run directly
./bin/unittests
./bin/integtests
./bin/guiunittests
```

### Running Specific Tests

```bash
# Run tests matching pattern
./bin/unittests --gtest_filter="ServerTest.*"
./bin/unittests --gtest_filter="*Clipboard*"

# List all tests
./bin/unittests --gtest_list_tests
```

### Writing Tests

Tests are located in `src/test/`:

```
src/test/
├── unittests/          # Unit tests (test individual components)
│   ├── inputleap/
│   ├── server/
│   ├── client/
│   └── ...
├── integtests/         # Integration tests
├── mock/               # Mock objects
└── global/             # Test utilities
```

#### Example Unit Test

```cpp
// src/test/unittests/server/ServerTests.cpp
#include <gtest/gtest.h>
#include "server/Server.h"

class ServerTest : public ::testing::Test {
protected:
    void SetUp() override {
        // Setup code
    }
    void TearDown() override {
        // Cleanup code
    }
};

TEST_F(ServerTest, HandleMouseMove) {
    // Test implementation
    EXPECT_TRUE(/* condition */);
}
```

### Code Coverage

```bash
# Configure with coverage
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_CXX_FLAGS="--coverage" \
      -DCMAKE_EXE_LINKER_FLAGS="--coverage" \
      ..

# Build and run tests
ninja
ctest

# Generate coverage report
gcovr -r .. --html --html-details -o coverage.html
```

---

## Code Style and Guidelines

### Formatting

The project uses a consistent coding style. Key conventions:

- 4-space indentation
- Braces on same line for functions and control structures
- CamelCase for class names
- camelCase for methods and variables
- m_ prefix for member variables
- UPPER_CASE for constants and macros

### Pre-Commit Checks

Before committing, ensure:

1. Code compiles without warnings:
   ```bash
   cmake -DCMAKE_CXX_FLAGS="-Wall -Wextra -Werror" ..
   ```

2. Tests pass:
   ```bash
   ctest --verbose
   ```

3. No memory leaks (for significant changes):
   ```bash
   valgrind --leak-check=full ./bin/unittests
   ```

### Release Notes

For user-visible changes, create a release note fragment:

```bash
# Create fragment in doc/newsfragments/
# Filename format: <issue_number>.<type>.md
# Types: feature, bugfix, security, doc, removal

echo "Fixed mouse movement on multi-monitor setups" > doc/newsfragments/1234.bugfix.md
```

---

## Contributing

### Pull Request Process

1. **Fork** the repository
2. Create a **feature branch** from `master`
3. Make your changes with **clear commits**
4. Add **tests** for new functionality
5. Create **release note fragment** if user-visible
6. Push and open a **Pull Request**
7. Address **review feedback**

### Commit Message Format

```
component: Brief description of change

Longer explanation of what and why (if needed).
Reference any related issues.

Fixes #1234
```

Examples:
```
server: Fix cursor jumping on screen switch
gui: Add dark mode support for settings dialog
net: Improve SSL handshake error messages
```

### Code Review

All PRs require review. Reviewers will check:

- Code correctness and logic
- Test coverage
- Documentation
- Platform compatibility
- Performance implications

---

## Common Development Tasks

### Adding a New Source File

1. Create the file in the appropriate directory
2. Update the corresponding `CMakeLists.txt` (if using explicit file lists)
3. Re-run CMake: `cmake ..`

### Adding a New Library Dependency

1. Add `find_package()` or `pkg_check_modules()` to root `CMakeLists.txt`
2. Add to `target_link_libraries()` for appropriate targets
3. Update build documentation

### Adding a New Platform

1. Create platform-specific files in `src/lib/platform/`
2. Add build conditions in `src/lib/platform/CMakeLists.txt`
3. Add platform detection in root `CMakeLists.txt`
4. Implement required interfaces (`IPlatformScreen`, etc.)

### Debugging Protocol Issues

1. Enable detailed logging:
   ```bash
   ./bin/input-leaps -f --debug DEBUG2 -c config.conf
   ```

2. Key files for protocol:
   - `src/lib/inputleap/ProtocolUtil.cpp` - Serialization
   - `src/lib/inputleap/protocol_types.h` - Protocol constants
   - `src/lib/server/ClientProxy1_6.cpp` - Server-side protocol handling
   - `src/lib/client/ServerProxy.cpp` - Client-side protocol handling

### Debugging Platform Issues

1. Add logging to platform-specific code:
   ```cpp
   LOG((CLOG_DEBUG "Platform event: %d", eventType));
   ```

2. Key platform files:
   - **Windows**: `src/lib/platform/MSWindows*.cpp`
   - **macOS**: `src/lib/platform/OSX*.cpp`
   - **X11**: `src/lib/platform/XWindows*.cpp`
   - **Wayland**: `src/lib/platform/Ei*.cpp`

### Testing Two Machines Locally

You can test server/client on the same machine:

1. Create a minimal config file:
   ```ini
   section: screens
       screen1:
       screen2:
   end
   section: links
       screen1:
           right = screen2
       screen2:
           left = screen1
   end
   ```

2. Run server:
   ```bash
   ./bin/input-leaps -f --debug DEBUG -c test.conf --name screen1
   ```

3. Run client (in another terminal):
   ```bash
   ./bin/input-leapc -f --debug DEBUG --name screen2 localhost
   ```

---

## Getting Help

- **IRC**: `#inputleap-dev` on LiberaChat
- **Issues**: [GitHub Issues](https://github.com/input-leap/input-leap/issues)
- **Wiki**: [GitHub Wiki](https://github.com/input-leap/input-leap/wiki)
