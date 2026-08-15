# AI Brand Compliance Agent

A Claude Skill that checks marketing decks and materials against a company's brand guidelines and returns a structured compliance report: flagged violations, severity ratings, and suggested rewrites. I built it during my growth internship at Milliman MedInsight to cut the manual back-and-forth of getting slides on-brand before they ship.

> **Note:** This is a sanitized, public version. The brand rules here are generic examples. The real internal guidelines stay internal.

---

## The problem

Every deck, one-pager, and social asset at a large company has to follow brand guidelines: fonts, colors, logo usage, approved messaging, tone, legal disclaimers. In practice someone eyeballs each asset, catches what's off, sends it back, and the cycle repeats. It's slow. Different reviewers catch different things, so it's inconsistent. And it doesn't scale as more teams produce more content.

I built an agent that runs the first-pass review the same way every time.

---

## What it does

You give it the content, or a description of a slide or asset. It checks that against a structured set of brand rules and returns a typed report:

- **Violations.** Each specific thing that breaks a guideline.
- **Severity.** Critical, moderate, or minor, so people fix the important stuff first.
- **Location.** Which slide or element the issue sits on.
- **Suggested rewrite.** Not just "this is wrong," but the on-brand version to use instead.

The output is structured, so a reviewer reads a clean checklist instead of a wall of maybe-true text.

---

## How I built it

It's a Claude Skill. A `SKILL.md` encodes the brand ruleset plus the review logic and output format. The design choices that matter:

- **Rules are explicit and structured, not vibes.** Each guideline is a checkable rule with a category and a severity, so the same input gets the same review every time.
- **The agent has to point to the rule it's enforcing.** A flag isn't valid unless it names the specific guideline it breaks. This stops the model from inventing violations that aren't real.
- **Output is typed** (violation, severity, location, suggested fix) so the result drops straight into a reviewer's workflow instead of needing interpretation.

See [`SKILL.md`](SKILL.md) for the full build.

---

## Result

- Built and demoed company-wide at Milliman MedInsight
- Adopted by early users on the marketing team for real deck reviews
- Rollout to 200+ employees in progress

Honest status: this is in early adoption with a broader rollout underway, not a finished company-wide deployment. What's proven is that it works, people used it on real work, and leadership backed pushing it wider.

---

## Stack

Claude (Skill / `SKILL.md`) · structured prompt engineering · Microsoft Copilot Studio (enterprise distribution)

---

## What I'd improve

- **Measure the actual time saved.** Right now the win is qualitative ("faster reviews"). The real proof is a before/after on revision cycles per deck, which is the number I'm working to capture as adoption grows.
- **Handle visual assets directly.** Text and messaging rules are strong. True layout and logo-placement checking needs image input, not just descriptions.
- **Version the ruleset.** Brand guidelines change. The rules need a version stamp so a review can say which guideline version it checked against.
