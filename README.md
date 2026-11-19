Week 3 – Cryptographic Hash Extraction & Password Strength Auditing

Programme: Cybersecurity & Ethical Hacking Internship – Networkwalks (in collaboration with Waqas Karim, CCIE)

Focus Areas: Offline Password Auditing, Cryptographic Hashing vs. Encryption, Dictionary Attacks, Defensive Hardening

Tools Used: John the Ripper (JTR Jumbo), Johnny GUI, Networkwalks Hash Calculator & Dictionary Cracker

1. Objective

The objective of Week 3 (Project Modules 1 & 2) was to evaluate the resilience of password-protected documents against offline credential recovery attacks. By extracting the cryptographic hash from an encrypted PDF file and executing dictionary/wordlist attacks across both desktop and browser-based tools, these labs demonstrate how weak, low-entropy passwords are compromised and why strong password policies are critical in enterprise security operations.

2. Core Technical Concepts

Encryption vs. Hashing

Encryption (Two-Way): Transforms plaintext into ciphertext using a cryptographic algorithm and key to protect data confidentiality. Authorized users with the corresponding decryption key can reverse the process.

Hashing (One-Way): Passes input data through a mathematical hash function to produce a fixed-length message digest. While hashes cannot be mathematically reversed, attackers who obtain an offline hash can compute hashes of candidate passwords (dictionary or brute-force attacks) until a digest match is found.

3. Methodology & Execution

Module 1: Offline Password Auditing with John the Ripper & Johnny

Environment Setup: Installed and configured John the Ripper (1.9.0-jumbo-1) and linked john.exe within the Johnny graphical interface on Windows.

Hash Extraction: Extracted the PDF encryption metadata into a crackable $pdf$ hash format ($pdf$4*4*128*...) and saved the sanitized hash string to a local text file (hash1.txt).

Cracking Execution: Loaded hash1.txt into Johnny and initiated an offline cracking session. JTR automatically identified the PDF hash format and recovered the plaintext credential (password1).

Verification: Verified document access using the recovered credential to confirm audit completion.

(Note: In enterprise or SOC environments, local CLI utilities such as pdf2john in Kali Linux are preferred over web-based extractors to ensure sensitive corporate files are never transmitted to third-party servers.)

Module 2: Browser-Based Hash Parsing & Dictionary Attack

Local Hash Parsing: Parsed the target PDF locally in the browser using the Networkwalks Hash Calculator to inspect its revision/version metadata (Revision: R4, Version: V4, 128-bit key length) and extract the $pdf$ digest.

Dictionary Attack: Loaded the extracted $pdf$ hash into the Networkwalks Password Cracker and executed a wordlist attack.

Result: The tool matched the digest against a standard dictionary list in seconds, highlighting the vulnerability of predictable, common passwords.

4. Defensive Recommendations & Remediation

From a Security Operations (SOC) and IT Infrastructure perspective, mitigating credential-based compromise requires layered controls:

Enforce High-Entropy Passphrases: Replace short, dictionary-based passwords with long, complex passphrases (14+ characters) that resist wordlist and rule-based attacks.

Modern Key Derivation Functions (KDFs): Ensure systems store credentials using salted, memory-hard hashing algorithms (e.g., Argon2id, bcrypt, or PBKDF2) rather than fast, unsalted digests (MD5/SHA-1) to slow down offline GPU/CPU cracking.

Multi-Factor Authentication (MFA): Enforce MFA across enterprise accounts and cloud platforms so compromised credentials alone do not grant unauthorized access.

Data Loss Prevention (DLP) & File Controls: Use enterprise Rights Management (e.g., Microsoft Purview Information Protection) rather than standalone legacy PDF passwords for sensitive corporate documents.

5. Disclaimer

All testing was conducted strictly within authorized Networkwalks training lab environments on sample files. Proprietary lab files and CTF verification flags have been intentionally omitted.
