# Kulal (Pipe)

> **The Universal Reliability Layer for your Webhooks.**
> *Ingest. Buffer. Transform. Deliver.*

**Kulal** is a self-hosted, single-binary infrastructure tool that acts as a "Smart Pipe" between chaotic third-party integrations (Stripe, GitHub, Slack) and your backend.

It absorbs traffic spikes, guarantees delivery via persistent queuing, and normalizes data before it ever hits your server.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Go Version](https://img.shields.io/badge/go-1.22+-cyan.svg)
![Status](https://img.shields.io/badge/status-alpha-orange.svg)

---

## The Problem

Building webhook integrations is painful:

1. **Downtime:** If your server is down for 5 minutes, you lose Stripe payment events forever.
2. **Spikes:** A viral marketing campaign triggers 10k webhooks/sec, crashing your database.
3. **Chaos:** Every integration sends data in a different weird format.

## The Kulal Solution

Run `kulal` in front of your API. It accepts the request immediately, saves it to disk, and reliably pushes it to you at a pace you can handle.

**Think of it as NGINX + Kafka + JQ, but just one binary.**

---

## Key Features

* **Universal Receiver:** Listens for webhooks from any source (Stripe, Shopify, Custom).
* **Durable Buffer:** Writes every request to a local SQLite WAL. Zero data loss if the process crashes.
* **Logic Pipeline:** Filter and Transform payloads using `JQ` syntax before they reach your app.
* **Smart Dispatch:**
  * **Rate Limiting:** Protect your backend from "Thundering Herds."
  * **Auto-Retries:** Exponential backoff (5s, 30s, 5m) if your server returns 500.
* **Dead Letter UI:** View and replay failed events via a built-in dashboard.

---

## Quick Start

### 1. Install

Download the binary or build from source:

```bash
go install [github.com/yourusername/kulal/cmd/kulal@latest](https://github.com/yourusername/kulal/cmd/kulal@latest)
```
