# Phrases to remove or replace

Word- and phrase-level clutter to cut. These crowd out the claim, inflate plain words, or stall a sentence before it starts; they also mark AI writing. Any one can appear in clean human prose, so the signal is a cluster. Before cutting, apply the core override: if removing a phrase would distort a claim or drop a citation, keep it.

This catalog covers word choice. Sentence- and paragraph-level patterns are in [structures.md](structures.md). Artifact conventions are in [technical.md](technical.md).

## Throat-clearing openers

Cut these and state the content directly.

- "Here's the thing:" / "Here's what's interesting:" / "Here's the kicker"
- "Here's what most people miss" / "Here's where it gets interesting"
- "The uncomfortable truth is" / "The real question is" / "Let me be clear"
- "It turns out (that)" / "The truth is," / "I'll say it again:"

Any "here's what / this / that" construction is a runway before the point. Cut it.

## Emphasis crutches

These add no information. Delete them.

- "Full stop." / "Period." / "Let that sink in."
- "This matters because" / "Here's why that matters" / "Make no mistake"

## Pedagogical hand-holding

These assume the reader needs a teacher. For reference and technical text, the reader does not.

- "Let's break this down" / "Let's unpack this" / "Let's explore" / "Let's dive in"
- "Think of it as..." / "Think of it like..." (the patronizing analogy; often less clear than the concept it explains)
- "Imagine a world where..."

## AI vocabulary

Words overrepresented in post-2023 text. They co-occur, so two or three together is a strong signal. Replace with the plain word or cut.

| Avoid | Use instead |
|-------|-------------|
| delve (into) | examine, look at |
| utilize | use |
| leverage (verb) | use |
| facilitate | help, ease |
| enhance | improve (or name the improvement) |
| showcase | show, demonstrate |
| underscore / highlight (verb) | show, emphasize |
| foster | encourage, build, support |
| garner | get, attract, earn |
| robust (figurative) | strong, reliable, stable |
| streamline | simplify |
| harness (verb) | use, apply |
| intricate / intricacies | complex, details |
| nuanced | complex, subtle, specific |
| crucial / pivotal | important (or name why) |
| vibrant | (usually deletable) |
| enduring | lasting (or name the timespan) |
| interplay | relationship, interaction |
| tapestry (abstract) | mix, combination, range |
| landscape (meaning "field") | field, area, situation |
| paradigm | model, approach |
| synergy | combined effect |
| ecosystem (figurative) | system, set of tools |
| additionally | also (or just start the sentence) |

Note for technical prose: "robust" is a real statistical term (robust estimator, robust standard errors). Keep it in that sense; flag it only when it means "good/strong" as a vague booster. Same logic for "significant" (statistical vs vague).

## The "serves as" dodge

AI replaces plain "is" and "has" with inflated substitutes because repetition penalties push it off the simple copula. Use the simple verb.

| Avoid | Use |
|-------|-----|
| serves as | is |
| stands as | is |
| acts as (when meaning "is") | is |
| represents (when meaning "is") | is |
| marks (when meaning "is") | is |
| boasts / features / offers (a) | has |

Before: "Gallery 825 serves as the exhibition space and boasts 3,000 square feet."
After: "Gallery 825 is the exhibition space and has 3,000 square feet."

## Business jargon

Replace with plain language.

| Avoid | Use instead |
|-------|-------------|
| navigate (challenges) | handle, address |
| unpack (analysis) | explain, examine |
| lean into | accept, focus on |
| game-changer | important (or name the effect) |
| double down | commit, increase |
| deep dive | analysis, examination |
| take a step back | reconsider |
| moving forward | next, from now on |
| circle back | return to |
| on the same page | agreed |
| at the end of the day | (usually deletable) |
| when it comes to | for, in (or cut) |

## Adverbs and intensifiers

Cut adverbs that soften, inflate, or signal fake significance. Keep adverbs that carry real precision (statistically, asymptotically, monotonically).

Frequent offenders: really, just, simply, actually, literally, basically, genuinely, honestly, truly, deeply, fundamentally, inherently, inevitably, interestingly, importantly, crucially, notably, remarkably, arguably, and "quietly" (AI's favorite for implying subtle importance).

Also cut these filler frames: "At its core", "In today's [X]", "It's worth noting", "It bears mentioning", "In a world where", "The reality is", "When it comes to".

## Filler phrases

Replace with the shorter form.

| Filler | Replace with |
|--------|--------------|
| in order to | to |
| due to the fact that | because |
| at this point in time | now |
| in the event that | if |
| has the ability to | can |
| it is important to note that | (cut) |
| despite the fact that | although |
| in light of the fact that | since |
| for the purpose of | to, for |
| a number of | several, many (or the count) |

## Meta-commentary and signposting

Cut self-referential asides and announcements. The text should move, not narrate its own structure.

- "In this section, we'll..." / "As we'll see..." / "The rest of this [doc] explains..."
- "Let me walk you through..." / "Without further ado" / "Now let's look at"
- "In conclusion" / "To sum up" / "As we've seen..." (let the writing conclude)

Exception: legitimate cross-references in long documents ("see Section 3 for the derivation") are navigation, not throat-clearing. Keep them.

## Vague declaratives

Sentences that announce importance without naming the thing. Replace with the specific thing or cut.

- "The implications are significant." / "The stakes are high." / "The consequences are real."
- "The reasons are structural." / "This is the deepest problem."

## Vague attributions

If you cannot name the source, you do not have one. Prefer a specific author, dataset, model, or metric.

- "Experts argue that..." / "Researchers have shown..." / "Studies suggest..."
- "Industry reports indicate..." / "It is widely believed that..."

Fix: "Beaulieu-Jones and Greene (2017) found that 40% of 68 papers reproduced." Name who, when, and what they actually found.

## Grandiose stakes inflation

Scale the claim to the actual stakes.

- "This will fundamentally reshape how we think about everything."
- "will define the next era of computing" / "a paradigm shift in..."

## Persuasive authority tropes

Phrases that pretend to cut to a deeper truth before restating an ordinary point.

- "The real question is" / "At its core" / "In reality" / "What really matters"
- "Fundamentally" / "The deeper issue" / "The heart of the matter"

## Chatbot artifacts

Correspondence that gets pasted into content. Always cut.

- "I hope this helps!" / "Let me know if..." / "Would you like me to..."
- "Great question!" / "Certainly!" / "Of course!" / "You're absolutely right!"
- "Here is a..." / "Here's an overview of..."

## Sycophantic tone

- "Great question!" / "That's an excellent point." / "You're absolutely right that..."

## Knowledge-cutoff disclaimers and gap-filling

Two related tells: leftover cutoff disclaimers, and inventing plausible filler when a source cannot be found. Say what is not known, or cut the sentence.

- "As of [date]" / "Up to my last training update"
- "While specific details are limited/scarce..." / "based on available information"
- "not publicly available, suggesting [a guess]" / "likely [grew up/began/studied]"

## Excessive hedging

Cut stacked qualifiers to the core claim. Keep one honest qualifier that reflects real uncertainty.

- "it could potentially possibly be argued that it might" -> "it may"
- "it is perhaps worth considering that" -> (cut, or state the consideration)

Technical note: genuine uncertainty is precise, not hedging. "Underpowered for the interaction term" and "wide CI due to small n" are claims, not hedges. Keep them.

## Generic positive conclusions

Replace vague upbeat endings with a specific next fact.

- "The future looks bright." / "Exciting times lie ahead."
- "a major step in the right direction" / "continues its journey toward excellence"

## Invented concept labels

AI appends an abstract problem-noun (paradox, trap, creep, divide, vacuum, inversion) to a domain word and uses it as if established.

- "the supervision paradox" / "the acceleration trap" / "workload creep"

Fix: if the concept needs a name, define it. Otherwise describe it in plain language.

## Hyphenated word-pair overuse

AI hyphenates these uniformly, including in predicate position. Humans hyphenate inconsistently: keep the hyphen when the compound is attributive ("a high-quality report"), drop it when it follows the noun ("the report is high quality").

Watch: third-party, cross-functional, client-facing, data-driven, decision-making, well-known, high-quality, real-time, long-term, end-to-end.
