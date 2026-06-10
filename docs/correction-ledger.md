# Correction Ledger

Blindspot Skill is built from correction-led product work.

The important evidence is not that an agent wrote code. The important evidence is what happened after the user, reviewer, teammate, or another agent looked at the result and said: this still does not match reality.

This ledger records those correction moments and turns them into reusable blindspot patterns. A correction is treated as stronger evidence than an invented edge case because it already survived contact with a real product, real device, real review process, or real user expectation.

## Source Coverage

Local sources inspected for this pass:

| Source | Local evidence found | How it is used |
| --- | ---: | --- |
| Codex session bodies | 300 | Full local JSONL session bodies: 296 active sessions plus 4 archived sessions. These provide the strongest correction evidence. |
| Codex project/action candidate turns | 1,428 | User turns where the request was project-related and action-oriented. Used to locate high-signal sessions. |
| High-signal KaloCam Codex thread | 1 | `019e8b8f-f84b-7e91-a439-2eb29deb93eb`, 296 user turns, covering TDEE, onboarding, Apple Health, Coach, iPad, release, and this skill. |
| Additional high-signal Codex threads | 10+ | App Review, TestFlight, iPad, Coach data mismatch, meal history, fasting, exercise, notification, payment, and build/deploy threads. |
| Claude Code retained main transcripts | 23 | Full local JSONL transcript bodies in `~/.claude/projects`. |
| Claude Code retained subagent traces | 6 | Execution traces used only as supporting evidence, not as user-facing main sessions. |
| Claude Code standalone transcript exports | 2 | Complete JSONL transcript-style exports. |
| Claude Desktop Code metadata | 30 | Titles, cwd, turn counts, and session links. Useful for locating sessions, not full message evidence. |
| Claude prompt history session IDs | 288 | User prompt history only. Used as lower-confidence evidence because assistant replies and diffs are missing. |
| Claude usage event session IDs | 94 | Session activity evidence only. |
| Unique Claude local session identifiers | 377 | Union of prompt-history and usage-event IDs. This is not the same as 377 retained full transcripts. |
| PieBox local sessions | 7 | Small local session set, mostly non-KaloCam, used as supporting evidence for general agent blindspots. |
| PieBox message files | 232 | Message metadata and parts; only 19 user-like messages with meaningful extracted text in this local store. |
| PieBox session diffs | 322 | Useful for future deeper repository-diff reconstruction. |
| PieBox LLM fetch dumps | 4,858 | Raw provider dumps, 2,983 Claude-named. Classified separately from user-facing coding-agent conversations. |

## Evidence Tiers

| Tier | Meaning | Use |
| --- | --- | --- |
| A | Full transcript or session body plus concrete user correction, code review, screenshot, build/release result, or App Review feedback | Can support a named ledger row |
| B | Prompt-history or metadata plus enough user text to infer the product issue, but missing assistant replies or full diffs | Can support a repeated pattern, not a precise defect claim |
| C | Diff-only, provider dump, queue task, or generic PieBox session with limited product context | Supporting signal only |

Public wording should not imply that every local session identifier was fully hand-labeled. The honest claim is that the skill was distilled from two real large product projects, 481 local conversations / task records, 1,132 correction-style interaction signals, and the highest-signal correction threads manually analyzed into the 69 traceable patterns below. The underlying local corpus contains 300 Codex session bodies, 377 Claude local session identifiers, and supporting PieBox logs.

## Conversation Inventory

| Source | Session | Evidence tier | What the user asked to modify or re-check | Blindspot exposed |
| --- | --- | --- | --- | --- |
| Codex | `019e8b8f-f84b-7e91-a439-2eb29deb93eb` | A | Fixed TDEE allowance, food preferences, onboarding activity, Apple Health, Coach cards, iPad HealthKit, release, Blindspot Skill | Main correction spine: source truth, user language, platform no-data, AI context, release evidence |
| Codex | `019e6736-25f4-72b2-add1-53577b33b0a6` | A | TestFlight/App Review build, offline flicker, exercise date, weight chain, camera entry points, HealthKit denial | Release-layer mismatch, offline state, business date, multi-entry drift |
| Codex | `019ea510-91b4-7e83-813a-ee9d65f98bd6` | A | App Review purpose strings, HealthKit compliance, onboarding Health page, calorie target explanation | Native/i18n release surfaces and reviewer-visible truth |
| Codex | `019e870b-e5f7-7d52-9f98-100fe7ac1640` | A | iPad UI compatibility, Apple account issue, iPhone-compatible window on iPad | Real runtime environment is not the same as hardware category |
| Codex | `019db51e-2594-7bf1-a15e-21611b8673d5` | A | Home vs Coach goal mismatch, Coach output content and visual treatment | Same-data consistency and structured explanation |
| Codex | `019e0aa4-dc62-7710-99ea-0024b66f0def` | A | Meal history, past meal detail, food photo/detail navigation | Historical data model and entry navigation |
| Codex | `019dd863-23a2-78e2-8b0b-1c8b5ed34410` | A | Fasting first-load flash and stop failure | Transition state and old async state |
| Codex | `019dd21a-2f7a-7b01-970b-1605d7b6934e` | A | Fasting reminders and stage display | Time-state modeling and notification wording |
| Codex | `019dccba-b030-7f11-867b-99a302876a73` | A | Natural-language meal logging error and verification | AI parsing path and real test proof |
| Codex | `019e0217-abf0-7013-a310-5a229c80afef` | A | Coach interaction after logging a meal, suggested prompts, fake affordances | Actual user flow vs imagined chat flow |
| Codex | `019db50b-80ca-7bf3-9dd5-d3b2fa87e390` | A | Coach streaming output looked wrong during generation | Streaming UX and partial-render states |
| Claude Code | `07dcd81a-be2e-4242-9557-cf209d728ac6` | A | Coach nutritionist conversation and visual cards requirement doc review | AI context leakage, prompt vs guardrail, actual pipeline path |
| Claude Code | `f4dffc8a-e5a8-46bd-9876-8d5dc2168d34` | A | Fixed TDEE and food preference documents reviewed against code | Spec-code contradiction and stale formula remnants |
| Claude Code | `bc98a5f6-31d9-4ef1-b524-da93fdbfe333` | A | App Store HealthKit and Coach citation/review documents | Native localized strings and compliance surfaces |
| Claude Code | `00123bd1-7658-4322-ace0-31fb40ccbc87` | A | Coach consistency, quality, and visual-tool documents reviewed against code | Avoid parallel architecture and inspect real routing |
| Claude Code | `59585b34-8473-43b9-b3a3-af0c2c213e0c` | A | Payment feature requirement document repeatedly reviewed | Cost/quota/payment source-of-truth and not-yet-implemented docs |
| Claude Code | `377470df-e034-44fb-9209-05973bc56f93` | A | Data-change weekly report rules, rank wording, deployment path | User-understandable metrics, ranking rules, wrong deploy cwd |
| Claude history | `cde4f3b9-f0a4-4cab-ac10-63972c1d2263` | B | KaloCam project errors, Coach rendering, weight chart, exercise options | Prompt-history support for multi-surface QA |
| Claude history | `cac8ce33-9e63-456f-aeb0-6b72ef855b6e` | B | Detail page clutter, photo opening, delete, snack mismatch, Coach card persistence | Detail-state cleanup and persistence mismatch |
| Claude history | `618e6145-97b1-4c90-b167-5f2b726c0d59` | B | Food recognition wrong foods, manual name edit not recalculating calories | AI extraction confidence and derived recalculation |
| PieBox | `ses_3de6ad419ffe3SlSfRL9dMYjGK` | C | 403 Forbidden page implementation continued from incomplete task | Good UI requires full state page, not just one illustration |
| PieBox | `ses_3de7f373effeHLMvdtq6NpJU8y` | C | Webpage reproduction and 403 page continuation | Visual fidelity and task continuation evidence |
| PieBox | `ses_3ba45da5affdShqLQ45cDHxR7w` | C | Research Midscene to create a skill | Skill-writing needs real API/library evidence |

## Correction Rows

| # | User correction / observed reality | Prior AI assumption | Reusable blindspot | Rule now added to the skill |
| ---: | --- | --- | --- | --- |
| 1 | Coach "set goal to 1800" still used a BMR baseline after the TDEE migration plan. | Changing display copy or output fields was enough. | Hidden reverse-calculation path. | When a number becomes canonical, audit setters, inverse math, display, cache, AI actions, and migrations together. |
| 2 | A hardcoded Coach sentence still told users exercise could add eating room. | Prompt/i18n changes covered all text. | Deterministic copy surface. | Search hardcoded server/client strings, not only prompts and locale files. |
| 3 | Weight endpoints changed the input but did not rewrite cached calorie/macros projections. | "Stored equals computed" can be an always-true invariant. | Write-time vs read-time invariant ambiguity. | State whether stored values are source of truth, projection, cache, or compatibility field. |
| 4 | Safety calorie floors differed across Coach, display, and write paths. | Existing behavior was unified enough to "reuse". | Cross-path rule drift. | Before saying "keep existing", prove all existing paths already agree. |
| 5 | Macro targets rose when calories moved from BMR to TDEE. | Only calorie goal would visibly change. | Derived-data blast radius. | List downstream derived numbers and user-visible surfaces for every formula migration. |
| 6 | Activity default appeared in more than one onboarding location. | One found default meant the default was handled. | Duplicate defaults. | Search for every initializer, fallback, and seed value when a default drives visible output. |
| 7 | An adaptive TDEE function already existed while the plan treated adaptive TDEE as future work. | Codebase matched the mental roadmap. | Existing-code ignorance. | Inspect current implementation before inventing "later" phases. |
| 8 | Taiwan/China flags created political and market risk. | Flags were harmless decorative icons. | Symbolic UI risk. | Treat flags, maps, regions, and identity markers as product/legal content, not decoration. |
| 9 | Country selection did not match the real intent: food preferences. | Original screen category was the product need. | Requirement-label anchoring. | Ask what decision the product actually needs, not what the old screen was called. |
| 10 | "Max 3" food preferences and weighting were unclear to users. | Internal scoring could be explained later. | Invisible ranking logic. | If user choices affect AI behavior, explain enough for fast choice or avoid arbitrary limits. |
| 11 | Two activeScore formulas remained in the same document. | Adding a corrected formula automatically superseded the old one. | Spec remnants. | Delete or explicitly retire old formulas, thresholds, and examples. |
| 12 | Append-only preference snapshots could grow per chat answer. | "Append-only" was enough as a design principle. | Lifecycle and retention missing. | Define creation cadence, reuse behavior, cleanup, and retention for every append-only table. |
| 13 | Deduplication keys could swallow legitimate repeated behavior events. | Idempotency is always safer. | Idempotency vs accumulation. | Separate retries from valid repeated events before adding dedupe keys. |
| 14 | Recommendation preference keys were not tied to the real recommendation registry. | Validation can be designed abstractly. | Unbacked validation. | Every enum/key validation must point to the actual registry or source file. |
| 15 | Food preference onboarding became dense, ugly, and unclear. | More collected preferences produce smarter AI. | Cognitive-load overcollection. | Onboarding should ask only what users can answer quickly and what the product immediately uses. |
| 16 | The page needed separate "meal styles" and "eating places." | One screen could collect all food preference dimensions. | Mixed mental models. | Split choices when they answer different real-world questions. |
| 17 | Activity page exposed TDEE multipliers. | Accuracy transparency helps users choose. | Internal formula leakage. | Do not show coefficients or formulas unless the user needs them to act. |
| 18 | Step ranges were less answerable than weekly workouts. | Quantified fields are clearer. | Wrong concrete metric. | Use numbers only for facts users likely know; use plain descriptions for fuzzy facts. |
| 19 | Estimated TDEE page needed to be a brief auto-transition, not a decision screen. | Every onboarding page needs a Continue button. | Information page vs action page. | If a page only confirms internal calculation, minimize copy and advance smoothly. |
| 20 | US launch meal options overemphasized Taiwan/China. | Broader global categories are always safer. | Launch-audience mismatch. | Weight examples and defaults to the launch market while keeping global inclusivity. |
| 21 | Apple Health allow, deny, skip, reconnect, return, and no-data states were blurred. | A permission flow has connected/not connected. | Missing state truth table. | Enumerate every user branch and attach UI copy to the real source of truth for each branch. |
| 22 | Denying Apple Health could still show "enabled" or "connected." | Returning from OS sheet means success. | Callback-as-proof. | A platform return is proof of return only; use an API/probe or show unknown/continue. |
| 23 | "Continue without Health" briefly flashed a Health page before moving on. | Final destination correctness is enough. | Transition-state blindness. | Test intermediate screens, not only final screens. |
| 24 | Onboarding and in-app reconnect used different logic. | Similar buttons probably shared behavior. | Entry-point drift. | Trace every button/route/modal that claims the same action. |
| 25 | iPad HealthKit had no movement data, so access looked broken. | Empty HealthKit reads mean no authorization. | No-data vs denial ambiguity. | Empty external data is not denied permission; design a no-data state. |
| 26 | A HealthKit write probe was needed to prove permission in the iPad no-data case. | Read permission status is observable enough. | Platform observability limit. | When read status is hidden, use a safe write/probe if the platform and product allow it. |
| 27 | After proof of setup, "saved but no data" copy overemphasized a non-problem. | Accurate caveats always improve trust. | Overexplained success. | Once truth is proven, lower the salience of missing optional data. |
| 28 | Home "No Health data yet" gray explainer made the product feel broken. | Empty state needs an explanation card. | Heavy empty-state copy. | For optional data, use a light title and numbers; keep setup help secondary. |
| 29 | Read-only-only and no-permission were indistinguishable to the app. | The app can always classify permission cause. | Unobservable state. | If states are indistinguishable, write UI that remains true for both. |
| 30 | OTA did not fix native permission and HealthKit behavior. | A live update fixes "the app." | Release-layer mismatch. | Name the changed layer and require matching release evidence. |
| 31 | Login buttons had mismatched font size/weight in Chinese. | Text replacement is enough for localization. | I18n typography surface. | Check layout and typography for each supported language, not just strings. |
| 32 | Region settings remained after country selection was removed. | Removing onboarding step does not affect settings. | Downstream setting cleanup. | When removing a concept, remove or repurpose all settings, storage, AI context, and copy. |
| 33 | Upload size limit had a technically true but poor prompt. | A validation error is sufficient. | User-facing failure copy. | Tell users exactly what happened and what they can do next. |
| 34 | Home UI lost the valued double-ring visual. | A cleaner redesign can replace old UI wholesale. | Existing visual contract. | Preserve user-valued interaction/visual contracts unless explicitly changing them. |
| 35 | Home Health reconnect first flashed a failed state. | Reconnect can reuse failure screen. | Wrong first responder state. | The next screen after a CTA should match the user's current intent. |
| 36 | Toast was invisible inside iOS modal. | A toast component works everywhere. | Native overlay hierarchy. | Verify modals, sheets, portals, and native containers separately. |
| 37 | Onboarding sync failure could log the user out or loop. | Initial sync is mandatory before app use. | Blocking failure state. | Non-critical setup should degrade gracefully and allow product entry. |
| 38 | Notification tap from a killed app was missed. | Warm-app event listeners cover notifications. | Lifecycle state gap. | Cover cold start, background, foreground, and killed-app entry paths. |
| 39 | Root router initialization could overwrite deep links. | Navigation setup is linear. | Initialization race. | Protect initial intents from later default route replacement. |
| 40 | Offline Coach caused severe flicker. | AI-backed panels can show loading until network works. | Offline/loading instability. | Give AI-backed UI stable offline, empty, and cached states. |
| 41 | Exercise logged for a past date saved/displayed as today. | Created time can stand in for event time. | Business date mismatch. | Store and display event date separately from created/updated timestamps. |
| 42 | Exercise and weight needed full chain audits after one visible bug. | The visible component contains the bug. | Chain-source blindness. | For records, audit create, edit, delete, sync, aggregation, display, and AI context. |
| 43 | Speech recognition cancel could still write stale text. | Leaving a screen cancels async work implicitly. | Old async overwrite. | Add cancellation/version guards for async results. |
| 44 | Permission denial could leave a dead-end. | Permission is required, so denial is just an error. | Partial usability. | Define what still works after denial and how users recover later. |
| 45 | iPad compatibility mode reported phone-width dimensions. | iPad hardware means tablet layout. | Runtime environment mismatch. | Verify actual runtime dimensions and app mode, not just device type. |
| 46 | App Store screenshots/materials had to use real product-visible states. | Generated or idealized visuals are safe for review assets. | Reviewer-visible material mismatch. | Review assets must match real app behavior and claims. |
| 47 | Native localized purpose strings overrode base config. | Updating one config file updates iOS permission copy. | Native localization override. | Inspect generated native files and localized resources in the build. |
| 48 | Apple Sign-In on iPad asked for Apple Account despite Settings being signed in. | OS account presence equals Sign in with Apple readiness. | Platform account-state nuance. | Treat system account/login provider failures as distinct recoverable states. |
| 49 | Coach meal review degraded to plain text instead of visual cards. | Prompting the model is enough to get structured UX. | Structured-output omission. | Required cards/actions should be server-built or deterministically inserted. |
| 50 | Coach mentioned a fasting window after fasting was not enabled. | Structured context was the only AI input. | AI context leakage. | Audit prompt, memory, summary, examples, tool results, and deterministic shortcuts. |
| 51 | `forbiddenClaims` were only prompt text. | A prompt constraint is a hard guardrail. | Soft guardrail mistaken for enforcement. | For "must never", add deterministic input filtering and output guardrails. |
| 52 | No first-class `fastingActive` field existed. | Absence of a note means false. | Missing source-of-truth field. | Model explicit booleans for sensitive states; absence can mean not loaded. |
| 53 | Broad fasting token scanning would block safe questions. | String match equals semantic guardrail. | Overbroad guardrail. | Guardrails need scope: block false current-state assertions, not safe discussion. |
| 54 | Card gating by meal count ignored `shouldAvoidDailyJudgment`. | Meal count is a good proxy for day completeness. | Wrong proxy metric. | Use the real decision function, not a convenient visible proxy. |
| 55 | Meal-diagnosis shortcut bypassed the planned Coach AI chain. | All Coach responses use the same planner/critic path. | Actual runtime path mismatch. | Trace the handler chain for each user entry before choosing where to fix. |
| 56 | Preset Coach questions sounded unlike real users. | Helpful prompt chips can be product-sounding. | Human phrasing gap. | Quick actions should sound like what a user would actually ask. |
| 57 | Post-meal "ask Coach" required extra taps or lost context. | Navigating to Coach is enough. | Broken handoff. | Contextual CTAs should carry context and trigger the intended analysis. |
| 58 | Nutritionist response needed emotional acknowledgement before advice. | Users mainly want macro/nutrient analysis. | Human conversation order. | Start with observed positives or empathy, then concrete goal-based adjustment. |
| 59 | Abstract wording like "more stable" created understanding cost. | A softer phrase is user-friendly. | Vague benefit language. | Say the concrete outcome or next meal action. |
| 60 | Home goal and Coach goal used different numbers. | Screens independently computing values is fine. | Same-data inconsistency. | One source of truth must feed all read surfaces, including AI. |
| 61 | Weekly report "score" was less understandable than rank movement. | Internal score communicates importance. | Internal metric leakage. | Prefer user-visible concepts like rank, trend, and category relevance. |
| 62 | Weekly report highlighted irrelevant newly collected products. | Biggest numeric change is the headline. | Ranking rule mismatch. | Define product significance in user/business terms, not raw delta only. |
| 63 | Crawler opened many tabs under retry/worker conditions. | One happy-path tab rule covers automation. | Resource lifecycle gap. | Audit retries, crashes, continuation, and cleanup for browser automation. |
| 64 | Deploy commands ran in the wrong server directory. | A command sequence is portable across servers. | Environment/cwd assumption. | Verify actual cwd, repo root, process manager, and branch before deployment instructions. |
| 65 | AI model/provider configuration was scattered. | One model env var captures the project. | Configuration locality blindness. | Map every provider/base_url/key/model/fallback surface before changing AI config. |
| 66 | README claimed a precise number of mistakes before a ledger existed. | Marketing claim can be directionally true. | Public claim without ledger. | Precise public claims need an audit trail or softer wording. |
| 67 | Selected logo option F was replaced with a different SVG-like asset. | Recreating the idea is equivalent to using the chosen design. | Reference fidelity. | When the user selects a visual option, compare final asset against that option, not just theme. |
| 68 | PieBox 403 work showed a page can be visually implemented while task continuation still needs remaining components. | Completing the main illustration completes the page. | Partial deliverable. | For UI implementation, verify every named component, route, state, and responsive variant. |
| 69 | PieBox/Midscene research task reinforced that a skill needs real API evidence, not a generic overview. | A skill can be written from high-level project description. | Shallow tool-skill abstraction. | Skills for tools/libraries should cite install, API, usage, constraints, and failure modes from real sources. |

## Patterns Extracted From The Ledger

The rows above collapse into a smaller reusable set:

1. **Correction request as evidence**: a follow-up fix request is a signal that the previous agent made an assumption. Name that assumption.
2. **State truth before UI truth**: connected, saved, enabled, synced, paid, deleted, fixed, and deployed need proof.
3. **No-data is its own state**: external systems often cannot distinguish no records, no permission, no account, delay, or platform limitation.
4. **Every entry point is a separate risk**: onboarding, settings, reconnect, deep link, modal, notification, shortcut, and detail page can bypass each other.
5. **Final state is not the full interaction**: wrong flashes, stale intermediate screens, and delayed transitions are bugs.
6. **Prompt is not a guardrail**: if false output is unacceptable, enforce it deterministically.
7. **AI has more inputs than structured context**: memory, summaries, examples, tools, and fallback shortcuts can leak old facts.
8. **Use the user-known fact**: ask for workouts, not coefficients; show rank, not hidden score; say no data, not platform-state theory.
9. **Release layer matters**: OTA, native build, backend deploy, config, migration, and App Review package are different evidence paths.
10. **Public claims need ledgers**: precise numbers and strong guarantees should point to traceable evidence.

## How The Skill Changed

This audit added or strengthened these parts of Blindspot Skill:

- `Correction-Ledger Pass`: follow-up corrections must be reverse-engineered into prior AI assumptions.
- `Source-of-Truth Audit`: callbacks, empty results, missing fields, local flags, and public metrics are proxy signals unless proven otherwise.
- `Human User Walkthrough`: includes impatient users, reviewers, tablets, long translations, no data, partial data, and stale state.
- `AI Context Audit`: requires checking prompt, memory, summaries, tools, examples, deterministic shortcuts, planners, guardrails, critics, and server-built cards.
- `Release Evidence`: requires matching the changed layer to actual user/reviewer delivery evidence.
- `Pattern Library`: now includes correction requests, visual-reference fidelity, and actual runtime path mismatches.
