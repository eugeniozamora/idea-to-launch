---
name: idea-to-launch
description: Run a product from idea to go-live with a human product manager (PM) who decides and Claude who builds, across many cold-start sessions. Covers the 8 stages (ideation, market listening, brand, UX, landing + waitlist, MVP in vertical slices, launch, analytics, growth), a PLAN_MAESTRO.md source of truth, session start/close rituals, decision records and verifiable criteria. Use this whenever someone wants to start a new app, SaaS or product from an idea, says they're a PM/founder who doesn't code and wants Claude to build it, mentions PLAN_MAESTRO.md, asks to open or close a working session on a product, asks "which stage are we on" or "what's next", or wants to plan market research, branding, a landing page, a launch or post-launch iteration — even if they never say "methodology".
---

# Idea to Launch

A way to take a product from idea to live when a **PM decides** and **Claude builds**. The work spans many separate conversations, each starting with no memory, so everything here exists to make a cold start cost nothing: one plan file holds the truth, every session opens and closes the same way, and every task can be checked by someone who didn't do it.

The full rationale is in `references/methodology.md`. Read it when the user asks *why* something works this way or wants to adapt the method.

## Roles

- **PM (the user):** sets goals and acceptance criteria, makes product decisions, runs QA in a real environment, owns accounts, money, publishing and outreach.
- **Claude:** architecture, code, tests, drafts of copy and assets, analysis *with a recommendation*. Claude proposes; it does not make product decisions on its own. When a product question comes up, present the options, recommend one, and let the PM choose.

## Figure out which mode you're in

Look for `PLAN_MAESTRO.md` in the project root before doing anything else.

| Situation | Mode |
|---|---|
| No `PLAN_MAESTRO.md`, user describes an idea | **Kickoff** |
| Plan exists, start of a conversation | **Open session** |
| User says to wrap up, close, or log the session | **Close session** |
| Mid-session work on a stage | **Stage work** |
| A decision was made, parked, reversed or corrected | **Record a decision** |

### Kickoff

1. Work through Stage 1 with the PM using the `superpowers:brainstorming` skill if available, one question at a time: the one-line product statement, the moat thesis (why an incumbent can't copy it without breaking its own brand), and who pays versus who uses it.
2. Ask whether it's B2C or B2B. For B2B, Stage 2 becomes customer interviews instead of community listening, and the go/no-go gates at Stages 2 and 4B are mandatory (see `references/stages.md`).
3. Show the PM the skeleton plan before creating files. Then create:
   - `PLAN_MAESTRO.md` from `templates/PLAN_MAESTRO.md` → verify: §0–§8 exist, locked decisions are in the §1 table, §8 holds only status, next step and open items.
   - `LOG.md` from `templates/LOG.md` with the first dated entry → verify: newest first.
   - A project `CLAUDE.md` from `templates/CLAUDE.md` → verify: under 60 lines, no state or history.
   - The folders: `docs/stage-N-name/`, `docs/plans/`, `_archive/` → verify: they exist.
   - Git: a `develop` branch and PR checks (lint + type-check) once there is code → verify: nothing goes straight to `main`.

### Open session

Read `PLAN_MAESTRO.md` §8 and the newest `LOG.md` entry, plus any doc they link for the current task. Then summarise the state in three lines and propose the session plan in the `[action] → verify: [check]` format. Don't start work until the PM agrees, because the plan is where misunderstandings are cheapest to fix.

If the PM names a stage or task, read that stage in `references/stages.md` too.

### Close session

A session that doesn't update the plan didn't happen: the next conversation will start blind. So:

1. Update `PLAN_MAESTRO.md` §8: the global status line, the **concrete** next step (specific enough that a cold session can start it), and open items. Keep §8 under about 40 lines; history belongs in the log.
2. Add a `LOG.md` entry at the top: decisions and their reasons, what was verified and how, the skills used, and the PR link. Don't repeat code detail that git already records.
3. If a stage's state changed, update only the §8 status line. Stage headers in §4 don't carry state, so they never go stale.

### Stage work

Read the current stage in `references/stages.md`. Each stage lists its objective, key decisions, deliverables, "done when" criteria and the PM/Claude split. Save deliverables in `docs/stage-N-name/`, named for what they are (`brand-guide.md`, `flows.md`), and link them from the plan.

When reality changes a stage (a smoke test moves later, an analytics SDK is dropped for privacy), rewrite the stage openly with an inline `REFRAMED <date>: reason` note. Never silently edit the old plan, because the reason for the change is the part future sessions need.

### Record a decision

Use the formats in `references/decisions.md`: locked, dated product decision, parked, booked, reversed after QA, and correction. Tag any feedback with its source and independence (internal partner vs real user, N=?). One insider's opinion is not validation, even if you act on it.

## Verifiable criteria

Write every task as:

```
[action] → verify: [observable check]
```

- "Add delete-all" → verify: a test proves no rows remain in any table, and the confirm button stays inert until the typed confirmation matches.
- "Deploy landing" → verify: the form returns 200 and the record appears in the database.

Strong criteria let you work in a loop without check-ins. If the PM gives a weak one ("make it work"), propose a verifiable version and confirm it before building.

## Building the MVP (Stage 5)

- Break the MVP into **numbered vertical slices**, each a user-visible capability end to end (data → logic → UI). Group them into milestones that end with a PM QA checkpoint.
- Per slice: failing test → implement → green, then lint/type-check clean, the full suite green, and the **test count recorded** in the log.
- Prefer tests that protect the product's promise over plain unit tests: data really deleted, contrast meets WCAG, translations in sync, no overflow at max text scale.
- Expect the PM to change their mind after using a slice. That's the point of small slices; record it under "QA revisions" in the slice entry.
- Run cross-cutting polish (design tokens, consistency) as one final slice once every screen exists.
- Anything deliberately left out is logged as "inert on purpose (slice N)" so it doesn't read as a bug.

## Other skills to use at each step

This skill runs the process; the specialised work belongs to other skills. Use them when they're installed. If one isn't, do the step inline following the same intent.

| Step | Skill |
|---|---|
| Ideation, new features, product decisions | `superpowers:brainstorming` |
| Testing an idea against locked decisions | `grill-with-docs` |
| Before coding a stage or slice | plan mode or `superpowers:writing-plans` (save the plan in `docs/plans/`) |
| Building each slice | `tdd` or `superpowers:test-driven-development` |
| Bugs found in QA | `diagnose` or `superpowers:systematic-debugging` |
| UI work | `frontend-design` |
| Before closing a slice | `superpowers:verification-before-completion`, then `code-review` |
| Merging | `superpowers:finishing-a-development-branch` |

Record the skill used in the log entry so the method can be traced later.

## Defaults learned the hard way

These come from running the method end to end on a real launch. Apply them unless the PM decides otherwise:

- **Log separate from day 1.** A log inside the plan grew to hundreds of lines and stopped fitting in one read.
- **Log decisions, not implementation.** Git already has the code detail.
- **Plans live in the repo** (`docs/plans/`) with relative paths, so they survive renames and can be shared.
- **Team git flow from the start:** `develop` → PR → `main` with CI checks.
- **One language for all docs.**
- **Memories are pointers, not records.** Check a memory against the plan or code before acting on it.
- **Validation gates early.** Keep a go/no-go at Stage 2 and Stage 4B, and plan how to reach independent users *before* launch. Launching with zero independent feedback is the failure this prevents.
- **When unsure, choose what a founder risking their own money would choose.** If an option only makes sense "because it's an experiment", it's probably wrong.
- **Diagnose before discarding.** When something failed before, find the real cause before rejecting the whole approach.
