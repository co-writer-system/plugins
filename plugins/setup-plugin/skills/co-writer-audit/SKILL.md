---
name: co-writer-audit
description: Run a quality check on your CLAUDE.md and workspace — flags what's thin, missing, outdated, or could be stronger. Use when you want to see how your system file holds up and where to improve it.
---

# Co-Writer System Audit

You are running a quality check on the user's Co-Writer System. This is a diagnostic — you flag issues and recommend improvements. You don't make changes unless the user asks.

**If no CLAUDE.md exists**, tell the user: "You don't have a CLAUDE.md yet. Create one in your workspace root first — start with the four core sections: You, Your Business, Your Ideal Client, Your Tools. Once you have a draft, run this skill again to audit it." Then stop.

## Step 1: Read Everything

Read the user's CLAUDE.md. Then scan their actual workspace folder structure on disk.

Also check for:
- A `context/` folder with reference documents
- Any voice profile skill installed
- Any connectors configured (check if tools mentioned in CLAUDE.md have connector entries)

## Step 2: Score Each Section

Evaluate each section against what a strong CLAUDE.md looks like. Use the criteria below as the benchmark.

Rate each section:

| Rating | Meaning |
|--------|---------|
| **Strong** | Complete, specific, actionable — Claude has what it needs |
| **Adequate** | Exists and has content, but could be more detailed or specific |
| **Thin** | Exists but too vague or has [TBD] placeholders |
| **Missing** | Section doesn't exist but should based on their setup |
| **Outdated** | Content doesn't match what's actually on disk or seems stale |

### What "Strong" Looks Like Per Section

**User Profile — Strong when:**
- Has name, role, timezone, background
- Background is specific (not just "marketing professional" — what kind, what experience)
- Online presence is complete with URLs

**Business Profile — Strong when:**
- Clear one-liner description
- Each product/service has type, pricing, and what buyers get
- Revenue model is explicit
- Content model is clear (self, clients, or both)
- Content channels listed
- In scope and out of scope defined

**Ideal Client Profile — Strong when:**
- Specific about who they are (not just "business owners")
- Problems are real frustrations, not generic
- Aspirations are specific outcomes
- Objections/barriers are named
- Customer language section exists with real phrases (bonus, not required)

**Tools & Infrastructure — Strong when:**
- Tools are split into Connected (with connector details) and Other
- Connected tools have config fields filled in (not placeholders)
- Connector source noted (Co-Writer platform vs Cowork official)

**Voice — Strong when:**
- Points to voice skill, nothing more
- Does NOT contain word lists, tone rules, or style descriptions

**Workspace Structure — Strong when:**
- Documented tree matches what actually exists on disk
- Each folder has a brief description of what goes in it

## Step 3: Present the Audit

Show the results as a clear report:

```
## CLAUDE.md Audit

| Section | Rating | Notes |
|---------|--------|-------|
| User Profile | Strong | — |
| Business Profile | Adequate | Products listed but missing pricing details |
| ICP | Thin | Generic descriptions — needs specific frustrations |
| Tools | Adequate | 2 tools could have connectors but aren't connected |
| Voice | Strong | — |
| Workspace | Outdated | 3 folders on disk not documented |

**Overall: [X/6 sections strong]**
```

Then expand on each non-strong section with a specific recommendation:

```
### Recommendations

**Business Profile → Adequate**
Your products are listed but without pricing or what buyers get. A strong
business profile lets Claude reference pricing and benefits in content
without asking you every time.
→ Recommendation: Add type, pricing, and deliverables for each product.

**ICP → Thin**
"Business owners who want to grow" isn't specific enough for Claude to
write resonant content. What industry? What stage? What's the actual
pain that makes them search for help?
→ Recommendation: Rewrite with specific roles, named frustrations, and
  real customer language if you have it.

**Tools → Adequate**
You're using Airtable and YouTube but neither is connected. Connectors
let Claude read and write to these tools directly.
→ Recommendation: Set up YouTube and Airtable connectors. Cowork has
  official connectors in Settings → Connectors. The Co-Writer platform
  (app.alexmcfarland.ai) also hosts connectors for YouTube, Substack,
  Kit, Notion, and more if you want additional options.

**Workspace → Outdated**
These folders exist on disk but aren't in your CLAUDE.md:
- content/podcast/
- content/social/drafts/
- assets/thumbnails/
→ Recommendation: Add these to your Workspace Structure section.
```

## Step 4: Workspace Scan

Compare what's documented in the CLAUDE.md workspace section against what actually exists on disk.

Flag:
- **Undocumented folders** — exist on disk, not in CLAUDE.md
- **Ghost folders** — documented in CLAUDE.md but don't exist on disk
- **Empty folders** — exist but have no files (might indicate unused channels)

If there are more than 10 mismatches, summarize by category. Otherwise list individually.

## Step 5: Connector Opportunities

Cross-reference their tools list against commonly-available connectors. Flag any tool they use that has a connector available but isn't connected.

Commonly available connectors (as of this writing):
- **Cowork official connectors:** Airtable, Notion, Google Drive, Gmail, Slack, Linear, GitHub, and others — available in Cowork's Settings → Connectors panel
- **Co-Writer platform connectors** (`app.alexmcfarland.ai`): YouTube, Substack, Kit, Perplexity, Firecrawl, Zulip, Discord, Gemini Image, WordPress
- **Anthropic-hosted connectors:** Check the Claude Desktop/Cowork "Add custom connector" directory for the latest list

Flag format:

```
### Connector Opportunities

You're using these tools without connectors — connecting them would
let Claude read/write directly:

| Tool | Connector Available | Where |
|------|-------------------|-------|
| YouTube | Yes | Co-Writer platform |
| Notion | Yes | Cowork official |
| Airtable | Yes | Cowork official |
```

## Step 6: Ask What They Want to Do

After presenting everything:

```
That's the audit. Want me to:

1. **Fix something specific** — tell me which section and I'll update it
2. **Rebuild a weak section from scratch** — point me at the section and I'll rewrite it
3. **Leave it** — you know what to improve, you'll handle it

Or just tell me what to work on.
```

Don't make changes unless they ask. This is a diagnostic, not an auto-fix.

## Rules

- **Diagnostic, not surgery** — present findings, don't auto-fix
- **Be specific** — "ICP is thin" is useless. "Your ICP says 'business owners' but doesn't specify what kind, what stage, or what their actual pain is" is actionable
- **Use the inline criteria as the benchmark** — compare against the "What 'Strong' Looks Like" section above
- **Flag connector opportunities** — if they're using a tool that could be connected, tell them
- **Don't be harsh** — this is a quality check, not a report card. "Here's how to make it stronger" not "this is bad"
- **If they ask you to fix something**, do it right there — don't punt to another skill
- **Voice section should ONLY be a pointer** — if it contains word lists or tone rules, flag it for cleanup
