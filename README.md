# Humanizer

A portable agent skill that removes signs of AI-generated writing from text,
making it sound more natural and human. Plain Markdown, runs in any harness
that supports skill-style instructions.

---

## What changed in version 3.0.0

Version 2.x focused on detecting and removing AI patterns. Version 3.0.0 adds
a decision layer before editing begins:

- **Principle of Minimal Intervention.** Edit only what has a clear AI tell.
  Leave everything else alone.
- **Text type classification.** Academic, technical, institutional, and personal
  text require different registers. The skill now identifies the type first.
- **Artificialness assessment.** Low, medium, or high. Determines how much to
  edit.
- **Three intervention modes.** Light (fix in place), Moderate (rewrite
  passages), Full (rewrite the whole text).
- **Type-specific rules.** Academic text, READMEs, API docs, software
  documentation, and institutional text each have their own editing rules.
- **33 patterns preserved.** No patterns were removed. Several were reorganized
  for clarity.

---

## Installation

### Skills CLI

```bash
npx skills add blader/humanizer
```

Update an existing install:

```bash
npx skills update humanizer
```

Install into every supported agent harness:

```bash
npx skills add blader/humanizer --agent '*'
```

Target one configured harness:

```bash
npx skills add blader/humanizer --agent <agent-name>
```

### Claude Code plugin

```
/plugin marketplace add blader/humanizer
/plugin install humanizer@humanizer
```

Invoke as `/humanizer:humanizer`.

### Manual

Clone the repo and copy `SKILL.md` wherever your harness expects skill files:

```bash
git clone https://github.com/blader/humanizer.git /path/to/your/skills/humanizer
```

Or copy only the skill file:

```bash
mkdir -p /path/to/your/skills/humanizer
cp SKILL.md /path/to/your/skills/humanizer/
```

---

## Usage

```
/humanizer

[paste your text here]
```

```
Please humanize this text: [your text]
```

### Voice calibration

To match your personal writing style, provide a sample of your own writing:

```
/humanizer

Here's a sample of my writing:
[paste 2-3 paragraphs of your own writing]

Now humanize this:
[paste AI text to humanize]
```

The skill will analyze your sentence rhythm, word choices, and quirks, then
apply them to the rewrite instead of producing generic clean output.

---

## Philosophy

Based on [Wikipedia's "Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
guide, maintained by WikiProject AI Cleanup, and expanded with a new
architectural layer in version 3.0.0.

> "LLMs use statistical algorithms to guess what should come next. The result
> tends toward the most statistically likely result that applies to the widest
> variety of cases."

### Core Principles (version 3.0.0)

1. **Preserve the author's identity.** Voice, rhythm, and deliberate quirks
   belong to the author.
2. **Edit the minimum necessary.** Touch only what has a clear AI tell.
3. **Eliminate clear AI signals.** Apply the 33 patterns to identify and remove
   them.
4. **Improve fluency and readability.** The result should read naturally aloud.
5. **Never invent content.** No added facts, examples, opinions, or emotional
   color.
6. **Respect the text type.** Different text types require different registers.

---

## Decision Flow

Before editing any text, the skill works through four steps:

1. **Identify the text type** — personal, technical, academic, institutional,
   or software docs.
2. **Assess the artificialness level** — low (1-3 tells), medium (4-8 tells),
   or high (pervasive markers).
3. **Choose the intervention mode** — Light, Moderate, or Full.
4. **Check for human signals** — specific details, mixed feelings, varied
   sentence length, self-corrections. These passages are left alone.

---

## Intervention Modes

### Light mode
**When:** Low artificialness, or human signals are dominant.
**What it does:** Fixes specific words and phrases in place. Does not
restructure sentences or paragraphs.
**Output:** Edited text with a brief note of changes.

### Moderate mode
**When:** Medium artificialness.
**What it does:** Rewrites the passages that contain tells. Leaves the rest
unchanged.
**Output:** Rewritten text with a summary of changes.

### Full mode
**When:** High artificialness, or the text is mostly AI-generated.
**What it does:** Rewrites the entire text, keeping meaning, length, and
structure. Includes a draft, an audit pass, and a final rewrite.
**Output:** Draft, audit bullets, final rewrite, summary of changes.

---

## Text Type Rules

| Type | What the skill does |
|------|---------------------|
| **Personal / creative** | Removes AI tells, adds voice and rhythm where appropriate |
| **Technical / README** | Fixes fragmented headers, inline lists, diff-anchored writing; keeps plain register |
| **Academic** | Fixes vague attributions and hedging; preserves formal vocabulary and impersonal voice |
| **API documentation** | Fixes copula avoidance and passive voice where the actor matters; no personality |
| **Institutional** | Fixes promotional language and significance inflation; keeps third-person neutral register |

---

## 33 Patterns Detected

### Content

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 1 | Significance inflation | "marking a pivotal moment in the evolution of..." | "was established in 1989 to collect regional statistics" |
| 2 | Notability name-dropping | "cited in NYT, BBC, FT, and The Hindu" | "In a 2024 NYT interview, she argued..." |
| 3 | Superficial -ing analyses | "symbolizing... reflecting... showcasing..." | Remove or expand with actual sources |
| 4 | Promotional language | "nestled within the breathtaking region" | "is a town in the Gonder region" |
| 5 | Vague attributions | "Experts believe it plays a crucial role" | "according to a 2019 survey by..." |
| 6 | Formulaic challenges | "Despite challenges... continues to thrive" | Specific facts about actual challenges |

### Language

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 7 | AI vocabulary | "Additionally... testament... landscape... showcasing" | Plain alternatives or cut |
| 8 | Copula avoidance | "serves as... features... boasts" | "is... has" |
| 9 | Negative parallelisms / tailing negations | "It's not just X, it's Y", "..., no guessing" | State the point directly |
| 10 | Rule of three | "innovation, inspiration, and insights" | Use the natural number of items |
| 11 | Synonym cycling | "protagonist... main character... central figure... hero" | Repeat the clearest word |
| 12 | False ranges | "from the Big Bang to dark matter" | List topics directly |
| 13 | Passive voice / subjectless fragments | "No configuration file needed" | Name the actor when it helps |

### Style

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 14 | Em/en dashes | "institutions—not the people—yet this continues—" | Period, comma, colon, or restructure |
| 15 | Boldface overuse | "**OKRs**, **KPIs**, **BMC**" | "OKRs, KPIs, BMC" |
| 16 | Inline-header lists | "**Performance:** Performance improved" | Convert to prose |
| 17 | Title Case headings | "Strategic Negotiations And Partnerships" | "Strategic negotiations and partnerships" |
| 18 | Emojis | "🚀 Launch Phase: 💡 Key Insight:" | Remove |
| 19 | Curly quotes | `"the project"` (curly) | `"the project"` (straight) |
| 26 | Hyphenated word pairs | "the report is high-quality" | "the report is high quality" |
| 27 | Persuasive authority tropes | "At its core, what matters is..." | State the point directly |
| 28 | Signposting announcements | "Let's dive in", "Here's what you need to know" | Start with the content |
| 29 | Fragmented headers | "## Performance" + "Speed matters." | Let the heading do the work |
| 30 | Diff-anchored writing | "This function was added to replace..." | Describe what it does now |
| 31 | Manufactured punchlines | "It had no preference. No prior. No nostalgia." | Varied length, concrete claims |
| 32 | Aphorism formulas | "Symmetry is the language of trust" | Replace with the actual claim |
| 33 | Conversational rhetorical openers | "Honestly? It depends..." | Remove the fake-candid setup |

### Communication

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 20 | Chatbot artifacts | "I hope this helps! Let me know if..." | Remove entirely |
| 21 | Cutoff disclaimers / speculative gap-filling | "maintains a low profile... likely grew up..." | Say what is not known, or omit |
| 22 | Sycophantic tone | "Great question! You're absolutely right!" | Respond directly |

### Filler and hedging

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 23 | Filler phrases | "In order to", "Due to the fact that" | "To", "Because" |
| 24 | Excessive hedging | "could potentially possibly" | "may" |
| 25 | Generic conclusions | "The future looks bright" | Specific plans or facts |

---

## Examples by Text Type

### Personal text (Full mode)

**Before:**
> I recently spent five unforgettable days in Lisbon, and let me tell you — this
> city completely stole my heart. Nestled along the banks of the Tagus River,
> Lisbon stands as a vibrant testament to Portugal's enduring spirit. The
> must-see São Jorge Castle offers stunning views. Would I go back? Absolutely.
> Lisbon isn't just a place to visit — it's a place to fall in love with. ✨

**After:**
> I spent five days in Lisbon last October and still have mixed feelings about
> it. Beautiful, yes. Also harder on the knees than anyone warned me. The castle
> is fine: the view is great, the queue is long, and I spent more time shuffling
> toward the entrance than looking at anything once I got inside. I would go
> back, but in spring and with better shoes.

---

### Academic text (Light mode)

**Before:**
> This pivotal study underscores the crucial role of mitochondrial dysfunction
> in neurodegenerative disorders, showcasing its enduring relevance to the field.
> Experts believe these findings will enhance our understanding significantly.

**After:**
> This study found that mitochondrial dysfunction contributes to neurodegenerative
> disorders. The mechanism is described in the following section.

*What changed: removed significance inflation (#1), AI vocabulary (#7), and
vague attribution (#5). Register preserved.*

---

### Technical documentation (Moderate mode)

**Before:**
> #### **Performance:** Performance has been significantly enhanced
> #### **Security:** Security has been strengthened with end-to-end encryption
> #### **UX:** The user experience boasts a groundbreaking new interface
>
> This function was added to replace the previous O(n²) approach. Let's dive
> into how to use it. Here's what you need to know.

**After:**
> The update improves load times, adds end-to-end encryption, and redesigns the
> main interface.
>
> This function uses a hash map for O(1) lookups. Pass the item ID as the first
> argument.

*What changed: collapsed inline-header list (#16), removed promotional language
(#4), fixed diff-anchored writing (#30), removed signposting (#28).*

---

### README (Moderate mode)

**Before:**
> ## Getting Started
>
> Getting started is easy!
>
> This library boasts a vibrant ecosystem of plugins and showcases
> groundbreaking performance. Additionally, it aligns with modern development
> practices. Let's dive in!
>
> **Installation:** Install the package using npm.
> **Configuration:** Configure using the config file.
> **Usage:** Use the library in your project.

**After:**
> ## Getting started
>
> Install the package:
>
> ```bash
> npm install my-library
> ```
>
> Add a `config.json` file at the project root, then import the library:
>
> ```js
> import myLib from 'my-library';
> ```

*What changed: title case (#17), promotional language (#4), AI vocabulary (#7),
signposting (#28), inline-header list (#16). Imperative voice applied throughout.*

---

### Software API documentation (Light mode)

**Before:**
> `getUser(id)` serves as the primary method for retrieving user data. It boasts
> efficient caching and features automatic retry logic. No configuration needed.

**After:**
> `getUser(id)` retrieves user data. It caches results and retries failed
> requests automatically. You do not need to configure caching manually.

*What changed: copula avoidance (#8), subjectless fragment (#13). Technical
precision preserved.*

---

### Institutional text (Moderate mode)

**Before:**
> Nestled in the heart of São Paulo, our firm stands as a vibrant testament to
> excellence in financial services. With a rich heritage and a commitment to
> innovation, we boast a groundbreaking approach that showcases our enduring
> dedication to client success. Despite challenges, we continue to thrive.

**After:**
> Our firm is a financial services company based in São Paulo, founded in 1998.
> We provide asset management, credit analysis, and corporate advisory services
> to mid-size companies across Brazil.

*What changed: promotional language (#4), significance inflation (#1), copula
avoidance (#8), formulaic challenges section (#6). Third-person neutral register
preserved.*

---

## Frequently Asked Questions

**Does the skill rewrite everything?**
No. Light mode fixes only the specific words that contain tells. Moderate mode
rewrites only the affected passages. Full mode rewrites the whole text, but only
when the artificialness level is high.

**Will it change my writing style?**
It should not. The skill is designed to remove AI markers while keeping your
voice intact. If you provide a writing sample, it will match your rhythm and
word choices in the rewrite.

**Can I use it on academic papers?**
Yes. The skill uses a neutral register for academic text: no opinions, no
first-person injection, no register flattening. It fixes vague attributions,
excessive hedging, and AI vocabulary without changing the scholarly tone.

**What about code comments and commit messages?**
Code comments use the technical documentation rules: imperative voice, plain
and precise, no personality. Commit messages are usually short enough to fix in
Light mode.

**Does it add content?**
Never. The skill does not add facts, examples, or opinions. If something needs
a source, it flags it rather than inventing one.

**What if only one or two patterns appear?**
If the text has only 1-3 isolated tells and otherwise reads naturally, the skill
uses Light mode and makes targeted fixes. It does not restructure or rewrite
passages that do not need it.

---

## Best Practices

- Provide a writing sample when voice consistency matters.
- For academic text, note the citation style so the skill does not touch
  reference formatting.
- For technical docs, include the target audience (beginner, intermediate,
  expert) so the skill calibrates vocabulary accordingly.
- Do not run the skill on content inside quotation marks, code blocks, or
  examples where the AI-sounding phrase is being discussed rather than used.
- For changelogs and release notes, tell the skill explicitly: diff-anchored
  writing (#30) is correct there and should not be changed.

---

## Version Comparison

| Feature | v2.x | v3.0.0 |
|---------|------|--------|
| AI pattern detection | 33 patterns | 33 patterns (reorganized) |
| Text type classification | No | Yes (5 types) |
| Artificialness assessment | No | Yes (Low / Medium / High) |
| Intervention modes | Single mode | Light / Moderate / Full |
| Type-specific rules | No | Yes (academic, technical, API, institutional) |
| Minimal intervention principle | Implied | Explicit, enforced first |
| Voice calibration | Yes | Yes (unchanged) |
| Draft → audit → final loop | Full mode only | Full mode (High artificialness) |

---

## References

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup)

---

## Version History

- **3.0.0** — Architectural refactor. Added the Principle of Minimal
  Intervention, text type classification (5 types), artificialness assessment
  (Low / Medium / High), three intervention modes (Light / Moderate / Full),
  type-specific editing rules for academic, technical, API, software docs, and
  institutional text, a decision flow before editing begins, and six before/after
  examples by text type. All 33 patterns preserved and reorganized for clarity.
  No patterns added or removed.
- **2.8.2** — Replaced the full before/after example with a first-person Lisbon
  trip recap.
- **2.8.1** — Added cross-agent installation docs and optional Claude Code plugin
  packaging.
- **2.8.0** — Added patterns #31-33 for manufactured punchlines, aphorism
  formulas, and conversational rhetorical openers.
- **2.7.0** — Added pattern #30 (diff-anchored writing); made em/en dashes a
  hard cut.
- **2.6.0** — Consolidated duplicated workflow sections.
- **2.5.1** — Added passive voice / subjectless fragment rule (#13).
- **2.5.0** — Added patterns for persuasive framing (#27), signposting (#28),
  and fragmented headers (#29).
- **2.4.0** — Added voice calibration.
- **2.3.0** — Added hyphenated word pair overuse (#26).
- **2.2.0** — Added final "obviously AI generated" audit and second-pass rewrite.
- **2.1.0** — Added before/after examples for all 24 patterns.
- **2.0.0** — Complete rewrite based on Wikipedia source.
- **1.0.0** — Initial release.

---

## License

MIT
