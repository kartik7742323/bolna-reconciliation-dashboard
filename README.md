# Bolna Reconciliation Dashboard

Interactive, self-contained audit of Mio AI Voice **next-retry-scheduled** calls reconciled 1:1 against the **Bolna** vendor execution API.

Open [`index.html`](index.html) in any browser — no build step, no dependencies (all data is embedded).

## What it shows

Scope: every call in our *next-retry-scheduled* bucket for campaigns started **13 Jul – 10 Aug 2026** — **195,311** executions across **27 colleges** — each checked against Bolna's live `GET /executions/{id}`. Ground truth is Bolna's own status flag + retry history, not our platform's synced record.

### Headline findings
- **26,332 (13.5%)** were actually **completed on Bolna** while our platform still holds them as "awaiting retry" — a sync gap. 99.9% are real billed conversations.
- Of those, **16,531** have the connecting attempt **invisible in Bolna's own `retry_history`** (only the top-level status reveals it) — flag `yes`.
- **8,339** retries were **stopped** vendor-side (all Anand Int'l).
- **2,693** retries were **blocked by low Bolna balance** (all CHRIST).
- Busy / no-answer / failed (157,946) verified **100% consistent** with Bolna — no hidden connects.

### Page contents
- Summary tiles + full Bolna status distribution.
- Per-college breakdown (completed / connect-invisible / stopped / balance-low).
- **Table 1** — the 26,332 completed calls (filter by connect-visibility flag).
- **Table 2** — the 11,032 stopped & balance-low calls (filter: both / stopped / balance-low).
- Every row: our status vs Bolna status, connected attempt/time, duration, cost, copyable `execution_id`, and an expandable ours-vs-Bolna `retry_history` comparison.

## Data note

The page embeds lead-level operational data (`user_id`, `execution_id`, `communication_log_id`, college names, call outcomes). It contains no names, phone numbers, or recordings. Keep this repository **private** — it is internal Meritto / client data.

## Source

Generated from `MIO_Voice.csv` (export through 14 Aug 2026) reconciled against Bolna. Full 195,311-row CSV (`Bolna_Reconciliation_all_colleges.csv`) is held separately and not committed here.
