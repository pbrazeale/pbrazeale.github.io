+++
tags = ['CompTIA', 'Security+','Bash', 'Cybersecurity']
title = 'Professor Messer CompTIA Security+ 1.0 General Security Concepts'
date = 2025-03-08T16:34:07+01:00
draft = false
+++

## 1.1 Compare and contrast various types of security controls

### Control Categories

Technical Controls

- Firewalls, anti-virus
  Managerial controls
- Security policy
  Operational Controls
- Security Guards
- Password training guide
  Physical Controls
- Fences, locks
- Badge Readers

### Control Types

- Preventative
- Deterrent
  - Warning signs
- Detective
  - Identify if and when breach occurs
- Corrective
  - Applied after the event
  - Restore from backups after ransomware
- Compensating
  - Firewall blacks app until fixed
  - Generator used for power outage
- Directive - Require employees to store data in encrypted drive. - "Authorized Personal Only"
  ![Control Type Examples.png](https://pbrazeale.github.io/images/control_type_examples.png)

## 1.2 Summarize fundamental security concepts.

### The CIA Triad

![The CIA Triad.png](https://pbrazeale.github.io/images/the_CIA_triad.png)
Also, AIC triad.

#### Security Objectives

- Availability
- Integrity
- Confidentiality

Encryption and Authentication.

Hashing ensures that our data matches both ends.

Digital signature:
Encrypt the Hash.

### Non-repudiation

1. Proof of integrity
2. Proof of origin

```powershell
(Get-FileHash .. -A SHA256).hash -eq "HASH#"
```

Integrity

- Prove the message has not changed
  Authentication
- prove the source of the message
  Non-repudiation
- Make sure the signature isn't fake
- Sign with a private key; paired with a public key.

### AAA framework

- Identification
- Authentication
- Authorization
- Accounting

#### CA (Certificate Authority)

- Manage certificates for devices and users
- _CA is a hashing and encryption algo?_

#### Authorization Model

The relationship of groups and users

### Gap Analysis

- Where we "are"
- Where we "want to go"

#### Determine end goal

- NIST Special Publication 800-171 R2
- ISO/IEC 27001

**_NIST National Institute of Standards & Technology_**
**_ISO International Standards Organization_**

#### GAP REPORT EXAMPLE

![gap report example.png](https://pbrazeale.github.io/images/gap_report.png)

### Zero Trust

Authenticate each time you want to use a device, process, or user.

#### Planes of operation

- Split the network into functional planes

##### Data Plane

- process the frames, packets, and network data
- processing, forwarding, trunking, encrypting, NAT

**_NAT Network Address Translation_**

##### Control Plane

- Manages the actions of the data plane
- Define policies and rules
- Determines how packets should be forwarded
- Routing tables, session tables, NAT tables

**Policy-driven access control**

**_PEP Policy Enforcement Point_**

- Where/the physical device, that allows traffic to move forward based upon the policies of the organization.
- Gatekeeper
  **_PDP Policy Decision point_**
- The actual machine with the rules.
  ![Zero Trust Across Planes.png](https://pbrazeale.github.io/images/zero-trust-across-planes.png)

### Physical Security

- Access Control Vestibules
- Barriers
- Keycard access doors

### Deception and Disruption

- Use a **honeypot** to keep them active and learn about the attackers
- **Honeynets** are when you build up entire faked networks (multiple honeypots)
- **Honeyfiles** are the fake files that appear top secret (passwords.csv)
- **Honeytokens** are the fake credentials that verify the honeynet has been hit.

## 1.3 Explain the importance of change management processes and the impact to security.

### Change Management

- Upgrade software
  - set on a defined timeline

#### Change Approval Process

- What
- When
- Where
- Why

Stakeholders are usually the best choice for taking ownership of the change process.

#### Impact Analysis

- Risk of changing, or not changing - Low - Medium - High
  Test in a sandbox environment.
- Create and Test backup process.

Covered in **_SOP (Standard Operating Procedue)_**

### Technical Change Management

Allow List/Deny List

- Core tool for IT group controls

DOWNTIME is our responsibility.

1. Learn the legacy application and document it to become the core expert.
2. Ongoing documentation is a must!

Version Control allows us to maintain what app on what dependencies.

## 1.4 Explain the importance of using appropriate cryptographic solutions.

### Public Key Infrastructure

**_PKI Public Key Infrastructure_**
Digital certificates

#### Symmetric encryption

The same key is used for encryption and decryption

- Offers speed advantages

#### Asymmetric encryption

- Public key, private key (example bitcoin)
  - public can encrypt
  - private only can decrypt
    - **_PGP Pretty Good Privacy_**
    - **_GPG Gnu Privacy Guard_**

### Encrypting Data

Protected data on storage devices

- Data at rest

#### Transport Encryption

- HTTPS
- VPN, SSL

#### Encryption Algorithms

**_DES Digital Encryption Standard_**

- 5 steps
  **_AES Advanced Encryption Standard_**
  **_AES-256 Advanced Encryption Standards 256-bit_**
- 3 steps encryption first, with multiple level choice

Cryptography keys are hidden, but the algo is public knowledge.

#### Key stretching

nesting the encryption like Russian Dolls

### Key Exchange

- Out-of-Band key exchange
  - exchange outside of the internet
- in-band key exchange
  - exchange over the internet
  - Public key cryptography

### Encryption Technologies

#### TPM Trusted Platform Module

- cryptography and random number generation

#### HSM Hardware Security Module

- a TPM for an entire cluster of devices
- allows for faster encryption and decryption
- Pairs with a key manager software

#### Secure enclave

- a hardware processor that manages security of the system

### Obfuscation

Steganography

- hiding the text inside a .jpeg
  Embedded messages in TCP packets

#### Tokenization

- Using a single use hash token from a credit card can go over the network openly, because it will only exist once.
  ![Tokenization.png](https://pbrazeale.github.io/images/tokenization.png)

#### Data masking

- hiding all but the last four of a credit card, or bank account number.

### Hashing and Digital Signatures

#### Hashes

- Represent data a short string of text.
  - A digital fingerprint
- Impossible to recover the original message form the digest
- Verify a downloaded document
- Digital signature
  - Authentication, non-repudiation, and integrity

#### SHA256

- 256 bits / as 64 hexadecimal characters

#### Collision

- where hashes match but original data does not.
- MD5 found in 1996 to have collision issues.

#### Practical hashing

- Verify a downloaded file

```powershell
(Get-FileHash .. -A SHA256).hash -eq "HASH#"
```

- Password storage vault
  - Hash plus a salted hash

#### Salt

- random data based on each user
- **Rainbow Tables**
  - backwards engineers the hash table, when not salted.

#### Digital Signature

- private key to encrypt
- public key to decrypt
  - Can also work the other way around

#### Creating a digital signature

![Alice Encrypts.png](<https://pbrazeale.github.io/images/alice-encrypts.png)

#### Verify signature

![Bob decrypts.png](https://pbrazeale.github.io/images/bob-decrypts.png)

### Blockchain Technology

A Distributed Ledger

- Open Source ledger information.
- As long as no party gains 50% control, the blockchain remains immutable.

### Certificates

- A public key certificate
- A digital signature
  - PKI uses Certificate Authorities for additional trust.
    - **_PKI Public Key Infrastructure_**
    - **_CA Certificate Authority_**
- Certificate creation can be built into the OS
  - Windows Domain services
- **X.509**
  - standard website certificate

#### Root of Trust

- IT security requires trust
- The trusted source that we rely on (_e.g. MS Windows_)
- website CA when we visit the website.

#### Private Certificate Authorities

- for internal network software
  - Windows Certificate Services
  - [OpenCA](https://www.openca.org/projects/openca/)
- Internal CA process is same as an external CA

#### Wildcard Certificates

- `*.google.com`
  - the `*` means any subdomain would be valid under the certificate.
  - ![domain-name](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/1c486335-2bad-48b4-674b-68f5236e5700/sharpen=1)

#### Key revocaiton

- **_CRL Certificate Revocation List_**
  - a centralized way to revoke certificates across a network
  - Built into a CA

#### OCSP stapling

- **_OCSP Online Certificate Status Protocol_**
  - provides scalability for OCSP checks
- the CA is responsible for responding to all OCSP requests
- OCSP status is "stapled" into the SSL/TLS handshake.
  - **_SSL Secure Sockets Layer_**
  - **_TLS Transport Layer Security_**
- Most modern browsers support OCSP

## Resources:

[CompTIA Security+ Certificate Exam Objectives: SY0-701](<https://partners.comptia.org/docs/default-source/resources/comptia-security-sy0-701-exam-objectives-(5-0)>)

[Professor Messer CompTIA Security+ SY0-701](https://www.youtube.com/watch?v=KiEptGbnEBc&list=PLG49S3nxzAnl4QDVqK-hOnoqcSKEIDDuv&index=1)

[CompTIA Security+ Acronym List](https://pbrazeale.github.io/posts/security-acronym-list/)
