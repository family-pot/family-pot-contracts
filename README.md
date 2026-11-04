# Family Pot — Contracts

Reserved repository for a future Soroban/Rust smart contract, if one turns out to be needed.

## Status: not started

Family Pot's current roadmap — tracking, dashboard, cost comparison, recurring reminders,
Stellar payment verification, and claimable balances — uses **classic Stellar operations**
(`PaymentOp`, `CreateClaimableBalanceOp`, `ClaimClaimableBalanceOp`) via the Stellar JS SDK in
[family-pot-api](https://github.com/family-pot/family-pot-api). None of that requires a smart
contract.

This repo exists so the name is reserved and the option is visible, not because work is planned
here yet.

## When this repo would activate

Only after:

1. The claimable-balance research issue (S1) in family-pot-docs is complete, and
2. A specific requirement is identified that classic Stellar operations cannot express
   (for example, conditional multi-step claims or on-chain recurring-transfer logic), and
3. An Architecture Decision Record documents the requirement, the trade-offs, and the security
   review plan, and is approved by the maintainers.

See ADR 0001 in [family-pot-docs](https://github.com/family-pot/family-pot-docs).

## Decision review

- **Last reviewed:** 2026-11-04
- **Scope:** Stellar milestones M4 (payment verification) and M5 (claimable balances).
- **Outcome:** ADR 0001 is reaffirmed. Every in-scope M4/M5 feature can be expressed with classic
  Stellar operations and has no requirement that classic operations cannot express:
  - M4 verifies a payment by reading Horizon and matching a submitted transaction hash
    (`PaymentOp`), which is read-only plus classic payment data.
  - M5 builds an unsigned claimable-balance transaction with a sender reclaim path and tracks the
    claim status (`CreateClaimableBalanceOp`, `ClaimClaimableBalanceOp`, and claimable-balance
    predicates), then lets the recipient claim without exposing keys.
  - Recurring transfers remain off-chain reminders in `family-pot-api`; no on-chain
    recurring-transfer enforcement is in scope.
- **ADR change:** none. No new ADR is required because the decision has not changed.
- **Revisit if:** a concrete requirement appears that classic operations cannot express, such as
  conditional multi-step claims or on-chain enforcement of recurring-transfer logic.

## Contributing

Do not open implementation PRs here until the ADR above is accepted. Research and proposals are
welcome as issues.

## License

MIT — see [LICENSE](LICENSE).
