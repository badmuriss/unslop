# unslop

A writing system that drafts, edits, audits and scores prose so it stops sounding like a language model. Works at three layers: the words on the page, the choices underneath them, and Brazilian Portuguese, which the English tell lists get wrong.

![license](https://img.shields.io/badge/license-CC--BY--SA--4.0-blue)
![type](https://img.shields.io/badge/type-LLM%20skill-black)
![version](https://img.shields.io/badge/version-2.0.0-green)

Most humanizers stop at the surface. They kill an em dash, swap "delve" for "explore", and call it done. That barely helps. When Russell and coauthors trained a classifier to spot AI fiction from narrative structure alone, with every stylistic cue stripped out, it still hit 93.2% macro-F1. Then they ran a state of the art surface rewriter over the AI text and detection dropped by 1.6 points. Almost nothing. The tell was never in the vocabulary. It was in what the story chose to do.

v1 cleaned both layers. v2 turns that into a system that also writes, audits and grades.

## What is new in 2.0

**Four modes.** v1 only edited. Now the entry point decides the pipeline.

| Mode | You say | It does |
|------|---------|---------|
| **write** | "write a post about X" | brief, voice calibration, draft, unslop pass, rubric, eval, delivery |
| **edit** | "unslop this", "humanize this" | the v1 flow, plus the eval at the end |
| **detect** | "is this AI?" | audit only, nothing rewritten |
| **score** | "grade this" | rubric with a number and a reason per dimension |

**Detect names the pattern.** The failure mode of every AI detector, human or machine, is the confident vibe check. This mode is not allowed to say "this feels like AI". Every finding is a row: line number, named pattern, the exact excerpt, severity. Nothing found means nothing found, and it says so instead of inventing a case.

**A rubric with a cut line.** Five dimensions, direction, rhythm, confidence, authenticity, density, each 1 to 10, each with concrete band descriptors so a 3 and an 8 are not a matter of mood. Below 35 out of 50, rewrite. Any single dimension at 3 or below, rewrite that dimension even if the total passes.

**A separate eval the skill runs on itself.** `eval.md` holds 20 binary checks, mechanical enough that there is nothing to argue about: zero em dashes in pt-br text, zero "estarei enviando", no number without a source, no set of lists where every list has exactly three items, no sentence containing a fact that was not in the original. The skill runs it against its own output before delivering, fixes what failed, and reports the result. It edits, then it checks its own edit.

**Factual integrity as a hard rule.** A rewrite may not add a fact, name, number, date or quote that was not in the source. Style operation, never a research operation. Quotes from real people are frozen, even when they contain patterns on the list.

**Voice calibration.** Paste 2 or 3 paragraphs you actually wrote, or point at a voice profile file. The skill extracts sentence length, person, formality, punctuation habits and rhythm, then mirrors those instead of its own defaults.

**Load on demand.** SKILL.md orchestrates and holds the two original layers. The long lists live in `references/` and are read only when the mode needs them.

## The Brazilian Portuguese layer

`references/ptbr.md`, loaded automatically and mandatorily whenever the text is pt-br. This is the part that did not exist anywhere else.

The English lists are not a translation away from working in Portuguese. Their number one item, the em dash, is a stylistic preference in English. In Portuguese it is close to proof of authorship: the character is not on the Brazilian keyboard layout, so a Brazilian writing at speed produces commas, periods and parentheses, and almost never a travessão in the middle of a marketing sentence. Meanwhile the tells that actually give away pt-br AI text have no English counterpart at all.

Covered, each with a bad example, its fix and a severity level: travessão, the call center gerund ("estarei enviando", "vamos estar acompanhando"), ceremonial openings ("no cenário atual", "vale destacar", "é importante ressaltar"), generic closings and self-answering rhetorical questions, the crutch vocabulary cluster (robusto, panorama, crucial, impulsionar, alavancar, potencializar, mergulhar, desvendar, ecossistema), Title Case in a language that does not have title case, negative parallelism, forced triads, synonym rotation, reveal colons, vague attribution, stacked hedging and bureaucratic passive voice, emoji as a bullet marker, and machine-translated corporate English.

It also carries a register calibration section for Portuguese, because the common overcorrection is turning an institutional text into a WhatsApp message. More human does not mean more slang.

Last piece: house rules. Editorial rules that belong to one author or one brand, marked as such and applied only in that context, so the public list stays clean and the local list stays enforceable.

### Em português

Se você escreve em português e testou algum "humanizador", já viu o problema: as listas são traduzidas do inglês, ignoram o travessão e não sabem o que é "estarei enviando". A camada `references/ptbr.md` é a régua pt-br que faltava, com exemplo ruim, correção e severidade em cada padrão, mais uma varredura mecânica que roda antes da entrega.

## The two original layers, still here

**Surface.** Em dashes, "testament to", rule of three, "It's not just X, it's Y", curly quotes, "Certainly! Here's an overview", bold-header bullet lists. Built from [Wikipedia's Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), assembled by the WikiProject AI Cleanup editors from thousands of real cases.

**Narrative.** What surface edits cannot reach, from [StoryScope](https://arxiv.org/abs/2604.03136):

- **Over-explaining the theme.** AI narrators state the moral 77% of the time. Humans, 52%.
- **Vague allusions.** Humans name real books, brands and places at nearly double the AI rate. AI reaches for "a popular streaming service" when it means Netflix.
- **Sensory over-writing.** AI renders emotion as body 81% of the time versus 38% for humans. Sometimes a person writes "she was scared" and moves on.
- **Tidy, linear plots.** Fewer subplots, protagonist-driven endings, everything resolved.
- **Low diversity.** The five models tested cluster tightly in one corner of narrative space. Human writing is measurably rarer.

Plus per-model fingerprints, because each model has its own habit: Claude keeps things reverent and quiet, GPT loves a dream sequence and secondhand gossip, Gemini defaults to bleak settings and outside-in description.

And the register gate that keeps it usable. The narrative layer was measured on fiction, so telling a B2B landing page to add an ambiguous ending would ruin it. Marketing copy gets only the universal signals. Long-form prose gets those plus structural variety. Storytelling gets everything.

## Files

```
SKILL.md              orchestration, modes, gates, surface + narrative layers
eval.md               20 binary checks, run on the skill's own output
references/ptbr.md    Brazilian Portuguese layer + house rules
references/rubrica.md 5 dimensions, 1 to 10, cut at 35/50
```

## Install

Cross-agent [skills](https://skills.sh) format — works with Claude Code, Codex, OpenCode, Cursor, and any agent that can follow an instruction file:

```bash
npx skills add badmuriss/unslop
```

Or plain git:

```bash
git clone https://github.com/badmuriss/unslop ~/.claude/skills/unslop
```

Then ask for any of the four modes: "write a launch post about X", "unslop this", "is this text AI?", "score this". Any capable LLM can also run it as a plain instruction set, as long as it can read the four files.

## Dogfooding

The files enforce their own rules. No em dash, no "not just X, it's Y", no Title Case, no decorative triads, no generic upbeat ending, in this README or in the skill itself. The v1 audit caught three things in the first draft of this file: an em dash splice in the opening, an "unslop stands as a comprehensive solution for" (inflated significance plus copula avoidance), and a closing paragraph about the future of authentic writing, which was deleted because the numbers already made the case.

If you spot a tell that got through, that is a good bug. Open an issue.

## Credit

The two sources the content comes from:

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), CC BY-SA 4.0. The surface layer is a derivative.
- Russell, Rajendhran, Pham, Iyyer, Wieting. *StoryScope: Investigating Idiosyncrasies in AI Fiction.* arXiv:2604.03136. [Code and data](https://github.com/jenna-russell/storyscope). The narrative layer, including every percentage quoted above.

Mechanics in v2 were inspired by three skills, none of whose text is reproduced here:


- [stop-slop](https://github.com/hardikpandya/stop-slop) by Hardik Pandya, for the scored rubric with a hard cut line instead of a checklist.
- [no-ai-slop](https://github.com/petergyang/no-ai-slop) by Peter Yang, for two ideas: a detect mode that must name the pattern and quote the line rather than guess, and keeping the eval in its own file so the skill can grade the edit it just made.
- [humanizer](https://github.com/blader/humanizer) by blader, for voice calibration from a pasted sample and for the rule that a rewrite may not introduce a fact the original did not have.

## License

CC BY-SA 4.0. The surface layer is a derivative of Wikipedia text, so the share-alike terms carry over to the whole work. Use it, fork it, ship it, keep the attribution.
