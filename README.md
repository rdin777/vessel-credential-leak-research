# vessel-credential-leak-research
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
