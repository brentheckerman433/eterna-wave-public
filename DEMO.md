# Demo — and how to verify it yourself

The point of Eterna is that you don't have to trust it. Every governed payment lands on the **public XRPL mainnet ledger**, where anyone can inspect it independently.

## Watch it

▶ **Live governed payment on XRPL:** https://youtu.be/4-34TXKdfVM

The walk shows, on mainnet:

1. **Settled · locked** — a real payment settles on XRPL, but the resource stays locked.
2. **Refused before existence** — an over-policy request is refused before signing; no transaction is created, no funds move.
3. **Independent verification** — Eterna reads the settled transaction back from the ledger and verifies it; only then does the resource unlock.

## Verify it yourself

You do not need this repository, the app, or our word for it. Verify on the public ledger:

1. Governed payments carry **SourceTag `2606150008`** on XRPL mainnet.
2. Open a public XRPL explorer such as **[Bithomp](https://bithomp.com)**.
3. Look up the settled transaction shown in the demo (or search by SourceTag), and confirm the on-chain details — amount, destination, and that it settled on mainnet.

The transaction is a public fact. Eterna's contribution is the layer that verifies that fact against what was *authorized* before releasing anything — which is the part settlement alone can't prove.

## What the demo does not show

The demo shows the product behavior and the public, verifiable result. It does **not** expose the internal verification logic, the settlement and verification internals, or any keys or configuration. Those are intentionally not part of this repository.

---

*Live on XRPL mainnet · human signs every payment · non-custodial by design.*
