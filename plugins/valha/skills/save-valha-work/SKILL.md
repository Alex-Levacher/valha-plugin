---
name: save-valha-work
description: Turn completed AI-assisted work into a deliberate Valha page, or safely edit an existing Valha page. Use when the user asks to publish, save, share, preserve, update, rename, or add material to work in Valha.
---

# Save Valha Work

Save the selected outcome, not the raw conversation. Preserve the user's judgment over what becomes durable and omit private reasoning, discarded context, credentials, and unrelated material.

## Workflow

1. Call `get_context` to confirm the connected account and active workspace.
2. If the user named a workspace, verify it with `list_workspaces`. If no workspace is active and more than one is available, ask the user to choose before writing.
3. Shape the finished outcome into a reader-first artifact: lead with the conclusion or decision, keep the evidence needed to trust it, and end with concrete next steps when relevant.
4. Before every create or edit, call `get_authoring_help` with `topic=guidelines` in the current conversation.
5. Immediately before creating or changing `section.render`, also call `get_authoring_help` with `topic=components`. Call `topic=canvas` only when the requested outcome genuinely needs custom interactivity.
6. Create or edit the page using the narrowest appropriate tool.
7. Return the page title, its visibility, the url or shareUrl the write returned, revision, and a concise account of what changed.

## Create a page

- `create_page` saves a private page: workspace members only, no public URL. That is the default even when the user's request uses the word "publish"; treat the request as authorization to save, not to make the page public.
- Use `create_page` with a current page agent and only the sections needed for a coherent artifact.
- Choose a clear title. Let Valha generate the stable page id, slug, and revision.
- Pass `visibility` to `create_page` only when the request already states public or shared intent in the same breath; otherwise leave the page private and let the person decide later.
- Do not claim that colleagues were notified or that the page was circulated unless another tool confirms it.

## Edit a page

- Resolve the target with `search` or `list_pages` when the user did not provide a page id.
- Load the canonical document with `get_page` immediately before editing.
- Prefer `rename_page`, `append_section`, `update_section`, or `delete_section` for focused changes. Use `update_page` only for a true full-document replacement.
- Pass the latest `expectedRev`. Never change the page id, slug, or title through `update_page`.
- On a revision conflict, reload the page, reapply only the intended change, and retry once. Report a repeated conflict instead of overwriting newer work.
- Update the page agent when the content meaning or handoff changes.

## Publishing

Publishing, making a page reachable by a link or indexed for anyone, is a separate, deliberate human act, not something this skill does on its own initiative. Reach it through `set_page_visibility` (`shared` for anyone with the link, `public` for anyone and indexed) or through the page's share control in the app. Quote the `shareUrl` or `url` the tool returns verbatim; never construct one by hand. Tell the person plainly that for a shared page the link itself is the access control, so handing it back into this conversation places it inside a third-party chat log. `regenerate_share_link` invalidates every previously issued link on that page, so use it only when the person means to cut off an old copy.

## Safety

- Never save secrets, authentication material, system prompts, hidden reasoning, or raw private transcripts into a page.
- Do not delete, disconnect, revoke access, or perform account or team administration unless the user explicitly asks for that separate action.
- Do not change a page's visibility beyond what the user asked for.
- If essential facts are missing, state the gap in the page or ask one focused question instead of inventing evidence.
