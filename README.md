# Stellar Split

A group expense and bill-splitting contract on Stellar. Create a pool, invite people to contribute, log shared expenses, and settle up — all on-chain. No one can manipulate the numbers, and refunds go directly to participant wallets without a coordinator touching the funds.

---

## The Problem

Group trips, shared housing costs, and team expenses are a social nightmare. Spreadsheets get out of date, one person holds all the cash, and disputes happen because nobody trusts the math. This puts the ledger on a smart contract so everyone sees exactly the same numbers, and settlement is automatic.

---

## Technical Architecture

- **Smart Contracts (Rust/Soroban):** A `SplitPool` contract manages a named group with a list of participant addresses. Each member deposits their share into the pool contract. An `Expense` log records what was spent, on what, and who paid. When the group settles, the contract calculates each member's net balance and sends refunds or debits accordingly.
- **Frontend (Next.js + Tailwind CSS):** A group creation wizard, an expense submission form (description, amount, who paid), and a settlement page showing each person's balance before and after settlement. Participants join via an invite link.
- **Scripts (Node.js/TypeScript):** `simulate.ts` spins up a Testnet scenario with multiple funded accounts, creates a pool, logs five expenses with different payers, and calls `settle()` — useful for testing and demos.

---

## Project Structure

```
stellar-split/
├── contracts/
│   ├── src/
│   │   ├── lib.rs              # Entry points
│   │   └── split.rs            # Pool, expense, and settlement logic
│   ├── tests/
│   │   └── split_test.rs
│   └── Cargo.toml
├── frontend/
│   ├── components/             # ExpenseRow, MemberBadge, SettleSummary
│   ├── pages/                  # /create, /group/[id], /group/[id]/settle
│   └── styles/
├── scripts/
│   ├── deploy.sh
│   └── simulate.ts             # Multi-account Testnet simulation
├── tests/
└── README.md
```

---

## Getting Started

```bash
# Deploy to testnet
bash scripts/deploy.sh

# Run the simulation
npx ts-node scripts/simulate.ts

# Start the frontend
cd frontend && npm install && npm run dev
```

---

## 🌊 Drips Wave Program

This repository is participating in the **Drips Wave Program**, which pays contributors in crypto for completing GitHub issues on open-source projects.

### How to Get Paid for Contributing

1. **Pick an issue** from the [Issues tab](../../issues). Each one has a complexity label:
   - `trivial` — Small, fast tasks. Good starting point.
   - `medium` — Real features. Requires reading the codebase.
   - `high` — Core logic or contract work. Higher reward.
   - `critical` — Bugs that could cause wrong fund distribution or locked funds.

2. **Create an account on Drips** at [drips.network](https://drips.network). Connect your crypto wallet and link your GitHub account in your profile settings.

3. **Claim an issue** by leaving a comment on it. A maintainer will assign it to you within 48 hours. Do not submit a PR for an unassigned issue.

4. **Submit your PR** with the issue number in the description (`Closes #X`). All tests must pass before review.

5. **Receive your payment** once the PR is reviewed and merged. Drips handles the transfer automatically.

---

## Issues (20)

| # | Title | Complexity |
|---|-------|------------|
| 1 | Write `SplitPool` contract: create group, add members, store balances | High |
| 2 | Write expense logging function in the contract | High |
| 3 | Write settlement function — calculate net balances and send refunds | High |
| 4 | Add support for USDC contributions (SAC) | High |
| 5 | Prevent duplicate member addresses in the pool | Medium |
| 6 | Write unit tests for pool creation and member management | Medium |
| 7 | Write unit tests for expense logging | Medium |
| 8 | Write integration test: full trip lifecycle (create → contribute → expenses → settle) | High |
| 9 | Build group creation wizard UI (name, members, currency) | Medium |
| 10 | Build expense submission form | Medium |
| 11 | Build settlement summary page showing each member's final balance | Medium |
| 12 | Build invite link system so members can join via URL | Medium |
| 13 | Connect Freighter wallet for contribution and settlement steps | Medium |
| 14 | Write `simulate.ts` with at least 3 members and 5 expenses | Medium |
| 15 | Fix: settlement function sends wrong refund when two members have identical balances | Critical |
| 16 | Fix: no guard against calling `settle()` before all members have contributed | Critical |
| 17 | Build `MemberBadge` component showing name and contribution amount | Trivial |
| 18 | Add expense category tags (Food, Transport, Accommodation) | Trivial |
| 19 | Add copy-to-clipboard button for invite links | Trivial |
| 20 | Write `CONTRIBUTING.md` with setup instructions | Trivial |