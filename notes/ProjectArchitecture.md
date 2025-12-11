# Input Leap Project Architecture

## Overview

Input Leap is a software KVM (Keyboard-Video-Mouse) switch that allows users to control multiple computers using a single keyboard and mouse. It enables seamless cursor movement between networked computers by moving the mouse to screen edges or using keyboard shortcuts.

**Current Version:** 3.0.3
**License:** GNU General Public License v2
**Origin:** Fork of Barrier (which was a fork of Synergy)

---

## High-Level Architecture

```
+------------------------------------------+
|              GUI Application              |
|           (Qt5/Qt6 Frontend)              |
|  - Configuration management               |
|  - System tray integration                |
|  - Zeroconf auto-discovery                |
+--------------------+---------------------+
                     |
                     | IPC (Inter-Process Communication)
                     |
      +--------------+---------------+
      |                              |
+-----v--------+           +---------v------+
| input-leaps  |           | input-leapc    |
| (Server)     |           | (Client)       |
|              |           |                |
| - Listens    |           | - Connects to  |
|   for clients|           |   server       |
| - Manages    |           | - Injects      |
|   screen     |           |   input events |
|   topology   |           |   locally      |
+--------------+           +----------------+
      |                              |
      +--------+  TCP + SSL  +-------+
               |             |
               v             v
      +------------------------+
      |    Network Layer       |
      | (Secure Sockets/SSL)   |
      +------------------------+
               |
               v
      +------------------------+
      |   Platform Layer       |
      | (OS-specific input/    |
      |  output handling)      |
      +------------------------+
               |
    +----------+----------+----------+
    |          |          |          |
+---v---+ +----v----+ +---v----+ +---v---+
|Windows| |  macOS  | |  X11   | | libei |
|  API  | | Carbon/ | |XTest/  | |(Wayland)
|       | | Quartz  | |XInput  | |       |
+-------+ +---------+ +--------+ +-------+
```

---

## Directory Structure

```
input-leap/
├── cmake/                    # CMake build modules
│   ├── Version.cmake         # Version number definitions
│   ├── Package.cmake         # Packaging configuration
│   └── gtest.cmake           # Google Test integration
│
├── dist/                     # Distribution/packaging files
│   ├── debian/               # Debian package configuration
│   ├── rpm/                  # RPM spec templates
│   ├── flatpak/              # Flatpak manifest
│   ├── snap/                 # Snap package config
│   ├── inno/                 # Inno Setup (Windows installer)
│   ├── wix/                  # WiX installer (Windows)
│   └── macos/                # macOS bundle resources
│
├── doc/                      # Documentation
│   ├── input-leapc.1         # Client man page
│   ├── input-leaps.1         # Server man page
│   ├── input-leap.conf.*     # Configuration examples
│   └── newsfragments/        # Release note fragments
│
├── ext/                      # External dependencies (git submodules)
│   ├── gtest/                # Google Test framework
│   └── gulrak-filesystem/    # C++17 filesystem backport
│
├── res/                      # Application resources
│   ├── *.svg, *.ico          # Application icons
│   ├── *.desktop             # Linux desktop entry
│   └── *.appdata.xml         # AppStream metadata
│
├── src/                      # Source code
│   ├── lib/                  # Core libraries
│   ├── client/               # Client executable
│   ├── server/               # Server executable
│   ├── daemon/               # Windows service daemon
│   ├── gui/                  # Qt GUI application
│   └── test/                 # Test suite
│
├── .github/                  # GitHub configuration
│   ├── workflows/            # CI/CD workflows
│   └── ISSUE_TEMPLATE/       # Issue templates
│
├── CMakeLists.txt            # Root build configuration
└── README.md                 # Project readme
```

---

## Core Library Modules (`src/lib/`)

### 1. Architecture Abstraction (`arch/`)

Provides OS abstraction layer hiding platform differences behind common interfaces.

**Key Interfaces:**
- `IArchDaemon` - Daemon/service management
- `IArchLog` - Logging abstraction
- `IArchMultithread` - Threading primitives
- `IArchNetwork` - Network operations
- `IArchSystem` - System information

**Platform Implementations:**
- `unix/` - POSIX systems (Linux, macOS, BSD)
- `win32/` - Windows

### 2. Base Utilities (`base/`)

Core utilities including the central event system.

**Key Components:**
- `EventQueue` - Central event dispatcher (pub-sub pattern)
- `EventTarget` - Base class for event subscribers
- `Event` - Event data structures
- `Log` - Logging infrastructure
- `PriorityQueue` - Priority-based message queue

### 3. Network Layer (`net/`)

Network communications with SSL/TLS encryption.

**Key Components:**
- `TCPSocket` / `TCPListenSocket` - TCP socket operations
- `SecureSocket` - SSL/TLS wrapper around sockets
- `SocketMultiplexer` - Async I/O multiplexing
- `NetworkAddress` - Address resolution
- `SecureUtils` - SSL utilities
- `FingerprintDatabase` - Certificate fingerprint management

### 4. Platform Abstraction (`platform/`)

Platform-specific input/output and screen handling.

**Windows (`MSWindows*`):**
- `MSWindowsScreen` - Screen management
- `MSWindowsKeyState` - Keyboard state tracking
- `MSWindowsClipboard` - Clipboard operations
- `MSWindowsHook` - Low-level input hooks

**macOS (`OSX*`):**
- `OSXScreen` - Screen management (Quartz)
- `OSXKeyState` - Keyboard handling
- `OSXClipboard` - Pasteboard access
- `OSXEventQueueBuffer` - Event queue integration

**Linux/X11 (`XWindows*`):**
- `XWindowsScreen` - X11 screen management
- `XWindowsKeyState` - Keyboard via XKB
- `XWindowsClipboard` - X11 selections
- `XWindowsEventQueueBuffer` - X11 event handling

**Linux/Wayland (`Ei*`, `Portal*`):**
- `EiScreen` - libei screen management
- `EiKeyState` - Keyboard via libxkbcommon
- `PortalRemoteDesktop` - XDG portal integration

### 5. Core Protocol (`inputleap/`)

Application framework and protocol implementation.

**Key Classes:**
- `App` / `ClientApp` / `ServerApp` - Application entry points
- `Screen` / `PlatformScreen` - Screen abstraction
- `Clipboard` / `IClipboard` - Clipboard handling
- `KeyState` / `KeyMap` - Keyboard state and mapping
- `ProtocolUtil` - Protocol serialization
- `protocol_types.h` - Protocol constants

**Interfaces:**
- `IPlatformScreen` - Screen operations
- `IPrimaryScreen` - Server screen interface
- `ISecondaryScreen` - Client screen interface
- `IKeyState` - Keyboard state interface

### 6. Client Library (`client/`)

Client-side connection and behavior management.

**Key Classes:**
- `Client` - Main client class, manages server connection
- `ServerProxy` - Represents server from client perspective
- `IClient` - Client interface

### 7. Server Library (`server/`)

Server-side orchestration and multi-client management.

**Key Classes:**
- `Server` - Main server orchestrator
- `ClientListener` - Accepts incoming connections
- `ClientProxy` / `ClientProxy1_6` - Client representation with version handling
- `PrimaryClient` - Represents the server's own screen
- `Config` - Screen topology, hotkeys, options
- `InputFilter` - Input filtering and hotkey processing

### 8. IPC (`ipc/`)

Inter-process communication between GUI and daemons.

**Key Classes:**
- `IpcServer` / `IpcClient` - IPC endpoints
- `IpcServerProxy` / `IpcClientProxy` - Message proxies
- `IpcMessage` - Message types

### 9. Multi-threading (`mt/`)

Threading utilities and synchronization primitives.

### 10. I/O Utilities (`io/`)

File operations and stream handling.

### 11. Common (`common/`)

Shared definitions, error codes, and utilities.

---

## Executables

### `input-leaps` (Server)

The server runs on the machine with the keyboard and mouse you want to share.

**Entry Point:** `src/server/input-leaps.cpp`

**Responsibilities:**
- Listen for client connections
- Manage screen topology configuration
- Capture keyboard/mouse input
- Route input to appropriate client screens
- Handle clipboard synchronization

### `input-leapc` (Client)

The client runs on machines you want to control.

**Entry Point:** `src/client/input-leapc.cpp`

**Responsibilities:**
- Connect to server
- Receive input events from server
- Inject keyboard/mouse events into local system
- Send clipboard data to server

### `input-leapd` (Daemon - Windows only)

Windows service daemon for background operation.

**Entry Point:** `src/daemon/input-leapd.cpp`

### `input-leap` (GUI)

Qt-based graphical configuration and control interface.

**Entry Point:** `src/gui/src/main.cpp`

**Key Features:**
- Visual screen topology configuration
- Zeroconf/Bonjour service discovery
- SSL certificate management
- Log viewing
- Server/client mode selection

---

## Data Flow

### Input Event Flow (Server to Client)

```
1. User moves mouse/presses key on server
              |
              v
2. Platform layer captures event (hooks/event queue)
              |
              v
3. Server detects cursor at screen edge OR hotkey pressed
              |
              v
4. Server determines target client from topology
              |
              v
5. Event serialized using InputLeap protocol
              |
              v
6. Encrypted and sent via TCP/SSL socket
              |
              v
7. Client receives and deserializes event
              |
              v
8. Client's platform layer injects event into local OS
              |
              v
9. Local application receives input
```

### Clipboard Flow

```
1. User copies data on any machine
              |
              v
2. Platform clipboard hook detects change
              |
              v
3. Clipboard data captured and chunked (StreamChunker)
              |
              v
4. ClipboardChunk sent to server
              |
              v
5. Server broadcasts to all connected clients
              |
              v
6. Clients update local clipboard
```

---

## Design Patterns

### 1. Proxy Pattern
- `ClientProxy` - Server's representation of a client
- `ServerProxy` - Client's representation of the server
- `IpcServerProxy` / `IpcClientProxy` - IPC message handling

### 2. Observer/Event Pattern
- `EventQueue` - Central event dispatcher
- `EventTarget` - Base class for event subscribers
- Components register handlers for specific event types

### 3. Strategy Pattern
- Platform implementations (`MSWindows*`, `OSX*`, `XWindows*`, `Ei*`) implement common interfaces
- Selected at compile time based on target platform

### 4. Factory Pattern
- Socket factories for creating appropriate socket types
- Screen factories for platform-specific screen objects

### 5. Adapter Pattern
- `PlatformScreenLoggingWrapper` - Adds logging to screen operations
- Clipboard format converters adapt between formats

---

## Network Protocol

### Protocol Characteristics
- Custom binary protocol over TCP
- SSL/TLS encryption mandatory
- Version negotiation on connection
- Big-endian byte order

### Message Types (from `protocol_types.h`)
- Handshake and version negotiation
- Mouse movement, button, wheel events
- Keyboard key press/release, repeat
- Clipboard data transfer (chunked)
- Screen information exchange
- Keep-alive/heartbeat

### Security
- TLS 1.2+ encryption
- Certificate fingerprint verification
- Self-signed certificates with fingerprint database

---

## Configuration

### Server Configuration File

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

section: aliases
    actual-hostname.local:
        screen1
end

section: options
    keystroke(control+alt+h) = switchToScreen(screen1)
end
```

### Configuration Sections
- **screens**: Define logical screen names
- **links**: Define screen adjacency relationships
- **aliases**: Map hostnames to logical names
- **options**: Hotkeys, clipboard settings, etc.

---

## Threading Model

- **Main Thread**: Event queue processing, UI (in GUI)
- **Network Thread**: Socket I/O multiplexing
- **Platform Threads**: OS-specific event handling

Thread-safe communication via `EventQueue` message passing.

---

## Platform Support Matrix

| Platform | Display Server | Status |
|----------|---------------|--------|
| Windows 10/11 | Win32 | Full support |
| macOS 10.12+ | Quartz/Carbon | Full support |
| Linux | X11 | Full support |
| Linux | Wayland (libei) | Experimental |
| FreeBSD | X11 | Supported |
| OpenBSD | X11 | Supported |

### Known Limitations
- Drag and drop: Not supported on Linux
- Clipboard: Not supported on Linux/Wayland
- UTF-8: Limited support, issues with some languages
- AltGr: Issues when Linux server -> Windows client

---

## Testing

### Test Organization (`src/test/`)

```
test/
├── unittests/          # Unit tests per module
│   ├── inputleap/
│   ├── server/
│   ├── client/
│   ├── net/
│   └── ...
├── integtests/         # Integration tests
├── mock/               # Mock objects
└── global/             # Test utilities
```

### Test Framework
- Google Test (gtest) for unit tests
- Google Mock (gmock) for mocking
- GUI tests using Qt Test

---

## Dependencies

### Core Dependencies
| Dependency | Version | Purpose |
|------------|---------|---------|
| CMake | 3.21+ | Build system |
| OpenSSL | 1.1.1+ | SSL/TLS encryption |
| Qt | 5.9+ or 6.2+ | GUI framework |
| pthreads | - | Threading |

### Platform-Specific Dependencies

**Linux/X11:**
- X11, Xext, Xrandr, Xinerama, Xtst, Xi
- ICE, SM (session management)
- Avahi (mDNS/Zeroconf)

**Linux/Wayland:**
- libei 0.99.1+
- libxkbcommon
- GLib, GIO
- libportal

**Windows:**
- Wtsapi32, Userenv, Wininet, Shlwapi
- Bonjour SDK (mDNS)

**macOS:**
- ScreenSaver, IOKit, ApplicationServices, Foundation, Carbon frameworks
