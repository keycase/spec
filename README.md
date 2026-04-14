# KeyCase Spec

## Vision

KeyCase is an open source cryptographic identity and encrypted communication platform. It is the spiritual successor to Keybase — not a fork, not a clone, but a ground-up rebuild informed by what Keybase got right and where it fell short.

The server is **KeyCase**. The client is **Keybae**.

## What Happened to Keybase

Keybase was acquired by Zoom in May 2020. Development effectively stopped. The client remains open source (Go, React Native) but the server is proprietary and unmaintained. The community that depended on Keybase has no path forward within that ecosystem.

KeyCase doesn't attempt to reverse-engineer or replace the Keybase server. We're building something new.

## Principles

- **Open source, top to bottom.** Server and client, fully open, from day one.
- **Self-hostable.** Run your own KeyCase server if you want. No vendor lock-in.
- **Platform-agnostic identity proofs.** No bespoke integrations with specific social platforms. No implicit endorsement of any platform. Users choose where their proofs live.
- **One language, one stack.** Dart everywhere — server, client, shared libraries. No serialization mismatch, no type drift, no maintaining three codebases.
- **Ship in layers.** Each layer is usable on its own. Don't wait for "everything" to ship "something."

## Technology Stack

| Component | Technology |
|-----------|-----------|
| Server | Dart |
| Client | Flutter (iOS, Android, desktop, web) |
| Shared library | Dart package (crypto, models, proof logic) |
| Database | PostgreSQL |
| Cryptography | libsodium via FFI (NaCl-compatible) |

### Why Dart + Flutter

Keybase was built across Go (core), React Native (mobile), and Electron (desktop) — three stacks with different languages, different build systems, and different failure modes. KeyCase uses Dart across the entire stack. The shared `core` library means identity models, proof verification, and encryption logic are written once and used by both server and client with zero drift.

Flutter gives us iOS, Android, macOS, Windows, Linux, and web from a single codebase.

## Repositories

| Repo | Purpose |
|------|---------|
| `keycase/keycase` | Dart server |
| `keycase/keybae` | Flutter client |
| `keycase/core` | Shared Dart package — crypto, models, proof verification |
| `keycase/spec` | This document |

## Identity Proof System

KeyCase does **not** maintain a list of blessed platforms. Instead, it supports two generic proof types that work everywhere:

### DNS Proof

Add a TXT record to a domain you own containing a signed identity statement. Proves domain ownership. Platform-independent. Permanent.

```
keycase-proof=ks1:BASE64_SIGNED_STATEMENT
```

### URL Proof

Publish a signed proof document at any publicly accessible URL. The URL can be on GitHub, a personal blog, a Mastodon instance, a Gist, a text file on a static server — anywhere. KeyCase fetches the URL and verifies the signature.

This means:
- No API integrations to maintain
- No platform politics
- No breakage when a platform changes their API
- Users decide which platforms matter to them

### Key Signing (Web of Trust)

A KeyCase user can sign another user's public key, vouching for their identity. Social proof without any platform involved.

## Feature Roadmap

### Layer 1 — Identity (MVP)

- Key pair generation and management
- User profiles tied to public keys
- DNS proofs
- URL proofs
- Key signing / web of trust
- Public key discovery and verification
- KeyCase server stores and serves identity proofs
- Keybae CLI and Flutter app for managing your identity

### Layer 2 — Encrypted Messaging

- End-to-end encrypted direct messages
- Forward secrecy
- Offline message delivery via server (messages encrypted to recipient's public key)
- Message history (client-side encrypted)

### Layer 3 — Teams

- Group key management
- Team membership with roles
- Encrypted team chat channels
- Shared team identity

### Layer 4 — Encrypted File Storage

- Client-side encrypted file storage
- Shared folders (encrypted to team or individual keys)
- Mountable local filesystem (FUSE or equivalent)
- Cloud storage backend (S3-compatible, self-hostable)

### Layer 5 — Ecosystem

- Bot platform
- Encrypted git hosting
- API for third-party integrations

## What We're Not Building (Yet)

- Cryptocurrency wallet or transactions
- Social feed or timeline
- Video/voice calling
- Anything that requires a platform-specific integration we have to maintain

## Contributing

KeyCase is an open source project organized through the [KeyCase team on Keybase](https://keybase.io/team/keycase). Join us there to discuss development, architecture, and roadmap.

## License

BSD-3-Clause
