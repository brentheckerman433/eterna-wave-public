# Architecture Overview

Eterna is a **governance and verification layer** for machine-initiated payments on XRPL. It describes *what* each part of the system does. It does not describe the internal implementation of the verification path — that is the core of the product and is intentionally not published here.

## The principle

A settled transaction proves money moved. It does not prove anyone allowed it. Eterna keeps **settlement** and **authorization** as two separate facts, and requires an independent verification between them before any resource is released.

**Settled ≠ unlocked.**

## The flow

```
Agent            proposes a payment (declares amount · destination · terms)
   │             — never moves money itself
   ▼
Policy gate      the request is evaluated against declared terms
   │             out-of-policy → refused before anything is signed
   ▼
Human wallet     the owner signs in their own wallet — keys never leave it
   │
   ▼
XRPL             the payment settles on the public ledger
   │             settlement alone does not authorize release
   ▼
Eterna           independently reads the settled transaction from the ledger
   │             and verifies it against the terms declared before signing
   ▼
Unlock / Refuse  the resource is released only on a verified match; otherwise
                 it stays locked, and a receipt records the outcome
```

## The layers

**Onboarding / UX (the `/doors` frontend).** Guides a person through the model — connect a wallet, set a rule, watch a refusal, run a governed spend, verify a receipt. Touches no keys and no funds. This is the surface published in this repository.

**Agent / request layer.** Declares the payment requirement — amount, destination, terms. Proposes; never moves money.

**Policy gate.** Evaluates a request against its declared terms *before* a transaction exists. An out-of-policy request is refused with no payload created — no transaction, no funds moved — and the refusal itself is recorded as evidence.

**Human wallet.** The owner's own wallet signs each payment. Keys never leave it. Eterna is not in this step.

**XRPL settlement.** The payment settles on the public mainnet ledger. Every governed payment carries SourceTag `2606150008`, so anyone can locate and inspect it.

**Independent verification.** Eterna reads the settled transaction back from the ledger itself and checks it against the declared terms. The resource unlocks only if that independent check passes. This layer's internals are not published.

## Non-custodial by design

Across the entire flow, Eterna **holds no keys, never signs, and is never in the flow of funds.** The verifier has no position in the transaction it verifies — the referee is not a player. Settlement providers are partners, not part of the trust model.

## What is proven vs. designed

Everything in the flow above — governance, refusal, signing, settlement, and independent post-settlement verification — is **proven on XRPL mainnet today**, with a human signing every payment. Longer-term architecture (delegated, bounded authority) is described in [ROADMAP.md](./ROADMAP.md) and is **designed, not yet live.**

---

*Core architecture is patent-pending — applications filed, not granted.*
