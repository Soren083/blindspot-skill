---
name: agent-blindspot
description: Use before implementation when a request could hide product, state, regression, source-of-truth, AI-context, visual, integration, or release-path blind spots. Especially useful for vague product requests, bug reports, screenshots, permissions, payments, app review, privacy/legal, health or sensitive data, async AI/upload flows, login/account, cross-surface data, existing UI changes, and any state that claims success, connected, synced, saved, authorized, paid, deleted, or complete. The skill makes the agent walk through the product like a real user, then produce a concrete development brief with negative cases and evidence requirements before coding.
---

# Blindspot Skill

> Make AI agents think through what they are about to miss.

Use this skill before writing code. The goal is not to create a long PRD. The goal is to catch the hidden product, state, regression, integration, AI, and release issues that make an implementation look correct while real users still hit bugs.

This skill does not write code, test the finished feature, or deploy. It produces a buildable brief and the evidence needed to know when the work is actually done.

---

## 0. Blindspot Read

Start with a one-line read:

> Reading this as: `<request type>` for `<user/audience>`, with likely blind spots around `<states/surfaces/release/data>`.

Classify the request:

| Type | Signs | Move |
| --- | --- | --- |
| Vague product ask | "make this better", screenshot, competitor reference, bad feeling | Expand 2-3 likely goals |
| Existing behavior change | bug fix, redesign, refactor, copy/UI edit, replacement | Run Regression Contract |
| High-risk state | permission, payment, sync, delete, login, app review, privacy, AI, upload | Run Source-of-Truth Audit |
| Cross-surface data | same value appears on home, settings, export, AI, notification | Map read/write paths |
| Release-sensitive | native build, backend, migration, config, cache, live update | Run Release Evidence |

If the user is asking to fix, rework, "look again", "this still feels wrong", or "why did this happen again", treat that as correction evidence, not just a new task. Infer what the previous AI implementation likely assumed, what real user behavior disproved, and which reusable blindspot would have caught it earlier.

Ask at most 3 questions, and only if the answer changes product direction. Avoid technical questions a non-code user cannot answer.

---

## 1. Human User Walkthrough

Before designing the fix, mentally use the product as real people would.

Walk through the flow as:

- first-time user who has no context
- impatient user who reads only titles and buttons
- user who denies, cancels, leaves, or returns later
- user on a small screen, tablet, long translation, or large font
- user on compatibility mode or reviewer hardware where runtime dimensions, permissions, or accounts differ from the design assumption
- user with no data, partial data, stale data, or offline state
- reviewer/support person checking whether the UI tells the truth

For each relevant persona, write:

| User moment | What they see | What they believe | What can go wrong | Safer design |
| --- | --- | --- | --- | --- |

Rules:

- Do not expose internal formulas, flags, model names, or implementation terms unless users need them.
- Use exact numbers only when users likely know or can verify them.
- If the UI can state the real situation simply, do not hide it behind vague reassurance.
- After the user completed an action, show state and next step first; put details behind secondary UI.

---

## 2. Source-of-Truth Audit

Run this for any UI state that says or implies: connected, synced, saved, authorized, paid, deleted, submitted, complete, successful, available, or up to date.

| UI says | User believes | Real source of truth | Can verify? | Safer UI if not verified |
| --- | --- | --- | --- | --- |

Acceptable proof can include:

- API response that confirms final state
- backend record or database row
- receipt, webhook, or transaction verification
- OS/platform permission API
- successful write/probe when read status is hidden
- query result from the true data source
- audit ledger for public metric, origin, release, or impact claims
- explicit user confirmation when no automatic proof exists

Rules:

- A local flag is proof of local intent only.
- A returned callback is proof that the flow returned, not that it succeeded.
- Empty data is not the same as denied permission or failed sync.
- A missing field is not automatically false; it can also mean not loaded, not modeled, or filtered out.
- A public numeric claim needs a ledger. If there is no ledger, soften the claim or create one.
- If success cannot be verified, use pending, unknown, attempted, no data yet, will try to sync, or continue without.
- Include stale-response protection when old requests, caches, webhooks, jobs, or live updates can overwrite newer user actions.

---

## 3. Regression Contract

Run this when changing existing behavior.

List what must stay true unless the user explicitly agrees to change it:

- Entry points: pages, buttons, routes, jobs, API callers, deep links, notifications.
- Visible content: labels, values, units, icons, buttons, empty/loading/error/disabled states.
- Interaction: tap, type, drag, back/cancel, repeat tap, return from external app, final commit timing.
- Data rules: source of truth, rounding, unit, timezone, persistence, sync, analytics, derived values.
- Layout: safe area, keyboard, small screen, tablet, long text, large font, orientation, clipping, overlap.
- Release: frontend, backend, native build, config, migration, feature flag, cache, live update.

For replacements, map old to new:

| Old contract | New component/library behavior | Covered? | Wrapper or extra work |
| --- | --- | --- | --- |

Do not accept type checks as proof of UI behavior. Visual and interaction risks need visual or manual evidence.

---

## 4. Correction-Ledger Pass

Run this whenever the request is a follow-up correction, bug report, screenshot after implementation, app review rejection, "still not fixed", "too ugly", "not clear", "this is not what users expect", or the user asks why an agent missed something.

Do not only answer the current fix. Reverse-engineer the miss:

| User correction | What the user actually observed | Prior AI assumption | Real blindspot | Rule to prevent next time |
| --- | --- | --- | --- | --- |

Look for these signals:

- The user says the final state is correct but there was a flash, delay, stale view, or wrong intermediate screen.
- The user says a state is false in reality: connected, enabled, saved, synced, logged in, authorized, deployed, fixed.
- The user says the UI is technically correct but confusing, too wordy, not human, or exposes internal formulas.
- The user tests a different device, language, permission choice, account state, old build, or entry point than the agent optimized for.
- The user asks why a previous fix worked on one surface but not onboarding, settings, reconnect, notification, modal, detail, or app-review build.
- The user points out that AI output used stale memory, old prompt examples, missing cards, or generic advice.

When updating a skill or a requirements document, preserve these correction rows as reusable patterns. A real correction from a real user is stronger evidence than an invented edge case.

---

## 5. Blindspot Scenario Pass

Pick the rows that apply. Do not dump the whole table into the user response.

| Blind spot | Failure mode | What to force into the brief |
| --- | --- | --- |
| Preview vs final | Half-edited or preview data becomes real | Define when data commits and what cancel/back does |
| Multiple entry points | One button is fixed, another still uses old logic | Enumerate all callers and require shared behavior |
| Same data everywhere | Home, detail, export, AI, notification disagree | Define source of truth and every read surface |
| Created time vs event time | Backfilled records appear in the wrong day/report | Define business date separately from created time |
| External integration no-data | Valid access looks broken because source has no records | Separate no-data from denied/failed |
| Proxy state | A missing field, callback, empty result, or local flag is treated as real proof | Name the proxy and require the true source of truth |
| Permission denial | Product blocks too much or says enabled falsely | Define partial usability and recovery path |
| Old async overwrites new | Slow response, cache, job, or webhook reverts UI | Add request/version/stale guards |
| Transition flicker | Final state is right but user sees wrong state briefly | Check loading, return, repeated tap, and intermediate states |
| Intended path mismatch | The user path bypasses the route, module, or guardrail you plan to change | Trace the actual handler chain for each entry point |
| Prompt as guardrail | AI ignores a soft instruction | Use deterministic input filter/output guardrail when "must never" matters |
| Old AI memory leaks | AI repeats outdated user setting or old facts | Audit prompt, structured context, memory, summary, examples, tools |
| Structured output missing | Required cards/actions degrade to text | Define server-built or required structured outputs |
| Copy is correct but unclear | User cannot choose quickly | Rewrite in user-known concepts and concrete actions |
| Non-default environment | Long language, tablet, small screen, review device breaks | Include device/language/layout acceptance |
| Release mismatch | Users/reviewers see old code or wrong layer | Require matching deploy/build/update evidence |
| Public claim without ledger | README, release note, or product claim uses a precise number or guarantee without proof | Link evidence, maintain a ledger, or use a softer claim |

---

## 6. AI Context Audit

Run this when AI output, recommendations, summaries, memory, tools, or generated UI cards are involved.

List every AI input channel:

- system/developer prompt
- user message
- structured context
- retrieved memory
- conversation summary
- tool results
- examples/few-shot text
- server-side card/action builders
- output critic, guardrails, repair step
- deterministic short-circuits or fallback responses that bypass the normal AI chain

For each sensitive or forbidden claim, label the enforcement level:

| Claim/rule | Input channel | Enforcement | Evidence |
| --- | --- | --- | --- |

Enforcement levels:

- Soft guidance: prompt asks the model to behave.
- Deterministic input filter: bad context is removed before the model sees it.
- Deterministic output guardrail: bad output is blocked, stripped, or rewritten.
- Server-rendered truth: numbers/actions/cards are generated outside the model.

If the product requirement is "must never", soft guidance is not enough.

Before proposing a new AI module, scan the existing planner, router, guardrail, critic, parser, card builder, and deterministic bypass paths. Many AI regressions happen because the proposed fix targets the intended chain while the real user path goes through another chain.

---

## 7. Release Evidence

Do not mark the brief ready until the release path matches the changed layer.

| Change layer | Evidence needed |
| --- | --- |
| JS/UI only | live-update id, frontend deploy id, or cache clear; plus visual/interaction check |
| Native permissions, entitlements, platform manifest, camera, login provider | new native build number and packaged build evidence |
| Backend/API/data model | deploy id, migration result, API/database proof |
| AI prompt/guardrail/tool | deterministic negative fixture or log sample |
| App review or public release | exact version/build reviewers or users will receive |

If users may still see an older version, say that plainly.

---

## 8. Output

If direction is not confirmed, output:

```md
## Blindspot Read
Reading this as...

## Possible Directions
1. Smallest useful version...
2. Fuller version...
3. Not recommended now...

## Main Blind Spots
- ...

## Questions
1. ...
```

After the user confirms direction, output:

```md
# Development Brief

## Background

## Goal

## Existing Behavior Contract

## User Path

## Pages and Interactions

## Data and Rules

## Source of Truth

## Reality Check
Counterexamples that could make this wrong: different entry point, denied/unknown/no-data state, stale cache, old AI memory, tablet/small screen, long translation, release mismatch, reviewer environment.

## Edge Cases

## AI Behavior

## Not Doing
| Not doing now | Why skip | What could go wrong | Guardrail |

## Acceptance
Include happy path, denial/failure/cancel/no-data/unknown, cross-page consistency, visual checks, and release evidence.

## Evidence Required
Screenshots/manual checks, tests, API/database proof, deploy id, update id, build number, code references, or explicit residual risk.

## Dependencies and Impact

## Later
```

Keep the response direct. Translate vague UX advice into a path, state, rule, or acceptance check.
