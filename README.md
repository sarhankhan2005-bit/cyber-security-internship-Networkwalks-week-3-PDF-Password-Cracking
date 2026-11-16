# PDF Hash Extraction & Password Cracking Lab Report

**Researcher / Intern:** Sarhan Khan  
**Program:** Networkwalks Cybersecurity Internship  
**Tools Used:** Networkwalks Tool (Lab 1) & John the Ripper (Lab 2)  
**Target Encryption:** PDF 1.4 / 128-bit Encryption (`$pdf$4*4*128`)

---

## 1. Executive Summary

This repository documents two hands-on password auditing and offline hash-cracking labs conducted on password-protected PDF files:
- **Lab 1 (Networkwalks Tool):** Extracted and cracked password hashes for three locked PDF documents (`My-Locked-PDF1` to `My-Locked-PDF3`).
- **Lab 2 (John the Ripper):** Extracted PDF encryption hashes using `pdf2john` and performed dictionary-based offline password recovery using **John the Ripper** (`john`) with the `rockyou.txt` wordlist.

---

## 2. Combined Summary Overview

| Lab / Tool Used | Order | Hash File Name | Cracked Password | Encryption Format |
| :--- | :---: | :--- | :--- | :--- |
| **Lab 1 — Networkwalks Tool** | 1 | `My-Locked-PDF1.hash.txt` | `password1` | PDF 1.4 / 128-bit (`$pdf$4*4*128`) |
| **Lab 1 — Networkwalks Tool** | 2 | `My-Locked-PDF2.hash.txt` | `password1` | PDF 1.4 / 128-bit (`$pdf$4*4*128`) |
| **Lab 1 — Networkwalks Tool** | 3 | `My-Locked-PDF3.hash.txt` | `1qaz2wsx` | PDF 1.4 / 128-bit (`$pdf$4*4*128`) |
| **Lab 2 — John the Ripper** | 1 | `hashpdf1.txt` | `good-luck` | PDF 1.4 / 128-bit (`$pdf$4*4*128`) |
| **Lab 2 — John the Ripper** | 2 | `hashpdf2.txt.txt` | `password1` *(matched hash)* | PDF 1.4 / 128-bit (`$pdf$4*4*128`) |
| **Lab 2 — John the Ripper** | 3 | `hashpdf3.txt` | `1qaz2wsx` | PDF 1.4 / 128-bit (`$pdf$4*4*128`) |

---

## 3. Part A — Lab 1: Networkwalks Tool Results

### 3.1 PDF 1 (`My-Locked-PDF1.hash.txt`)
- **Tool Used:** Networkwalks Tool
- **Cracked Password:** `password1`
- **Extracted Hash:**
```text
$pdf$4*4*128*-1060*1*16*55d1a5c14175da449753199e44971d32*32*777fd021a7f3c5ae598c0c6495c7f76e00000000000000000000000000000000*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
```

### 3.2 PDF 2 (`My-Locked-PDF2.hash.txt`)
- **Tool Used:** Networkwalks Tool
- **Cracked Password:** `password1`
- **Extracted Hash:**
```text
$pdf$4*4*128*-1028*1*16*0853f2cde0ef15b1c0f93ed229d3b1ad*32*8f13ce5aa39ad974364d36a057da76790021446990b9e4114071a4d9104984c1*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
```

### 3.3 PDF 3 (`My-Locked-PDF3.hash.txt`)
- **Tool Used:** Networkwalks Tool
- **Cracked Password:** `1qaz2wsx`
- **Extracted Hash:**
```text
$pdf$4*4*128*-1028*1*16*34eb542eff4e1b0b32d25ce15a9a7281*32*b77872bfc9a24fb2f845066283a8fc1b0021446990b9e4114071a4d9104984c1*32*e7572256e4b552cd57988f5134214b91920d94d7a6bf550ea94a2995c7f2ab02
```

---

## 4. Part B — Lab 2: John the Ripper Results

### 4.1 Commands Used (Kali Linux)
```bash
# Step 1: Extract PDF password hash
pdf2john locked-file.pdf > hashpdf.txt

# Step 2: Crack hash using John the Ripper and rockyou wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt hashpdf.txt

# Step 3: Display recovered plaintext password
john --show hashpdf.txt
```

### 4.2 PDF 1 (`hashpdf1.txt`)
- **Tool Used:** John the Ripper
- **Cracked Password:** `good-luck`
- **Extracted Hash:**
```text
$pdf$4*4*128*-1028*1*16*ca7f72f11459cba469f1005a8765ed51*32*f32d8fa1bfbe2648226dffc39f7909ea0021446990b9e4114071a4d9104984c1*32*9322f50c29569712067a775264635e4954ccb1b99e209d664984054ffad30a6a
```

### 4.3 PDF 2 (`hashpdf2.txt.txt`)
- **Tool Used:** John the Ripper
- **Cracked Password:** `password1` *(Hash matches PDF 2 from Lab 1)*
- **Extracted Hash:**
```text
$pdf$4*4*128*-1028*1*16*0853f2cde0ef15b1c0f93ed229d3b1ad*32*8f13ce5aa39ad974364d36a057da76790021446990b9e4114071a4d9104984c1*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
```

### 4.4 PDF 3 (`hashpdf3.txt`)
- **Tool Used:** John the Ripper
- **Cracked Password:** `1qaz2wsx`
- **Extracted Hash:**
```text
$pdf$4*4*128*-1028*1*16*34eb542eff4e1b0b32d25ce15a9a7281*32*b77872bfc9a24fb2f845066283a8fc1b0021446990b9e4114071a4d9104984c1*32*e7572256e4b552cd57988f5134214b91920d94d7a6bf550ea94a2995c7f2ab02
```

---

## 5. Key Findings & Security Recommendations

1. **Dictionary & Keyboard-Pattern Passwords:** Passwords such as `password1`, `1qaz2wsx`, and `good-luck` appear in standard password wordlists (`rockyou.txt`) and are cracked within seconds during offline attacks.
2. **Legacy PDF Encryption (`$pdf$4*4*128`):** All six PDF files rely on PDF 1.4 / 128-bit encryption, which allows rapid hash verification compared to modern AES-256 standards.
3. **Remediation:**
   - Use strong, randomly generated passphrases of at least **14–16 characters** mixing uppercase, lowercase, numbers, and symbols.
   - Upgrade PDF security settings to **AES-256 encryption** (PDF 1.7 ExtensionLevel 3 / PDF 2.0).

---

## Disclaimer
*All testing in this repository was conducted strictly in a controlled educational lab environment for authorized cybersecurity training.*<img width="1438" height="723" alt="WhatsApp Image 2026-11-16 at 12 07 38 PM" src="https://github.com/user-attachments/assets/d3adef9e-fb1f-4936-aa97-dd0ad3d0af3e" />
<img width="1288" height="1027" alt="WhatsApp Image 2026-11-16 at 12 16 11 PM" src="https://github.com/user-attachments/assets/3a70c7c9-2805-4648-be40-5af1d01213c0" />
<img width="1288" height="1027" alt="WhatsApp Image 2026-11-16 at 12 16 11 PM" src="https://github.com/user-attachments/assets/117ac40d-e692-4efa-b9bc-f3948f35356a" />
<img width="1577" height="1010" alt="WhatsApp Image 2026-11-16 at 12 17 02 PM" src="https://github.com/user-attachments/assets/f8cd9b63-3a44-456b-8612-b2c212a52cab" />
<img width="1600" height="865" alt="WhatsApp Image 2026-11-16 at 11 21 26 AM" src="https://github.com/user-attachments/assets/84402c00-91df-4c3c-bc8b-4d5f8cba4b30" />
<img width="1600" height="846" alt="WhatsApp Image 2026-11-16 at 11 13 25 AM" src="https://github.com/user-attachments/assets/8e23c103-354d-44d3-b7fd-b055d7371115" />
<img width="1537" height="908" alt="WhatsApp Image 2026-11-16 at 11 12 58 AM" src="https://github.com/user-attachments/assets/2bce2387-2eb8-4535-b2c4-54de1232dffa" />
<img width="1422" height="867" alt="WhatsApp Image 2026-11-16 at 11 11 37 AM" src="https://github.com/user-attachments/assets/b8b45fa6-8efc-4f45-9be9-905b21e23612" />
# cyber-security-internship-Networkwalks-week-3-PDF-Password-Cracking
PDF Hash Extraction &amp; Offline Password Cracking Lab using Networkwalks Tool and John the Ripper (Networkwalks Cybersecurity Internship)
