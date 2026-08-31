---
name: use-valha-blueprints
description: Find, apply, improve, or capture reusable Valha methods. Use for a multi-step operational goal, work requiring tools or organization data plus verification, a recurring process whose method matters beyond one factual answer, or when the user explicitly asks to find, apply, improve, or capture a Blueprint. Do not use automatically for translation, formatting, one factual lookup, trivial edits, or casual conversation; an explicit Blueprint request always wins.
---

# Use Valha Blueprints

Blueprints provide reusable methods. Valha pages provide factual evidence and context; use `use-valha-knowledge` when the task needs facts rather than a method.

## Find a method

1. For substantial work, call `search_blueprints` with `mode: "automatic"` and the smallest specific method query. If it returns no candidate, continue silently. A technical failure is not a no-result claim; continue the task and mention the unavailable search only when it matters.
2. Offer at most two returned strong candidates. For each, state why it matches and list its current prerequisites. Do not expose its score or opaque result ID, and do not present a method as a factual answer.
3. Call `inspect_blueprint` only when more detail, including current prerequisites, is needed to explain a possible candidate. Do not call `use_blueprint` until the user explicitly selects one.
4. Before loading, compare the prerequisites with capabilities known in this session. If a prerequisite is known to be missing, state the blocker and do not load. State unknown prerequisites as unknown rather than inventing them.
5. After explicit selection, call `use_blueprint` with the exact opaque result ID and add `pageId` only when that page is genuinely the application target. Follow the exact loaded revision instead of remembered content.

When the user explicitly asks to search, use `mode: "explicit"`. Label possible matches clearly; distinguish no relevant match from search being temporarily unavailable.

## Record the attempt

After attempting the loaded method, ask exactly one short question covering both resolution and possible improvements: “Did this resolve the task, and should anything be added or changed?”

Call `record_blueprint_outcome` only from the user's explicit answer:

- use `applied` when the user confirms the method was performed but does not confirm resolution;
- use `resolved` only when the user confirms resolution;
- use `failed` only when the user explicitly reports failure.

Silence, elapsed time, a successful tool call, or assistant confidence is not an outcome.

## Improve a shared method

When use reveals a durable improvement, show the current method and proposed difference concisely, then explain why it is reusable rather than specific to this session. Only after explicit approval call `update_blueprint` with the current version and a non-empty reason.

On a version conflict, call `inspect_blueprint`, reapply the proposed difference once, and retry. Report a repeated conflict instead of overwriting. Never automatically update, disable, reactivate, or delete a shared Blueprint.

## Capture a new method

After meaningful resolved work produces a repeatable method:

1. Call `search_blueprints` in explicit mode to check exact and semantic duplicates.
2. If an equivalent method exists, offer an improvement instead of creation.
3. Otherwise explain its reusable value and offer a canonical Markdown draft with title, keywords, objective, when to use, prerequisites, steps, checks, and expected outcome.
4. Keep the draft in the conversation and revise it there until the user approves it.
5. Call `create_blueprint` only after a separate explicit confirmation.
6. If publishing returns a safe duplicate candidate, show it and ask whether the method is genuinely different. Supply a non-empty difference reason only from that explicit decision.

Never auto-create a Valha page, store raw conversation or task text, publish from a mere successful tool call, or claim retrieval quality is validated. Automatic thresholds remain provisional until the benchmark passes.

## Browse and lifecycle requests

Use `list_blueprints` to browse the accessible catalogue. Use `set_blueprint_status` or `delete_blueprint` only when the user explicitly asks for that exact lifecycle operation. Explain before deletion that it is permanent and restricted to the original author, and keep its confirmation separate from any other request.

Changed plugin skills enter host capability snapshots only in a new task/session. Do not assume this workflow is active in a session that started before the plugin was regenerated and loaded.
