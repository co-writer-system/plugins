---
name: voice-audit
description: Quality check an existing voice profile — find what's strong, what's thin, and what's missing. Use when you want to evaluate whether a voice profile is good enough to produce authentic output.
---

# Voice Profile Audit

You are evaluating the quality of an existing voice profile. Your job is to assess whether this profile gives Claude enough internalized understanding to write authentically as this person — or whether it reads like a generic style guide that will produce mechanical output.

## Step 1: Find the Profile

Look for voice skill files in the workspace. Check common locations:
- `skills/` directory
- Any file with "voice" in the name
- Any SKILL.md with a `voice-profile` name in its frontmatter

If you find multiple voice profiles, list them and ask which one to audit.

If you find none, say: "I can't find a voice profile in your workspace. Run `/voice:create` to build one from scratch."

## Step 2: Evaluate

Read the voice profile and evaluate it against these criteria. For each one, assess whether it's **strong**, **thin**, or **missing**.

### Voice Identity (the character brief)

**Strong:** Specific enough that you could distinguish this person from anyone else. Written as character direction ("You are someone who..."), not a trait list. If Claude only read this section, it would still produce recognizably correct output.

**Thin:** Exists but is generic. Could describe many people. "Writes in a conversational, professional tone" tells Claude almost nothing.

**Missing:** No character brief at all — the profile jumps straight into patterns or rules.

### Signature Moves

**Strong:** 5-8 concrete, observable patterns with real examples from the person's writing. Each one describes a specific structural or stylistic habit, not a vague quality.

**Thin:** Vague descriptions without examples. "Uses humor" instead of "drops dry one-liners mid-paragraph without setup." Or has patterns but no examples to anchor them.

**Missing:** No section covering recurring patterns or structural habits.

### Tone Modes

**Strong:** 2-3 distinct contexts with clear descriptions of how the voice shifts in each. Includes examples.

**Thin:** One flat description that doesn't capture how the voice changes across contexts. Or mentions multiple modes but without enough detail to be useful.

**Missing:** No acknowledgment that the voice has different modes.

### Never List

Before evaluating this section, read `${CLAUDE_PLUGIN_ROOT}/references/ai-tells.md` — the universal AI suppression list. Check the profile's Never Do section against those categories.

**Strong:** Covers the major AI-tell categories that apply to this voice (contrast flips like "This isn't X, it's Y", throat-clearing phrases, corporate vocabulary, hollow superlatives, metaphor overreach, closing cliches, structural tells). Each suppression is framed voice-specifically with an alternative, not just a generic ban. Phrases are concrete enough for Claude to pattern-match.

**Thin:** Misses major AI-tell categories, too vague ("avoid jargon"), or lists generic cliches without explaining why they conflict with this specific voice. Missing the contrast-flip ban when the target voice doesn't actually use that construction is a major gap.

**Missing:** No anti-patterns documented at all.

### Calibration Examples

**Strong:** 3-5 real excerpts with annotations explaining what makes each one sound like this person. The annotations point to specific moves and choices.

**Thin:** Examples exist but without annotations. Or annotations are vague ("this is a good example of their style").

**Missing:** No real writing samples included in the profile.

### Internalization vs. Rules

**Strong:** The profile reads like character direction an actor would use. Claude can inhabit this voice, not just follow instructions about it.

**Thin:** Mixed — some sections are character direction, others are rule lists. The overall effect is that Claude would partially inhabit and partially checklist.

**Weak:** The profile is fundamentally a style guide — a list of do's and don'ts. Claude will follow it mechanically, producing a caricature rather than an authentic voice.

## Step 3: Report

Present a concise audit. Don't overwhelm — flag what matters.

```
## Voice Profile Audit: [Name]

| Section | Status | Notes |
|---------|--------|-------|
| Voice Identity | [Strong/Thin/Missing] | [Specific note] |
| Signature Moves | [Strong/Thin/Missing] | [Specific note] |
| Tone Modes | [Strong/Thin/Missing] | [Specific note] |
| Never List | [Strong/Thin/Missing] | [Specific note] |
| Calibration Examples | [Strong/Thin/Missing] | [Specific note] |
| Overall Approach | [Internalized/Mixed/Rules-based] | [Specific note] |
```

After the table, give 2-3 sentences on the overall assessment. Be direct: "This profile will produce [good/mediocre/generic] output because [reason]."

Then list the highest-impact fixes — the 1-3 changes that would most improve the profile's effectiveness.

## Step 4: Offer Next Step

```
Want to fix these now? Run `/voice:update` and I'll walk you through targeted improvements.
```

## Rules

- Be specific in every assessment — not "thin" but "thin because [exact reason]"
- Lead with the highest-impact issues, not an exhaustive list
- The "internalization vs. rules" criterion is the most important — a profile with great patterns but written as a checklist will still produce mechanical output
- Don't rewrite the profile during audit — that's the update skill's job
- If the profile is genuinely strong, say so. Don't manufacture issues.
