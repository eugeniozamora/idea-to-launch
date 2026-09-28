# Idea to Launch — Methodology

A reusable way to take a product from idea to live, iterating product with a PM
who decides and an AI (Claude) that builds. The work runs across many separate
conversations, and each one starts with no context. Everything below exists so
that doesn't cost anything.

---

## 1. Principles

- **One source of truth.** A single `PLAN_MAESTRO.md` anchors the project. If it
  isn't there, it wasn't decided.
- **Treat it as a real business.** When unsure, pick what a founder risking their
  own money would pick. If an option only makes sense "because it's an
  experiment", it's probably wrong.
- **Verifiable criteria, always.** Every task is written so it can be checked by
  someone who didn't do it (§6).
- **Small, vertical, tested.** Build thin end-to-end slices, test first, and
  have the PM check each one (§7).
- **Diagnose before discarding.** When something failed before, find the real
  cause before rejecting the whole approach.

---

## 2. Stage structure

Stages follow dependency order, not a strict waterfall; some overlap is normal.
Every stage uses the same template:

> **Objective · What you learn · Key decisions · Deliverables · Tools ·
> Done when · Split (PM / Claude)**

| # | Stage | Produces | Done when |
|---|---|---|---|
| 1 | Ideation & concept | One-line product statement, moat thesis (why an incumbent can't copy it) | Both written down |
| 2 | Market listening | Doc of what real users said in their own words: pains, triggers, vocabulary, competitors they actually use | Voice and hooks documented with real quotes |
| 3 | Positioning & brand | Brand guide: name (legal/domain checked), promise, manifesto, voice do/don't, competitive map | Name secured; voice and differentiation vs 3 competitors written |
| 4 | UX/UI | Flow map, style guide with tokens, clickable prototype of the core screens | Prototype approved; tokens ready to implement |
| 4B | Landing + waitlist | Live landing page (fake door) collecting real sign-ups | Form stores real data end-to-end |
| 5 | Development (MVP) | Working product, built as numbered vertical slices | Per-slice criteria pass; PM QA done in a real environment |
| 6 | Launch | Accounts, compliance and privacy docs, listing copy, beta → production | A stranger can sign up and use it |
| 7 | Analytics | Measurement plan, dashboard, first cohort read | Dashboard answers "who comes back?" and "who pays?" with real data |
| 8 | Growth & iteration | Channel experiments, measured CAC, one full data → change → measure loop | One channel with measured CAC and one closed iteration loop |

**Stages get rewritten when reality changes.** Mark the change inline
(`REFRAMED <date>: reason`). Don't silently edit the old plan. Examples: moving
a smoke test to a later stage because the creative would be better, or replacing
an analytics SDK with platform-native stats after a privacy decision.

---

## 3. Folder conventions

```
/PLAN_MAESTRO.md            ← source of truth (context, locked decisions, stages, state)
/LOG.md                     ← session log, newest first (see §10 — split this out from day 1)
/docs/stage-N-name/         ← deliverables of each stage
/docs/plans/                ← detailed implementation plans per stage/slice
/docs/<Ops manual>.md       ← repeatable manual procedures (release, deploy, consoles)
/_archive/                  ← superseded docs, kept for learning, never used as guidance
/app/  /landing/  ...       ← code, one folder per deployable
```

Name deliverable docs by what they are (`brand-guide.md`, `flows.md`,
`style-guide.md`), and link them from the stage entry in the plan.

---

## 4. PLAN_MAESTRO.md structure

| § | Content |
|---|---|
| 0 | How to use this document (the session rituals below) |
| 1 | Context, goal, **role split**, **locked decisions table**, constraints |
| 2 | Product concept: core loop, what makes it different, red lines (e.g. privacy) |
| 3 | Stack and architecture (recommendation and the reasons for it) |
| 4 | The stages, using the template from §2 |
| 5 | Working method (a short pointer to this file) |
| 6 | Risks and mitigations |
| 7 | Meta-learnings (lessons about the product and market) |
| 8 | **State and log**: global status line, next step, open items |

### Session rituals

- **Start:** *"Read PLAN_MAESTRO.md §8. We're on Stage N, task X."* Claude reads
  the plan and the linked docs before doing anything.
- **Close:** update §8 with what was done, the decisions made (with the reason),
  what was verified and how, and the **concrete next step**. A session that
  doesn't update §8 didn't happen.
- Ready-to-paste versions of these prompts, plus the project kickoff prompt, are
  in `PROMPTS.md`.
- **Global status line** at the top of §8: one glance shows every stage's state
  (✅ / 🔨 / ⬜ / ⚠️ reframed).

---

## 5. Recording decisions

| Kind | Where | Format |
|---|---|---|
| **Locked** | §1 table | Decision · Choice · Notes. Reopen only on purpose, with a dated note. **Hard rules** get a ⚠️ and the past failure that justifies them. |
| **Product decision (dated)** | §8 entry, titled `📌 DECISION (<date>)` | What, why (policy, brand, data), what it cancels, and what stays dormant in the code |
| **Parked** | §8 or the stage doc, titled `📌 PARKED` | The question, the options (a/b/c), the recommendation, the trigger that would reopen it. "Not a forgotten slice" is stated explicitly. |
| **Booked** | §8, titled `📌 BOOKED <stage>` | Analysis already done plus the order to execute it in, so the future stage starts warm |
| **Reversed after QA** | Inside the slice entry, under "QA revisions" | Numbered list: what was built, why it confused or failed with the product in hand, and what replaced it. Rejected options are marked "do not reopen". |
| **Corrections** | Where the wrong note was | Say explicitly that it corrects an earlier entry and what was wrong. Don't just overwrite it. |

Tag every piece of feedback with its **source and independence** (internal
partner vs real user; N=?). One insider's opinion is not validation, even if
you act on it.

---

## 6. Verifiable criteria

Every task is written as:

```
[action] → verify: [observable check]
```

- "Add delete-all" → verify: test proves no rows remain in any table, and the
  typed confirmation button stays inert until armed.
- "Deploy landing" → verify: form submission returns 200 and the record appears
  in the DB.

Multi-step work is planned as a numbered list with one verify per step. Strong
criteria let Claude work in an autonomous loop. Weak ones ("make it work") need
constant check-ins. Writing good criteria is the PM's main skill here.

---

## 7. Vertical slices + TDD

- Each stage-5 plan breaks the MVP into **numbered vertical slices**, each
  delivering one user-visible capability end-to-end (data → logic → UI).
- **Milestones** group slices and end with a PM QA checkpoint (e.g. slices 1–4 =
  the core loop works).
- Per slice: failing test → implement → green. Then **lint/type-check clean, the
  full suite green, and the test count recorded** in the log.
- The tests that matter are **invariants of the promise**, not only units: data
  really deleted, contrast meets WCAG, translations in sync, no overflow at max
  text scale.
- **PM QA in a real environment** after each slice. Expect decisions to change
  here. That's the point, and small slices keep it cheap.
- **Cross-cutting polish goes last.** Design-token and consistency passes run
  as one final slice, once every screen exists, so the sweep happens once.
- Anything left out on purpose is logged as "inert on purpose (slice N)" so it
  doesn't read as a bug.

---

## 8. Roles and context tools

**Split:**
- **PM / Product Owner / QA (human):** sets goals and criteria, decides, runs QA,
  owns accounts, money, publishing and outreach.
- **Claude:** architecture, code, tests, drafts of copy and assets, analysis
  with a recommendation. Proposes; doesn't decide product questions.
- **Operator (optional, cheaper model or human):** issue and board admin, so
  the main model's reasoning budget goes to the actual work.

**Where context lives:**

| Tool | Holds | Doesn't hold |
|---|---|---|
| `CLAUDE.md` (global) | How you work everywhere: language, commit format, git safety, simplicity rules, UI rules | Anything project-specific |
| `CLAUDE.md` (project) | Stack, commands, commit scopes, project hard rules, "read PLAN_MAESTRO first" | State or history |
| `PLAN_MAESTRO.md` | Decisions, stages, state | Code-level detail that git already records |
| Plans (`docs/plans/*.md`) | The detailed plan for a stage or slice, written before coding and approved by the PM | Status updates after the work |
| Memories | Short, non-obvious facts that survive across sessions: environment gotchas, user corrections, pointers to docs | Copies of plan content. Point to the source instead. |

Memories reflect when they were written. **Check them against the code or doc
before acting**, and fix or delete ones that turn out wrong.

---

## 9. Skills per step

Skills are packaged workflows in Claude Code. Invoke them by name
(e.g. `/tdd`) or ask for them ("use the diagnose skill").

| Step | Skill | Why |
|---|---|---|
| Ideation, new features, product decisions | `superpowers:brainstorming` | Looks at intent and options before anything gets built |
| Checking an idea against locked decisions | `grill-with-docs` | Tests the idea against the plan and updates the docs as decisions firm up |
| Before coding a stage or slice | Plan mode / `superpowers:writing-plans` | Plan approved by the PM, saved in `docs/plans/` |
| Building each slice | `tdd` | Write a failing test, make it pass, then clean up |
| Bugs found in QA | `diagnose` | Reproduce → hypothesis → fix → regression test |
| UI work | `frontend-design` | Deliberate visual choices inside the design tokens |
| Before closing a slice | `superpowers:verification-before-completion`, then `code-review` | Evidence before claiming it's done; review before the PR |
| Merging | `superpowers:finishing-a-development-branch` | Wraps up the branch and PR (develop → PR → main) |

Record the skill used in the session log entry ("TDD", "diagnose") so the
method can be traced later.

---

## 10. Lessons about the process

### What worked
- **The plan plus the start/close ritual** meant dozens of cold-start
  conversations with almost no lost context or repeated work.
- **Locked decisions with their reasons** stopped the same debates from
  restarting in new sessions.
- **Parked decisions with options and a recommendation** could be picked up
  and shipped weeks later in one session.
- **QA reversals were cheap** because slices were small. Several designs were
  replaced after the PM used the real thing, without much rework.
- **Invariant tests** (deletion, accessibility, translations) caught regressions
  that humans don't notice.
- **Reframing stages openly** when reality changed kept the plan honest instead
  of a fiction.
- **Keeping unfinished capabilities behind a seam, off by default** (e.g.
  payments) let the product launch without selling features that didn't exist
  yet.

### What I'd change
1. **Split the log out from the start.** The §8 log grew to ~460 lines inside
   the plan and no longer fits in one read. Keep §8 to status, next step and
   open items (under 40 lines), and move history to `LOG.md`, newest first.
2. **Log decisions, not implementation.** Many entries repeated code detail that
   the commits already had. Log: decision, reason, how it was verified, and a
   link to the PR.
3. **Keep status in one place.** The stage headers in §4 went out of date while
   §8 was current. Only the §8 status line carries state.
4. **Keep plans in the repo, with relative paths.** Plans stored in a personal
   `~/.claude/plans/` folder, with absolute machine paths, broke on renames and
   machine changes and can't be shared with a team.
5. **Use a team git flow from day 1:** `develop` → PR → `main`, with CI checks.
   Moving to it once more people joined caused a direct-to-main slip.
6. **Use one language for docs.** Mixed-language docs are fine solo but not for
   a team or client.
7. **Treat memories as pointers, not records.** A memory once recorded feedback
   backwards, and a later session acted on it. Always check the source.
8. **Put the validation gate earlier.** Building regardless of validation fit a
   learning-first goal. For a product with real stakes (B2B), keep a go/no-go at
   the listening and landing stages, and plan how to reach independent users
   before launch, not after (we ended launch with N=0 independent feedback).
