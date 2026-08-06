# Engineering Humanizer

A portable agent skill for making software-engineering writing and code feel deliberate, precise, and consistent with the surrounding repository.

Engineering Humanizer adapts [blader/humanizer](https://github.com/blader/humanizer). It retains the original writing patterns and adds guidance for pull requests, commit messages, documentation, design notes, incident reports, code comments, reviews, tests, and source code.

The runtime artifact is a single [`SKILL.md`](SKILL.md), so the skill can run in any agent harness that supports skill-style instructions.

## Installation

### Skills CLI

Install globally with the cross-agent Skills CLI:

```bash
npx skills add Floneyyang/engineering-humanizer-skill --global
```

Update an existing installation:

```bash
npx skills update engineering-humanizer-skill --global
```

Install globally into every supported agent harness:

```bash
npx skills add Floneyyang/engineering-humanizer-skill --global --agent '*'
```

To target one configured harness, pass its agent name:

```bash
npx skills add Floneyyang/engineering-humanizer-skill --global --agent <agent-name>
```

Omit `--global` for a project-local installation that can be committed and shared with collaborators. Start a new agent session or reload skills after installation.

### Manual installation

Clone the repository into the directory where your agent discovers skills:

```bash
git clone https://github.com/Floneyyang/engineering-humanizer-skill.git /path/to/your/skills/engineering-humanizer-skill
```

For a typical Codex installation:

```bash
git clone https://github.com/Floneyyang/engineering-humanizer-skill.git "${CODEX_HOME:-$HOME/.codex}/skills/engineering-humanizer-skill"
```

You can also copy `SKILL.md` into an existing skill folder if your harness only needs the runtime instructions.

## Usage

Invoke the skill through your agent harness or ask for it directly:

```text
/engineering-humanizer-skill

[paste an engineering document here]
```

```text
Use the engineering humanizer on this pull request description.
```

Point it at a file:

```text
Humanize the prose in docs/caching-design.md.
```

## Operating modes

Engineering Humanizer has two explicit modes:

- **Audit:** Inspect the artifact and report concrete findings without changing it. Findings identify the location, the pattern or engineering problem, its effect, and a direction for correction.
- **Rewrite:** Produce the improved artifact while preserving technical meaning and protected content. The skill audits its work internally and returns the final rewrite rather than an intermediate draft.

Use audit mode when you want diagnosis only:

```text
Audit this pull request description with the engineering humanizer. Do not rewrite it.
```

Use rewrite mode when you want the artifact changed:

```text
Rewrite docs/caching-design.md with the engineering humanizer.
```

`Rewrite` is the default when you ask the skill to humanize, improve, edit, or revise something. Source-code review defaults to audit unless you ask to implement, refactor, or fix the code.

Use it for repository-aware review:

```text
Review this change with the engineering humanizer. Check whether the code fits
the repository, duplicates an existing abstraction, or adds unnecessary tests.
```

### Voice calibration

Provide a sample of your own engineering writing when you want the result to match your voice:

```text
/engineering-humanizer-skill

Here is a sample of my writing for voice matching:
[paste two or three paragraphs]

Now rewrite this design note:
[paste the draft]
```

The skill matches sentence rhythm, terminology, punctuation, and recurring habits without overriding technical correctness or repository conventions.

## What it covers

The skill contains 46 editing and review patterns:

| Group | Patterns | Focus |
|---|---:|---|
| Original humanizer foundation | 33 | Inflated claims, generic vocabulary, formulaic structure, filler, hedging, and chatbot artifacts |
| Engineering writing | 5 | Uniform structure, polished-but-empty openings, missing operational evidence, prompt echo, and missing judgment |
| Engineering code | 8 | Duplication, low-value comments, happy-path assumptions, defensive theater, repository mismatch, dependency verification, system fit, and test inflation |

It classifies the artifact before editing because a pull request, runbook, code comment, incident report, and source file have different jobs.

## Technical safeguards

Engineering Humanizer follows several hard constraints:

- Preserve technical meaning and stated uncertainty.
- Never invent behavior, causes, benchmarks, test results, guarantees, compatibility claims, or implementation details.
- Preserve identifiers, commands, paths, URLs, versions, error messages, configuration keys, and literal output unless asked to change them.
- Follow established repository terminology and conventions before generic style preferences.
- Treat writing patterns as editing heuristics, not proof of AI authorship.
- Do not rewrite code merely to make it appear human-written.

## How it differs from Humanizer

[blader/humanizer](https://github.com/blader/humanizer) focuses on removing common AI-writing patterns from prose. Engineering Humanizer keeps that foundation but makes several rules context-sensitive:

- Passive voice can be appropriate when the actor is unknown or irrelevant.
- Em dashes and other punctuation are evaluated by context instead of banned mechanically.
- Standard technical compounds such as `end-to-end`, `third-party`, and `real-time` are preserved.
- Structured lists remain when they help engineers scan steps, risks, requirements, or results.
- Diff-oriented writing remains valid in pull requests, commits, changelogs, and migration guides.

It also adds repository-level checks for code that may work locally while duplicating infrastructure, ignoring established utilities, using an unverified API, or testing implementation details instead of behavior.

## Sources

The skill synthesizes and adapts observations from:

- [blader/humanizer](https://github.com/blader/humanizer), based on [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [Signs of AI Generated Content](https://ali-dev.medium.com/signs-of-ai-generated-content-6f672aaab7e0), Ali Kamalizade
- [These are 6 Signs You are Reading Truly Human Writing](https://aaiguy.medium.com/these-are-6-signs-of-reading-truly-human-writing-5e2dffdbf428), Usman
- [AI Content Detection: 11 Signs Writers & Editors Can Spot](https://intender.com.au/ai-content-detection-signs/), Intender
- [These 15 Signs Indicate You Used AI For Writing](https://medium.com/illumination/these-15-signs-indicate-you-used-ai-for-writing-fc6d96b9e55e), Waqas Liaqat

These sources provide observations and heuristics, not reliable authorship tests.

## License

MIT. This project retains the original copyright and license notice from `blader/humanizer`.
