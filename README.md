# WPA3 SAE & EAPOL Handshake Analysis

A technical deep-dive and Wireshark capture analysis exploring how **WPA3 (Wi-Fi Protected Access 3)** secures wireless networks by replacing legacy WPA2 vulnerabilities with the **Simultaneous Authentication of Equals (SAE)** handshake and **Elliptic Curve Diffie-Hellman (ECDH)** key exchange.

---

## 🎯 Project Objectives
* **Demystify WPA3 SAE:** Break down the Commit and Confirm phases of the Dragonfly handshake.
* **Inspect Raw Packets:** Analyze Wireshark captures of Scalar, Finite Field Element, ANonce, SNonce, and MIC fields.
* **Understand Attack Mitigation:** Demonstrate why WPA3 renders offline dictionary attacks ineffective compared to WPA2.

---

## 📂 Directory Overview
* [`/docs`](./docs): Comprehensive markdown breakdowns of the SAE Dragonfly cryptographic exchange and the modified EAPOL 4-way handshake.
* [`/captures`](./captures): Wireshark display filter references and capture documentation notes.

---

## 🔍 Key Security Takeaways
1. **Zero Cleartext/Hashed Password Transmission:** The password never traverses the air. Devices use ECDH to collaboratively derive a shared secret.
2. **Forward Secrecy & Dynamic PMK:** Each connection generates a unique Pairwise Master Key (PMK). Sniffing air traffic and capturing the handshake later yields zero cracking vector.

---

## 🚀 Author
I built this project as a prove of really deep understanding of Secure Network Enterprise Topic in CompTIA Security+ Certificate.
Which I believe Cyber world needs actions and deep understanding with hands on stuffs , not reading and skip pages 

hope you find this repo useful:)



