# Security Policy

## Audit status

`PLG_SMART_CONTRACT` has completed a third-party security audit prior to testnet deployment.  
All findings have been resolved. The protocol is currently in testnet phase.

**Do not deploy funds to mainnet contracts until mainnet deployment is announced in [DEPLOY-MAINTAIN](https://github.com/The-Galactic-Federation-Of-Light/DEPLOY-MAINTAIN).**

---

## Phase 2E - Security Audit findings — 

Six findings were identified during the audit. All were resolved before proceeding to testnet.

| # | Severity | Fix |
|---|---|---|
| 1 | Critical | `transferFrom` return value enforced |
| 2 | High | EIP-712 digest uses attestor-committed timestamp, not `block.timestamp` |
| 3 | High | `txId` includes `donorNonce` — same-block collision impossible |
| 4 | High | ETH node rewards use pull-payment (`pendingWithdrawals` + `withdrawNodeRewards()`) |
| 5 | Medium | `LOCK` does not finalize `resolved=true` — governance can re-solve |
| 6 | Medium | `setNode(false)` removes node from `activeNodes` immediately |

> Final state 72/72 tests passing across all suites.

For each finding, the resolution is traceable in the `src/` commit history under the Phase 2E tag.

---

## Core Architecture of PLG_SMART_CONTRACT

*10 Foundational Principles:*

  1. **Child-First Routing** – 25% minimum ( **minChildShareBps = 2500** ) of all incoming value routes to BARNEFONDET before anything else

  2. Non-Custodial – **No hidden admin keys, no "pausable rug pull"**; transparent on-chain verification

  3. **Resonance Validation** – Transfers require field-signature (on-chain proof + off-chain attestation)
    confirming "REAL_INTENT == LOVE_REAL"

  4. Everglow-SEED Filter – **An immutable gate preventing synthetic misuse**

  5. Open governance, **20 sjeler = Ekte desentralisert system**, On-chain Voting with quorum & proposals – Multi-sig + timelock on critical parameter changes

  6. **Audit-ready** – Minimal, modular, testable

  7. Reversal-resistant – **No auto-rollback**; failures handled via separate "refund-streams" with traceability

  8. **Genesis-event reference** – Immutable proof of contract's original configuration; enables auditor verification without multi-layer view functions

  9. Open-source resonance – **Bridges human intention, machine enforcement, and soul-based governance** via CLA + PLG_SMART_CONTRACT + RI_GIFT_PORTAL

  10. **Universally structured, not democratically operated – Not all will participate, but all can receive**

---

## Immutable guarantees

The following constant is immutable and cannot be altered by governance, contract owner, or any other actor:

```solidity
uint16 public constant MIN_CHILD_FLOOR = 2500; // 25% hard floor (immutable)
```

This is the protocol's core guarantee. No proposal, vote, or upgrade can reduce the children's allocation below 25%.

The following variables operate within this floor:

```solidity
uint16 public minChildShareBps;   // Default: 2500 (25%) — governance may increase, never decrease below MIN_CHILD_FLOOR
address public childAnchor;       // BARNEFONDET primary anchor address
```

Governance can vote to allocate *more* than 25% to children. The floor is a minimum, not a ceiling.

All three are verifiable by anyone reading `src/PLGGiftRouter.sol`.

---

## Scope

The following contracts are in scope for security review:

- `src/PLGGiftRouter.sol`
- `src/PLGVotingToken.sol`
- `src/PLGTimelock.sol`
- `src/PLGGovernor.sol`

The following are out of scope:

- `lib/` — OpenZeppelin contracts (reviewed upstream by OpenZeppelin)
- `script/` — deployment scripts (no user funds flow through these)
- `test/` — test suite

---

## Known limitations

**Testnet phase:** Sepolia deployment is for verification only. No real funds.

**Governance bootstrapping:** In the initial phase, token distribution is concentrated. This is intentional and documented in the governance model. See [RI_GIFT_PORTAL](https://github.com/ARKITEKTENXxREAL/RI_GIFT_PORTAL) for the full decentralization roadmap across four chapters.

**Multi-sig dependency:** At genesis, governance tokens are held in a multi-sig wallet. The security of this phase depends on the multi-sig configuration, which will be documented in [GOVERNANCE](https://github.com/The-Galactic-Federation-Of-Light/GOVERNANCE).

---

## Reporting a vulnerability

Please use GitHub's private vulnerability reporting:

**[Report a vulnerability](https://github.com/The-Galactic-Federation-Of-Light/PLG_SMART_CONTRACT/security/advisories/new)**

Do not open a public Issue. Reports submitted here are visible only to repository maintainers.

Include:
- Contract and function name
- Description of the vulnerability
- Proof of concept or test case if possible
- Your assessment of severity

You will receive a response within 72 hours.

---

*∞INTENT==LOVE∞*
