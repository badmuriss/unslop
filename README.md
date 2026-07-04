# unslop

Strip the "this was written by AI" tells out of text. Works at two layers: the words on the page, and the choices underneath them.

![license](https://img.shields.io/badge/license-CC--BY--SA--4.0-blue)
![type](https://img.shields.io/badge/type-LLM%20skill-black)

Most humanizers stop at the surface. They kill an em dash, swap "delve" for "explore", and call it done. That barely helps. When Russell and coauthors trained a classifier to spot AI fiction from narrative structure alone, with every stylistic cue stripped out, it still hit 93.2% macro-F1. Then they ran a state of the art surface rewriter over the AI text and detection dropped by 1.6 points. Almost nothing. The tell was never in the vocabulary. It was in what the story chose to do.

So unslop cleans both.

## The two layers

**Layer 1, surface.** The stuff you already know is AI: em dashes everywhere, "testament to", rule of three, "It's not just X, it's Y", curly quotes, "Certainly! Here's an overview", bold-header bullet lists. Built from [Wikipedia's Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), which the WikiProject AI Cleanup editors assembled from thousands of real cases. Cheap to fix. Still worth fixing.

**Layer 2, narrative.** What surface edits can't reach. From [StoryScope](https://arxiv.org/abs/2604.03136) (Russell, Rajendhran, Pham, Iyyer, Wieting). The signals:

- **Over-explaining the theme.** AI narrators state the moral 77% of the time. Humans, 52%. It spells out the point instead of trusting you to get it.
- **Vague allusions.** Humans name real books, brands, and places at nearly double the AI rate. AI reaches for "a popular streaming service" when it means Netflix.
- **Sensory over-writing.** AI renders emotion as body 81% of the time (tightening chest, cold sweat) versus 38% for humans. Sometimes a person just writes "she was scared" and moves on.
- **Tidy, linear plots.** Fewer subplots, protagonist-driven endings, everything resolved. Humans jump in time and leave loose ends.
- **Low diversity.** The five models tested cluster tightly in one corner of narrative space. Human writing is measurably rarer and more spread out.

It also ships per-model fingerprints, because each model has its own habit: Claude keeps things reverent and quiet, GPT loves a dream sequence and secondhand gossip, Gemini defaults to bleak settings and outside-in description.

## The part that keeps it usable

Layer 2 was measured on fiction. Telling a B2B landing page to "add an ambiguous ending and a morally gray protagonist" would ruin it. So the skill gates every narrative rule by register:

| Register | Gets |
|----------|------|
| Marketing / B2B copy | Only the universal signals (don't over-explain, name real things) |
| Long-form prose | Universal, plus vary your structure |
| Storytelling / fiction | Everything |

Removing tells is also only half of it. Clean but voiceless text reads as AI too. The skill pushes for an actual opinion, varied rhythm, and specific feelings over neutral reporting.

## Install

It's one Markdown file. Point any capable LLM at it as an instruction, or drop it into Claude Code:

```bash
git clone https://github.com/badmuriss/unslop ~/.claude/skills/unslop
```

Then ask Claude to "run unslop on this" and paste your text. The skill runs a draft pass, an audit ("what still reads as AI here?"), and a final revision.

## Dogfooding

This README was written under its own rules, then audited with them. The audit caught three things in the first draft:

1. An em dash splice in the opening (Layer 1). Replaced with a period.
2. "unslop stands as a comprehensive solution for..." (Layer 1, inflated significance and copula avoidance). Cut to "unslop cleans both."
3. A closing paragraph about "the future of authentic writing" (Layer 2, over-explaining plus a generic upbeat ending). Deleted. The numbers already make the case.

If you spot a tell I missed, that's a good bug. Open an issue.

## Credit

Two sources, both worth reading:

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), CC BY-SA 4.0.
- Russell, Rajendhran, Pham, Iyyer, Wieting. *StoryScope: Investigating Idiosyncrasies in AI Fiction.* arXiv:2604.03136. [Code and data](https://github.com/jenna-russell/storyscope).

## License

CC BY-SA 4.0. The surface layer is a derivative of Wikipedia text, so the share-alike terms carry over. Use it, fork it, ship it, keep the attribution.
