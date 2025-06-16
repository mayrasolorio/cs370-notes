# Web Security

### Intro
- Web security != just encrypting data with TLS.
- Real threats usually hit the **Application Layer**, not the transport layer.
- 2023 Breaches:
    - **MOVEit Transfer** (SQL injection): attackers stole data via a file-sharing app flaw.
    - **T-Mobile API**: public API gave up customer data. No broken encryption, just bad logic.
- **Main Point**: TLS helps, but secure app logic matters more.

### Web Architecture 101
- Client-Server model: 
    - Browser (client): renders HTML, runs JavaScript
    - Server: processes requests, sends responses
    - **HTTPS + TLS** = encrypts traffic, but trust goes *way* deeper
    - Originally: client and server were the only major players
    - Now: multiple scripts/domains per page, more surface area = more risk
    - Main security Q : Who should have access to what?