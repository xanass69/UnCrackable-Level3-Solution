\# UnCrackable-Level3 - Solution



\## Challenge Description

This is a solution for the OWASP MSTG Crackme Level 3. The application verifies a 24-character secret code through native code obfuscation and implements multiple anti-tampering protections.



\## Protections Bypassed

\- ✅ Root detection (3 different methods)

\- ✅ Anti-debug (ptrace)

\- ✅ Anti-Frida detection (/proc/self/maps scanning)

\- ✅ Integrity checks (CRC verification)

\- ✅ XOR-encoded secret in native library



\## Tools Used

\- \*\*jadx-gui\*\* - Java decompilation

\- \*\*apktool\*\* - APK decompilation/rebuilding

\- \*\*Ghidra\*\* - Native library analysis

\- \*\*apksigner\*\* - APK signing

\- \*\*adb\*\* - Installation on emulator



\## Solution Steps



\### 1. Java Layer Patching (smali)

Patched `MainActivity.smali` to bypass root detection:



\# Replaced dialog call with return-void

:cond\_0

return-void



2\. Native Layer Patching

Patched FUN\_001030d0 in libfoo.so:



assembly

\# Original anti-debug function start

001030d0 fc 5f bc a9    stp x28, x23, \[sp, #-0x40]!



\# Patched with RET instruction

001030d0 c0 03 5f d6    ret

3\. Secret Extraction

The encoded key was found in .rodata section at DAT\_001034b0:



python

\# decode\_key.py

encoded = bytes.fromhex("1d0811130f1749150d0003195a1d1315080e5a0017081314")

xor\_key = b"pizzapizzapizzapizzapizzapizza"

secret = bytes(a ^ b for a, b in zip(encoded, xor\_key))

print(f"Secret: {secret.decode()}")

Result: making owasp great again



Files Included

text

UnCrackable-Level3-Solution/

├── apk\_patched/

│   └── UnCrackable-Level3-patched-final.apk

├── lib\_patched/

│   └── libfoo\_patched.so

├── scripts/

│   └── decode\_key.py

├── analysis/

│   └── (Ghidra project files)

└── README.md

Key Learnings

Obfuscation patterns: LCG + malloc chains = Tigress/O-LLVM signature



Anti-debug bypass: RET patch at function entry is highly effective



XOR encoding: Secret data often stored encoded in .rodata


<img width="880" height="292" alt="verifyLibs1" src="https://github.com/user-attachments/assets/e0cb41ab-349f-424f-9a3c-7d1b7abf7ae3" />
<img width="943" height="212" alt="FUN" src="https://github.com/user-attachments/assets/acb9ac22-c891-4276-8f0f-081544a96272" />
<img width="447" height="59" alt="ret" src="https://github.com/user-attachments/assets/3c00b3df-2a95-45ad-a8d9-34fe7b9c3287" />
<img width="202" height="395" alt="mdp" src="https://github.com/user-attachments/assets/3f438552-264d-45b7-8e15-836808dd31ed" />
<img width="178" height="293" alt="correctt" src="https://github.com/user-attachments/assets/812e9fe0-af38-4580-b27c-79dc777e8c3a" />






Follow the data: Focus on final buffer writes, not obfuscation noise



Verification

bash

\# Install patched APK

adb install apk\_patched/UnCrackable-Level3-patched-final.apk



\# Enter secret

making owasp great again

\# Expected output: "Success!"

