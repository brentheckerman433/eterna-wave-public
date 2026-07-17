# Roadmap

**Live today** is a governed payment where a human signs each transaction. The direction is **delegated, bounded authority** — where the human signs the authority once, and an agent acts within it, while independent verification still proves every action stayed inside what was signed.

> Everything below is **designed, not yet live on mainnet.** What is live today: governed payment, refusal path, and independent post-settlement verification, human-signed.

## The concept: bounded authority

The next primitive is not a payment authorization — it is a **delegation of bounded authority.** The human signs a policy, not each payment. Once authority is bounded, everything else follows from it: limits, revocation, versioning, composition, and proof are all ways of defining and proving the bound.

## The security transition

```
Today   —  the human signs every payment
   ↓
Next    —  the human signs authority, once
   ↓
Then    —  the agent acts within that delegated authority
   ↓
Always  —  an independent verifier proves every action stayed inside
           the authority that was signed
```

## Planned capabilities

Each item exists to limit, prevent, or mitigate a specific class of failure — not by trust, but by construction.

- **Policy Envelope** — the human signs authority: spend ceilings, destination scope, expiration, revocation, single-use/recurring, versioned.
- **Policy Composition** — multiple independent policies evaluated together; a payment unlocks only if every applicable authority evaluates to true.
- **Velocity Controls** — authority that applies across time, not just per payment (caps the aggregate).
- **Envelope Lifecycle** — active / suspended / revoked / expired / superseded; a revoked policy can't retroactively authorize.
- **Delegated Authority** — one human, many scoped authorities, each independently governed.
- **Envelope Succession** — versioned policies, so authority can be reconstructed through time.
- **Authorization Binding** — every settlement references the exact policy that authorized it, on-ledger.
- **Multi-Rail Verification** — the same verification model, rail-agnostic (the settlement rail is an implementation detail).
- **Evidence Layer** — every decision produces independently replayable evidence.

## Design principles the roadmap holds to

- Humans delegate authority, not individual payments.
- Authority is bounded, versioned, and revocable.
- Settlement is never sufficient for unlock.
- Independent verification is required before release.
- Eterna never holds custody or signing keys.
- Every authorization decision produces replayable evidence.
- Favor fail-closed over fail-open.
- Keep authorization rail-agnostic.

---

*Roadmap items are designed, not commitments or shipped features. Core architecture is patent-pending — applications filed, not granted.*
