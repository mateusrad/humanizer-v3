# AGENTS.md

Guidance for AI coding agents (Claude Code, Codex, Warp, OpenCode, and others)
working in this repository.

---

## What this repo is

A portable agent skill implemented entirely as Markdown. The runtime artifact is
`SKILL.md`: the agent reads its YAML frontmatter (metadata and allowed tools)
followed by the editor prompt. There is no build step and no code to run.

The skill can run in any harness that supports skill-style instructions. Do not
write documentation that limits support to one or two harnesses.

---

## Philosophy (version 3.0.0)

The skill operates on a single guiding principle: **edit the minimum necessary**.

This has two consequences for maintainers:

1. New rules must earn their place. A pattern is worth adding only if it
   represents a real, recurring AI tell that causes genuine problems and cannot
   be handled by an existing rule.
2. Refactors must not increase intervention. If a change causes the skill to
   edit more aggressively, it is a regression, even if the output looks cleaner.

---

## Key files

- `SKILL.md` — the skill itself. YAML frontmatter (`name`, `version`,
  `description`, `compatibility`, `allowed-tools`) followed by the decision
  flow, 33 patterns, type-specific rules, and the full example. **Source of
  truth.**
- `README.md` — for humans: installation, usage, philosophy, decision flow,
  intervention modes, type-specific behavior, before/after examples by text
  type, FAQ, best practices, and version history.
- `AGENTS.md` — this file. For AI agents: architecture, maintenance contract,
  versioning policy, and change checklist.
- `.claude-plugin/plugin.json` — optional Claude Code plugin manifest.
- `.claude-plugin/marketplace.json` — optional single-repo marketplace entry.

---

## Architecture (version 3.0.0)

The skill has three layers, applied in order:

### Layer 1 — Decision (before any editing)

1. Identify the text type: personal, technical, academic, institutional, or
   software docs.
2. Assess artificialness: low (1-3 tells), medium (4-8 tells), high (pervasive).
3. Choose the intervention mode: Light, Moderate, or Full.
4. Check for human signals and mark those passages as protected.

### Layer 2 — Pattern detection (the 33 patterns)

Grouped into five categories:
- Content patterns (1-6)
- Language patterns (7-13)
- Style patterns (14-19, 26-33)
- Communication patterns (20-22)
- Filler and hedging (23-25)

### Layer 3 — Type-specific rules

Applied after the patterns, based on the text type identified in Layer 1:
- Academic: neutral register, no opinion injection, fix vague attributions.
- Technical / README: imperative voice, plain register, fix diff-anchored writing.
- API documentation: fix copula avoidance and passive voice where the actor
  matters; no personality.
- Institutional: fix promotional language and significance inflation; keep
  third-person.

---

## Maintenance contract

`SKILL.md` and `README.md` must stay in sync. When you change behavior or
content, update both files in the same commit.

### Patterns

The skill defines **33 numbered patterns**. If you add, remove, or renumber
any:
- Update the README pattern table.
- Update every cross-reference in `SKILL.md` (section references like §7 or §14).
- Update the version history in both files.
- Keep numbering stable unless you are deliberately renumbering the entire list.

### Version

Three files carry a version field:
- `SKILL.md` frontmatter (`version:`)
- `README.md` version history
- `.claude-plugin/plugin.json` (`version`)

Bump all three together. `marketplace.json` intentionally omits a version field
so `plugin.json` stays the package source of truth.

### Examples

`README.md` contains six before/after examples, one per text type. If the skill
behavior changes, update the relevant example. If you add a new text type, add
a corresponding example.

### Non-obvious fixes

If you change the prompt to handle a tricky failure mode, add a short note to
the README version history explaining what was fixed and why.

---

## Versioning policy

Follow Semantic Versioning.

- **Patch** (x.x.N) — corrections to existing patterns: fixing a false positive,
  clarifying wording, correcting a before/after example, fixing a documentation
  error. No behavior change.
- **Minor** (x.N.0) — new functionality that does not break existing behavior:
  a new pattern, a new text type, a new intervention mode, a new example.
- **Major** (N.0.0) — architectural changes: new decision layers, changes to
  the core philosophy, renumbering all patterns, or any change that alters how
  the skill approaches a text type it already handled.

---

## Change policy

No change may:
- Modify the core philosophy (Principle of Minimal Intervention)
- Remove an existing pattern without replacing it with a strictly better one
- Increase intervention for a text type that the skill already handled correctly
- Introduce redundancy (two patterns that catch the same thing in the same way)
- Degrade humanization quality (the output reads worse, or sounds more robotic,
  than before the change)

---

## Mandatory checklist for every change

Before opening a pull request, verify:

1. **Compatibility.** Does the skill still run without error in all supported
   harnesses? (Claude Code, OpenCode, Codex, Warp, and any harness that loads
   Markdown skill files.)
2. **Clarity.** Is the changed section unambiguous? Could an agent misread it?
3. **Consistency.** Does the change conflict with any other section of
   `SKILL.md`?
4. **Context consumption.** Is the change as concise as it can be without losing
   meaning? Unnecessary length degrades performance in context-constrained
   harnesses.
5. **Humanization quality.** Run the changed skill on at least one before/after
   example from each affected text type. Does the output improve or stay the
   same? If it degrades, the change is a regression.

For new patterns, also verify:

6. The pattern cannot already be caught by an existing rule.
7. The before/after example is clear and representative.
8. The README pattern table has been updated.
9. The pattern count in the README heading ("33 Patterns Detected") has been
   updated if the total changed.

---

## Editing SKILL.md

- Preserve valid YAML frontmatter (formatting and indentation).
- The decision flow (Layer 1) must remain the first substantive section after
  the introduction. Agents must classify and assess before they scan patterns.
- Pattern numbering in the body must match the numbering in the README table.
- The em dash rule (§14) is a hard constraint, not a preference. Do not soften
  its wording.
- The full example at the end is canonical. If the skill's behavior changes,
  update the example to reflect the new output. Do not leave a stale example.

---

## Editing README.md

- The README must be sufficient for a new user to understand the full project
  without opening `SKILL.md`.
- Keep the six text-type examples (personal, academic, technical, README, API,
  institutional). If you add a text type to the skill, add a corresponding
  example here.
- The version comparison table must reflect the current version accurately.
- The FAQ must be updated if new behavior changes how users should interact with
  the skill.

---

## What maintainers must not do

- Break harness-neutral wording. The skill works in any agent harness that loads
  Markdown. Do not add installation or usage language that implies Claude Code
  is the only option.
- Add personality to technical or academic text types. The correct register for
  those types is neutral and plain.
- Invent content in examples. Before/after examples must demonstrate real AI
  patterns and real corrections. Do not fabricate claims inside examples.
- Merge a change that increases the pattern count without updating all
  cross-references.
- Merge a change that introduces an em dash or en dash into `SKILL.md` itself.
  The skill forbids them in output; the source file should not model them either.

---

## Known open questions (documented decisions)

These are not bugs. They surfaced during real-world testing (v3.0.2) and are
recorded here so a future contributor does not "fix" a deliberate or
undecided behavior by accident.

### Pattern #26 in non-English text

The canonical example for hyphenated word pair overuse ("cross-functional" →
"cross functional") assumes English text. In other languages, the same
compound terms (cross-functional, data-driven, real-time, end-to-end,
client-facing) are often used as English loanwords. Dropping only the hyphen
in a non-English sentence tends to read as a typo rather than a correction
("é cross functional" in Portuguese looks broken, not fixed). In testing,
the skill instead translated the term into the target language's own
predicate form (for example, "é multidisciplinar," "responde em tempo
real"). This looks like a reasonable editorial adaptation, not a failure to
apply the pattern, but it has only been observed in Portuguese and has not
been tested across other languages. Treat this as an open question, not a
confirmed rule, until it has been tested more broadly.

### Editing punctuation inside a directly attributed quotation

The Final Check and patterns #14 and #19 currently apply to the entire
delivered text, with no stated exception for quoted, attributed speech. In
testing, the skill rewrote an em dash and adjusted quote style inside a
direct quotation attributed to a named speaker. Detection Guidance already
exempts quoted or titled text from AI-pattern flagging under "Secondhand
text," but it does not address whether the Final Check's hard-constraint
patterns (em/en dashes, curly quotes) should carry the same exemption for
attributed quotes. No decision has been made. Until one is, the skill will
continue correcting this punctuation inside attributed quotes, which may not
be the desired behavior for journalistic, transcript, or legal use cases
where a quotation's exact characters carry evidentiary weight.
