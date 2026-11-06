---
name: lofi-design
description: Design, iterate and review low-fidelity wireframes in Lofi. Use when the user asks to wireframe, mock up, sketch screens or flows, compare design alternatives on a Lofi board, open or list their Lofi projects, or review a Lofi board they sent to the conversation.
---

# Lofi design workflow

Lofi is a wireframe canvas. The connected Lofi server exposes read tools,
guided host-authoring tools, explicit Lofi-model generation tools, and an
editable canvas UI. This skill describes how to combine them; the server
enforces ownership, revisions and evaluation on its own.

## Choose the path

- **You author the design (default).** Zero Lofi generation credits. Use this
  for new boards, redesigns, added screens and same-board alternatives.
- **Lofi model generation.** Only when the user explicitly asks for Lofi's
  model. `generate_wireframe` (new project) or `generate_variation` (additive
  alternative on the current board) use Lofi credits: Default 1, Thinking 10.
  Never switch to this path silently after a failed host-authored proposal.

## Author a new board

1. `get_design_guidance` with no project: read the catalog, skills and the
   worked example in the result.
2. Draft `addScreen` operations with catalog components. Link later screens
   from earlier new screen IDs in the same plan.
3. `evaluate_iteration` with the `guidanceToken`, the user's intent verbatim,
   the plan, and `newProject` holding a fresh UUID `requestId` and a title.
4. Fix blocking issues and evaluate again. Advisory layout or similarity
   notes do not block; report them honestly.
5. `create_wireframe_from_design` with the exact evaluated plan, the same
   intent, title and `requestId`, plus the `evaluationToken`. Retry a timeout
   with identical inputs; the server returns the same project.

## Change or extend an existing board

1. `list_frames` for the project: capture the current `version` and the frame
   IDs you will touch.
2. `get_design_guidance` with the project and the selected frame IDs.
3. Draft, then `evaluate_iteration` with the token, the unchanged intent and
   the plan.
4. `apply_canvas_update` with the exact evaluated plan, the same intent, the
   `evaluationToken` and the latest `baseVersion`. A conflict means the board
   changed: read the latest version and evaluate again.
5. Copy-only edits (`editElements` that change text) may skip evaluation.

## Add an alternative on the same board

Alternatives are additive. Use `plan.additionLayout: "independentRow"` with
`addScreen` operations only, new IDs, no `afterFrameId` on the first new
screen, and links only between new screens. Supply a variant brief with the
direction, benefit, tradeoff, preserved requirements and observable changes.
Preserve every existing element and connection. Never rename, replace or move
originals, and never create a second project for an alternative.

## Review a board the user sent

"Send to Claude" delivers the board's structure and, when this surface
supports images, a PNG. If an image is attached, read it directly. If only a
`handoffId` is supplied, call `get_board_handoff` before making any visual
claim; previews expire after 15 minutes. Distinguish the snapshot revision
from the current saved version, and do not edit, generate or spend credits
when the user asked for feedback only.

## What Lofi cannot do

Lofi does not book, pay, transfer funds, convert a Claude subscription into
Lofi credits, create editable Figma components, or enable live Figma sync.
Say so plainly and offer a wireframe, a text implementation brief, or Lofi's
own export instead.
