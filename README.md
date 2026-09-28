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

## Ask Jev in natural language

Once your agent has loaded the skill and you have configured your API key, ask
in ordinary conversation. You do not need to write JSON, provide a skill path,
or type a command. Phrasing and capitalization do not need to match exactly.

For example:

- “Ask Jev which existing test suite we should run first for this change.”
- “Use Jev to choose which component to investigate based on these error logs.”
- “Consult Jev on which of these files is most relevant to the bug.”
- “Run these two implementation options by Jev.”
- “Let Jev decide between the approaches we just discussed.”

If the decision is already clear from the conversation, a short follow-up such
as “Ask Jev” or “Run this through Jev” is enough. Otherwise, include the choice
and the evidence that matters. For example:

> Ask Jev whether to investigate authentication, invoice rendering, or the
> database first. Sign-in succeeds, the database query returns the invoice,
> and the download fails with an error in renderInvoicePdf.

The agent uses the current task to prepare a focused question, concrete options,
and relevant context, then calls Jev. It asks for clarification only when it
cannot infer the decision. Jev selects among the supplied options; the agent
reports the actual recommendation, confidence, and probabilities when available.
Any explanation supplied by the agent is its interpretation, not a written
rationale from Jev.

To inspect the request without calling the API, say:

> Prepare a Jev decision for these options, but only preview it. Do not make a
> live call.

Requests for Jev's decision normally make a live call when credentials are
configured. Merely discussing Jev or asking to edit the skill does not. If the
key is missing, the API is unavailable, or the answer is too uncertain, the agent
reports the fallback and continues with ordinary judgment. A recommendation is
advisory and does not grant permission for additional actions or waive checks.

## Repository contents

- `skills/jev-decide/` — portable skill, agent metadata, and CLI helper.
- `tests/jev-decide.test.mjs` — offline tests.
- `examples/decision.json` — sample decision input.
- `.env.example` — empty credential template.
- [CREDITS.md](CREDITS.md) — project provenance and references.

Local credentials and private decision files are excluded from version control.
