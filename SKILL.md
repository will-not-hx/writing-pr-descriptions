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

**What tests does this PR have** — the automated command and resulting counts, then one line per test file naming what it pins. A verification claim names the artefact and the number: *"byte-identical, 640,597 bytes"*, not *"verified byte-identical"*.

**How can this be tested** — include both automated commands that run as written and manual testing instructions. A manual check names its prerequisites or test data, the action to take, and the expected result. Keep instructions proportional to the layer: a user-facing change gets the real journey; a transport or persistence layer gets the narrow integration path that exercises it. If manual execution genuinely does not apply, say why and give the reviewer a concrete inspection path instead. Distinguish steps a reviewer can run from checks already performed; never imply an unperformed live test passed.

**Any tech debt** — debt this PR adds or clears, and any decision you want overturned, as the decision and its cost.

## Splitting is not a quality exemption

A smaller PR is a review aid, not a reason to reduce code quality. Do not justify misplaced ownership, duplicated contracts, weaker validation or tests, or bypassed release checks as necessary for a stack. If the rationale depends on such a compromise, fix the split or combine the layers before presenting them as ready.

Explain the concrete benefit of separate review without disguising a quality regression as preparation. Report genuine limitations and debt plainly; do not write "no debt" because a later PR is expected to clean them up. This applies to intermediate layers as well as the completed stack.

## Audience

Written for an engineer who has not read the ticket and does not know the sub-domain. Name the thing, not its category: *"one of four outcomes — `next_question`, `screening_complete`, `requires_review`, `restart_required`"* beats *"a four-variant discriminated union"*. A term the diff does not define gets defined in six words or leaves.

## Currency

The description describes the PR as it stands now. Re-read the base branch, version, file count, test count and any byte figure from the PR before posting — a rebase or retarget invalidates all of them, and a stale base name misdirects the reviewer.

## Links

Each link does a job the sentence names: what this unblocks, the convention it follows, where the follow-up was flagged, its counterpart in another repo.

Include every relevant source of context a reviewer needs to verify the change: the ticket, current HLD or architecture decision, external specification or vendor documentation, counterpart implementation, and any tracked follow-up. Put the link at the claim it supports and name the relevant section when the source is long. Do not leave an authoritative source out merely because its conclusion is repeated in the ticket, and do not add an unlabelled link dump.

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
| A ticket link with no design source | Link the ticket and the current HLD or specification at the behaviour each one establishes. |
| Automated commands as the entire testing section | Add manual prerequisites, action and expected result, or explain why manual execution does not apply and give a concrete inspection path. |
| "**⚠️ Please read before merging**" on a resolved issue | Delete the block. |
