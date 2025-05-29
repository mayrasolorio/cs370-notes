# Internet Security

### Why the Internet is Insecure by Default
- The internet was built for researchers who **trusted** each other.
- Focus was on **connectivity, not security**.
- No built-in encryption or tamper protection.
- Attackers can hijack data remotely, no need to be nearby.

#### Real-World Comparison
- Bank robbers deal with guards and cameras.
- Online attackers just send malicious data from anywhere.

### How the Internet Works (Basics)
#### OSI Model Layers (Top &rarr; Bottom)
- **Application/Presentation/Session Layers**: web browsing, file sharing
- **Transport**: breaks data into chunks, handles missing pieces
- **Network**: routes data (packets) accross networks
    - Routers work here &rarr; every jump = "a hop"
- Data travels as 1s and 0s, through cables or wirelessly
#### Packets
- Data is split into packets (like sending a postcard in pieces).
- Each router reads and forwards packets.
- Every hop is a risk &rarr; easy for data to get intercepted.

### Transport Layer Security (TLS)
#### What TLS Does
- Fixes internets insecure design by **making a secure channel**.
- Used when you see `https://` or a padlock in your browser.
- Makes messages **private + safe even if someone gets server keys later**.

### TLS Handshake Steps (EDH Example)
1. **ClientHello**
    -  Client says "hi" and lists:
        - Max TLS version it supports
        - Cipher suites it can use
        - A random value
        - Extra info (?)

2. **ServerHello + Certificate**
    - Server replies with:
        - Agreed TLS version + cipher suite
        - Its certificate (includes public key)
        - Ceritificate signed by a trusted CA

3. **Server Key Exchange**
    - If using Ephemeral DH:
        - Sends prime numbers + private key
    - May also ask for client certificate (rare)

4. **ServerHelloDone**
    - Server says "I'm done sending stuff!"

5. **ClientKeyExchange**
    - Client:
        - Verifies server cert
        - Sends its own EDH public value
6. (Optional) **Certificate Verify**
    - If server asked for a client cert:
        - Client proves it own the private key
7. **ChangeCipherSpec and Finished (Client)**
    - Tells server: "From now on, I'm encrypting stuff!"
    - Sends encrypted "Finished!" message (proves handshake wasn't messed with)
8. **ChangeCipherSpec and Finished (Server)**
    - Server replies "Me too!"
    - Also sends encrypted "Finished"

### After the Handshake
- Both sides switch to using **symmetric encryption**.
- Everything after that is encrypted.
- TLS = Confidentiality + Integrity + (optional) Authentication