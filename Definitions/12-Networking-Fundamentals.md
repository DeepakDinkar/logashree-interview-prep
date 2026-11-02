# 📖 Networking Fundamentals — Definitions & Examples

> Not on the resume explicitly, but **VPC, ELB, CloudFront, DNS all rest on these**. Service/consulting interviewers ask "what happens when you type a URL" and basic protocol questions. Know these cold.

### 📚 Reference docs
- [MDN — How the web works](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works)
- [Cloudflare Learning Center](https://www.cloudflare.com/learning/) (DNS, TLS, CDN, DDoS — excellent plain-English)
- [HTTP overview (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) · [DNS (Cloudflare)](https://www.cloudflare.com/learning/dns/what-is-dns/)
- [AWS VPC networking](https://docs.aws.amazon.com/vpc/latest/userguide/) · [How DNS works (comic)](https://howdns.works/)

---

## OSI / TCP-IP model 🔥
7 layers (top→bottom): **Application, Presentation, Session, Transport, Network, Data Link, Physical.**
- You mostly care about: **L7 Application** (HTTP), **L4 Transport** (TCP/UDP), **L3 Network** (IP).
- **ALB = L7** (sees HTTP, path routing). **NLB = L4** (TCP, fast). This is *why* that distinction matters.

## TCP vs UDP 🔥
| | TCP | UDP |
|---|-----|-----|
| Connection | connection-oriented (handshake) | connectionless |
| Reliability | guaranteed, ordered, retransmits | best-effort, no guarantee |
| Speed | slower (overhead) | faster |
| Use | web, APIs, SSH, databases | DNS, video, VoIP, gaming |

**TCP 3-way handshake:** SYN → SYN-ACK → ACK (establishes connection before data).

## IP & ports
- **IP address** — identifies a host (IPv4 `10.0.1.5`, IPv6).
- **Port** — identifies a service on that host (HTTP 80, HTTPS 443, SSH 22, PostgreSQL 5432).
- **CIDR** — IP range notation: `10.0.0.0/16` = 65,536 addresses; `/24` = 256. (VPC/subnet sizing.)
- **Public vs private IP** — routable on internet vs internal (RFC1918: `10.x`, `172.16–31.x`, `192.168.x`).

## DNS 🔥 (how a name becomes an IP)
1. Browser checks cache → OS cache → **resolver** (ISP/Route 53).
2. Resolver asks **root** → **TLD** (`.com`) → **authoritative** nameserver.
3. Returns the IP; cached per **TTL**.
- **Record types:** A (name→IPv4), AAAA (IPv6), **CNAME** (alias), MX (mail), TXT, NS, **Alias** (Route 53 → AWS resources).
- **Route 53** = AWS's DNS; routing policies: simple, weighted, latency, failover, geolocation.

## HTTP / HTTPS 🔥
- **HTTP** — request/response; **methods** GET, POST, PUT, PATCH, DELETE.
- **Status codes:** 2xx success, 3xx redirect, **4xx client error** (401 unauth, 403 forbidden, 404 not found, 429 rate limit), **5xx server error** (500, **502 bad gateway**, **503 unavailable**, 504 timeout). 🔥 Know 502 vs 503 vs 504 for ALB debugging.
- **HTTPS** — HTTP over **TLS**; encrypts in transit. **TLS handshake:** client hello → cert exchange → key agreement → encrypted session. Certs via **ACM** on AWS.
- **Idempotency** — GET/PUT/DELETE safe to retry; POST is not. Matters for retries + payments.

## Load balancing & CDN (ties to AWS) 🔥
- **Load balancer** — spreads traffic across targets + health checks (ALB/NLB).
- **CDN (CloudFront)** — caches content at edge locations near users → lower latency, less origin load.
- **Reverse proxy** — sits in front of servers (nginx, ALB); forward proxy sits in front of clients.

## "What happens when you type a URL?" 🔥🔥 (classic question)
1. Browser parses URL.
2. **DNS** resolves domain → IP (cache → resolver → root/TLD/authoritative).
3. **TCP handshake** to the server IP (SYN/SYN-ACK/ACK) on port 443.
4. **TLS handshake** (HTTPS) → encrypted session.
5. Browser sends **HTTP GET** request.
6. Request hits **CloudFront/CDN** → **ALB** → **target (ECS/EC2)**.
7. Server processes, queries DB, returns **HTTP response**.
8. Browser renders HTML, fetches CSS/JS/images (more requests).

---

## 🎯 Likely interview Qs
- What happens when you type a URL and press enter?
- TCP vs UDP — when each?
- How does DNS resolution work? What is a CNAME vs A record?
- Explain 502 vs 503 vs 504 (great for ALB troubleshooting).
- What is a CIDR block? How many IPs in a /24?
- What is TLS / how does HTTPS work?
- How does a CDN reduce latency?
- Which OSI layer does an ALB vs NLB operate at?
