# writing-pr-descriptions

A [Claude Code skill](https://code.claude.com/docs/en/skills) for writing pull request
descriptions that a reviewer can actually use: short, specific, and free of narration about
how the work went.

## Install

```sh
git clone https://github.com/will-not-hx/writing-pr-descriptions.git \
  ~/.claude/skills/writing-pr-descriptions
```

Claude Code picks it up from the description in the frontmatter, and invokes it when you ask
for a PR description, before `gh pr create`, or when you ask for an existing one to be
tightened.

## What it does

It states what each section of a PR description **is**, and routes three kinds of content
somewhere else:

- how the work went, and what was checked in what order
- how confident the author is, or what they got wrong earlier
- offers of alternatives — *"happy to switch if you'd rather"*

Those belong in the message to the reviewer, not in the description.

It also has a **Currency** rule, which is the one that earns its place most often: re-read the
base branch, version, file count and test count from the PR itself before posting. A rebase or
a retarget silently invalidates all of them, and a description naming a base the PR no longer
has sends the reviewer to the wrong diff.

It fills your repository's own PR template rather than replacing it — the template's reviewer
checklist is usually what the approver signs.

## Why it's a recipe and not a list of rules

The obvious way to write this skill is a list of things to avoid: don't narrate, don't restate
the diff, never pad. That form is the wrong fit for this problem.

Anthropic's `writing-skills` guidance distinguishes two failure modes. One is *discipline* — an
author who knows the rule and skips it under pressure. The other is *shaping* — an author who
complies with the instruction but produces the wrong-shaped output. A bloated PR description is
the second kind: nobody set out to ignore a rule, they just wrote a description that answered
the wrong questions.

Prohibitions measurably backfire on shaping failures. Under a competing pull — "make sure the
reviewer has all the context" — an author negotiates with *don't do X*, and in head-to-head
wording tests the prohibition form produced more of the unwanted content than either a recipe
or no guidance at all. A recipe leaves nothing to negotiate with: the output either matches the
stated shape or it doesn't.

So each section says what it contains, in order, and the three routed categories are stated as
destinations rather than bans.

## Calibration

The rule of thumb at the end of the skill came from a real edit: a nine-paragraph draft where
the reviewer kept two paragraphs, quoted them, and added a sentence of their own. Write those
two first.

## Licence

MIT — see [LICENSE](./LICENSE).
