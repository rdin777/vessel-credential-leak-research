# vessel-credential-leak-research

*If this research helped you, please consider giving it a ⭐ Star.*


## 🚀 Stay Updated
Found this research useful?
* **Star ⭐** this repo to keep track of it.
* **Follow me** on GitHub for more DeFi security research.
* **Fork** it if you want to run your own experiments.

### ☕ Support the Research
If you appreciate the work and want to support further security research:

<img src="456.PNG" alt="Donate QR" width="200"/>

**Wallet Address (ETH/EVM):** 0xBDDD7973D0DE27B715A4A5cbdb87d0DF78757b3A 


Analysis of plaintext credential disclosure in the vessel.jib.pusher component (Infrastructure Security Research)
# Research: Plaintext Credential Exposure in vessel.jib.pusher

## Overview
This repository documents a security research into the `vessel.jib.pusher` module. The research identifies a critical flaw where sensitive authentication credentials (registry tokens, passwords) are leaked in plaintext into standard error logs during failed operations.

## Technical Details
The vulnerability occurs during the image push process. When an error is encountered (e.g., 401 Unauthorized), the component logs the full request context. Due to insufficient sanitization, this context contains raw authentication data.


## Potential Impact
- **Credential Theft**: Attackers with access to centralized logging (ELK, Splunk) can harvest active registry tokens.
- **Supply Chain Risk**: Compromised registry credentials allow for malicious image injections.

## Remediation
- Implement log masking for all fields containing `auth`, `token`, or `password`.
- Use short-lived dynamic credentials to minimize the window of opportunity for stolen tokens.
