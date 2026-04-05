# 🔓 UnCrackable-Level3 - Solution

[![Platform](https://img.shields.io/badge/platform-Android-brightgreen.svg)](https://developer.android.com)
[![Tools](https://img.shields.io/badge/tools-Ghidra%20%7C%20apktool%20%7C%20jadx-blue.svg)](https://ghidra-sre.org/)
[![License](https://img.shields.io/badge/license-Educational%20Use-orange.svg)](LICENSE)

## 📋 Table of Contents
- [Challenge Description](#-challenge-description)
- [Protections Bypassed](#-protections-bypassed)
- [Tools Used](#-tools-used)
- [Solution Walkthrough](#-solution-walkthrough)
- [Files Structure](#-files-structure)
- [Quick Test](#-quick-test)
- [Key Learnings](#-key-learnings)
- [References](#-references)

---

## 🎯 Challenge Description

This repository contains a complete solution for the **OWASP MSTG Crackme Level 3**. 

The application is an Android crackme that:
- Verifies a **24-character secret code**
- Implements validation logic in **native code** (`libfoo.so`)
- Uses multiple **anti-tampering** protections
- Stores the secret in **XOR-encoded** format

**Objective:** Extract the secret code by bypassing all protections.

---

## 🛡️ Protections Bypassed

| Protection | Implementation | Bypass Method |
|------------|----------------|----------------|
| **Root Detection** | 3 different `checkRoot()` methods | Smali patch (`return-void`) |
| **Anti-Debug** | `ptrace` system calls | RET instruction patch |
| **Anti-Frida** | `/proc/self/maps` scanning | RET instruction patch |
| **Integrity Checks** | CRC verification of `.so` and `classes.dex` | Smali variable override |
| **Code Obfuscation** | LCG + malloc chains in native code | Static analysis of `.rodata` |
| **XOR Encoding** | Secret stored encoded in memory | XOR decryption with found key |

---

## 🔧 Tools Used

| Tool | Purpose | Version |
|------|---------|---------|
| **jadx-gui** | Java bytecode decompilation | 1.5.0+ |
| **apktool** | APK decompilation/rebuilding | 3.0.1 |
| **Ghidra** | Native binary analysis & patching | 11.0+ |
| **apksigner** | APK signing for installation | build-tools 36.1.0 |
| **adb** | Emulator/device communication | Latest |
| **Python** | XOR decryption script | 3.x |

---

<img width="880" height="292" alt="verifyLibs1" src="https://github.com/user-attachments/assets/e0cb41ab-349f-424f-9a3c-7d1b7abf7ae3" />
<img width="943" height="212" alt="FUN" src="https://github.com/user-attachments/assets/acb9ac22-c891-4276-8f0f-081544a96272" />
<img width="447" height="59" alt="ret" src="https://github.com/user-attachments/assets/3c00b3df-2a95-45ad-a8d9-34fe7b9c3287" />
<img width="202" height="395" alt="mdp" src="https://github.com/user-attachments/assets/3f438552-264d-45b7-8e15-836808dd31ed" />
<img width="178" height="293" alt="correctt" src="https://github.com/user-attachments/assets/812e9fe0-af38-4580-b27c-79dc777e8c3a" />

