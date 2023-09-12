
# 1. Introduction

**▰** System hacking is how hackers access individual computers on a network. Ethical hackers learn system hacking to detect, prevent, and counter these types of attacks.

**▰** It is the procedure of obtaining unauthorized access to a system and its resources, exploiting the weaknesses in a computer system.

**▰** Generally use password cracking, viruses, malware, Trojans, worms, phishing techniques, email spamming, social engineering, and exploit operating system vulnerabilities, to get access to any victim's system.

### Goals

**▻** Gaining Access

**▻** Escalating privileges

**▻** Executing applications

**▻** Hiding files

**▻** Clearing tracks

---

## 1.1. Password Cracking

- Password cracking techniques are used to recover passwords from computer systems.
- Attackers use password-cracking techniques to gain unauthorized access to the vulnerable system.
- Most password-cracking techniques are successful due to weak or easily guessable passwords.

### 1.1.1. Password Complexity

**Password Strength:**

- 2015 annual public sector information security survey says “Weak authentication security is the leading cause of data breaches, accounting for 76% of compromised records.”
- ***Complexity defines the character set used.***
- Length is a crucial factor, over complexity, **c0mpl3x** can be cracked much faster than **`thisismypasswrd`**.
- ***The formula is **log(C) / log(2) * L** where C is the size of the character set and L is the length of the password**8***
    - Ex : Small and Upper case 26+26=52 with full-length L

### 1.1.2. Types of Password Attacks

- **Non-Electronic Attacks**: Attackers need not possess technical knowledge to crack passwords, hence known as non-technical attacks.
    - Shoulder Surfing
    - Social Engineering
    - Dumpster Diving
- **Active Online Attacks**: The attacker performs password cracking by directly communicating with the victim’s machine.
    - Dictionary and Brute Forcing Attack
    - Hash Injection and Phishing
    - Trojan/Spyware/Keyloggers
    - Password Guessing
- **Passive Online Attacks**: The attacker performs password cracking without communicating with the authorizing party.
    - Wire Sniffing (Eavesdropping)
    - Replay
- **Offline Attack**: The attacker copies the target's password file and then tries to crack passwords in his own system at different locations.
    - Pre-Computed Hashes (Rainbow Table)
    - Distributed Network