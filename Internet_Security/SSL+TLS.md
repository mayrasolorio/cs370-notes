# SSL/TLS Protocols

### Intro to TLS 
- TLS = **Transport Layer Security** - secure data in transit (CIA).
- **Started as SSL (by Netscape)** in the 90s to secure HTTP.
- TLS wraps TCP in an encrypted tunnel to prevent snooping.

### History of SSL/TLS
#### SSL 1.0 (1994)
- Never released - had major flaws (replay attacks, plaintext manipulation)
#### SSL 2.0 (1995)
- First public version
- Introduced encryption + cert based auth.
- Still weak: no handshake authentication = vulnerable to MITM attacks
#### SLL 3.0 (1996)
- Big improvements: authentication handshake, better crypto negotiation
- Later broken by POODLE (2014) - padding oracle flaw
#### TLS 1.0 (1999)
- Standardized by IETF (Basically SSL 3.1)
- New name = New open standard
#### TLS 1.1 (2006) + TLS 1.2 (2008)
- Better CBC protections, stronger crypto (SHA-256 over MD5/SHA-1)
- TLS 1.2 became the gold standard
#### TLS 1.3 (2018)
- Major upgrade:
    - Removes old/weak features
    - Enforces **forward secrecy**
    - 1 RTT handshake = faster, more secure
- TLS 1.0 + 1.1 deprecated by 2020-2021

### TLS Attacks and Exploits
1. **TLS Stripping**
    - MITM strips HTTPS &rarr; downgrades to HTTP
    - Victim stays on insecure connection, attacker relays to real server
    - **Tool**: `SSLStrip` by Moxie Marlinspike (2009)
    - Fix: HSTS - Forces browser to use HTTPS after first visit

2. **Fake Certificates**
    - Abuse of CA Trust Model:
        - **DigiNotar (2011)**: CA breach &rarr; attackers got certs for Google.
        - **Superfish (Lenovo)**: Pre-Installed root cert used to intercept HTTPS traffic.
    - Victims can't tell if it's fake if the browser trusts the cert.

3. **Protocol Downgrade Attacks**
    - Exploits backwards compatability
    - Tricks clients/servers into using weak protocols/ciphers
    - Examples:
        - **Logjam (2015)**: Downgrade to 512-bit DH &rarr; easy to break.
        - **POODLE (2014)**: Forces SSL 3.0 abuses padding oracle.
    - **Fix**: TLS 1.3 adds "downgrade markers" in handshake to detect tampering.


### Takeaways
- Always use TLS 1.2 or 1.3
- Legacy support = Attack surface
- Proper implementation > Just having encryption
- Be cautious about certs, browser warnings, and HTTPS enforcement

