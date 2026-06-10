# Blindspot Pattern Library

These patterns are the core of Blindspot Skill. They are written for product thinking before code starts.

## 1. Temporary Result vs Final Result

Question: when does this become real?

Examples:

- An import preview should not create real customers until confirmed.
- A checkout preview should not reserve stock unless the product intends that.
- A draft approval should not notify reviewers before submit.

## 2. New Entry Reusing Old Entry

Question: is this actually the same flow?

Examples:

- Manual create and CSV import both create customers, but validation and error recovery differ.
- Text input and voice input both create notes, but transcription can fail.
- Photo upload and file URL import both create media, but timeout and permissions differ.

## 3. Same Data Shown In Many Places

Question: which number is the source of truth?

Examples:

- Dashboard revenue and exported revenue must use the same definition.
- Wallet balance and checkout balance must not disagree.
- Progress shown on home and detail page should follow the same rule.

## 4. Page Context Inheritance

Question: what should carry over from where the user started?

Examples:

- Creating an event from May 1 should default to May 1.
- Creating a task inside Project A should attach to Project A.
- Adding a product from Store B should not save under the default store.

## 5. Business Time vs Created Time

Question: when did it happen, not when was it entered?

Examples:

- Backfilled expenses belong to the purchase date.
- A delayed sales note belongs to the visit date.
- Inventory backfill belongs to the stock movement date.

## 6. Completion, Expiry, And Late Confirmation

Question: what counts as done?

Examples:

- A course watched to 90% may still need a finish rule.
- A task after deadline may be late, failed, or accepted.
- An appointment may need manual confirmation after the scheduled time passes.

## 7. Non-default Environment

Question: what real environments must work?

Examples:

- Translated copy may be longer.
- Small screens may hide primary buttons.
- Dark mode may break contrast.
- A streaming request may miss headers that normal requests include.

## 8. Old Request Overwrites New Action

Question: can stale data replace fresh user action?

Examples:

- Old profile response overwrites a newly uploaded avatar.
- Old cart response resets a changed quantity.
- Old cache restores a deleted item.

## 9. Failure Retry And Loading State

Question: what happens when it fails?

Examples:

- Upload progress should not loop forever.
- Payment retry should not duplicate charges.
- AI generation failure should unlock the button and explain what happened.

## 10. Permission Denial And Partial Usability

Question: can the user keep going without this permission?

Examples:

- Deny location, but allow manual address input.
- Deny photos, but allow taking a new photo if camera is allowed.
- Deny notifications, but keep in-app reminders visible.

## 11. Release Path And Version

Question: how will users get the change?

Examples:

- A frontend change may need cache invalidation.
- A backend API change may require old frontend compatibility.
- A mobile change may require a native build, not just an OTA update.

## 12. UI Promise Vs Real Behavior

Question: does the system really do what it says?

Examples:

- Delete account should delete or anonymize the right data.
- Privacy copy should match actual permission requests.
- Refund text should match support and payment behavior.

## 13. Unverifiable Success State

Question: what proves this success state is true?

Examples:

- A platform permission flow can return without proving whether the user allowed access, so the UI should not say "connected" unless another reliable check exists.
- A payment redirect can return before a webhook confirms the subscription, so the UI should show pending or verifying instead of instantly unlocking paid features.
- An upload job can be queued but not processed, so the UI should say uploaded or processing only according to the backend state it can verify.
- A local flag can prove user intent, but it cannot prove that a permission, sync, deletion, or payment actually succeeded.

## 14. Human User Language

Question: would a first-time user understand what this means and what to do next?

Examples:

- Users may understand "exercise 3-4 times a week" faster than an internal activity coefficient.
- Users may need "No data yet" rather than a long explanation of hidden platform permission status.
- Users may need one concrete next action instead of a vague recommendation like "be more balanced."

## 15. AI Context Leakage

Question: where can the AI learn an outdated or forbidden fact?

Examples:

- Structured state may be correct, but old conversation memory can still contain the previous user setting.
- Prompt examples can teach the model to mention a mode that is currently disabled.
- A tool result can be stale even when the latest screen state changed.
- A "must never say this" requirement needs deterministic input filtering or output guardrails, not only a prompt instruction.

## 16. Release Layer Mismatch

Question: does the release mechanism match the layer changed?

Examples:

- A UI copy change may ship through a live update.
- A native permission, entitlement, manifest, or SDK change usually needs a new app build.
- A backend schema change needs deploy and migration proof.
- An app-review issue needs the exact version/build reviewers will receive, not just local code.

## 17. Proxy Signal vs Real State

Question: are you treating an indirect signal as proof?

Examples:

- Empty external data can mean no records, no permission, no account setup, a platform limitation, or a sync delay.
- A callback from a platform flow can mean the user returned, not that the user accepted.
- A missing field can mean "false", "not loaded", "not modeled yet", or "filtered out".
- A local "attempted" flag can prove the app tried something, but not that the external system accepted it.

## 18. Public Claim vs Evidence Ledger

Question: can you prove the public claim you are about to ship?

Examples:

- If a README says "distilled from 1,132 correction-style interaction signals", there should be a ledger or audit trail for that number.
- If a product says "connected", it needs platform, backend, or probe evidence.
- If a release note says "fixed", it should match the version/build/update users will receive.
- If an AI feature says it follows a rule, decide whether that rule is prompt guidance or deterministic enforcement.

## 19. Intended Flow vs Actual Runtime Path

Question: does the user's real path execute the code you plan to change?

Examples:

- A normal chat route may use planner/guardrail/critic, while a "just logged a meal" route returns from a deterministic shortcut before those layers run.
- A tablet device may run an iPhone-only app in compatibility mode and report phone-width dimensions.
- A permission button in onboarding and a reconnect button in settings may look similar but call different handlers.
- A live update may change JS while App Review still sees a previously packaged native permission string.

## 20. Correction Request As Evidence

Question: what did the user's correction reveal about the previous agent's hidden assumption?

Examples:

- "It still flashes the wrong page" means the final state may be correct, but the transition state is wrong.
- "It says connected after I denied permission" means the agent treated a callback or local attempt flag as proof.
- "This entry still behaves the old way" means another button, route, modal, shortcut, or settings page bypassed the fix.
- "The AI still mentioned a disabled setting" means stale prompt text, memory, examples, summaries, or tool results leaked into the answer.
- "This wording is technically right but users will not understand it" means the agent optimized for correctness, not user-known concepts.

When the user asks for a rework, write one row before proposing a fix:

| User correction | Prior AI assumption | Real blindspot | Preventive rule |
| --- | --- | --- | --- |

## 21. Selected Reference Fidelity

Question: did the final output actually match the reference the user selected?

Examples:

- If the user chooses logo option F, do not recreate "something inspired by F" and call it done. Compare shape, material, colors, subject, composition, and tone against F.
- If the user provides a prototype screenshot, preserve the chosen information hierarchy unless the user explicitly agrees to change it.
- If a generated image is used as a source asset, save and use the generated bitmap unless there is a clear reason to rebuild it as vector or code.
- If a UI redesign is based on a mature product, identify which behaviors are being borrowed and which should not be copied.

Visual work needs reference-level acceptance, not only "looks polished."
