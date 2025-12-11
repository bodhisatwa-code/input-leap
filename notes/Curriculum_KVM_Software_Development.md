# Complete Curriculum: Building Cross-Platform KVM Software in C++

## Course Overview

**Title:** Systems Programming Masterclass: Building Production-Grade Cross-Platform Software
**Duration:** 16 Weeks (1 Semester) + 8 Weeks Capstone Project
**Prerequisites:** Basic programming knowledge (variables, loops, functions, basic OOP concepts)
**Final Project:** Build a fully functional KVM (Keyboard-Video-Mouse) software from scratch

---

## Learning Outcomes

Upon completion, students will be able to:
1. Write professional-grade C++ code (C++17/20)
2. Understand operating system internals relevant to input handling
3. Design and implement cross-platform applications
4. Build networked applications with security (SSL/TLS)
5. Create GUI applications using Qt framework
6. Set up professional build systems with CMake
7. Package and distribute software for multiple platforms
8. Write comprehensive tests and documentation

---

# PART I: C++ FOUNDATIONS (Weeks 1-4)

---

## Module 1: Modern C++ Fundamentals

### Class 1.1: C++ Environment & Toolchain Setup

#### Chapter 1: Development Environment
**Topics:**
- Installing compilers (GCC, Clang, MSVC)
- Understanding compilation vs interpretation
- Setting up IDEs (VS Code, CLion, Visual Studio)
- Terminal/Shell basics for developers
- Version control with Git fundamentals

**Lab:** Set up complete C++ development environment on three platforms

#### Chapter 2: The Compilation Process
**Topics:**
- Preprocessor directives and macros
- Compilation units and object files
- Linking: static vs dynamic
- The role of headers and source files
- Understanding compiler errors vs linker errors

**Lab:** Manually compile a multi-file program using command line

#### Chapter 3: Your First C++ Program
**Topics:**
- Program structure: main() function
- #include and the standard library
- Namespaces: std and custom
- Comments and documentation
- Basic I/O with iostream

**Lab:** Create a "Hello, World" program and trace through compilation

---

### Class 1.2: Data Types & Memory Model

#### Chapter 1: Fundamental Types
**Topics:**
- Integer types: int, short, long, long long
- Floating point: float, double, long double
- Character types: char, wchar_t, char16_t, char32_t
- Boolean type and truthiness
- The void type
- Size guarantees and `<cstdint>` fixed-width types
- Type modifiers: signed, unsigned, const, volatile

**Lab:** Write a program exploring sizeof() for all fundamental types

#### Chapter 2: Variables & Constants
**Topics:**
- Variable declaration and initialization
- Uniform initialization (C++11 brace syntax)
- const and constexpr
- auto type deduction
- decltype for type inspection
- Variable scope and lifetime
- Static variables

**Lab:** Build a unit converter demonstrating type conversions

#### Chapter 3: The C++ Memory Model
**Topics:**
- Stack vs Heap memory
- Memory layout of a program (text, data, bss, heap, stack)
- Automatic storage duration
- Static storage duration
- Dynamic storage duration
- Memory alignment and padding

**Lab:** Visualize memory layout using debugger

---

### Class 1.3: Operators & Control Flow

#### Chapter 1: Operators
**Topics:**
- Arithmetic operators
- Comparison and relational operators
- Logical operators (&&, ||, !)
- Bitwise operators (&, |, ^, ~, <<, >>)
- Assignment operators
- Increment/decrement operators
- Ternary conditional operator
- Operator precedence and associativity
- Type casting operators (static_cast, reinterpret_cast, const_cast, dynamic_cast)

**Lab:** Build a bitwise flag system (like Unix file permissions)

#### Chapter 2: Control Structures
**Topics:**
- if, else if, else statements
- switch statements and fall-through
- while and do-while loops
- for loops (traditional and range-based)
- break, continue, and goto
- Structured bindings in conditionals (C++17)
- if with initializer (C++17)

**Lab:** Implement a command-line menu system

#### Chapter 3: Error Handling Basics
**Topics:**
- Return codes and error checking
- errno and system errors
- Introduction to exceptions
- try, catch, throw
- Standard exception hierarchy
- RAII principle introduction

**Lab:** Build error-handling wrapper for file operations

---

### Class 1.4: Functions & Program Organization

#### Chapter 1: Function Fundamentals
**Topics:**
- Function declaration vs definition
- Parameter passing: by value, by reference, by pointer
- Return values and return type deduction
- Default arguments
- Function overloading
- inline functions
- constexpr functions

**Lab:** Create a math library with overloaded functions

#### Chapter 2: Advanced Function Concepts
**Topics:**
- Recursion and tail recursion
- Function pointers
- std::function and callable objects
- Lambda expressions (C++11/14/17)
- Capture clauses in lambdas
- Generic lambdas (C++14)
- Higher-order functions

**Lab:** Implement sorting algorithms with custom comparators

#### Chapter 3: Program Organization
**Topics:**
- Header files and include guards
- #pragma once
- Forward declarations
- Separate compilation
- Header-only libraries
- Circular dependencies and solutions
- The One Definition Rule (ODR)

**Lab:** Refactor monolithic code into proper multi-file structure

---

## Module 2: Object-Oriented Programming in C++

### Class 2.1: Classes & Objects

#### Chapter 1: Class Fundamentals
**Topics:**
- Class declaration and definition
- Member variables (fields)
- Member functions (methods)
- Access specifiers: public, private, protected
- The this pointer
- Struct vs Class in C++
- Object instantiation

**Lab:** Design a Screen class representing a monitor

#### Chapter 2: Constructors & Destructors
**Topics:**
- Default constructors
- Parameterized constructors
- Constructor overloading
- Member initializer lists
- Delegating constructors (C++11)
- Destructors and cleanup
- Order of construction and destruction
- explicit keyword

**Lab:** Implement a Connection class with proper resource management

#### Chapter 3: Special Member Functions
**Topics:**
- Copy constructor
- Copy assignment operator
- Move constructor (C++11)
- Move assignment operator (C++11)
- Rule of Three / Rule of Five / Rule of Zero
- = default and = delete
- std::move and std::forward

**Lab:** Build a Buffer class with proper copy and move semantics

---

### Class 2.2: Inheritance & Polymorphism

#### Chapter 1: Inheritance
**Topics:**
- Base and derived classes
- Inheritance access specifiers
- Constructor/destructor in inheritance
- Method overriding
- Hiding vs overriding
- Multiple inheritance
- Virtual inheritance (diamond problem)
- final keyword

**Lab:** Create a platform abstraction hierarchy (Platform -> WindowsPlatform, LinuxPlatform, MacPlatform)

#### Chapter 2: Polymorphism
**Topics:**
- Virtual functions
- Pure virtual functions
- Abstract classes and interfaces
- Virtual destructors (critical!)
- Runtime type information (RTTI)
- dynamic_cast and type checking
- The vtable mechanism
- override and final specifiers

**Lab:** Implement a plugin system using polymorphism

#### Chapter 3: Design Patterns for OOP
**Topics:**
- Factory pattern
- Abstract Factory pattern
- Singleton pattern (and its problems)
- Strategy pattern
- Observer pattern
- Decorator pattern
- Template Method pattern

**Lab:** Implement Event system using Observer pattern

---

### Class 2.3: Advanced OOP Concepts

#### Chapter 1: Operator Overloading
**Topics:**
- Overloadable operators
- Member vs non-member overloading
- Overloading arithmetic operators
- Overloading comparison operators
- Overloading stream operators (<< and >>)
- Overloading function call operator ()
- Overloading subscript operator []
- Conversion operators

**Lab:** Create a Vector2D class with full operator support

#### Chapter 2: Friends & Static Members
**Topics:**
- Friend functions
- Friend classes
- Static member variables
- Static member functions
- Static initialization order fiasco
- Meyers' Singleton

**Lab:** Implement a Logger singleton with friend access

#### Chapter 3: Nested & Local Classes
**Topics:**
- Nested classes
- Local classes within functions
- Anonymous classes
- Pimpl idiom (Pointer to Implementation)
- Opaque pointers for ABI stability

**Lab:** Refactor classes using Pimpl for binary compatibility

---

## Module 3: Memory Management & Resource Handling

### Class 3.1: Pointers & References Deep Dive

#### Chapter 1: Pointers
**Topics:**
- Pointer declaration and initialization
- Dereferencing and address-of operators
- Pointer arithmetic
- Pointers and arrays
- Pointers to pointers
- void pointers
- nullptr vs NULL vs 0
- const correctness with pointers

**Lab:** Implement a dynamic array from scratch

#### Chapter 2: References
**Topics:**
- Reference declaration and initialization
- References vs pointers
- const references
- Reference collapsing rules
- Rvalue references (C++11)
- Universal/forwarding references
- Reference lifetime extension

**Lab:** Create wrapper functions demonstrating perfect forwarding

#### Chapter 3: Dynamic Memory
**Topics:**
- new and delete operators
- new[] and delete[] for arrays
- Placement new
- Custom allocators introduction
- Memory leaks and detection
- Tools: Valgrind, AddressSanitizer, Dr. Memory

**Lab:** Find and fix memory leaks in provided code

---

### Class 3.2: Smart Pointers & RAII

#### Chapter 1: RAII Pattern
**Topics:**
- Resource Acquisition Is Initialization explained
- Scope-based resource management
- Exception safety guarantees
- Cleanup in face of exceptions
- RAII wrappers for C APIs

**Lab:** Wrap file handles and sockets in RAII classes

#### Chapter 2: Smart Pointers
**Topics:**
- std::unique_ptr
  - Ownership semantics
  - Custom deleters
  - unique_ptr for arrays
- std::shared_ptr
  - Reference counting
  - Control block
  - Custom deleters
  - make_shared optimization
- std::weak_ptr
  - Breaking circular references
  - Observer pattern use case
- Choosing the right smart pointer

**Lab:** Convert raw pointer codebase to smart pointers

#### Chapter 3: Memory Management Strategies
**Topics:**
- Object pools
- Arena allocators
- Small object optimization
- Copy-on-write
- Memory-mapped files
- Custom operator new/delete

**Lab:** Implement an object pool for frequently allocated objects

---

## Module 4: Standard Template Library (STL)

### Class 4.1: Containers

#### Chapter 1: Sequence Containers
**Topics:**
- std::array
- std::vector
  - Capacity vs size
  - Iterator invalidation
  - reserve() vs resize()
- std::deque
- std::list and std::forward_list
- Container selection criteria
- Contiguous vs node-based containers

**Lab:** Implement a message queue using appropriate container

#### Chapter 2: Associative Containers
**Topics:**
- std::set and std::multiset
- std::map and std::multimap
- Red-black tree implementation details
- std::unordered_set and std::unordered_multiset
- std::unordered_map and std::unordered_multimap
- Hash functions and equality
- Bucket interface

**Lab:** Build a configuration system using maps

#### Chapter 3: Container Adaptors & Special Containers
**Topics:**
- std::stack
- std::queue
- std::priority_queue
- std::span (C++20)
- std::optional (C++17)
- std::variant (C++17)
- std::any (C++17)
- std::string and std::string_view

**Lab:** Implement event priority queue for KVM events

---

### Class 4.2: Iterators & Algorithms

#### Chapter 1: Iterators
**Topics:**
- Iterator categories (Input, Output, Forward, Bidirectional, Random Access, Contiguous)
- Iterator traits
- Iterator operations
- Reverse iterators
- Insert iterators
- Stream iterators
- Move iterators
- Custom iterator implementation

**Lab:** Implement a custom iterator for a tree structure

#### Chapter 2: STL Algorithms - Part 1
**Topics:**
- Non-modifying algorithms (find, count, search, etc.)
- Modifying algorithms (copy, move, transform, etc.)
- Sorting algorithms
- Binary search algorithms
- Set algorithms
- Algorithm complexity guarantees

**Lab:** Process log files using STL algorithms

#### Chapter 3: STL Algorithms - Part 2
**Topics:**
- Heap algorithms
- Min/max algorithms
- Comparison algorithms
- Permutation algorithms
- Numeric algorithms (<numeric>)
- Parallel algorithms (C++17)
- Ranges library (C++20) introduction

**Lab:** Implement parallel data processing pipeline

---

### Class 4.3: Templates

#### Chapter 1: Function Templates
**Topics:**
- Template syntax
- Type deduction
- Explicit template arguments
- Template argument deduction guides (C++17)
- Multiple template parameters
- Non-type template parameters
- Template specialization
- Overloading vs specialization

**Lab:** Create generic serialization functions

#### Chapter 2: Class Templates
**Topics:**
- Class template syntax
- Member function templates
- Template specialization (full and partial)
- Template template parameters
- Default template arguments
- Variadic templates
- Parameter packs and fold expressions

**Lab:** Implement a generic Result<T, E> type

#### Chapter 3: Advanced Template Techniques
**Topics:**
- SFINAE (Substitution Failure Is Not An Error)
- std::enable_if
- Type traits (<type_traits>)
- constexpr if (C++17)
- Concepts (C++20) introduction
- CRTP (Curiously Recurring Template Pattern)
- Expression templates
- Template metaprogramming basics

**Lab:** Build compile-time type validation utilities

---

# PART II: SYSTEMS PROGRAMMING (Weeks 5-8)

---

## Module 5: Operating System Fundamentals

### Class 5.1: Process & Thread Management

#### Chapter 1: Processes
**Topics:**
- What is a process?
- Process creation (fork, exec, CreateProcess)
- Process states and lifecycle
- Process memory layout
- Environment variables
- Process exit and termination
- Inter-process communication overview
- Process priority and scheduling

**Lab:** Create a process manager utility

#### Chapter 2: Threads
**Topics:**
- Threads vs processes
- std::thread basics
- Thread creation and joining
- Detached threads
- Thread local storage
- Thread IDs
- Hardware concurrency
- Platform-specific threads (pthreads, Windows threads)

**Lab:** Implement multi-threaded file processor

#### Chapter 3: Thread Synchronization
**Topics:**
- Race conditions
- Critical sections
- std::mutex and std::recursive_mutex
- std::lock_guard and std::unique_lock
- std::scoped_lock (C++17)
- Deadlock prevention
- std::condition_variable
- std::semaphore (C++20)

**Lab:** Build thread-safe message queue

---

### Class 5.2: Advanced Concurrency

#### Chapter 1: Atomic Operations
**Topics:**
- std::atomic types
- Memory ordering (relaxed, acquire, release, seq_cst)
- Compare-and-swap operations
- Lock-free programming introduction
- ABA problem
- False sharing and cache lines

**Lab:** Implement lock-free stack

#### Chapter 2: Futures & Promises
**Topics:**
- std::async
- std::future and std::promise
- std::shared_future
- std::packaged_task
- Exception propagation in futures
- Future continuations (future of C++)

**Lab:** Build async task scheduler

#### Chapter 3: Concurrent Data Structures
**Topics:**
- Thread-safe containers
- Reader-writer locks (std::shared_mutex)
- Concurrent queue implementations
- Double-checked locking pattern
- Thread pool pattern
- Work stealing

**Lab:** Implement a thread pool for event processing

---

### Class 5.3: File Systems & I/O

#### Chapter 1: File I/O
**Topics:**
- C++ file streams (ifstream, ofstream, fstream)
- Binary vs text mode
- File positioning (seekg, seekp, tellg, tellp)
- Low-level file I/O (open, read, write, close)
- File descriptors
- Buffered vs unbuffered I/O
- Memory-mapped files

**Lab:** Implement configuration file parser

#### Chapter 2: Filesystem Library (C++17)
**Topics:**
- std::filesystem::path
- Directory iteration
- File status and permissions
- Creating and removing files/directories
- Copying and moving files
- Symbolic links
- Filesystem errors

**Lab:** Build file synchronization utility

#### Chapter 3: Serialization
**Topics:**
- Binary serialization
- Text serialization (JSON, XML)
- Endianness considerations
- Versioning serialized data
- Protocol Buffers / FlatBuffers introduction
- Custom serialization formats

**Lab:** Design wire protocol for KVM messages

---

### Class 5.4: Inter-Process Communication

#### Chapter 1: Pipes & FIFOs
**Topics:**
- Anonymous pipes
- Named pipes (FIFOs)
- Pipe buffering
- Bidirectional communication
- Windows named pipes specifics

**Lab:** Implement CLI-to-GUI communication via pipes

#### Chapter 2: Shared Memory
**Topics:**
- System V shared memory
- POSIX shared memory
- Windows shared memory
- Synchronization with shared memory
- Memory-mapped files for IPC

**Lab:** Build shared clipboard using shared memory

#### Chapter 3: Sockets for IPC
**Topics:**
- Unix domain sockets
- Windows local sockets
- Socket pairs
- Abstract namespace (Linux)
- IPC performance comparison

**Lab:** Implement local socket IPC for daemon communication

---

## Module 6: Network Programming

### Class 6.1: Network Fundamentals

#### Chapter 1: Networking Concepts
**Topics:**
- OSI model overview
- TCP/IP stack
- IP addressing (IPv4 and IPv6)
- Ports and services
- DNS basics
- NAT and firewalls
- Network byte order (endianness)

**Lab:** Build network diagnostic tool

#### Chapter 2: Socket Programming Basics
**Topics:**
- Berkeley sockets API
- Socket types (stream, datagram)
- Creating sockets
- Binding to addresses
- Listening and accepting
- Connecting to servers
- Sending and receiving data
- Closing sockets

**Lab:** Create echo server and client

#### Chapter 3: TCP Programming
**Topics:**
- TCP connection establishment (3-way handshake)
- TCP connection termination
- TCP states
- Graceful shutdown
- TCP options (nodelay, keepalive)
- Handling partial sends/receives
- Message framing

**Lab:** Implement reliable message protocol over TCP

---

### Class 6.2: Advanced Networking

#### Chapter 1: Non-blocking I/O
**Topics:**
- Blocking vs non-blocking sockets
- Setting non-blocking mode
- select() system call
- poll() system call
- epoll (Linux) / kqueue (BSD/macOS) / IOCP (Windows)
- Event-driven architecture
- Reactor pattern

**Lab:** Build event-driven server using select/poll

#### Chapter 2: Multiplexing & Event Loops
**Topics:**
- Event loop design
- Handling multiple connections
- Timer integration
- Signal handling in event loops
- Cross-platform event abstraction
- libevent/libuv overview

**Lab:** Create cross-platform event loop

#### Chapter 3: UDP & Multicast
**Topics:**
- UDP socket programming
- Datagram handling
- UDP reliability concerns
- Broadcast
- Multicast groups
- Service discovery concepts
- mDNS/DNS-SD (Bonjour/Avahi)

**Lab:** Implement service discovery for KVM servers

---

### Class 6.3: Secure Networking

#### Chapter 1: Cryptography Fundamentals
**Topics:**
- Symmetric encryption (AES)
- Asymmetric encryption (RSA, ECC)
- Hash functions (SHA-256)
- Digital signatures
- Key exchange (Diffie-Hellman)
- Random number generation
- Key derivation functions

**Lab:** Implement basic encryption utilities

#### Chapter 2: SSL/TLS
**Topics:**
- TLS protocol overview
- TLS handshake
- Certificates and PKI
- Certificate validation
- Self-signed certificates
- Certificate fingerprints
- TLS versions and cipher suites
- Perfect forward secrecy

**Lab:** Set up TLS connection with certificate validation

#### Chapter 3: OpenSSL Integration
**Topics:**
- OpenSSL library overview
- SSL context configuration
- Creating SSL sockets
- Certificate loading and verification
- Error handling in OpenSSL
- Memory management with OpenSSL
- Thread safety considerations

**Lab:** Wrap TCP sockets with SSL/TLS support

---

## Module 7: Platform-Specific Programming

### Class 7.1: Windows Systems Programming

#### Chapter 1: Windows API Fundamentals
**Topics:**
- Windows API overview
- HANDLE and kernel objects
- Unicode in Windows (WCHAR, TCHAR)
- Error handling (GetLastError)
- Windows data types
- Registry access
- Windows services

**Lab:** Create Windows service skeleton

#### Chapter 2: Windows Input System
**Topics:**
- Windows message loop
- Keyboard messages (WM_KEYDOWN, WM_KEYUP, etc.)
- Mouse messages
- Raw input API
- Low-level hooks (SetWindowsHookEx)
- SendInput for input injection
- Virtual key codes

**Lab:** Capture and replay keyboard/mouse input

#### Chapter 3: Windows Display & Clipboard
**Topics:**
- Multi-monitor handling (EnumDisplayMonitors)
- Screen coordinates and DPI
- Desktop and window management
- Clipboard API
- Clipboard formats
- Clipboard viewers and listeners

**Lab:** Implement multi-monitor screen management

---

### Class 7.2: Linux/Unix Systems Programming

#### Chapter 1: POSIX APIs
**Topics:**
- POSIX overview
- System calls vs library calls
- File descriptors
- Signal handling
- Process control
- User and group IDs
- Daemon creation

**Lab:** Create proper Unix daemon

#### Chapter 2: X11 Programming
**Topics:**
- X Window System architecture
- Xlib basics
- Creating windows
- Event handling
- Keyboard and mouse events
- XTest extension for input injection
- XRandR for multi-monitor
- X selections (clipboard)

**Lab:** Capture X11 input events

#### Chapter 3: Linux Input Subsystem & Wayland
**Topics:**
- Linux input event subsystem (/dev/input)
- evdev interface
- uinput for input injection
- Wayland architecture overview
- libei (emulated input)
- XDG portals
- D-Bus integration

**Lab:** Implement input capture for both X11 and Wayland

---

### Class 7.3: macOS Systems Programming

#### Chapter 1: macOS/Darwin Fundamentals
**Topics:**
- macOS architecture (Darwin, Cocoa, etc.)
- Objective-C++ basics
- Framework linking
- Code signing requirements
- Accessibility permissions
- Launch agents and daemons

**Lab:** Create macOS background service

#### Chapter 2: macOS Input & Display
**Topics:**
- Quartz Event Services
- CGEvent for input capture
- CGEvent for input injection
- Core Graphics display management
- IOKit for HID devices
- NSPasteboard for clipboard

**Lab:** Implement macOS input capture and injection

#### Chapter 3: Cross-Platform Abstraction
**Topics:**
- Designing platform abstraction layers
- Compile-time platform detection
- Runtime platform detection
- Conditional compilation
- Platform-specific implementations
- Testing on multiple platforms

**Lab:** Create unified platform abstraction layer

---

# PART III: KVM SOFTWARE ARCHITECTURE (Weeks 9-12)

---

## Module 8: KVM Concepts & Design

### Class 8.1: Understanding KVM Software

#### Chapter 1: KVM Software Overview
**Topics:**
- What is software KVM?
- Hardware KVM vs software KVM
- Use cases and scenarios
- Existing solutions analysis (Synergy, Barrier, Input Leap)
- Architecture overview
- Server vs client model
- Screen arrangement concepts

**Lab:** Document requirements for KVM software

#### Chapter 2: Input Handling Concepts
**Topics:**
- Keyboard input model
  - Physical keys vs virtual keys
  - Scan codes vs key codes
  - Key modifiers (Shift, Ctrl, Alt, Meta)
  - Key repeat handling
- Mouse input model
  - Absolute vs relative positioning
  - Button states
  - Scroll wheel
  - Multi-button mice
- Input capture vs input forwarding
- Input synthesis/injection

**Lab:** Design input event data structures

#### Chapter 3: Screen & Coordinate Systems
**Topics:**
- Screen topology
- Coordinate transformations
- Edge detection
- Screen transitions
- Multi-monitor configurations
- DPI and scaling considerations
- Relative vs absolute mouse positioning

**Lab:** Implement screen topology manager

---

### Class 8.2: Core Architecture Design

#### Chapter 1: Component Architecture
**Topics:**
- Clean architecture principles
- Separation of concerns
- Core vs platform-specific code
- Library design
- Dependency injection
- Interface-based design

**Lab:** Design component diagram for KVM software

#### Chapter 2: Event System Design
**Topics:**
- Event-driven architecture
- Event types (input, screen, clipboard, etc.)
- Event queuing
- Event dispatching
- Event handlers
- Priority handling
- Event filtering

**Lab:** Implement core event system

#### Chapter 3: Protocol Design
**Topics:**
- Message-based protocols
- Protocol versioning
- Message framing
- Serialization format
- Handshake sequence
- Keep-alive mechanism
- Error handling in protocols

**Lab:** Design and document KVM wire protocol

---

### Class 8.3: Server Implementation

#### Chapter 1: Server Architecture
**Topics:**
- Server responsibilities
- Connection management
- Client tracking
- Screen configuration
- Active screen management
- Input capture integration

**Lab:** Implement server core

#### Chapter 2: Server-Side Input Processing
**Topics:**
- Input capture on server
- Input transformation
- Key mapping and translation
- Modifier state tracking
- Mouse coordinate transformation
- Edge detection and screen switching

**Lab:** Implement server input processing

#### Chapter 3: Multi-Client Management
**Topics:**
- Client registration
- Client authentication
- Screen assignment
- Client state management
- Connection loss handling
- Reconnection logic

**Lab:** Implement multi-client handling

---

### Class 8.4: Client Implementation

#### Chapter 1: Client Architecture
**Topics:**
- Client responsibilities
- Server discovery
- Connection establishment
- Input injection
- Screen integration

**Lab:** Implement client core

#### Chapter 2: Client-Side Input Processing
**Topics:**
- Receiving input events
- Input translation for local platform
- Key code mapping
- Mouse movement handling
- Input injection methods
- Handling platform differences

**Lab:** Implement client input injection

#### Chapter 3: Client State Management
**Topics:**
- Connection state machine
- Active/inactive states
- Enter/leave screen events
- Clipboard synchronization triggers
- Error recovery

**Lab:** Implement client state machine

---

## Module 9: Clipboard & Data Transfer

### Class 9.1: Clipboard Architecture

#### Chapter 1: Clipboard Fundamentals
**Topics:**
- How clipboards work
- Clipboard ownership model
- Clipboard formats (text, rich text, HTML, images)
- Format negotiation
- Delayed rendering
- Platform clipboard differences

**Lab:** Document clipboard formats across platforms

#### Chapter 2: Platform Clipboard Integration
**Topics:**
- Windows clipboard API
- X11 selections (PRIMARY, SECONDARY, CLIPBOARD)
- macOS NSPasteboard
- Clipboard change detection
- Clipboard format conversion

**Lab:** Implement platform clipboard wrappers

#### Chapter 3: Network Clipboard Sync
**Topics:**
- Clipboard change notification
- Format negotiation over network
- Chunked transfer for large data
- Compression considerations
- Handling conversion failures

**Lab:** Implement network clipboard synchronization

---

### Class 9.2: Advanced Data Transfer

#### Chapter 1: File Transfer
**Topics:**
- Drag and drop concepts
- File transfer protocol design
- Chunked file transfer
- Transfer progress reporting
- Transfer cancellation
- Handling large files

**Lab:** Design file transfer protocol

#### Chapter 2: Image & Rich Content Transfer
**Topics:**
- Image format handling
- Bitmap conversion
- Rich text formats
- HTML clipboard content
- Format priority handling

**Lab:** Implement image clipboard transfer

#### Chapter 3: Security Considerations
**Topics:**
- Clipboard content risks
- Content filtering
- Size limits
- Sandboxing clipboard access
- User consent for transfers

**Lab:** Implement clipboard security measures

---

## Module 10: GUI Development with Qt

### Class 10.1: Qt Fundamentals

#### Chapter 1: Qt Overview
**Topics:**
- Qt framework introduction
- Qt modules
- Qt licensing (LGPL vs commercial)
- Qt vs other GUI frameworks
- Setting up Qt development environment
- qmake vs CMake for Qt

**Lab:** Set up Qt project with CMake

#### Chapter 2: Widgets & Layouts
**Topics:**
- QWidget and widget hierarchy
- Common widgets (QLabel, QPushButton, QLineEdit, etc.)
- Layout managers (QHBoxLayout, QVBoxLayout, QGridLayout)
- Size policies and hints
- Custom widgets
- Widget styling with CSS

**Lab:** Create main window layout

#### Chapter 3: Signals & Slots
**Topics:**
- Signal and slot mechanism
- Connecting signals to slots
- Signal/slot with parameters
- Custom signals and slots
- Lambda slots
- Queued connections
- Thread-safe signals

**Lab:** Implement interactive configuration dialog

---

### Class 10.2: Qt Application Development

#### Chapter 1: Model-View Architecture
**Topics:**
- MVC/MVP in Qt
- QAbstractItemModel
- QStandardItemModel
- QListView, QTableView, QTreeView
- Custom models
- Proxy models for filtering/sorting
- Delegate pattern

**Lab:** Create screen configuration list view

#### Chapter 2: Graphics View Framework
**Topics:**
- QGraphicsScene
- QGraphicsView
- QGraphicsItem
- Custom graphics items
- Scene coordinates
- View transformations
- Interactive items

**Lab:** Build visual screen arrangement editor

#### Chapter 3: Dialogs & Windows
**Topics:**
- QDialog basics
- Standard dialogs
- Modal vs modeless dialogs
- QMainWindow features
- Menus and toolbars
- Status bar
- System tray integration

**Lab:** Implement settings dialog with system tray

---

### Class 10.3: Qt Application Services

#### Chapter 1: Settings & Persistence
**Topics:**
- QSettings for configuration
- INI vs registry vs plist
- Application data locations
- Saving/restoring window state
- User preferences management

**Lab:** Implement configuration persistence

#### Chapter 2: Threading in Qt
**Topics:**
- QThread basics
- Worker objects pattern
- Thread affinity
- Signal/slot across threads
- QtConcurrent
- Thread pools in Qt

**Lab:** Implement background connection manager

#### Chapter 3: Network in Qt
**Topics:**
- QTcpSocket and QTcpServer
- QUdpSocket
- QNetworkAccessManager
- SSL/TLS in Qt
- Asynchronous networking

**Lab:** Integrate Qt networking with core library

---

# PART IV: BUILD, TEST & DISTRIBUTION (Weeks 13-16)

---

## Module 11: CMake Build System

### Class 11.1: CMake Fundamentals

#### Chapter 1: CMake Basics
**Topics:**
- What is CMake?
- CMakeLists.txt structure
- Minimum version and project declaration
- Variables and cache variables
- Commands and functions
- Generator expressions
- Build types (Debug, Release, RelWithDebInfo)

**Lab:** Convert simple project to CMake

#### Chapter 2: Targets & Dependencies
**Topics:**
- add_executable and add_library
- target_include_directories
- target_link_libraries
- PUBLIC, PRIVATE, INTERFACE
- Transitive dependencies
- Object libraries
- Alias targets

**Lab:** Create multi-library CMake project

#### Chapter 3: Finding Dependencies
**Topics:**
- find_package
- Config mode vs Module mode
- Writing Find modules
- pkg-config integration
- Imported targets
- FetchContent for dependencies
- External projects

**Lab:** Set up project with external dependencies

---

### Class 11.2: Advanced CMake

#### Chapter 1: Cross-Platform CMake
**Topics:**
- Platform detection
- Compiler detection
- Generator selection
- Toolchain files
- Cross-compilation
- Platform-specific sources

**Lab:** Make build work on Windows, macOS, Linux

#### Chapter 2: CMake for Qt
**Topics:**
- Finding Qt packages
- AUTOMOC, AUTOUIC, AUTORCC
- Qt resource files
- UI file compilation
- Translation files
- Qt deployment

**Lab:** Integrate Qt GUI with CMake build

#### Chapter 3: Build Configuration
**Topics:**
- Options and cache variables
- Conditional compilation
- Feature detection
- Version handling
- Git integration for version
- Compile definitions

**Lab:** Add configurable build options

---

### Class 11.3: Advanced Build Topics

#### Chapter 1: Custom Commands & Targets
**Topics:**
- add_custom_command
- add_custom_target
- Code generation
- Pre/post build steps
- File copying and installation
- Dependency tracking

**Lab:** Add code generation step to build

#### Chapter 2: Installation & Packaging
**Topics:**
- install() command
- Component-based installation
- CMake package configuration
- Export targets
- CPack introduction
- Generator-specific settings

**Lab:** Configure installation rules

#### Chapter 3: Build Performance
**Topics:**
- ccache integration
- Precompiled headers
- Unity builds
- Parallel compilation
- Dependency analysis
- Incremental builds

**Lab:** Optimize build times

---

## Module 12: Testing & Quality Assurance

### Class 12.1: Unit Testing

#### Chapter 1: Google Test Framework
**Topics:**
- Google Test introduction
- TEST and TEST_F macros
- Assertions (EXPECT vs ASSERT)
- Test fixtures
- Setup and teardown
- Test filtering
- Death tests

**Lab:** Write unit tests for core classes

#### Chapter 2: Test Design
**Topics:**
- Test-driven development (TDD)
- Unit test best practices
- Testing private members
- Testing with dependencies
- Test organization
- Code coverage

**Lab:** Achieve high coverage for critical components

#### Chapter 3: Mocking
**Topics:**
- Google Mock introduction
- Creating mock classes
- EXPECT_CALL and ON_CALL
- Matchers
- Actions
- Mock verification
- Dependency injection for testing

**Lab:** Test networking code with mocks

---

### Class 12.2: Integration & System Testing

#### Chapter 1: Integration Testing
**Topics:**
- Integration test strategies
- Testing component interactions
- Database/file testing
- Network testing
- Test environments
- Test data management

**Lab:** Write integration tests for client-server

#### Chapter 2: System Testing
**Topics:**
- End-to-end testing
- GUI testing challenges
- Platform-specific testing
- Virtual machine testing
- Test automation
- Continuous testing

**Lab:** Create automated system tests

#### Chapter 3: Testing Infrastructure
**Topics:**
- CTest integration
- Test discovery
- Test fixtures in CMake
- Parallel test execution
- Test reporting
- CI/CD integration

**Lab:** Set up comprehensive test suite

---

### Class 12.3: Code Quality

#### Chapter 1: Static Analysis
**Topics:**
- Compiler warnings
- Clang-tidy
- Cppcheck
- PVS-Studio
- SonarQube
- Custom checks

**Lab:** Configure and run static analysis

#### Chapter 2: Dynamic Analysis
**Topics:**
- AddressSanitizer
- MemorySanitizer
- ThreadSanitizer
- UndefinedBehaviorSanitizer
- Valgrind
- Profiling tools

**Lab:** Find and fix issues with sanitizers

#### Chapter 3: Code Style & Documentation
**Topics:**
- Code formatting (clang-format)
- Naming conventions
- Documentation standards
- Doxygen documentation
- API documentation
- Architecture documentation

**Lab:** Document public APIs

---

## Module 13: Packaging & Distribution

### Class 13.1: Binary Distribution Fundamentals

#### Chapter 1: Binary Compatibility
**Topics:**
- ABI compatibility
- Symbol visibility
- Versioning shared libraries
- Runtime dependencies
- Static vs dynamic linking decisions
- Portable builds

**Lab:** Analyze binary dependencies

#### Chapter 2: Dependency Management
**Topics:**
- Bundling vs system dependencies
- RPATH and RUNPATH
- Windows DLL search path
- macOS @rpath and @loader_path
- Dependency walker tools
- Creating portable binaries

**Lab:** Create self-contained build

#### Chapter 3: Code Signing
**Topics:**
- Why code signing?
- Windows code signing (Authenticode)
- macOS code signing and notarization
- Linux package signing
- Certificate management
- Timestamping

**Lab:** Set up code signing workflow

---

### Class 13.2: Platform-Specific Packaging

#### Chapter 1: Windows Packaging
**Topics:**
- MSI installers
- WiX Toolset
- Inno Setup
- Installer UI customization
- Prerequisites and dependencies
- Registry and shortcuts
- Silent installation
- Portable packages

**Lab:** Create Windows installer with WiX

#### Chapter 2: macOS Packaging
**Topics:**
- App bundle structure
- Info.plist configuration
- DMG creation
- PKG installers
- Notarization process
- Gatekeeper requirements
- Sparkle for updates

**Lab:** Create macOS DMG package

#### Chapter 3: Linux Packaging
**Topics:**
- DEB package creation
- RPM package creation
- Flatpak
- Snap
- AppImage
- Desktop file integration
- Package repositories

**Lab:** Create DEB and Flatpak packages

---

### Class 13.3: Release Engineering

#### Chapter 1: Version Management
**Topics:**
- Semantic versioning
- Version embedding in binaries
- Changelog management
- Release notes
- Git tags for releases
- Branch strategies for releases

**Lab:** Implement version management system

#### Chapter 2: CI/CD Pipeline
**Topics:**
- GitHub Actions overview
- Multi-platform CI
- Build matrices
- Artifact management
- Automated testing in CI
- Release automation
- Nightly builds

**Lab:** Create complete CI/CD pipeline

#### Chapter 3: Distribution & Updates
**Topics:**
- Release hosting (GitHub Releases)
- Mirror management
- Update mechanisms
- Delta updates
- Crash reporting
- Telemetry (ethical considerations)

**Lab:** Set up release workflow

---

# PART V: CAPSTONE PROJECT (Weeks 17-24)

---

## Module 14: Capstone - Building Your KVM Software

### Phase 1: Foundation (Weeks 17-18)

#### Milestone 1.1: Project Setup
**Deliverables:**
- Git repository with proper structure
- CMake build system
- CI/CD pipeline (basic)
- Development environment documentation
- Coding standards document

#### Milestone 1.2: Core Libraries
**Deliverables:**
- Platform abstraction layer
- Event system
- Logging system
- Configuration system
- Basic networking layer

---

### Phase 2: Core Implementation (Weeks 19-20)

#### Milestone 2.1: Input Handling
**Deliverables:**
- Input capture on all platforms
- Input injection on all platforms
- Key mapping system
- Mouse handling system
- Cross-platform input abstraction

#### Milestone 2.2: Network Protocol
**Deliverables:**
- Protocol specification document
- Message serialization
- TCP connection handling
- SSL/TLS integration
- Server-client handshake

---

### Phase 3: Features (Weeks 21-22)

#### Milestone 3.1: Screen Management
**Deliverables:**
- Multi-monitor detection
- Screen topology configuration
- Edge detection and switching
- Coordinate transformation

#### Milestone 3.2: Clipboard & Data
**Deliverables:**
- Clipboard capture and injection
- Text clipboard sync
- Image clipboard sync
- Format conversion

---

### Phase 4: Polish (Weeks 23-24)

#### Milestone 4.1: GUI Application
**Deliverables:**
- Qt-based configuration GUI
- Visual screen arrangement
- System tray integration
- Settings persistence

#### Milestone 4.2: Distribution
**Deliverables:**
- Windows installer
- macOS DMG package
- Linux packages (DEB, Flatpak)
- User documentation
- Final presentation

---

## Assessment Criteria

### Technical Requirements
- [ ] Cross-platform support (Windows, macOS, Linux)
- [ ] Secure encrypted connections
- [ ] Reliable input forwarding
- [ ] Clipboard synchronization
- [ ] GUI configuration tool
- [ ] Professional installers

### Code Quality
- [ ] Clean architecture
- [ ] Comprehensive testing (>70% coverage)
- [ ] Documentation
- [ ] No critical static analysis warnings
- [ ] Memory safety (no leaks)

### Professional Skills
- [ ] Git history (meaningful commits)
- [ ] CI/CD pipeline
- [ ] Release management
- [ ] User documentation

---

# Appendices

## Appendix A: Recommended Reading

### C++ Books
1. "A Tour of C++" - Bjarne Stroustrup
2. "Effective Modern C++" - Scott Meyers
3. "C++ Concurrency in Action" - Anthony Williams
4. "The C++ Programming Language" - Bjarne Stroustrup

### Systems Programming
1. "Advanced Programming in the UNIX Environment" - W. Richard Stevens
2. "Windows System Programming" - Johnson M. Hart
3. "Linux System Programming" - Robert Love
4. "Unix Network Programming" - W. Richard Stevens

### Qt Development
1. "C++ GUI Programming with Qt 4" - Jasmin Blanchette
2. Qt Official Documentation

### Build Systems
1. "Professional CMake" - Craig Scott
2. CMake Official Documentation

---

## Appendix B: Tools Reference

### Development Tools
| Tool | Purpose |
|------|---------|
| GCC/Clang/MSVC | C++ compilers |
| CMake | Build system generator |
| Ninja | Fast build tool |
| Git | Version control |
| VS Code / CLion | IDE |

### Debugging & Profiling
| Tool | Purpose |
|------|---------|
| GDB/LLDB | Debuggers |
| Valgrind | Memory analysis |
| perf | Linux profiler |
| VTune | Intel profiler |
| Instruments | macOS profiler |

### Static Analysis
| Tool | Purpose |
|------|---------|
| clang-tidy | Linter/checker |
| cppcheck | Static analyzer |
| clang-format | Code formatter |

### Testing
| Tool | Purpose |
|------|---------|
| Google Test | Unit testing |
| Google Mock | Mocking |
| gcov/lcov | Coverage |

---

## Appendix C: Input Leap Source Code Reference

Throughout the course, students should reference the Input Leap source code:

### Key Files to Study

**Core Architecture:**
- `src/lib/inputleap/App.cpp` - Application base class
- `src/lib/inputleap/ClientApp.cpp` - Client application
- `src/lib/inputleap/ServerApp.cpp` - Server application

**Platform Abstraction:**
- `src/lib/platform/` - All platform-specific code
- `src/lib/arch/` - Architecture abstraction

**Networking:**
- `src/lib/net/TCPSocket.cpp` - TCP implementation
- `src/lib/net/SecureSocket.cpp` - SSL/TLS wrapper

**Event System:**
- `src/lib/base/EventQueue.cpp` - Event handling

**Protocol:**
- `src/lib/inputleap/protocol_types.h` - Protocol definitions
- `src/lib/inputleap/ProtocolUtil.cpp` - Protocol utilities

**GUI:**
- `src/gui/src/` - Qt GUI application

---

## Appendix D: Weekly Lab Schedule

| Week | Primary Lab Focus |
|------|------------------|
| 1 | C++ environment setup, basic programs |
| 2 | Memory model, types, operators |
| 3 | Functions, program organization |
| 4 | Classes, OOP basics |
| 5 | Processes, threads, synchronization |
| 6 | File I/O, IPC |
| 7 | Socket programming |
| 8 | Platform-specific programming |
| 9 | KVM core design |
| 10 | Server/client implementation |
| 11 | Clipboard, data transfer |
| 12 | Qt GUI development |
| 13 | CMake build system |
| 14 | Testing |
| 15 | Packaging |
| 16 | Release engineering |
| 17-24 | Capstone project |

---

## Appendix E: Project Checkpoints

### Checkpoint 1 (Week 6)
- C++ proficiency demonstrated
- Basic systems programming concepts understood
- Simple networked application working

### Checkpoint 2 (Week 10)
- Platform abstraction layer complete
- Basic server-client communication working
- Input capture/injection on one platform

### Checkpoint 3 (Week 14)
- Full feature implementation
- GUI functional
- Tests passing

### Final (Week 24)
- Complete KVM software
- Professional packaging
- Documentation complete
- Presentation delivered

---

*Course designed based on Input Leap architecture - a production-grade open-source KVM software*
