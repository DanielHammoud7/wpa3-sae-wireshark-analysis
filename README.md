# WPA3 SAE & EAPOL Handshake Analysis

A hands-on technical deep-dive and Wireshark packet analysis exploring how **WPA3 (Wi-Fi Protected Access 3)** replaces WPA2 vulnerabilities with the **Simultaneous Authentication of Equals (SAE)** Dragonfly key exchange. This project provides real packet captures, visual breakdowns, and cryptographic explanations.

---

## 📚 Project Purpose

This project was built as a hands-on study resource for the **CompTIA Security+ Network Enterprise Security domain**, specifically WPA2/WPA3 authentication protocols. Rather than just reading about wireless security concepts, this repository demonstrates **how WPA3 SAE actually works** by capturing, analyzing, and explaining real Wireshark frames.

The goal is to bridge the gap between theory and practice: understanding not just *what* WPA3 does, but *why* it's more secure than WPA2 by examining the actual packet flow, cryptographic operations, and attack mitigation built into the protocol.

---

## 🎯 What You'll Learn

* **SAE Dragonfly Handshake:** Break down the Commit and Confirm phases step-by-step with real packet examples
* **Packet-Level Analysis:** Inspect raw Wireshark frames showing Scalar, Finite Field Element, ANonce, SNonce, and MIC fields
* **Why Offline Attacks Fail:** Understand how dynamic PMK derivation and ECDH make WPA3 resistant to dictionary attacks
* **WPA2 vs WPA3:** See concretely why WPA2's static PSK-based approach is vulnerable and how WPA3 fixes it

---

## 📂 What's Inside

### `/docs` Folder
This folder contains the complete technical walkthrough:

- **`01-sae-dragonfly-handshake.md`**
  - Explains the SAE Commit phase: how both devices map the password to an elliptic curve
  - Explains the SAE Confirm phase: mutual validation via confirmation tokens
  - Includes annotated Wireshark screenshots of actual commit and confirm frames
  - Key takeaway: the password is *never* transmitted; only derived cryptographic values cross the air

- **`02-eapol-4way-handshake.md`**
  - Details the 4-message EAPOL key exchange specific to WPA3
  - Breaks down each message: ANonce, SNonce, MIC, and GTK distribution
  - Explains why offline dictionary attacks are ineffective under WPA3
  - Key takeaway: the dynamic PMK cannot be cracked from captured handshake traffic

- **`PassPort_AX_5_WPA3-SAE.pcapng`**
  - Real Wireshark packet capture of a complete WPA3 SAE handshake
  - Source: TP-Link PassPort AX5 router with WPA3 enabled
  - Contains all SAE Commit/Confirm and EAPOL frames needed for full analysis
  - Load this in Wireshark and follow the `/docs` guides to see each frame live

### Root Files
- **`filters.txt`** - Essential Wireshark display filters to isolate SAE and EAPOL traffic
- **`/images`** - Annotated screenshots showing key packet fields and protocol stages

---

## 🔍 How to Use This Repo

### Quick Start
1. **Read the context:** Start with `docs/01-sae-dragonfly-handshake.md` for the SAE overview
2. **Open the capture:** Load `docs/PassPort_AX_5_WPA3-SAE.pcapng` in Wireshark
3. **Apply filters:** Use the filters in `filters.txt` to isolate relevant frames
4. **Follow the walkthrough:** Cross-reference the packet screenshots in `/images` with the real capture
5. **Read the implications:** Finish with `docs/02-eapol-4way-handshake.md` to understand why WPA3 is more secure

### Command-Line Workflow
```bash
# View capture summary
tshark -r docs/PassPort_AX_5_WPA3-SAE.pcapng -Y 'wlan.fc.type_subtype == 0xb0 || wlan.fc.type_subtype == 0x00 || eapol' -T text

# Extract all authentication/association frames
tshark -r docs/PassPort_AX_5_WPA3-SAE.pcapng -Y 'wlan.fc.type_subtype == 0xb0 || wlan.fc.type_subtype == 0x00'

# Extract all EAPOL frames
tshark -r docs/PassPort_AX_5_WPA3-SAE.pcapng -Y 'eapol'
```

---

## 🔐 Key Security Insights

| Aspect | WPA2 | WPA3 SAE |
|--------|------|----------|
| **Password Transmission** | Pre-Shared Key (PSK) hashed and used in HMAC | Password never transmitted; mapped to elliptic curve point |
| **Key Derivation** | Static PMK derived from PSK | Dynamic PMK derived per-connection via ECDH |
| **Offline Attack** | Feasible: capture handshake, brute-force PSK | Ineffective: PMK changes every session |
| **Handshake** | 4-way EAPOL only | SAE Dragonfly (Commit/Confirm) + 4-way EAPOL |
| **Defense** | Vulnerable to dict attacks if weak PSK | Resistant to dict attacks even with weak PSK |

---

## 🚀 Learning Path

This repo is designed for:
- **Security+ Candidates** studying the Network Enterprise Security domain
- **Wireless Network Engineers** wanting to understand WPA3 implementation details
- **Cybersecurity Professionals** interested in hands-on protocol analysis
- **Students** who prefer "learning by seeing" over just reading theory

The philosophy: **Deep understanding requires hands-on evidence.** Theory without packet analysis is incomplete; this repo provides both.

---

## 📝 Files & What to Look For

| File | Purpose | What to Notice |
|------|---------|-----------------|
| `01-sae-dragonfly-handshake.md` | SAE protocol walkthrough | Scalar/FE values, no password in payload |
| `02-eapol-4way-handshake.md` | EAPOL key exchange | ANonce, SNonce, MIC, why offline attacks fail |
| `PassPort_AX_5_WPA3-SAE.pcapng` | Real capture | Frame sequence, field values, timing |
| `filters.txt` | Wireshark filters | How to isolate the handshake from noise |
| `/images` | Annotated frames | Visual layout of each message type |

---

## 🛠️ Next Steps

- Open the PCAP in Wireshark and apply the filters
- Compare the commit frames in your capture to the annotated screenshots
- Trace through the entire handshake from first SAE Commit to final EAPOL Message 4
- Research the Dragonfly algorithm (RFC 7748) for even deeper understanding

---

## 📖 References

- [IEEE 802.11ax (Wi-Fi 6) SAE Standard](https://standards.ieee.org/standard/802_11ax-2021.html)
- [RFC 7748: Elliptic Curves for Security](https://tools.ietf.org/html/rfc7748)
- [CompTIA Security+ Exam Objectives](https://www.comptia.org/certifications/security)
- Wireshark Protocol Analysis Guide

---

## 💡 Author's Note

This project embodies the principle that **cyber security requires hands-on understanding, not just reading.** Too much security education stops at theory; this repo goes further by providing real evidence.

Built as a proof of deep understanding for the CompTIA Security+ certification, with the belief that the cybersecurity world needs practitioners who can explain protocols at the packet level, not just at a conceptual level.

Hope this repo helps you understand WPA3 at a deeper level. 🔒

