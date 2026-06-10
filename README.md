<p align="center">
  <img src="assets/readme-banner.png" alt="Blindspot Skill - Make AI agents think through what they are about to miss" width="100%" />
</p>

<p align="center">
  <a href="README.md"><img src="https://img.shields.io/badge/README-English-111827?style=for-the-badge&labelColor=1e293b" alt="English README"/></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/README-中文说明-22c55e?style=for-the-badge&labelColor=1e293b" alt="中文说明"/></a>
</p>

# Blindspot Skill

<p align="center">
  <em>Make AI coding agents think through what they are about to miss.</em>
</p>

<p align="center">
  <img src="assets/blindspot-skill-logo.png" width="84" height="84" alt="Blindspot Skill" />
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-fbbf24?style=for-the-badge&labelColor=1e293b" alt="MIT License"/></a>
  <a href="#install"><img src="https://img.shields.io/badge/Tools-Codex%20%C2%B7%20Claude%20Code-111827?style=for-the-badge&labelColor=1e293b" alt="Supported agents"/></a>
</p>

Blindspot Skill is a pre-implementation skill for AI coding agents.

Have you run into this?

The agent writes the code. It runs. The UI looks fixed. Then you test it on a real device and find that it missed another entry point, misread a state, wrote copy no real user understands, or treated "returned from the system flow" as "success."

**Blindspot Skill exists for that exact moment.**

It was distilled from two real large product projects. Across local Codex, Claude Code, and other agent-tool history, I found **481 local conversations / task records** and **1,132 correction, rework, follow-up, and plan-review interaction signals** left by the product builder during real-device testing, code review, App Review iteration, and deployment.

I then reviewed the highest-signal chains and did not just record "what was wrong." I reverse-engineered what the agent had assumed, why that assumption failed in the real product, and distilled the result into **69 traceable agent blind spots**.

These were not compiler errors. They were the product mistakes Codex, Claude Code, and other coding agents most often make and least often catch by themselves: permission states that lie, old logic that survives in another route, AI memory leakage, technically correct copy that users cannot understand, OTA updates that cannot fix native behavior, and one entry point fixed while another remains broken.

The goal is simple: **before the agent writes code, make it think through how a real user could break the feature.**

The audit trail is here: [docs/origin-audit.md](docs/origin-audit.md). The correction-level ledger is here: [docs/correction-ledger.md](docs/correction-ledger.md).

The pattern was painfully consistent: AI agents are fast at code, but they miss the boring product reality around the code. They forget entry points. They trust local flags. They confuse empty data with failure. They call prompt text a guardrail. They ship UI copy that only engineers understand. They fix the screen in front of them and miss the release path users actually receive.

Blindspot Skill turns those mistakes into a repeatable pre-build pass. Before the agent writes code, it has to walk through the request like a real user and hunt for the hidden product, state, regression, source-of-truth, AI-context, visual, integration, and release-path blind spots it would normally skip.

## Who This Is For

Blindspot Skill is mainly for people using AI agents to build real products.

You do not need to be a professional engineer or a full-time product manager to use it. In fact, it is most useful when you have a product idea, screenshot, bug report, competitor reference, or "this feels wrong" instinct, but you do not know how to spell out every state, API, permission, edge case, regression, and release constraint before asking an agent to code.

Use it if you are:

- an indie builder, founder, designer, operator, creator, or domain expert building with Codex, Claude Code, or another coding agent
- a non-technical or semi-technical product owner who wants the agent to ask better questions before implementation
- a product manager who wants a fast pre-build pass over user flows, success states, copy, edge cases, and release risk
- an engineer who wants the agent to stop at the product boundary before jumping into code

The skill does not replace your judgment. It helps both you and the agent notice the things neither side had fully specified yet.

## What Human Corrections Revealed

| What the audited corrections exposed | Agent blind spot |
| --- | --- |
| The UI claimed something was connected, saved, or enabled when the system could not prove it | False success states |
| Empty external data was treated as failed permission or failed sync | No-data vs denied/unknown ambiguity |
| One entry point was fixed while onboarding, settings, modal, or detail page still used old logic | Entry-point drift |
| The final screen was correct, but the transition briefly flashed the wrong state | Transition-state blindness |
| A live update was expected to fix behavior that actually required native, backend, config, or review changes | Release-layer mismatch |
| AI output repeated outdated facts from old memory, summaries, examples, or prompt text | AI context leakage |
| Prompt instructions were described as hard guardrails even though the model could ignore them | Soft guardrails mistaken for deterministic enforcement |
| A required visual or structured response degraded into plain text | Structured-output omission |
| Copy was technically accurate but real users could not quickly understand what to do | User-language blindness |
| A read path was unified but write paths, caches, projections, or related surfaces stayed stale | Partial-chain fixes |

The core move is simple: when a user asks an agent to "fix this again", Blindspot Skill treats that as evidence. It asks what the previous agent assumed, what the real user observed, and which reusable rule would have caught the miss before code was written.

If you use AI coding agents to build real products, this skill is meant to catch the mistake before your users, reviewers, or teammates do.

## Why It Exists

Most AI coding failures do not start with syntax.

They start when the agent does not ask:

- What would make this success state false?
- What does a first-time user believe after seeing this copy?
- Which other button, route, modal, job, or setting uses the same behavior?
- Can old data, cache, memory, or async responses overwrite the latest user action?
- Is this prompt rule actually enforceable?
- Will users and reviewers receive the matching frontend, backend, native, and config version?

Blindspot Skill makes the agent answer those questions before it writes code.

## Quick Demo

User:

```md
Make this permission flow simpler.
```

Without Blindspot Skill:

```md
The agent rewrites the copy and ships a cleaner screen.
```

With Blindspot Skill:

```md
The agent first checks:

1. What proves the permission is really enabled?
2. What should the UI say if the platform returns but the result is unknown?
3. Do onboarding, settings, and reconnect buttons use the same flow?
4. Can this ship through a live update, or does it need a native build?
5. What does an impatient first-time user understand from the title and button?
```

The second version prevents a cleaner-looking UI from lying to users.

## What It Catches

| Blind spot | What it prevents |
| --- | --- |
| False success state | UI says saved, connected, synced, or paid before there is proof |
| Preview vs final | Half-edited or preview data becomes real too early |
| Entry-point drift | Similar buttons behave differently across screens |
| Same data everywhere | Home, detail, export, notification, and AI summary disagree |
| External no-data ambiguity | Empty source data is mistaken for denial or failure |
| Old state overwrite | Slow requests, caches, jobs, or webhooks revert fresh user actions |
| Permission denial | Rejecting one permission blocks the whole product unnecessarily |
| AI context leakage | Old memory, summaries, prompt examples, or tool results leak stale facts |
| Soft guardrails | Prompt-only rules are mistaken for deterministic validation |
| Visual regression | Type checks pass while small screens, tablets, long text, or large font break |
| User-language blindness | Internal formulas and vague abstractions reach the user |
| Release mismatch | Users, reviewers, frontend, backend, native build, and config see different versions |

## Install

### Codex

Copy the skill directory into your Codex skills folder:

```bash
mkdir -p ~/.codex/skills
cp -R skills/codex/blindspot ~/.codex/skills/blindspot
```

Restart Codex or open a new session if the skill list does not refresh immediately.

### Claude Code

Copy the skill directory into your Claude skills folder:

```bash
mkdir -p ~/.claude/skills
cp -R skills/claude/blindspot ~/.claude/skills/blindspot
```

You can also import the packaged file:

```text
packages/blindspot.skill
```

## Use

```md
Use agent-blindspot before coding.

My request:
Build a customer import feature.
```

The skill should output:

- a blindspot read
- likely directions
- real-user walkthrough
- source-of-truth audit for success states
- existing behavior contract for regressions
- AI context audit when AI output is involved
- release evidence requirements
- at most 3 important questions
- after confirmation, a buildable development brief

## Examples

See:

- [Customer import](examples/customer-import.md)
- [Subscription paywall](examples/subscription-paywall.md)
- [Calendar event](examples/calendar-event.md)
- [Admin dashboard](examples/admin-dashboard.md)
- [AI summary feature](examples/ai-summary-feature.md)

Each example includes:

1. Original fuzzy request
2. Skill questions
3. Development brief outline

## Evaluation Ideas

This skill is not evaluated by whether it writes code. It is evaluated by whether it catches hidden product decisions before code is written.

A good response should:

- ask no more than 3 questions at a time
- avoid database/API/schema questions before product rules are clear
- include a not-doing section when scope is cut
- explain what could break if something is skipped
- catch hidden state, data, context, failure, permission, AI, visual, or release problems
- downgrade success states that do not have a verifiable source of truth
- include negative acceptance checks for high-risk requests
- produce a brief a coding agent can implement after the user confirms direction

See [eval prompts](evals/prompts.json).

## Project Structure

```text
blindspot-skill/
  README.md
  README.zh-CN.md
  assets/
  skills/
    codex/blindspot/SKILL.md
    claude/blindspot/SKILL.md
  packages/
    blindspot.skill
  docs/
    origin-audit.md
    correction-ledger.md
    patterns.md
  examples/
  evals/
```

## License

MIT
