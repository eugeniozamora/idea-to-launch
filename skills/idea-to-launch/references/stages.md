# The 8 stages

Stages follow dependency order, not a strict waterfall; some overlap is normal. Each stage uses the same template, and the plan's §4 copies it per stage:

> **Objective · What the product manager (PM) learns · Key decisions · Deliverables · Tools · Done when · Split (PM / Claude)**

State never lives here or in §4: only the §8 status line carries it (✅ done · 🔨 in progress · ⬜ not started · ⚠️ reframed).

## Contents
- [Stage 1 — Ideation & concept](#stage-1--ideation--concept)
- [Stage 2 — Market listening](#stage-2--market-listening)
- [Stage 3 — Positioning & brand](#stage-3--positioning--brand)
- [Stage 4 — UX/UI](#stage-4--uxui)
- [Stage 4B — Landing + waitlist](#stage-4b--landing--waitlist)
- [Stage 5 — Development (MVP)](#stage-5--development-mvp)
- [Stage 6 — Launch](#stage-6--launch)
- [Stage 7 — Analytics](#stage-7--analytics)
- [Stage 8 — Growth & iteration](#stage-8--growth--iteration)

---

## Stage 1 — Ideation & concept
- **Objective:** turn a hunch into a product concept with a defensible difference.
- **Key decisions:** the one-line product statement; who pays vs who uses; the moat thesis. A feature is never a moat (an incumbent clones it in a sprint). Positioning an incumbent *can't copy without betraying its own brand* can be.
- **Deliverables:** product statement and moat thesis in `PLAN_MAESTRO.md` §2.
- **Done when:** both are written down and the PM agrees with them.
- **Split:** PM owns the vision and picks between options. Claude challenges the thesis and names the incumbents it has to beat.

## Stage 2 — Market listening
- **Objective:** learn how real users describe the pain, in their own words.
- **Key decisions:** which communities or customers to listen to; which hypotheses to test.
- **Deliverables:** `docs/stage-2-listening/` with real quotes grouped by pain, trigger, vocabulary and the competitors people actually use.
- **B2B variant:** replace community listening (Reddit, TikTok, forums) with customer interviews.
- **Done when:** voice and hooks are documented with real quotes. **Go/no-go gate:** the PM decides explicitly whether the evidence supports continuing. It's mandatory for B2B and recommended for everything else.
- **Split:** PM does interviews and approves findings. Claude designs the listening plan, synthesises sources and flags which hypotheses held.

## Stage 3 — Positioning & brand
- **Objective:** a name and voice that make the difference obvious.
- **Key decisions:** name (checked for legal conflicts and domain availability), promise, voice do/don't, competitive map.
- **Deliverables:** `docs/stage-3-brand/brand-guide.md` with name, promise, manifesto, voice and differentiation against 3 competitors.
- **Done when:** the name is secured (domain bought, no obvious trademark clash) and the voice and differentiation are written.
- **Split:** PM chooses the name and buys the domain. Claude generates options, checks conflicts it can check, and drafts the guide.

## Stage 4 — UX/UI
- **Objective:** screens built around the one mechanic that matters.
- **Key decisions:** the core flow, what stays out of it, design tokens.
- **Deliverables:** `docs/stage-4-ux/flows.md` (flow map), `style-guide.md` with tokens, and a clickable prototype of the core screens.
- **Done when:** the PM approves the prototype and the tokens are ready to implement.
- **Split:** PM reviews and decides on flows. Claude drafts flows, tokens and the prototype, using `frontend-design` for visual choices.

## Stage 4B — Landing + waitlist
- **Objective:** a fake-door test that collects real sign-ups before the product exists.
- **Deliverables:** a live landing page with its own privacy policy and a waitlist that stores real data.
- **Done when:** a form submission returns success and the record appears in the store, end to end. **Go/no-go gate:** review sign-up numbers against a target the PM set beforehand.
- **Split:** PM owns the domain, hosting account and outreach. Claude builds the page and the waitlist wiring.

## Stage 5 — Development (MVP)
- **Objective:** a working product built as numbered vertical slices.
- **Key decisions:** stack (with reasons in §3), slice order, what's inert on purpose.
- **Deliverables:** a detailed plan in `docs/plans/stage-5-mvp.md` (approved by the PM before coding), then the slices themselves.
- **Done when:** every slice's criteria pass and the PM has done QA in a real environment (device or deployed build, not only the simulator).
- **Split:** PM writes or approves acceptance criteria and runs QA. Claude builds each slice test-first. See "Building the MVP" in SKILL.md for the per-slice loop.

## Stage 6 — Launch
- **Objective:** a stranger can find it, sign up and use it.
- **Deliverables:** store or hosting accounts, compliance and privacy docs, listing copy and assets, beta then production release. Repeatable manual steps go in `docs/<ops-manual>.md`.
- **Done when:** someone outside the project installs or signs up and completes the core loop.
- **Split:** PM owns accounts, payments, legal sign-off and pressing "publish". Claude drafts copy, docs and assets and prepares the release build.

## Stage 7 — Analytics
- **Objective:** answer "who comes back?" and "who pays?" with real data.
- **Key decisions:** what to measure and what *not* to collect (privacy promises limit this; say so explicitly).
- **Deliverables:** a measurement plan, a dashboard and the first cohort read.
- **Done when:** the dashboard answers both questions from real data.
- **Split:** PM decides what matters and reads the results. Claude designs the plan, wires events and drafts the analysis.

## Stage 8 — Growth & iteration
- **Objective:** one repeatable acquisition channel and one full learning loop.
- **Deliverables:** channel experiments with measured CAC, and one data → change → measure loop closed and logged.
- **Done when:** one channel has a measured CAC and one iteration loop is closed.
- **Split:** PM runs campaigns and owns spend. Claude designs experiments, builds the changes and analyses the results.
