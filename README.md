# Eterna

This is the public reference repository for Eterna. The production stack is private: the architecture is patent-pending across 11 families (filed, not granted) and the running system holds live mainnet configuration. This repo contains the public interface surface and documentation. The system itself is evaluated live at https://governance-coach.com/doors — no credentials, no build required.

**The independent control layer for AI-initiated payments on XRPL.**

## 1. What this is

Eterna separates payment settlement from authorization. A transaction can settle on the ledger while the protected resource remains locked; release occurs only after Eterna independently reads the ledger and verifies that the settled transaction matches the terms authorized before signing.

Eterna is non-custodial by construction: it holds no keys, never signs, and is never in the flow of funds. The human signs each live payment in their own wallet.

Live today on XRPL mainnet:

- a human-signed governed payment;
- refusal of an out-of-policy request before signing;
- independent post-settlement verification before release.

Longer-term bounded authority is designed, not live. The core architecture is patent-pending; applications are **filed, not granted**.

This public repository contains high-level architecture documentation and four generic, synthetic frontend examples. It intentionally omits the verification internals, policy-evaluation implementation, production backend, signing flow, credentials, and deployment configuration.

- [`ARCHITECTURE_OVERVIEW.md`](./ARCHITECTURE_OVERVIEW.md) — public architecture boundaries
- [`SECURITY_MODEL.md`](./SECURITY_MODEL.md) — high-level security properties
- [`ROADMAP.md`](./ROADMAP.md) — designed, not-yet-live direction
- [`examples/`](./examples) — standalone synthetic interface examples

## 2. Setup

### Prerequisites

- Git, if cloning the repository
- Node.js 20 or newer, required only for the repository's test command
- A modern web browser for the standalone HTML examples

### Clone

```bash
git clone https://github.com/brentheckerman433/eterna-wave-public.git
cd eterna-wave-public
```

### Environment-variable names

The repository declares these names in `.env.example`:

- `PUBLIC_LEDGER_URL`
- `PUBLIC_LEDGER_NETWORK`
- `SOURCE_TAG`

The static examples do not load `.env.example`, so no environment file is required to open them or run the current test command. Do not place real credentials or signing material in this public repository.

### Public repository use

The production stack is not built from this repository. The production backend, build and start configuration, container configuration, and deployment configuration are intentionally not published here.

Evaluation is through the [live system](https://governance-coach.com/doors) and the [recorded run](https://youtu.be/4-34TXKdfVM). No credentials or local production build are required.

The files that are runnable from this repository are the standalone HTML examples. Open any `.html` file in [`examples/`](./examples) directly in a browser; they make no backend connection and require no build step.

To confirm that the hosted walkthrough is reachable, run:

```bash
curl -s -o /dev/null -w "%{http_code} %{content_type}\n" https://governance-coach.com/doors
```

A healthy response is `200 text/html; charset=utf-8`.

## 3. How to test

Start with the live walkthrough at **https://governance-coach.com/doors**. No credentials are required, and judges are not expected to rebuild the production stack.

1. Open the walkthrough in a browser.
2. Follow the on-screen governed-payment sequence.
3. Confirm that an out-of-policy request is refused before signing.
4. Confirm that settlement and release are presented as separate states.
5. Use the displayed public-ledger reference to inspect the settled transaction independently.

The four files under [`examples/`](./examples) can also be opened directly to review responsive layout, accessibility, state presentation, filtering, and client-side parsing with synthetic data.

The repository's only automated command is:

```bash
npm test
```

This runs Node's native test runner and currently discovers no test files. A successful run confirms that the published manifest and Node requirement are compatible; it is not a substitute for the live walkthrough.

## 4. How Codex was used

Codex accelerated development through a repeatable, reviewable cycle:

1. A human-authored specification defined one bounded change and its acceptance checks.
2. Codex wrote only the scoped code, tests, or documentation.
3. The affected production service was rebuilt without cache:

   ```bash
   docker compose build --no-cache eterna-backend
   docker compose up -d eterna-backend
   ```

4. The result was verified from outside the container through the public HTTP surface, browser behavior, and independent ledger evidence rather than an in-process success claim.
5. A security reviewer checked the change and the publication boundary by role, without becoming part of the runtime trust model.
6. The reviewed change closed as a single commit.

Concrete checkpoints from the actual Git history include:

- `7ec811e` — added the independently ledger-validated release path;
- `240c3ee` — added pre-signing, fail-closed refusal with persisted evidence;
- `1715c47` — exposed the seven-door walkthrough at `/doors`;
- `79b822f` — recorded the browser verification pass for the hosted flow;
- `faa6742` — created this public repository boundary in one commit with the architecture documents and four synthetic examples.

The public repository intentionally preserves only the final reviewed publication commit, not the private implementation iterations.

## 5. How GPT-5.6 is used

> **Placeholder:** The project owner will supply this section before submission.

## 6. Key engineering decisions

### Evaluate before, not after

Requests are evaluated against their declared authority before anything is signed. Post-settlement review cannot undo an unauthorized payment.

### Independent ledger read, not a facilitator report

Release depends on Eterna's own read of the public ledger. A facilitator's success response is not treated as proof of settlement or authorization.

### Fail-closed anomaly hold

Missing, conflicting, delayed, or unverifiable evidence keeps the resource locked. Ambiguity never becomes permission.

### Evidence-first state

State transitions are backed by durable evidence so an outcome can be reconstructed and independently checked rather than inferred from UI state.

### Non-custodial by construction

Eterna holds no keys, never signs, and never enters the flow of funds. The verifier is structurally separate from the transaction it verifies.

### Rail-agnostic

The control model separates authorization, settlement, verification, and release so the same security properties can apply across payment rails without making a rail or settlement provider the authority.

## License

Licensed under the MIT License. See [`LICENSE`](./LICENSE).

---

*Eterna.AI LLC (Delaware) · non-custodial by design.*
