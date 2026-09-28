# Jev Decide skill repository

When the user asks to use, ask, consult, or run a decision by Jev, read and apply
`skills/jev-decide/SKILL.md`. Infer the decision from the current conversation.
Discussing, exporting, or editing the skill does not trigger a live API call.

Keep the skill self-contained and preserve its advisory role and fallback behavior.
Run `npm test` and `npm run jev:preview` after helper changes. Tests use offline
fixtures; do not describe them as model-quality validation. Keep credentials in
an ignored `.env` file and private decision inputs in ignored `.jev/`.
