# Eterna

**The independent control layer for AI-initiated payments on XRPL.**

The payment settles, but the door stays locked until Eterna independently verifies it on XRPL.

**Settled ≠ unlocked.** The ledger proves a payment moved. It does not prove anyone allowed it. Eterna is the layer that proves it was allowed — independently, and non-custodially.

---

## The problem

x402 gave machines a way to pay. It did not give anyone a way to say *no*. When an AI agent spends, the transaction settles on the ledger — final and correct — and settlement is treated as permission. No one independently verifies that the money that moved was the payment the agent declared, the human approved, and the policy cleared.

At machine volume, human review disappears, and settlement silently becomes authorization by default.

## What Eterna does

Eterna sits between an agent's request and the release of value. It independently reads the settled transaction back from XRPL and verifies it, field-by-field, against the terms declared before signing. Only if that check passes does the protected resource unlock.

- The agent proposes.
- The human's own wallet signs.
- XRPL settles.
- **Eterna independently verifies before anything unlocks.**

Eterna never holds keys, never signs, and is never in the flow of funds. The referee is not a player.

## Live today, on XRPL mainnet

- Governed payment — a real settled transaction on mainnet.
- Refusal path — an over-policy request is refused before anything is signed; no transaction is created.
- Independent post-settlement verification — the resource unlocks only on Eterna's own verified ledger read.
- Human signs every payment.

Every governed payment carries **SourceTag `2606150008`** on XRPL mainnet — publicly inspectable on [Bithomp](https://bithomp.com). You don't have to trust this repo; you can verify it on the public ledger yourself. See [DEMO.md](./DEMO.md).

## What's in this repository

This repository contains the architecture documentation and generic, synthetic frontend examples that demonstrate engineering craft. It intentionally does **not** contain the verification internals — those are the core of the system.

- [`ARCHITECTURE_OVERVIEW.md`](./ARCHITECTURE_OVERVIEW.md) — how the layers fit together
- [`SECURITY_MODEL.md`](./SECURITY_MODEL.md) — the design properties, at a high level
- [`DEMO.md`](./DEMO.md) — watch it, then verify it yourself on Bithomp
- [`ROADMAP.md`](./ROADMAP.md) — where the architecture goes next
- [`/examples`](./examples) — four synthetic frontend examples: `control-panel.html`, `conversation-preview.html`, `workspace-dashboard.html`, and `x402-challenge-inspector.html`

## Examples

All examples use synthetic data and connect to no backend.

| File | What it demonstrates |
|---|---|
| [`control-panel.html`](./examples/control-panel.html) | Responsive dashboard layout and interaction |
| [`conversation-preview.html`](./examples/conversation-preview.html) | Conversational UI, states, and typography |
| [`workspace-dashboard.html`](./examples/workspace-dashboard.html) | Filtering, accessibility, and component organization |
| [`x402-challenge-inspector.html`](./examples/x402-challenge-inspector.html) | Client-side parsing and display of a public x402 challenge |

## Quick Start

### Open an example

Open any `.html` file in [`examples/`](./examples) directly in a browser. There is no build step and no backend.

### Run tests

Requires Node.js 20 or newer.

```bash
npm test
```

## Demo

▶ **Live governed payment on XRPL:** https://youtu.be/4-34TXKdfVM

## Status

- Live on XRPL mainnet: governed payment, refusal path, independent verification.
- XRPL Make Waves submission — July 2026.
- Core architecture is **patent-pending** — applications filed, not granted.

## License

Licensed under the MIT License — a permissive open-source license. See LICENSE.

---

*Eterna.AI LLC (Delaware) · non-custodial by design, from the first commit.*
