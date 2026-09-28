# Jev Decide

A standalone agent skill for asking TypeSafe Jev to choose among concrete options.
The agent prepares the question and candidates; Jev returns a recommendation,
probabilities, and confidence. The agent interprets the result and performs the
authorized work. Uncertain or unavailable results fall back to ordinary judgment.

Exported from Jev 1.0 with independent Git history. The skill and helper are
unchanged; the Unity workflow and hello-world demo are not part of this repository.

## Quick start

Requires Node.js 22+; no third-party packages to install.

```sh
npm test
npm run jev:preview
```

Both commands run offline. The preview uses `examples/decision.json` and does not
simulate a Jev answer. The tests exercise transport fixtures and validation, not
model quality.

For a live call, copy `.env.example` to `.env` and set `TYPESAFE_API_KEY` locally.
Obtain a key from [TypeSafe](https://console.typesafe.ai). Optionally set
`TYPESAFE_MODEL` (default: `jev-latest`). The `.env` file is ignored by Git.

```sh
npm run jev:check
npm run jev:try
```

The check reports credential availability without displaying the key. The live
command sends the example decision to TypeSafe using your account. Replace the
example with your own narrow question and candidates as needed.

## Use the skill

The portable skill directory is `skills/jev-decide/`; it contains `SKILL.md`,
agent metadata, and the dependency-free helper. Copy that whole directory into
your agent's skill directory, or have your agent read its `SKILL.md` directly.
No files outside the skill directory are needed to run the helper.

Within this repository, `AGENTS.md` routes requests such as “Ask Jev which test
suite to run first” to the skill. See [the skill instructions](skills/jev-decide/SKILL.md)
for the input format, direct CLI usage, privacy controls, and result semantics.

## Repository contents

- `skills/jev-decide/` — portable skill, agent metadata, and CLI helper.
- `tests/jev-decide.test.mjs` — offline tests.
- `examples/decision.json` — sample decision input.
- `.env.example` — empty credential template.
- [CREDITS.md](CREDITS.md) — project provenance and references.

Local credentials and private decision files are excluded from version control.
