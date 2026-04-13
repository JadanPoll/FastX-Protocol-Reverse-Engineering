FastX Protocol v10.0

The canonical wire-level reference and real-time debugger for the **WARP-Web** binary protocol, specifically tailored for the **UIUC EWS** environment.

---

## 🛰️ Overview

This userscript provides a complete, 100% (on a happy day of course) decoded mapping of the proprietary WebSocket protocol used by FastX 3. Since no public documentation for the WARP protocol exists as of 2026, this tool serves as the primary technical specification for developers and researchers working within the University of Illinois Engineering Workstation ecosystem.

### Key Protocol Milestones Decoded:
* **Checksum Verification:** Fully implemented the 128-byte alignment formula:
    $$\text{checksum} = (\text{len} + \text{ceil128}(\text{len})) \land 0\text{xFFFF}$$
* **Tier Multiplexing:** Full separation and parsing for **Tier 0x00** (Control), **Tier 0x01** (Aux/Clipboard), and **Tier 0x02** (JSON-RPC).
* **Geometry Engine:** Precise mapping of `0x05` (Screen Info), `0x0c` (Resolution Ack), and `0x0a` (Geometry Hints).
* **Image Reconstruction:** Extraction logic for JPEG/PNG tiles (`0x0d`) and full-screen PNG updates (`0x1c`).

---

## Features

* **Real-time Interception:** Proxies native WebSockets to capture and classify binary frames without disrupting the session.
* **Integrated UI Panel:** A low-profile, draggable dashboard to monitor packet flow, filter noise (like mouse movements or pings), and track opcode frequency.
* **Binary Data Export:**
    * **JSON Capture:** Download the entire session state for external analysis.
    * **Image Extraction:** Save individual frame tiles or the first captured screen state directly to disk.
* **Clipboard Sniffing:** Automatically reconstructs text and image data sent over the `aux_data_send` channel.

---

## 🛠 Installation

1.  Install the **Tampermonkey** browser extension.
2.  Create a new script and paste the contents of `fastx_interceptor.user.js`.
3.  Navigate to any UIUC EWS FastX session (e.g., `fastx.ews.illinois.edu`).
4.  The ZeroLabs debug panel will appear in the bottom-left corner.

---

## 📜 Technical Reference

| Opcode | Name | Description |
| :--- | :--- | :--- |
| **0x02** | `handshake` | Initial role negotiation (Client/Server) |
| **0x04** | `token` | **Warning:** Plaintext authentication token transmission |
| **0x0d** | `image_tile` | JPEG/PNG tile with coordinate-based origin |
| **0x1c** | `image_screen_png` | Full-canvas lossless region update |
| **0x20** | `cursor_update` | Remote hotspot and bitmap synchronization |

---

## ⚖️ License & Ethics

Developed by **ZeroLabs**. This tool is intended for **educational and debugging purposes only**. Ensure you adhere to the UIUC University Policy on Responsible Computing when utilizing this interceptor on university infrastructure.

---
