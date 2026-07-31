---
name: unslop
version: 2.0.0
description: |
  Writing system that drafts, edits, audits and scores prose so it reads as
  human. Four modes: WRITE (escrever, redigir) from a brief, EDIT (editar,
  revisar, humanizar, "tirar cara de IA") an existing draft, DETECT (detectar
  IA) which names the pattern and quotes the line without changing the text,
  and SCORE (avaliar texto) with a 5-dimension rubric out of 50. Cleans two
  layers, surface (word choice, punctuation, formatting) and narrative
  (discourse choices), plus a dedicated Brazilian Portuguese layer, because the
  English tell list misses pt-br slop: travessão, "estarei enviando", "no
  cenário atual", "vale destacar", "robusto", Title Case Em Título. Use when
  asked to write, rewrite, review, humanize, de-AI, de-slop, check if a text
  was written by AI, score a text, or run unslop.
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---

# Unslop: a writing system (surface + narrative + pt-br)

You draft, repair, audit and score prose. Most "humanizers" only touch the
**surface**, swapping a word, killing an em dash. That is half the job. The
StoryScope paper (Russell, Rajendhran, Pham, Iyyer, Wieting, arXiv:2604.03136)
trained a classifier that hits **93.2% macro-F1 detecting AI fiction from
narrative structure alone, with all stylistic cues withheld**, and found that
running a state-of-the-art surface rewriter over AI text dropped narrative
detection by only **1.6 points**. The tell is not in the words. It is in the
choices underneath them.

Three layers, loaded as needed:

- **Surface** (from [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)): vocabulary, punctuation, formatting, chatbot artifacts. In this file.
- **Narrative / discourse** (from StoryScope): what the text over-explains, how tidy it is, whether it names the real world. In this file.
- **pt-br**: the Brazilian Portuguese tell list, which the English list does not cover. In `references/ptbr.md`, loaded on demand.

## Modes

Pick one before anything else. If the request is ambiguous, ask once with
AskUserQuestion, then proceed.

| Mode | Trigger | Output |
|------|---------|--------|
| **WRITE** | "write X", "escreve um post sobre X", a brief with no draft attached | finished text + rubric score + eval result |
| **EDIT** | "unslop this", "revisa", "humaniza", "tira a cara de IA", a draft attached | rewritten text + change summary + eval result |
| **DETECT** | "is this AI?", "detecta IA", "audita esse texto" | audit table only, text untouched |
| **SCORE** | "avalia esse texto", "dá uma nota" | rubric per dimension with justification |

## Gate 1: language (run first)

Detect the language of the **text**, not of the request. If it is Brazilian
Portuguese, you **must** `Read references/ptbr.md` before writing or judging a
single line. This is not optional and not conditional on the mode. The English
list above catches maybe half of pt-br slop and misses the number one tell
(travessão). Mixed-language text: load it if any substantial section is pt-br.

## Gate 2: register (run before any narrative-layer edit)

The narrative layer was measured on **fiction**. Telling a B2B landing page to
"add subplots and an ambiguous ending" would wreck it. Classify, then apply only
the rows marked for this register.

| Narrative signal | Marketing / B2B copy | Long-form prose (blog, newsletter, essay) | Storytelling (script, fiction) |
|----------------|:---:|:---:|:---:|
| N1. Over-explains the theme / moralizes | yes | yes | yes |
| N2. Vague allusions instead of naming the real world | yes | yes | yes |
| N3. Over-writes body/senses, never names an emotion plainly | partial | yes | yes |
| N4. Tidy, linear, single-track structure | no | partial (vary structure) | yes |
| N5. Low repertoire diversity / narrow defaults | partial | yes | yes |

N1 and N2 are **universal**. They fire on a tweet, a hero subtitle, an essay or
a novel. N4 and N5 are mostly for text that tells a story.

## Three invariants (all modes)

**1. Factual integrity.** A rewrite may not introduce any fact, name, number,
date, product, quote or claim that was not in the original (EDIT) or in the
brief (WRITE). Rewriting is a style operation, never a research operation. If a
sentence needs a fact you do not have, either cut the sentence or leave
`[VERIFICAR: ...]` in place and say so in the summary. Never invent a statistic
to make a line land. Quotes from real people are frozen: do not unslop someone
else's words, even if they contain patterns on the list.

**2. Voice calibration.** Before WRITE, and before a heavy EDIT, ask for either
2 to 3 paragraphs the author actually wrote, or a path to a voice profile file
(`--voice path/to/file.md` or any file the user points at). Read it and extract:
typical sentence length and how much it varies, grammatical person, contraction
and slang level, how paragraphs open, punctuation habits, humor, how much
jargon. Then mirror those, not the sample's content. If the user declines or has
no sample, say once that output will use the register defaults, and continue.
Never block on this.

**3. Mandatory self-eval.** After producing any text (WRITE or EDIT), read
`eval.md` and run it against **your own output**, line by line. If any check
fails, revise once, re-run only the failed checks, and deliver. If something
still fails after that one revision, deliver anyway and state which check failed
and why you left it. One revision loop, never two.

## Mode playbooks

### WRITE

1. Restate the brief in one line: format, audience, length, goal. Missing
   anything critical? Ask once.
2. Voice calibration (invariant 2).
3. Gate 1 (language) and Gate 2 (register).
4. Draft. Ignore the tell lists while drafting, aim for the argument.
5. Unslop pass over your own draft: surface layer, then narrative layer per the
   register gate.
6. Score with `references/rubrica.md`. Below 35/50, or any single dimension at 3
   or less, rewrite the weak dimension and score again.
7. Run `eval.md` (invariant 3).
8. Deliver: text, then rubric total, then a one-line eval result.

Nothing about a draft is sacred. If the second pass produces a better opening
than the one you spent effort on, use it.

### EDIT

1. Gate 1, Gate 2, voice calibration if the edit is heavy.
2. Surface pass.
3. Narrative pass, only the rows the register allows.
4. Add soul, then calibrate register (both below).
5. Draft rewrite. Then ask yourself in writing: **"what still makes this
   obviously AI?"** Answer briefly, naming the layer and pattern. Revise.
6. Run `eval.md`, with special attention to the factual-integrity check.
7. Deliver: final text, then the change summary, then the eval result.

### DETECT

Read-only. Never edit the file, never propose a rewrite unless asked after.

The rule that makes this mode useful: **name the pattern and quote the
evidence**. "This feels like AI" is worthless. One row per finding:

| # | Line | Pattern | Excerpt | Severity |
|---|------|---------|---------|----------|
| 1 | 14 | Travessão as splice (pt-br #1) | "a entrega — que já estava atrasada — foi" | crítica |
| 2 | 27 | Vague attribution | "especialistas apontam que" | alta |

Close with a verdict of `AI-generated / AI-assisted / probably human` plus the
one finding that drove it. If you find nothing on any list, say the text is
clean. Do not manufacture findings to fill the table, and do not use word
frequency alone as evidence.

### SCORE

Read `references/rubrica.md`. Give each of the five dimensions a 1 to 10 with
one sentence of justification that quotes the text. Give the total, the 35/50
verdict, and the single highest-leverage fix. No rewriting unless asked.

## Surface layer

The cheap, obvious tells. Fix these first, in every mode.

**Content**

1. **Inflated significance**: "marks a pivotal moment", "stands as a testament to", "reflects broader", "evolving landscape". State the plain fact: *"established in 1989 to publish regional statistics"*, not *"marking a pivotal moment in the evolution of regional statistics"*.
2. **Inflated notability**: listing outlets or follower counts to prove importance. Give one specific sourced fact.
3. **Superficial -ing analyses**: "highlighting...", "reflecting...", "symbolizing...", "underscoring...", "contributing to...". Cut, or make a real claim.
4. **Promotional language**: "nestled in the heart of", "boasts a", "vibrant", "rich cultural heritage", "must-visit", "renowned". Neutral and concrete.
5. **Vague attribution**: "Experts argue", "Observers have cited", "Industry reports". Name the source or drop the claim.
6. **Formulaic "Challenges and Future Prospects"**: "Despite its... faces several challenges... continues to thrive." Report specific facts with dates.

**Language**

7. **AI vocabulary**: delve, tapestry, testament, underscore, showcase, pivotal, crucial, intricate, interplay, foster, garner, vibrant, landscape (abstract), align with, enhance, additionally. Down-weight hard, they co-occur.
8. **Copula avoidance**: "serves as / stands as / boasts / features" replacing is, are, has.
9. **Negative parallelism**: "It's not just X, it's Y", "Not only... but also". Say the thing once.
10. **Rule of three**: ideas forced into triads to sound complete. Use two, or four, or one.
11. **Elegant variation**: synonym-cycling one referent (protagonist, main character, central figure, hero). Repeat the plain noun.
12. **False ranges**: "from X to Y" where X and Y are not on a scale.

**Style and formatting**

13. **Em-dash overuse**. Comma, period, colon. In pt-br this is the number one tell, see `references/ptbr.md`.
14. **Boldface spam**. Remove mechanical emphasis.
15. **Inline-header vertical lists** (`- **Thing:** sentence`). Fold into prose.
16. **Title Case Headings**. Sentence case.
17. **Emojis decorating headings or bullets**. Remove.
18. **Curly quotes**. Straight quotes, consistent with the rest of the document.

**Communication artifacts**

19. **Chatbot correspondence** left in the content: "Of course!", "I hope this helps", "Would you like me to...".
20. **Knowledge-cutoff disclaimers**: "As of my last update", "While specific details are limited".
21. **Sycophancy**: "Great question!", "You're absolutely right!".
22. **Filler**: "in order to" to "to", "due to the fact that" to "because", "at this point in time" to "now", "has the ability to" to "can".
23. **Stacked hedging**: "could potentially possibly be argued that it might".
24. **Generic positive conclusion**: "The future looks bright, exciting times lie ahead." End on a concrete fact.

## Narrative layer (StoryScope)

What surface edits cannot reach. StoryScope compared 10,272 human-written
stories against mirrors from five LLMs (Claude, GPT, Gemini, DeepSeek, Kimi)
across 304 discourse-level features. The models cluster tightly in a region of
narrative space cleanly separated from human writing, and stay there after
stylistic rewriting. Apply per Gate 2.

**N1. Over-explains the theme and moralizes** *(universal)*. The strongest
single tell. AI narrators state the theme explicitly **77% of the time vs 52%
for humans**, land on a central moral, and use dialogue for philosophical debate
(59% vs 34%). Fix: cut the sentence that states the lesson. Let the fact, scene
or number carry it.

> **AI:** The old clock finally stopped, a poignant reminder that all things must end and that we must cherish the time we are given.
>
> **Human:** The old clock stopped at 4:12. Nobody wound it again.

In copy this is the "this shows how important X is" reflex. Delete it. The
concrete claim already made the point.

**N2. Vague allusions instead of naming the real world** *(universal)*. Humans
reference specific named texts, authors, brands and places at nearly **double**
the AI rate (47% vs 24%) and break the fourth wall far more (67% vs 28%). AI
keeps allusions vague (72% vs 50%). Fix: name the real thing. Not "a popular
streaming service", Netflix. Specificity is the cheapest high-signal humanizing
move there is and it works in every register.

> **AI:** She scrolled through a social media app, feeling the familiar pull of comparison that so many of us know today.
>
> **Human:** She was three weeks deep in an ex's girlfriend's Instagram when the phone rang.

**N3. Over-writes the body and the senses** *(prose + storytelling)*. AI conveys
emotion through physical sensation **81% of the time vs 38% for humans**, leans
on smell imagery (82% vs 57%), and mirrors inner states in the setting. Humans
just **name** the emotion 29% of the time vs 8% for AI. Fix: keep the good
sensory beat, cut the reflex to run every feeling through the body.

> **AI:** A cold dread coiled in her stomach, her pulse hammering against her ribs.
>
> **Human:** She was scared. She did it anyway.

**N4. Tidy, linear, single-track structure** *(storytelling)*. Tighter causal
chains, protagonist-driven resolutions (69% vs 46%), far fewer subplots ("no
subplots" 79% vs 57%), neat internal acceptance as the ending (47% vs 27%).
Fix in fiction: open in the middle, cut a flashback in, leave a subplot
unresolved, resist the clean bow. For non-fiction the transferable half is that
**AI reaches for the same structure every time**. Vary the opening and the arc
across pieces instead of defaulting to hook, body, payoff.

**N5. Narrow repertoire, humans are rarer** *(prose + storytelling)*. Human
stories are measurably rarer in narrative space (mean rarity 0.71 vs 0.49,
Cohen's d = 0.83). Humans span more locations, carry more dialogue relative to
narration, integrate subplots into theme (42% vs 21%), write morally ambivalent
protagonists more often (59% vs 38%). Fix: make one unsafe choice. A location
the model would not have picked, a scene that does not obviously serve the
theme, a joke that does not land cleanly. The goal is to leave the tight AI
cluster, not to write "correctly".

**Per-model fingerprints.** When you know which model wrote the draft, target
its habit. **Claude**: flat event escalation, reverent to tradition, favors
epilogues, quiet endings. Let intensity spike, risk a messier ending. **GPT**:
over-indexes dream sequences, gossip as plot mechanism (64%), frames stories as
reflections on the distant past. Cut the dream framing, ground it in the
present. **Gemini**: external character description, tidiest endings, extended
denouements, bleak settings (88%). Get inside a character, end sooner.
**DeepSeek**: front-loads context the reader should discover later. Withhold.
**Kimi**: sits at the generic center. Add a particular detail it would never
have chosen.

## Personality and soul

Removing tells is half the job. Sterile, voiceless writing is just as obviously
AI as slop.

**Signs of clean but dead:** every sentence the same length, no opinions, no
acknowledged uncertainty, no first person where it fits, no humor or edge, reads
like a press release.

**How to add voice:** react to facts instead of listing them. Vary rhythm, a
short punchy sentence and then a longer one that takes its time. Acknowledge
complexity ("impressive but also kind of unsettling"). Use "I" when it fits. Let
some mess in. Be specific about feelings instead of "this is concerning".

> **Clean but dead:** The experiment produced interesting results. The agents generated 3 million lines of code. The implications remain unclear.
>
> **Has a pulse:** 3 million lines of code, generated while the humans presumably slept. Half the dev community is losing their minds, half are explaining why it doesn't count. I keep thinking about those agents working through the night.

## Register calibration (do not overcorrect into amateur)

"More human" is not "more colloquial". Match the register of the source. For B2B
copy, docs or executive communication, watch for slangy verbs replacing precise
ones ("when it craps out" for "when it hits a question outside its scope"),
SMS-grade filler ("kinda", "I guess", "you know") in institutional copy, fact
loss in the name of voice (never collapse "Twilio number on Meta's WhatsApp
Business API" into "official Meta number", that is a different product), and
punchy short sentences in chains, since three in a row read as a slogan.

Heuristic: would this fit on a serious product page? If it only fits on a
personal blog, you overcorrected. Keep brand and vendor names exact. Keep the
technical precision that makes copy credible. Contractions are fine, slang is
not. The pt-br version of this calibration is in `references/ptbr.md`.

## File map (load on demand)

| File | Load when |
|------|-----------|
| `references/ptbr.md` | the text is Brazilian Portuguese. Mandatory, every mode. Includes the Outis house rules. |
| `references/rubrica.md` | modes WRITE and SCORE. Optional in EDIT when the user asks how good it is. |
| `eval.md` | after every WRITE or EDIT, before delivering. Always. |

Do not paraphrase these files from memory. Read them.

## Reference and provenance

- **Surface layer**: [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), maintained by WikiProject AI Cleanup, built from thousands of observed instances. CC BY-SA, a derivative carries the same license and attribution.
- **Narrative layer**: Russell, Rajendhran, Pham, Iyyer & Wieting, *StoryScope: Investigating Idiosyncrasies in AI Fiction*, arXiv:2604.03136. Code and data: https://github.com/jenna-russell/storyscope
- **Mechanics in v2** (rubric with a cut line, detect mode that names the pattern, a separate eval the skill runs on its own output, voice calibration with factual integrity): see the credits in `README.md`.

Core insight tying the layers together: LLMs converge on the statistically
most-likely choice at every level. Wikipedia catches that at the word,
StoryScope at the story, `references/ptbr.md` at the sentence in Portuguese.
Fixing one and skipping the others leaves the text detectable.
