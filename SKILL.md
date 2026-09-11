---
name: writing-pr-descriptions
description: Use when writing or updating a pull request description, before running `gh pr create` or `gh pr edit --body`, when asked to make a description shorter, tighter, clearer or less waffly, or after a PR has been rebased or retargeted so its description may state a stale base, version or test count.
---

# Writing PR Descriptions

## Overview

A reviewer reads a description to answer three questions, in order: **what changes for anyone using this code, where do I look to check it, and what do I have to decide?** Every sentence answers one of those.

Fill the repository's own template — do not replace it. Its reviewer checklist is what the approver signs.

## What each section is

**What does this PR do** — one opening line saying what changes, then one numbered item per independent change. Each item states what it is in plain words, then why it exists. A behaviour change leads with the consequence a caller sees: *"`search` would pass a downstream 403 straight through — a status its own Swagger docs never mention, so a client has no reason to handle it."*

For a preparatory or no-public-behaviour layer, the opening also names the concrete capability in the immediate consuming layer, the current constraint that makes this preparation necessary, the duplication, coupling or risk it avoids, and why reviewing it separately helps. *"Extracts a shared boundary for future work"* says what changed but not why the PR exists. Before PR numbers exist, name the next layer and capability; link the actual consuming PR once it is open.

**What tests does this PR have** — the command and resulting counts, then one line per test file naming what it pins. A verification claim names the artefact and the number: *"byte-identical, 640,597 bytes"*, not *"verified byte-identical"*.

**How can this be tested** — commands that run as written, then the order to read the diff in and what to compare each file against.

**Any tech debt** — debt this PR adds or clears, and any decision you want overturned, as the decision and its cost.

## Audience

Written for an engineer who has not read the ticket and does not know the sub-domain. Name the thing, not its category: *"one of four outcomes — `next_question`, `screening_complete`, `requires_review`, `restart_required`"* beats *"a four-variant discriminated union"*. A term the diff does not define gets defined in six words or leaves.

## Currency

The description describes the PR as it stands now. Re-read the base branch, version, file count, test count and any byte figure from the PR before posting — a rebase or retarget invalidates all of them, and a stale base name misdirects the reviewer.

## Links

Each link does a job the sentence names: what this unblocks, the convention it follows, where the follow-up was flagged, its counterpart in another repo.

In a stack, a preparatory layer links its immediate consumer and states the dependency, such as *"unblocks #214's DELETE client without duplicating the POST client's resilience policy."* The Stack table gives position; it does not supply this rationale.

## Routing

Sentences in the description are statements about the code. Three things go to the author in chat instead, one line each: how the work went, how confident you are, and offers of alternatives.

## Calibration

Draft it, then keep the sentences that would survive the author's own edit. On a nine-paragraph draft, two survived. Write those two first.

## Common mistakes

| Instead of | Write |
|---|---|
| "Verified the mirror rather than asserting it" | "The published request schema is identical to the deployed one, compared field-by-field." |
| "Stacked on #101, rebased onto the old base after #112" | "Split out from #120 so that PR contains only the new endpoint." |
| "This PR was built against the target contract from its own open PR" | Delete — say what the contract is now. |
| "Extracts a method-neutral boundary in preparation for later work" | "The next layer adds a DELETE client, but transport policy lives inside the POST helper; this separates it so DELETE does not duplicate resilience and telemetry behaviour." |
| "**⚠️ Please read before merging**" on a resolved issue | Delete the block. |
