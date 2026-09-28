# Recording decisions

Decisions are what cold-start sessions need most. Without the reason attached, the same debate restarts every few conversations.

| Kind | Where | Format |
|---|---|---|
| **Locked** | `PLAN_MAESTRO.md` §1 table | Decision · Choice · Notes. Reopen only on purpose, with a dated note. **Hard rules** get a ⚠️ and the past failure that justifies them. |
| **Product decision (dated)** | `LOG.md` entry, titled `📌 DECISION (<date>)` | What, why (policy, brand, data), what it cancels, what stays dormant in the code. |
| **Parked** | §8 open items or the stage doc, titled `📌 PARKED` | The question, the options (a/b/c), the recommendation, and the trigger that would reopen it. Say explicitly that it isn't a forgotten slice. |
| **Booked** | §8 open items, titled `📌 BOOKED <stage>` | Analysis already done plus the order to execute it in, so the future stage starts warm. |
| **Reversed after QA** | Inside the slice's log entry, under "QA revisions" | Numbered list: what was built, why it confused or failed once the product manager (PM) used it, and what replaced it. Mark rejected options "do not reopen". |
| **Correction** | Where the wrong note was | Say explicitly that it corrects an earlier entry and what was wrong. Don't just overwrite it. |

## Examples

**Locked, hard rule:**

| Decision | Choice | Notes |
|---|---|---|
| Platform | Flutter, Android + iOS only | ⚠️ HARD RULE: no web/PWA target. A previous attempt failed by starting on web and dragging that architecture to mobile. |

**Parked:**

> 📌 PARKED — Pricing model (one-time vs subscription)
> Options: (a) lifetime only, (b) monthly only, (c) both. Recommendation: (c), because the data needed to choose doesn't exist yet. Reopen when: 100 paying users or Stage 7 cohort data. Not a forgotten slice.

**Feedback tagging:**

> Source: internal partner (not independent), N=1. Acted on because it matched Stage 2 quotes, not as validation.
