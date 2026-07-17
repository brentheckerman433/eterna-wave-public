# Security Model

This describes Eterna's security **properties** at a high level — the guarantees the design is built to provide. It does not describe how any of them is implemented.

## The properties

**Non-custodial.** Eterna holds no keys, never signs, and is never in the flow of funds. The owner's own wallet signs every payment; keys never leave it. The verifier has no position in the transaction it verifies.

**Settlement is not authorization.** A settled transaction proves money moved. It does not prove anyone allowed it. Eterna treats settlement and authorization as separate facts and never conflates them.

**Independent verification before release.** Nothing unlocks until Eterna verifies the settled transaction — from its own read of the public ledger — against the terms that were declared before signing. No client-supplied result is trusted as the basis for release.

**Refusal before existence.** An out-of-policy request is refused *before* anything is signed. No payload is created, no transaction exists, no funds move — and the refusal itself is recorded as evidence.

**Fail-closed.** When verification cannot complete, or state is uncertain, the default is to keep the resource locked. Eterna does not release on ambiguity.

**Replayable evidence.** Every outcome — pass, refusal, verification failure — produces a receipt that can be independently checked against the public ledger, without trusting Eterna.

**Publicly verifiable.** Governed payments are inspectable on XRPL mainnet (SourceTag `2606150008`). The trust model does not require trusting Eterna's backend; it requires only the public ledger.

## Why the verifier must be independent

A custodian verifying its own settlements is marking its own homework. A wallet gating its own signatures has a position in every transaction it would referee. Verification only has value if the verifier has no stake in the transaction. Eterna has none.

## What is not covered here

This document is intentionally high level. The implementation of the verification path, the settlement-verification handling, the policy evaluation, and the evidence mechanism are the core of the system and are **not** described in this repository.

---

*Core architecture is patent-pending — applications filed, not granted.*
