# AI Brand Compliance Agent

A Claude Skill that builds brand-compliant presentations, decks, templates, and visuals from a single prompt, and fixes existing ones to match brand guidelines. I built it during my growth internship at Milliman MedInsight so anyone on the team could produce on-brand slides without a manual review cycle.

> **Note:** This is a sanitized, public version. The brand rules here are generic examples. The real internal guidelines stay internal.

---

## The problem

Every deck, one-pager, and social asset at a large company has to follow brand guidelines: fonts, colors, logo usage, approved messaging, tone, legal disclaimers. In practice someone builds the asset, another person eyeballs it, catches what's off, sends it back, and the cycle repeats. It's slow. Different reviewers catch different things, so it's inconsistent. And it doesn't scale as more teams produce more content.

I built a Skill that bakes the guidelines into the creation step, so the asset comes out on-brand the first time.

---

## What it does

Two modes, one Skill.

**Create from scratch.** A user loads the Skill and asks for a presentation, template, or visual. The Skill generates the full asset already following the brand guidelines: correct fonts, colors, logo usage, approved messaging, and tone. No separate design or review pass needed.

**Fix an existing asset.** A user pastes a deck or document they already made. The Skill checks it against the guidelines and returns a corrected, brand-compliant version, plus a note on what it changed and why.

The point is that a non-designer can produce something on-brand in one step, and the guidelines get applied the same way every time.

---

## How I built it

It's a Claude Skill. A `SKILL.md` encodes the brand ruleset plus the generation and correction logic. The design choices that matter:

- **Rules are explicit and structured, not vibes.** Each guideline is a concrete rule with a category, so the same request produces the same on-brand result every time.
- **The guidelines drive creation, not just review.** Instead of building an asset and then checking it, the Skill applies the rules while it generates, so compliance is the default state rather than a cleanup step.
- **Corrections come with a reason.** When it fixes an existing asset, it names the guideline each change enforces, so the user learns the rule instead of just accepting an edit.

---

## Result

- Built and demoed company-wide at Milliman MedInsight
- Adopted by early users on the marketing team for real deck creation and cleanup
- Rollout to 200+ employees in progress

Honest status: this is in early adoption with a broader rollout underway, not a finished company-wide deployment. What's proven is that it works, people used it on real work, and leadership backed pushing it wider.

---

## Stack

Claude (Skill / `SKILL.md`) · structured prompt engineering · Microsoft Copilot Studio (enterprise distribution)

---

## What I'd improve

- **Measure the actual time saved.** Right now the win is qualitative ("faster, on-brand decks"). The real proof is a before/after on build and revision time per deck, which is the number I'm working to capture as adoption grows.
- **Handle visual assets directly.** Text, layout, and messaging rules are strong. True pixel-level logo-placement checking needs image input, not just structured content.
- **Version the ruleset.** Brand guidelines change. The rules need a version stamp so an asset can say which guideline version it was built against.
