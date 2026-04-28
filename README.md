# Anthosphere Projects Network

> **Life is the irreducible value of any sustainable system.** — Grand Axiom

A decentralized network of life-aligned projects, where AI and a human
moderator community evaluate real-world impact on a shared ontology of
**17 Foundations** across **5 Domains**.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Status: Active Development](https://img.shields.io/badge/status-active--development-gold.svg)](#status)
[![Domain](https://img.shields.io/badge/domain-network.anthosphere.com-teal.svg)](https://network.anthosphere.com)

---

## What this is

**Anthosphere Projects Network** is a working PHP/MySQL system where:

- Authors submit projects that work in service of life
- Builders pick up tasks from those projects and earn points
- Every project and submission is scored by **Claude (AI)** and reviewed by
  **community moderators**
- Points reflect real impact through the formula
  `base × (ai_score / 100) × LIS × FAS`
- The best projects rise organically, by demonstrated usefulness

It is not a freelance marketplace, not a voting platform, not a catalog,
not a crowdfunding site. It is a **civic infrastructure** for collective
evaluation of life-aligned action.

---

## Why an axiom

Most engineering systems are values-neutral by design. This one is not.

The **Grand Axiom** — *life is the irreducible value of any sustainable
system* — is not a mission statement. It is **mathematically embedded** in
the points formula and **structurally embedded** in the database schema:

- `project_foundations` — many-to-many alignment with 17 Foundations
- Domain scores (Ecology, Energy, Psychology, Peace, Tech)
- LIS (Life Impact Scale) and FAS (Foundations Alignment Scale) as multipliers
- Audit pipeline that detects **weak foundations** — what a project lacks

A project that does not align with life cannot accumulate points in this
network. The architecture enforces the axiom; it is not a slogan.

---

## Architecture at a glance

```
Author → Submit → Claude audit (17 Foundations + LIS) → Community moderator
   ↓
Approved project → AI generates 5–7 tasks → Moderator reviews
   ↓
Builders claim tasks (soft contract, 72h, max 10 active)
   ↓
Submit result → Claude evaluates → Moderator confirms pass/fail
   ↓
points_log → members.points_total → leaderboard
```

**Stack:** PHP 8.x + MySQL 8, no framework, PDO, sessions
**AI Layer:** `AIProvider` interface, `AIConsensus` Singleton, multi-provider
strategies (single / average / weighted / majority)
**Hosting:** DirectAdmin (manual upload, no CI)
**Database:** 17 InnoDB tables + 3 VIEWs
**Active model:** `claude-sonnet-4-6`

For the full technical specification, see [`TZ_v8.md`](./TZ_v8.md).

---

## Status

**As of April 2026 — cycle is closed and operational.**

✅ Auth, registration, onboarding
✅ Project submission with re-audit guard
✅ AI task generation (5–7 per project)
✅ Soft-contract claims (72h, parallel-safe)
✅ AI evaluation + moderator confirmation
✅ Points ledger with full provenance
✅ Profile, skills auto-assignment, Impact Spectrum

🟡 In progress: admin/tasks queue, /commons catalog, real `/leaderboard`,
memory layer (Python sidecar), GPT/Gemini providers

See [`TZ_v8.md` § "Що залишилося"](./TZ_v8.md) for the full backlog.

---

## Filiation

This repository is the **engineering layer**. The **theoretical layer** —
Grand Axiom, 17 Foundations, 5 Domains, the Architect of Reality framework
— lives in:

📘 [`TonyParf/architect-of-reality`](https://github.com/TonyParf/architect-of-reality)

The two repositories are interdependent:

- *Architect of Reality* defines **what is true** about life-aligned systems
- *Anthosphere Projects Network* defines **what is built** to enact it

Neither stands alone. Both are CC BY 4.0.

---

## Authorship

- **Architect & Author:** Tony Parf (Anton Parf)
- **AI co-author:** Claude (Anthropic)
- **First public commit:** April 2026
- **Contact:** via [anthosphere.com](https://anthosphere.com)

---

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

You are free to share and adapt this work, including for commercial purposes,
**provided you give appropriate credit**, link to this repository, and
indicate if changes were made.

---

## Citation

If you reference this architecture in academic, technical, or public work:

> Parf, T. (2026). *Anthosphere Projects Network — Technical Specification v8*.
> Repository: TonyParf/anthosphere-network. Filiation: Architect of Reality
> (Parf, 2025). License: CC BY 4.0.

---

## Related work

- [anthosphere.com](https://anthosphere.com) — main platform, philosophy, articles
- [network.anthosphere.com](https://network.anthosphere.com) — this system, live
- [dfc.anthosphere.com](https://dfc.anthosphere.com) — Drone Flight Calculator
- [TonyParf/architect-of-reality](https://github.com/TonyParf/architect-of-reality) — theoretical foundation

---

*The formula is reproducible. The schema is open. The axiom is the part
that makes them coherent.*
