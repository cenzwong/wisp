# Distributed macOS Workspace

## Project Ideation Record

| Metadata | Details |
|---|---|
| Project | Distributed macOS Workspace |
| Codename | TBD |
| Document Type | Project Ideation Record |
| Version | 0.1.0 |
| Created | 26 November 2026 |
| Project Stage | Ideation / Discovery |
| Status | PARKED |
| Priority | Unassigned |
| Target Platform | macOS |
| Product Category | Personal Distributed Computing |
| Implementation Status | Not started |

---

## 1. Executive Summary

Distributed macOS Workspace is a proposed native macOS application that enables applications running on one physical Mac to appear and operate as independent application windows on another Mac.

The inspiration comes from Parallels Desktop's Coherence Mode, where applications running inside a Windows virtual machine appear alongside native macOS applications without exposing the entire Windows desktop.

This project extends that concept across physical computers rather than virtual machines.

A user should be able to operate applications hosted across multiple Macs through a single desktop environment, without constantly switching between remote desktop sessions.

The long-term vision is to transform multiple independently operating Macs into a unified personal computing workspace.

Rather than treating each computer as an isolated desktop, applications and computational resources become accessible across a trusted network of personal devices.

The project is currently parked. This document preserves the concept, initial architectural direction, technical feasibility, risks, and future opportunities for subsequent evaluation.

---

## 2. Problem Statement

Modern computing environments remain predominantly device-centric.

Users commonly own or operate multiple computers, including:

- Personal laptops.
- Desktop workstations.
- Always-on home servers.
- Dedicated AI inference machines.
- Development machines.
- Remote office computers.

Despite these devices being connected through increasingly capable networks, their graphical application environments remain largely isolated.

Existing remote desktop solutions generally expose an entire remote desktop inside another desktop.

This introduces several usability problems:

- Nested desktop environments.
- Unnecessary window management.
- Frequent context switching.
- Poor integration with local application workflows.
- Difficulty combining applications from multiple computers.
- Limited integration with native application launchers.
- An experience that emphasises remote machines rather than remote applications.

Users frequently need access to a particular application rather than an entire computer.

The fundamental problem is therefore not remote access itself.

It is the absence of a seamless application-level abstraction across physical computers.

---

## 3. Core Product Hypothesis

A computer should not necessarily be the boundary of a user's desktop workspace.

Instead, the workspace should act as a unified interaction layer across multiple computing devices.

Applications should be accessible independently of the physical machine on which they execute.

The user should primarily interact with applications, rather than manage remote computers.

**The application is the unit of interaction. The machine is the unit of execution.**

This separation could enable a more flexible personal computing architecture.

---

## 4. Product Vision

Create a native macOS experience in which remotely executing applications behave as naturally as possible alongside locally executing applications.

The intended experience is:

1. Discover another trusted Mac.
2. Browse applications available on that Mac.
3. Launch or select an application.
4. Display its window on the local Mac.
5. Interact with it using local input devices.
6. Move, resize and organise it alongside local applications.
7. Disconnect without necessarily terminating the remote application.

The physical execution location should become a secondary concern.

### Long-term vision

A unified personal workspace composed of:

- Multiple computers.
- Multiple operating system sessions.
- Distributed application execution.
- Distributed computational resources.
- Persistent remote workloads.
- A consistent user interaction layer.

The project is not intended to combine physical RAM, CPU or GPU resources transparently into a single machine. It distributes application execution across independently operating hosts.

---

## 5. Motivating Scenario

Consider a personal computing environment containing three Macs.

| Device | Primary Responsibility |
|---|---|
| MacBook Air | Portable interaction device |
| Mac mini | Always-on development and personal services |
| Mac Studio | High-performance AI and compute workloads |

The MacBook becomes the primary human-computer interaction interface.

The Mac mini provides persistent services and development applications.

The Mac Studio provides computationally intensive applications and AI workloads.

Example distribution:

| Application or Workload | Execution Host |
|---|---|
| Safari | MacBook |
| Slack | MacBook |
| Mail | MacBook |
| Xcode | Mac mini |
| Docker | Mac mini |
| Coding Agents | Mac mini |
| MLX | Mac Studio |
| Local LLM Inference | Mac Studio |
| AI Agent Management UI | Mac Studio |
| Data Processing | Mac Studio |

The user operates graphical applications from these devices without needing to expose their complete desktop environments.

Remote applications continue running when the MacBook disconnects, provided the host remains operational.

---

## 6. Product Positioning

The product sits at the intersection of several existing computing concepts.

| Concept | Relationship |
|---|---|
| Remote Desktop | Provides remote graphical interaction |
| Application Publishing | Exposes individual remote applications |
| Parallels Coherence | Demonstrates seamless window integration |
| Thin Client Computing | Separates interaction from computation |
| Distributed Computing | Distributes workloads across devices |
| Personal Cloud | Provides privately controlled infrastructure |
| Edge Computing | Executes workloads on nearby devices |
| Universal Control | Demonstrates cross-device interaction |
| Desktop Virtualisation | Provides alternative desktop execution environments |

The initial product should be positioned as:

**A native, peer-to-peer, application-level remote access system for macOS.**

The longer-term product category could be described as:

**Personal Distributed Computing Infrastructure.**

---

## 7. Design Principles

### 7.1 Application-centric

The primary user-facing abstraction is an application or application session, not a remote computer.

### 7.2 Native-first

Use native macOS frameworks wherever practical.

Avoid unnecessary Electron applications, cross-platform abstraction layers and external runtime dependencies.

### 7.3 Local-first

The product should operate on a local network without requiring an internet connection or central cloud service.

### 7.4 Peer-to-peer

Trusted devices should communicate directly whenever possible.

Centralised coordination infrastructure should not be required for the initial product.

### 7.5 Symmetric architecture

Every participating Mac should be capable of operating as either a host or a client.

A device may perform both roles simultaneously.

### 7.6 Privacy by design

Application content, input events and credentials should remain within the user's trusted device network.

No application content should be collected for analytics.

### 7.7 Public API first

Prefer documented Apple APIs.

Private APIs may be investigated separately where they unlock important capabilities, but should not become an unquestioned architectural dependency.

### 7.8 Incremental complexity

A functional single-window remote session should precede advanced desktop integration.

### 7.9 Interoperability

Networking should not be tightly coupled to a particular VPN, cloud provider or device discovery mechanism.

### 7.10 User sovereignty

Users should retain control over device identity, authorisation, shared applications and active connections.

---

## 8. Existing Product Landscape

### 8.1 Wisp

Website: https://pier20.com/wisp

Repository: https://github.com/pier20-ai/wisp

Wisp is a particularly relevant technical reference.

Its documented approach includes:

- Individual remote application windows.
- Phantom applications on the client.
- Virtual displays.
- Tailscale connectivity.
- Native macOS integration.

Wisp demonstrates that a seamless Mac-to-Mac application streaming experience is technically achievable.

However, its use of undocumented virtual display APIs introduces compatibility and maintenance risks.

Wisp should be studied as an architectural reference before deciding whether to implement a new product, contribute upstream or develop a compatible extension.

### 8.2 oriel

Website: https://tealmac.com/oriel/

oriel demonstrates a commercial application-centric remote Mac experience.

Relevant capabilities include:

- Remote application discovery.
- Individual window sharing.
- Remote application launching.
- Audio streaming.
- Clipboard integration.
- File transfer.
- Local and remote network connectivity.

It is an important reference for product usability and feature prioritisation.

### 8.3 Parallels Desktop Coherence Mode

Parallels demonstrates the interaction model that originally inspired this project.

Its ability to present Windows applications alongside native macOS applications establishes a useful usability benchmark.

Unlike the proposed product, Parallels primarily operates across a virtualisation boundary within a computer.

### 8.4 Apple Screen Sharing

Apple Screen Sharing provides a native baseline for remote graphical interaction.

However, the standard experience is desktop-centric rather than application-centric.

It remains a useful fallback and comparison point.

### 8.5 Additional reference products

Other products worth investigating during project reactivation:

- Microsoft RemoteApp.
- Citrix Virtual Apps.
- Xpra.
- Beam.
- Wormhole.
- Jump Desktop.
- Parsec.

### 8.6 Competitive implication

Basic remote application streaming is not a unique product proposition.

Existing implementations validate the concept but also raise the threshold for differentiation.

A new implementation should only proceed if it provides meaningful advantages in extensibility, privacy, interoperability, reliability, automation or distributed workspace orchestration.

---

## 9. Proposed User Experience

### 9.1 Device discovery

The application discovers trusted Macs on the network.

Example:

- This Mac
- Mac mini — Home
- Mac Studio — AI Server
- MacBook Pro — Office

Devices may be discovered through Bonjour or manually configured using their network addresses.

### 9.2 Application discovery

Selecting a remote host displays:

- Running applications.
- Available applications.
- Open windows.
- Existing remote sessions.
- Device availability.

### 9.3 Remote application launch

The user selects an application.

The host launches the application when necessary.

The client establishes a remote graphical session and creates a corresponding local window.

### 9.4 Remote application interaction

The local window supports:

- Mouse input.
- Keyboard input.
- Scrolling.
- Window resizing.
- Focus management.
- Clipboard operations.
- Session reconnection.

The graphical interface continues to execute remotely.

### 9.5 Session persistence

Closing a client window should not automatically terminate the remote application.

The system should distinguish between:

- Disconnecting a session.
- Closing a remote window.
- Quitting a remote application.
- Terminating a host connection.

### 9.6 Native integration

Future versions may support:

- Dedicated Dock icons.
- Cmd+Tab integration.
- Mission Control.
- Remote application menu bars.
- Spotlight integration.
- Raycast integration.
- macOS Shortcuts.
- Notifications.

These capabilities should be treated as progressively advanced integration features.

---

## 10. Conceptual Architecture

```text
                 Personal Workspace
                        |
                 Local Client UI
                        |
              Distributed Session Manager
                        |
         +--------------+--------------+
         |              |              |
      Local Mac      Mac mini      Mac Studio
         |              |              |
      Local Apps    Remote Apps    Remote Apps
```

Each participating device runs a Workspace Node.

A Workspace Node contains both hosting and client capabilities.

```text
Workspace Node
├── Host Service
├── Client Service
├── Device Discovery
├── Identity Management
├── Session Manager
├── Application Registry
├── Window Manager
├── Video Streaming
├── Input Bridge
└── Transport Layer
```

The architecture should separate the application control plane from the media data plane.

---

## 11. Remote Application Streaming Architecture

```text
HOST MAC

Remote Application
        |
ScreenCaptureKit
        |
CVPixelBuffer
        |
VideoToolbox Encoder
        |
Encoded Video Stream
        |
======== Network Transport ========
        |
VideoToolbox Decoder
        |
Rendering Surface
        |
Local NSWindow

CLIENT MAC
```

Input flows in the opposite direction.

```text
Local Keyboard / Mouse
        |
AppKit Event Handling
        |
Input Normalisation
        |
Authenticated Control Channel
        |
Host Input Bridge
        |
CoreGraphics / Accessibility
        |
Remote Application
```

Separate components are responsible for graphical streaming, input delivery and window lifecycle management.

---

## 12. Proposed Technology Stack

| Component | Proposed Technology |
|---|---|
| Primary language | Swift |
| Application UI | SwiftUI |
| Window integration | AppKit |
| Screen capture | ScreenCaptureKit |
| Video encoding | VideoToolbox |
| Video decoding | VideoToolbox |
| Rendering | AVFoundation / Metal |
| Input events | CoreGraphics |
| Accessibility | AXUIElement |
| Application discovery | NSWorkspace |
| Networking | Network.framework |
| Device discovery | Bonjour / DNS-SD |
| Encryption | TLS |
| Secure storage | Keychain |
| Clipboard | NSPasteboard |
| Concurrency | Swift Concurrency |
| CLI | Swift Argument Parser |
| Configuration | Codable / JSON |
| Packaging | Xcode / Swift Package Manager |
| Distribution | Signed and notarised macOS application |
| Testing | Swift Testing / XCTest |

### Technology decision

Pure Swift is the preferred initial implementation language.

Rust is not currently required because the critical functionality depends heavily on native Apple frameworks.

Rust may be reconsidered if a portable networking core or cross-platform client becomes strategically important.

The provisional minimum deployment target is macOS 14.

The deployment target must be reassessed against actual API availability before implementation.

---

## 13. Core Technical Components

### 13.1 Application Registry

Responsible for:

- Enumerating running applications.
- Discovering installed applications.
- Tracking bundle identifiers.
- Retrieving application metadata.
- Launching applications.
- Monitoring termination events.

The registry should distinguish between installed applications, processes and individual windows.

### 13.2 Window Capture Engine

Responsible for:

- Discovering capturable windows.
- Starting and stopping capture sessions.
- Configuring frame rates and resolutions.
- Monitoring capture state.
- Handling window closure.
- Responding to resolution changes.

ScreenCaptureKit provides the initial implementation foundation.

### 13.3 Video Codec Engine

Responsible for:

- Hardware-accelerated encoding.
- Hardware-accelerated decoding.
- Bitrate configuration.
- Keyframe management.
- Frame timestamping.
- Backpressure management.
- Resolution changes.

H.264 and HEVC should be evaluated.

The initial codec decision should be based on latency, compatibility and implementation complexity rather than theoretical compression efficiency alone.

### 13.4 Transport Layer

Responsible for:

- Device connections.
- Authentication.
- Control messages.
- Media streaming.
- Heartbeats.
- Connection recovery.
- Network quality monitoring.

A reliable encrypted TCP-based transport is a reasonable starting point for a LAN prototype.

UDP, QUIC or other low-latency transports may be evaluated if measurements justify the additional complexity.

The system should avoid developing an unnecessary custom cryptographic protocol.

### 13.5 Input Bridge

Responsible for:

- Keyboard event forwarding.
- Mouse event forwarding.
- Scroll events.
- Modifier key management.
- Coordinate transformation.
- Focus management.
- Input ownership.

Remote input must only be accepted from explicitly authorised devices.

### 13.6 Window Manager

Responsible for:

- Identifying remote windows.
- Maintaining local window representations.
- Synchronising window state.
- Managing resizing.
- Tracking focus.
- Detecting application-created secondary windows.
- Handling window closure.

Window identity must be scoped to a host and session because native window identifiers are not necessarily permanent.

### 13.7 Session Manager

Responsible for managing:

- Session creation.
- Session identity.
- Application association.
- Stream lifecycle.
- Control permissions.
- Session persistence.
- Disconnections.
- Reconnection.
- Cleanup.

Suggested lifecycle:

```text
Discovered
    |
Connecting
    |
Authenticating
    |
Initialising
    |
Streaming
    |
Disconnected
    |
Reconnecting
    |
Streaming / Terminated
```

### 13.8 Device Identity and Trust

Responsible for:

- Stable device identities.
- Explicit pairing.
- Authentication.
- Authorisation.
- Credential storage.
- Trust revocation.

Network discovery must not be treated as proof of identity.

---

## 14. Control Plane and Data Plane

### Control plane

The control plane carries structured messages.

Examples:

```text
DeviceHello
PairingRequest
ListApplications
ListWindows
LaunchApplication
OpenSession
CloseSession
FocusWindow
ResizeWindow
KeyboardEvent
PointerEvent
ClipboardUpdate
SessionStatus
Heartbeat
```

Messages should be versioned and validated.

### Data plane

The data plane carries:

- Encoded video frames.
- Audio frames in future versions.
- Stream metadata.
- Frame timestamps.
- Codec configuration.

The two planes may initially share a connection but should remain logically separate.

This enables independent optimisation in later versions.

---

## 15. Window Hosting Strategies

Three possible architectural strategies have been identified.

### Strategy A: Direct window capture

Capture a specific existing application window using ScreenCaptureKit.

Advantages:

- Uses documented APIs.
- Relatively low implementation complexity.
- Suitable for an initial prototype.
- No requirement for virtual displays.

Limitations:

- Complex popup and menu handling.
- Potential issues with minimised windows.
- Host focus conflicts.
- Incomplete isolation.
- Headless behaviour requires validation.

### Strategy B: Dedicated virtual display per session

Move remote windows onto independent virtual displays.

Advantages:

- Improved window isolation.
- Potentially better resolution control.
- Less interference from unrelated windows.
- Potential headless operation.

Limitations:

- May require undocumented APIs.
- macOS compatibility risks.
- Increased WindowServer complexity.
- Additional resource consumption.
- Potential distribution restrictions.

Wisp provides a relevant reference implementation.

### Strategy C: Shared virtual workspace

Create a larger remote graphical workspace and manage several application windows within it.

Advantages:

- Potential encoder resource efficiency.
- Centralised workspace management.
- Supports multiple remote applications.

Limitations:

- Complex placement and coordinate mapping.
- Potential window overlap.
- Additional cropping and compositing requirements.

### Provisional decision

Begin with Strategy A.

Investigate Strategies B and C only after validating capture, streaming and input fundamentals.

---

## 16. Native Desktop Integration

There are three proposed levels of integration.

### Level 1 — Remote window viewer

A standard macOS application creates independent windows for remote sessions.

All remote windows belong to the same local application.

This is sufficient for the initial MVP.

### Level 2 — Remote application representation

The client associates each remote application with:

- Its original application name.
- Its icon.
- Its window title.
- Its session metadata.

The application may provide a unified launcher and window grouping.

### Level 3 — Phantom applications

Each remote application is represented by a dedicated local application identity.

Potential capabilities:

- Independent Dock icons.
- Independent Cmd+Tab entries.
- Application-specific menus.
- Native Mission Control behaviour.
- Application-specific launching.

This provides the closest experience to Parallels Coherence Mode.

However, it introduces substantial complexity involving application bundles, process identities, code signing and macOS application lifecycle behaviour.

It should be treated as a research initiative rather than an initial requirement.

---

## 17. Security and Privacy

Remote graphical control introduces significant security responsibilities.

The product must be designed as a privileged application.

### Required principles

- Explicit device pairing.
- Encrypted communication.
- Authenticated control messages.
- Revocable device trust.
- Visible remote session indicators.
- User-controlled application sharing.
- No unauthenticated remote input.
- No silent permission bypassing.
- No automatic exposure to the public internet.
- Immediate session termination controls.

### macOS permissions

Depending on the implementation, the application may require:

- Screen and System Audio Recording.
- Accessibility.
- Local Network access.
- Other permissions required by optional integrations.

Permission requirements must be documented and tested.

### Input control policy

A host must be able to reject remote input.

The initial version should assume one active controlling client per host user session.

Simultaneous independent control by multiple users should not be promised.

### Sensitive content

The application should respect platform restrictions concerning:

- Protected content.
- Secure input.
- Locked screens.
- Authentication dialogs.
- System security prompts.

These restrictions should not be bypassed.

### Credentials

Device secrets and long-lived credentials should be stored securely using Keychain.

Clipboard sharing and file transfer should be individually configurable.

---

## 18. Minimum Viable Product

### MVP objective

Validate whether an individual graphical application window can be streamed between two Macs and operated with sufficiently low latency and reliability for practical daily use.

### Included

- Two Macs on the same trusted network.
- Manual connection configuration.
- Explicit device pairing.
- Remote window discovery.
- Single-window capture.
- Hardware-assisted video encoding where available.
- Video streaming.
- Local native window rendering.
- Keyboard and mouse forwarding.
- Basic scrolling.
- Session disconnect.
- Host application persistence.
- Basic latency and resource measurements.

### Excluded

- Phantom applications.
- Virtual displays.
- Guaranteed headless operation.
- Remote menu bar integration.
- Multiple independent controlling users.
- WAN optimisation.
- Audio streaming.
- File transfer.
- Clipboard synchronisation.
- AI scheduling.
- Cross-platform clients.
- Cloud infrastructure.

The MVP should prioritise end-to-end functionality over completeness.

---

## 19. Development Roadmap

No implementation dates are committed.

### Phase 0 — Research and feasibility

Investigate:

- Wisp architecture.
- Apple sample applications.
- ScreenCaptureKit behaviour.
- Input injection restrictions.
- Transport alternatives.
- Existing open-source licensing.
- Headless operation.
- macOS version compatibility.

Deliverable: Technical feasibility report and architecture decisions.

### Phase 1 — Local capture prototype

Implement:

- Window enumeration.
- Window selection.
- Live local preview.
- Capture lifecycle management.
- Basic instrumentation.

### Phase 2 — Remote video streaming

Implement:

- Host and client connections.
- Hardware-assisted encoding and decoding.
- Native remote window rendering.
- Frame timing.
- Basic reconnect behaviour.

### Phase 3 — Interactive remote window

Implement:

- Keyboard forwarding.
- Mouse forwarding.
- Scroll forwarding.
- Focus management.
- Coordinate mapping.
- Secure session authorisation.

Completion of this phase establishes the core technical MVP.

### Phase 4 — Personal workspace

Implement:

- Multiple remote windows.
- Multiple hosts.
- Bonjour discovery.
- Remote application launcher.
- Session management.
- Basic clipboard integration.

### Phase 5 — Daily-use reliability

Investigate and implement:

- Adaptive bitrate.
- Improved reconnection.
- Audio.
- File transfer.
- Network diagnostics.
- Resource management.
- Sleep and wake handling.

### Phase 6 — Native application integration

Investigate:

- Phantom applications.
- Dock integration.
- Remote menu bars.
- Mission Control.
- Virtual displays.
- Headless operation.

### Phase 7 — Distributed workspace orchestration

Investigate:

- Resource-aware application placement.
- Distributed application search.
- CLI integrations.
- Automation.
- Raycast and Shortcuts.
- MCP integration.
- AI-assisted workload placement.

---

## 20. Validation and Success Criteria

The following are provisional engineering targets, not measured capabilities.

| Metric | Initial Target |
|---|---|
| Supported hosts | 2 Macs |
| Concurrent sessions | 1 initially |
| Frame rate | Up to 60 FPS |
| Resolution | 1080p initially |
| LAN interaction latency | Below 100 ms at p95 |
| Session startup | Below 5 seconds |
| Reconnection | Below 10 seconds |
| Encoding | Hardware-assisted where supported |
| Network dependency | Local network sufficient |
| Cloud dependency | None |
| Session endurance | At least 8 hours |
| Permission model | Explicitly authorised |

Measurements should include:

- Capture latency.
- Encoding latency.
- Network latency.
- Decoding latency.
- Rendering latency.
- Input-to-display latency.
- CPU consumption.
- Memory consumption.
- Network bandwidth.
- Dropped frames.
- Thermal behaviour.

Input-to-display latency should be measured independently rather than inferred solely from network round-trip time.

### Application compatibility matrix

Initial testing should include:

| Application | Purpose |
|---|---|
| TextEdit | Basic keyboard interaction |
| Finder | File and window operations |
| Safari | Scrolling and web interaction |
| Terminal | Keyboard-intensive workloads |
| VS Code | Development workflows |
| Xcode | Complex application behaviour |
| Preview | Document interaction |
| System Settings | Permission and compatibility boundaries |

Complex graphical, protected-content and system-level applications should be evaluated separately.

---

## 21. Technical Risks

| Risk | Severity | Mitigation |
|---|---|---|
| WindowServer instability | High | Public APIs first; isolate experimental features |
| Private API changes | High | Avoid mandatory private API dependencies |
| Remote focus conflicts | High | Define explicit input ownership |
| Popup and dialog capture | High | Research application-level session tracking |
| macOS permission restrictions | High | Early feasibility testing |
| Headless compatibility | High | Treat as a separate research milestone |
| Remote control security | High | Explicit pairing, authentication and revocation |
| Network latency | Medium | Instrumentation and adaptive streaming |
| Multi-window resource consumption | Medium | Limit concurrency and measure encoder capacity |
| Retina text quality | Medium | Evaluate resolution and scaling strategies |
| Clipboard privacy | Medium | Optional, session-scoped synchronisation |
| Distribution limitations | Medium | Research signing and notarisation early |
| Existing product competition | High | Evaluate build versus buy before committing |

The most significant engineering risk is not basic video streaming.

It is achieving a seamless, reliable and secure application-level abstraction over macOS window management.

---

## 22. CLI Concept

The command-line interface should eventually expose the same capabilities as the graphical application.

Illustrative commands:

```bash
workspace hosts

workspace pair mac-mini

workspace apps --host mac-mini

workspace windows --host mac-mini

workspace open Xcode --host mac-mini

workspace open Terminal --host mac-studio

workspace sessions

workspace disconnect session-123

workspace status

workspace doctor
```

Future scheduling examples:

```bash
workspace open Xcode --auto

workspace open Terminal --host least-loaded

workspace open MyAIApp --require-memory 64GB
```

These commands are conceptual and do not constitute a final CLI contract.

---

## 23. Proposed Repository Structure

```text
distributed-workspace/
├── Package.swift
├── Workspace.xcodeproj/
├── Sources/
│   ├── WorkspaceApp/
│   ├── WorkspaceCLI/
│   ├── WorkspaceCore/
│   ├── HostService/
│   ├── ClientService/
│   ├── ApplicationRegistry/
│   ├── SessionManager/
│   ├── WindowCapture/
│   ├── WindowManager/
│   ├── VideoCodec/
│   ├── InputBridge/
│   ├── Transport/
│   ├── Discovery/
│   ├── DeviceIdentity/
│   └── Protocol/
├── Tests/
├── Examples/
├── docs/
│   ├── IDEATION.md
│   ├── ARCHITECTURE.md
│   ├── PRD.md
│   ├── SECURITY.md
│   └── adr/
├── AGENTS.md
├── README.md
└── LICENSE
```

The repository structure is indicative.

Module boundaries should be revisited following feasibility experiments.

---

## 24. Long-Term Opportunities

### 24.1 Personal Compute Fabric

Multiple personal computers become a discoverable pool of application execution environments.

The system could eventually expose host capabilities such as:

- Available memory.
- CPU utilisation.
- GPU capabilities.
- Supported applications.
- Network availability.
- Power state.

### 24.2 Resource-aware application scheduling

Applications may be launched on a host selected according to user-defined policies.

Example policies:

- Prefer always-on hosts.
- Prefer hosts with sufficient memory.
- Prefer low-latency devices.
- Prefer hosts containing required software.
- Prefer energy-efficient devices.

This is workload placement, not transparent hardware aggregation or live process migration.

### 24.3 Agent-native computing

AI agents could eventually discover and select execution environments.

An agent might identify an available development Mac, launch an application and establish an authorised interaction session.

Potential integrations include:

- MCP.
- Coding agents.
- Personal assistants.
- Agent harnesses.
- Automation workflows.

Agent access must remain subject to the same explicit permission and trust boundaries as human access.

### 24.4 Distributed application launcher

A single application launcher could search across installed applications on multiple computers.

For example:

```text
Xcode
  ├── MacBook Pro
  └── Mac mini

AI Workbench
  └── Mac Studio

Safari
  ├── This Mac
  ├── Mac mini
  └── Mac Studio
```

The user selects the application without first manually connecting to its host.

### 24.5 Unified personal AI infrastructure

Always-on Mac devices could host:

- Local LLM servers.
- Coding agents.
- Vector databases.
- Personal knowledge systems.
- Background automation.
- Development environments.

Distributed macOS Workspace would provide a graphical interaction layer for these services, complementing SSH, HTTP APIs and command-line interfaces.

### 24.6 Cross-platform expansion

Potential future clients include:

- iPadOS.
- iOS.
- Linux.
- Windows.
- Web browsers.

Cross-platform support should not compromise the initial native macOS experience.

---

## 25. Build Versus Buy Assessment

Before allocating development resources, the project should be evaluated against four possible approaches.

| Approach | Description |
|---|---|
| Buy | Adopt an existing product such as oriel |
| Contribute | Improve an existing open-source project |
| Extend | Build orchestration or integrations around existing streaming technology |
| Build | Develop a new implementation |

Building an entire remote application streaming stack may not be justified if existing products satisfy the core personal use case.

The strongest rationale for independent development would be:

- Full architectural control.
- Open-source extensibility.
- CLI-first operation.
- Automation integration.
- Distributed application discovery.
- Resource-aware workload placement.
- Agent-native capabilities.
- Vendor independence.

The project should not recreate existing functionality solely because it is technically interesting.

---

## 26. Preliminary Architecture Decisions

| ID | Decision | Status |
|---|---|---|
| ADR-001 | Application-centric rather than desktop-centric | Proposed |
| ADR-002 | Native Swift implementation | Proposed |
| ADR-003 | SwiftUI and AppKit for UI | Proposed |
| ADR-004 | Symmetric host and client architecture | Proposed |
| ADR-005 | Local-first and peer-to-peer connectivity | Proposed |
| ADR-006 | ScreenCaptureKit for initial capture | Proposed |
| ADR-007 | VideoToolbox for codec implementation | Proposed |
| ADR-008 | Public Apple APIs first | Proposed |
| ADR-009 | Separate logical control and media planes | Proposed |
| ADR-010 | Direct window capture for MVP | Proposed |
| ADR-011 | Explicit device pairing and trust | Proposed |
| ADR-012 | CLI and GUI share a common core | Proposed |
| ADR-013 | Virtual displays deferred | Proposed |
| ADR-014 | No mandatory central cloud infrastructure | Proposed |
| ADR-015 | Evaluate existing implementations before building | Proposed |

These decisions are provisional.

Formal ADRs should be created after project reactivation and technical validation.

---

## 27. Open Research Questions

1. Can ScreenCaptureKit reliably capture minimised or occluded windows across supported macOS versions?

2. How should application-created dialogs, contextual menus and popups be represented remotely?

3. Can remote input be reliably targeted without interfering with other host applications?

4. What limitations exist when the host has no physical display?

5. Can multiple remote windows share a hardware encoder efficiently?

6. How many concurrent encoding sessions can different Apple Silicon devices sustain?

7. Can independent Dock entries be implemented using documented APIs and supported application bundle mechanisms?

8. What is the most reliable approach to remote menu bar integration?

9. How should local and remote window resizing be synchronised?

10. Is a TCP-based transport sufficient for the intended LAN-first experience?

11. Would QUIC provide measurable advantages for remote operation over less reliable networks?

12. How should device identities and application-level permissions be managed?

13. How should the system respond to sleep, screen locking and user switching?

14. Can existing open-source projects provide reusable components without undesirable licensing or architectural constraints?

15. Would a thin orchestration layer over Wisp or another streaming product provide greater value than a complete implementation?

---

## 28. Project Naming

The name is intentionally undecided.

Potential naming directions:

| Name | Concept |
|---|---|
| AppMesh | Network of distributed applications |
| MacMesh | Interconnected Mac devices |
| AppBridge | Applications crossing device boundaries |
| Continuum | Continuous multi-device computing |
| Relay | Application interaction relay |
| Habitat | Unified personal computing environment |
| Workfabric | Distributed workspace infrastructure |
| MacFabric | Personal Mac computing fabric |
| Node | Device-independent workspace node |
| a-relay | Minimal Apple-oriented developer utility |

These names are brainstorming candidates only.

Availability, trademarks, repository conflicts and existing product names have not been investigated.

---

## 29. Reference Material

### Existing products

- Wisp: https://pier20.com/wisp
- Wisp repository: https://github.com/pier20-ai/wisp
- oriel: https://tealmac.com/oriel/
- oriel features: https://tealmac.com/oriel/features

### Apple developer documentation

- ScreenCaptureKit: https://developer.apple.com/documentation/screencapturekit
- Capturing screen content: https://developer.apple.com/documentation/screencapturekit/capturing-screen-content-in-macos
- VideoToolbox: https://developer.apple.com/documentation/videotoolbox
- Low-latency video encoding: https://developer.apple.com/documentation/videotoolbox/encoding-video-for-low-latency-conferencing
- Network Framework: https://developer.apple.com/documentation/network
- AppKit: https://developer.apple.com/documentation/appkit
- CoreGraphics: https://developer.apple.com/documentation/coregraphics

All references should be revalidated when the project is resumed.

---

## 30. Project Reactivation Protocol

When revisiting this project:

1. Review this Ideation Record.

2. Reassess the original problem and personal computing requirements.

3. Review the current capabilities of Wisp, oriel and competing products.

4. Determine whether the problem has already been adequately solved.

5. Evaluate build, buy, contribute and extend strategies.

6. Reassess Apple API availability and macOS restrictions.

7. Select a provisional deployment target.

8. Create a concise Product Requirements Document.

9. Conduct a technical feasibility spike.

10. Record validated architectural decisions.

11. Define MVP acceptance criteria.

12. Produce an Engineering Handoff.

13. Establish a project backlog and implementation milestones.

Recommended documentation progression:

```text
IDEATION.md
     |
     v
Feasibility Report
     |
     v
PRD.md
     |
     v
ARCHITECTURE.md + ADRs
     |
     v
Engineering Handoff
     |
     v
Implementation Backlog
     |
     v
MVP
```

---

## 31. Parking Decision

**Project status: PARKED**

The concept demonstrates sufficient technical feasibility and potential personal utility to justify preservation.

However:

- Existing products already validate and partially satisfy the use case.
- Independent implementation requires substantial engineering effort.
- Several important macOS integration challenges remain unresolved.
- Differentiation has not yet been validated.
- No implementation resources have been committed.

The idea should be revisited when there is a concrete requirement that existing solutions cannot adequately fulfil, or when distributed personal computing becomes a strategic priority.

No implementation, repository creation, product naming commitment or delivery schedule is authorised by this document.

---

## 32. Closing Thesis

The conventional personal computer combines the user interface, applications and computational resources within a single physical device.

Increasingly, those responsibilities do not need to reside on the same machine.

A future personal computing environment may instead consist of multiple specialised devices connected through a unified application experience.

The laptop becomes an interaction surface.

The desktop becomes a compute node.

The always-on server becomes persistent infrastructure.

The application becomes independent of its physical execution location from the user's perspective.

Distributed macOS Workspace explores how this future could be achieved using existing Mac hardware, native operating system capabilities and privately controlled networking.

**One workspace. Multiple machines. Applications without device boundaries.**

---

*End of Project Ideation Record.*