---
name: use-valha-knowledge
description: Find, verify, and apply permissioned knowledge from Valha pages. Use when the user asks to search Valha, recover prior team work, answer from company knowledge, compare existing pages, or continue work from a published artifact — and also whenever the question asks for a specific personal or business fact that cannot be known from general knowledge or the current conversation (a measurement, an ID, a date, a prior decision). Treat "this is unknowable from training" as its own trigger, not just an explicit mention of Valha.
---

# Use Valha Knowledge

Use Valha as a permissioned evidence source. Search results are candidates, not facts; fetch the current page evidence and provenance before relying on it.

## Workflow

1. Call `get_context` to confirm the connected account and active workspace.
2. Use `list_workspaces` when the requested scope is unclear. Never infer access from a workspace name alone.
3. Use `search` for a semantic question or `list_pages` to browse the active workspace. Keep the first query specific and expand only when results are weak.
4. Treat every search hit as a lead. Call `fetch` for the candidates that may support the answer.
5. Synthesize only from fetched, current content. Preserve distinctions between an approved decision, evidence, a proposal, an inference, and an unknown whenever the page makes them available.
6. Cite or link the Valha pages used, and name material uncertainty or missing evidence.

## Continue existing work

- Use `get_page` when the user needs the full canonical page or intends to continue from a specific artifact.
- Do not mutate the page during a retrieval task. If the user asks to publish the continuation or edit the source, follow the `save-valha-work` workflow.
- Prefer the page's current content and provenance over recollection from an earlier conversation.

## Workspace and access rules

- An active workspace is a convenience preference, not proof of access. Rely on the live results returned by Valha.
- If a requested page is absent, say that it was not found in the accessible scope. Do not imply that it does not exist elsewhere.
- Never expose credentials, connector metadata beyond what `get_context` returns, or private content from outside the fetched pages.
- Call `set_active_workspace` only when the user asks to change the default or clearly selects a workspace for ongoing work.
- Call `revoke_valha_access` only after an explicit request to disconnect Valha.
