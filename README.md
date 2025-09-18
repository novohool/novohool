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
participant DNS as DNS Resolver
participant E as ECHConfig Provider
participant Cache as Local Cache
participant CQ as Client QUIC/TLS
participant NET as Network
participant SQ as Server QUIC/TLS
participant S as Server App

%% ECH Config Discovery
C ->>+ DNS: Query example.com (A/AAAA + SVCB/HTTPS)
DNS -->>- C: Response (IP + SVCB + ECH hint)

Note over C,Cache: If cached & valid ECHConfig exists, skip fetch
C ->>+ E: Fetch ECHConfigList (if needed)
E -->>- C: Return ECHConfigList
C ->> Cache: Store/Update ECHConfig

Note over C: Select ECHConfig, build Outer(ClientHello, public_name) + Inner(ClientHello, real SNI encrypted)

%% QUIC + TLS 1.3 Handshake
C ->>+ CQ: Initiate QUIC connect
CQ ->>+ NET: QUIC Initial (ClientHello outer + encrypted inner)
NET ->>+ SQ: Deliver Initial
Note over NET: Observer sees only public_name (outer SNI)
Note over SQ: Try to decrypt Inner ClientHello with ECH private key

Note over SQ,CQ: Success: proceed with real SNI<br>Failure: send rejection, client fallback

SQ -->> CQ: ServerHello + EncryptedExtensions + Certificate + Finished
Note over CQ: Verify cert chain via CA/OCSP
CQ -->> SQ: Client Finished
Note over CQ,SQ: TLS 1.3 handshake complete, 1-RTT keys ready

%% HTTP/3 Encrypted Data
CQ ->>+ NET: HTTP/3 request (1-RTT encrypted)
NET ->>+ SQ: Deliver request
SQ -->>- NET: HTTP/3 response (encrypted)
NET -->>- CQ: Deliver response
CQ ->> C: Response to app

%% Fallback
Note over C,CQ: If ECH decryption failed:<br>1. Client retries handshake<br>2. Outer ClientHello carries real SNI<br>3. QUIC+TLS handshake proceeds normally<br>4. SNI visible on the wire

```

## GitHub Stats
![Your GitHub stats](https://github-readme-stats.vercel.app/api?username=novohool&show_icons=true&theme=radical)

<code>
</code>
