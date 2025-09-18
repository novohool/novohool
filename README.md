## Hi there 👋

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/novohool/novohool/output/github-contribution-grid-snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/novohool/novohool/output/github-contribution-grid-snake.svg">
  <img alt="github contribution grid snake animation" src="https://raw.githubusercontent.com/novohool/novohool/output/github-contribution-grid-snake.svg">
</picture>

```mermaid
sequenceDiagram
autonumber
    participant C as Client
    participant Q as QUIC Layer
    participant T as TLS 1.3 Handshake
    participant S as Server

    C ->>+ Q: INITIAL (QUIC) packet
    Note over Q: contains TLS ClientHello

    Q ->>+ T: ClientHello
    Note over T: includes SNI (unencrypted) <br/> or ECH (Encrypted ClientHello)

    alt With ECH
        T ->> S: Outer ClientHello (public_name)
        Note over T: Real SNI encrypted (ECHConfig) <br/> only decryptable by server
    else Without ECH
        T ->> S: Plain ClientHello with SNI
        Note over T: Server sees actual domain
    end

    S -->>- T: ServerHello + EncryptedExtensions
    Note over T: handshake keys established

    T -->>- Q: Handshake complete
    Note over Q: secure QUIC connection

    Q ->> S: Encrypted HTTP/3 request
    S -->> C: Encrypted HTTP/3 response

```

## GitHub Stats
![Your GitHub stats](https://github-readme-stats.vercel.app/api?username=novohool&show_icons=true&theme=radical)

<code>
</code>
