# Structures to avoid

Sentence-, paragraph-, and document-level patterns that bury the point: manufactured drama, false structure, and shapes that hide who did what. They also mark AI writing. As with the phrase catalog, one instance can be fine; the signal is repetition or clustering. Apply the core override: never mangle a sentence or drop a claim just to break a pattern.

Word- and phrase-level clutter is in [phrases.md](phrases.md). Artifact conventions are in [technical.md](technical.md).

## Negative parallelism (binary contrast)

The most reliable AI tell. It frames an ordinary point as a surprising reversal. One can work; several is a confession.

| Pattern | Problem |
|---------|---------|
| "It's not X, it's Y." | Telegraphed reversal |
| "Not because X. Because Y." | Causal variant |
| "The question isn't X. It's Y." | Rhetorical misdirection |
| "It feels like X. It's actually Y." | Setup/reveal cliche |
| "It's not just about X, it's about Y." | Additive hedge |
| "stops being X and starts being Y" | False transformation arc |

Fix: state Y directly. Drop the negation. "The bottleneck is disk I/O" beats "It's not the CPU, it's the disk."

## Negative listing

Listing what something is *not* before revealing what it *is*.

- "Not a bug. Not a feature. A design flaw."
- "Not ten. Not fifty. Five hundred."

Fix: state the conclusion. The reader does not need the runway.

## Tailing negations

A clipped negation fragment tacked onto a sentence instead of a real clause.

- "The options come from the selected item, no guessing."
- "Clean output every time, no exceptions."

Fix: write the full clause. "The options come from the selected item, so the user does not have to guess."

## Self-posed rhetorical questions

The model asks a question nobody asked, then answers it for drama.

- "The result? Devastating." / "The worst part? Nobody saw it coming."
- "What if [reframe]?" / "Think about it:" / "Here's what I mean:"

Fix: make the point as a statement. In technical writing, a real question that the text then investigates is fine ("Does performance-weighting beat equal weighting? Across 54 forecasts, no."). The tell is the manufactured-suspense version.

## Dramatic fragmentation

Sentence fragments stacked for emphasis. RLHF pushes models toward one thought per sentence; no one drafts this way.

- "[Noun]. That's it. That's the [thing]."
- "X. And Y. And Z."
- "He published this. Openly. In a book."

Fix: complete sentences. One short sentence for emphasis is fine; a run of them is the tell.

## Anaphora abuse

Repeating the same sentence opening several times in a row. Common in grant narratives and roadmaps.

- "We will develop... We will apply... We will validate... We will disseminate..."
- "They assume that... They assume that..."

Fix: vary the openings, or combine related points into one sentence that names specifics. "We will develop and validate multi-ancestry fine-mapping methods on UK Biobank and TOPMed, then release them as an R package."

## Tricolon abuse (rule of three)

Forcing ideas into groups of three to sound comprehensive. One tricolon is fine; back-to-back triples are an AI pattern.

- "workflows, decisions, and interactions"
- "innovation, inspiration, and industry insights"
- "Products impress; platforms empower; ecosystems endure."

Fix: use the natural number of items. Two is often better than three. List the items that are actually there.

## False agency

Giving an inanimate thing a human verb to avoid naming the actor.

| Pattern | Who actually acted |
|---------|--------------------|
| "the data tells us" | someone read it and drew a conclusion |
| "the results emerged" | we computed them |
| "the model decides" | the model outputs; a threshold or person decides |
| "the literature suggests" | named authors argued |
| "uncertainty naturally increased" | the interval widened because [mechanism] |

Fix: name the actor. "We found", "the team fixed it", "Author et al. argued". In results sections especially, "we" is correct and clearer than disembodied agency.

## Passive voice that hides the actor

Passive drains energy and hides who did what. Find the actor and make them the subject.

- "It is believed that..." -> name who believes it.
- "Mistakes were made." -> name who made them.
- "The results are preserved automatically." -> "The pipeline writes results to disk."

**Methods-section exception:** passive voice is conventional and correct in methods. "Samples were incubated at 37C", "Models were fit with Stan", "Sequences were aligned with BWA-MEM" should stay passive. Flag passive only when it hides an actor in results, discussion, or documentation, where active voice is clearer.

## Listicle in a trench coat

Numbered or labeled points dressed up as continuous prose.

- "The first limitation is... The second limitation is... The third limitation is..."
- "The first wall is... The second wall is..."

Fix: if the content is a list, format it as a list. If it should be prose, weave the points together with real connective tissue and specifics, not ordinals.

## Superficial participle analyses

Tacking an "-ing" phrase onto a sentence to inject shallow significance.

- "...highlighting its enduring legacy."
- "...contributing to the region's rich cultural heritage."
- "...underscoring its role as a dynamic hub."
- "...reflecting broader trends in the field."

Fix: make a specific analytical claim or delete the phrase. "...which reduced mean WIS by 12%" is a claim; "...highlighting the importance of evaluation" is filler.

## False ranges

"From X to Y" where X and Y are not endpoints of any real scale.

- "from innovation to implementation to cultural transformation"
- "from the Big Bang to the cosmic web"

Fix: if the items are a list, list them. If there is a real spectrum (forecast horizons from 1 to 4 weeks), keep it.

## Historical/analogy stacking

Rapid-fire name-drops to build false authority.

- "Apple didn't build Uber. Facebook didn't build Spotify. Stripe didn't build Shopify."
- "Every shift (web, mobile, social, cloud) followed the same pattern."

Fix: examine one example in depth. One analyzed case beats five name-drops.

## "Despite its challenges..."

Acknowledging problems only to dismiss them with a formula.

- "Despite these challenges, the initiative continues to thrive."
- "Despite its promise, the method faces several challenges that must be addressed."

Fix: if a limitation matters, analyze it with its cause and consequence. If it does not, cut it. In a discussion section, name the specific limitation and what it does to the conclusion.

## Synonym cycling (elegant variation)

Rotating synonyms for the same referent because of repetition penalties.

- "The protagonist... the main character... the central figure... the hero..."
- "the study... the research... the investigation... the analysis..."

Fix: pick the clearest word and repeat it. In technical writing, consistent terminology is a virtue: call the same thing by the same name every time. "The model" stays "the model", not "the framework... the system... the approach".

## One-point dilution

Making one argument and restating it many ways with different framings.

Fix: state the point once, support it with a specific example or number, move on.

## Fractal summaries

"What I'll tell you; what I'm telling you; what I told you" at every level.

- "In this section we'll explore... [content] ...as we've seen in this section."
- Conclusions that restate every prior point.

Fix: say it once. An abstract and a conclusion serve different functions and may legitimately overlap; verbatim restatement within a section does not.

## The dead metaphor

Latching onto one metaphor and beating it across the whole piece. A human introduces a metaphor, uses it, moves on.

Fix: use the metaphor once if it clarifies, then drop it. Prefer the literal mechanism in technical text.

## Diff-anchored writing

Documentation or comments written as if narrating a change rather than describing the thing as it is.

Before: "This function was added to replace the previous approach of iterating through all items, which caused O(n^2) performance."
After: "This function uses a hash map for O(1) lookups."

Fix: unless the document is version-scoped (changelog, release notes, migration guide), describe the current state. The history belongs in the commit message.

## Fragmented headers

A heading followed by a one-line paragraph that restates the heading before the real content.

Before:
> ## Performance
>
> Speed matters.
>
> When users hit a slow endpoint, they retry, multiplying load.

After:
> ## Performance
>
> When users hit a slow endpoint, they retry, multiplying load.

## Sentence openers to watch

| Pattern | Fix |
|---------|-----|
| Opening with "So," as a discourse marker | Start with the content |
| Opening with "Look," / "Honestly," as a hook | Remove |
| A string of clauses opening with What/When/Which as a crutch | Lead with subject and verb |

## Rhythm

| Pattern | Fix |
|---------|-----|
| Three sentences in a row of identical length | Break one |
| Every paragraph ending on a punchy one-liner | Vary the endings |
| Staccato fragment stacking | Use complete sentences |

## Formatting tells

| Tell | Fix |
|------|-----|
| Em or en dashes | Remove. Use a period, comma, colon, or parentheses. Scan the final draft for both. |
| Bold-first bullets ("**Speed:** ...") | Drop the bold lead or convert to prose |
| Inline-header lists masquerading as content | Convert to plain bullets or prose |
| Emojis decorating headings or bullets | Remove unless the context genuinely calls for them |
| Title Case In Headings | Use sentence case |
| Curly/smart quotes | Use straight quotes |
| Unicode arrows (->) as decoration | Use plain text or real notation |
| Signposted conclusions ("In conclusion...") | Let the writing conclude |
