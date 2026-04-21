---
name: figma-cleanup-and-resume
description: Make Figma generate/modify workflows resumable and safely reversible. Use when a Figma task spans multiple use_figma calls or when you need to resume after context loss, avoid duplicates, or delete only agent-created nodes.
---
## Goal

Enable long-running Figma edits to be:

- **Resumable** (after context truncation or a new chat)
- **Idempotent** (re-running doesn’t duplicate screens)
- **Safely cleanable** (delete only what the agent created)

## Core idea

Tag everything the agent creates with shared plugin data and maintain a state ledger that maps logical keys → node IDs/keys.

Use:

- `node.setSharedPluginData(namespace, key, value)`
- `node.getSharedPluginData(namespace, key)`

## Required conventions (always)

Pick a stable namespace + keys:

- **namespace**: `"cursor"`
- **fields**:
  - `run_id`: unique run identifier for this session of work
  - `logical_key`: deterministic key like `screen/Homepage/Header`
  - `owner`: `"agent"`

Every write call MUST:

- tag created nodes immediately
- return all created/mutated IDs
- return an updated ledger

## State ledger (persist in-repo)

Persist to:

- `.cursor/figma/state.json`

Recommended shape:

```json
{
  "runId": "figma-YYYY-MM-DD-001",
  "fileKey": "optional",
  "root": { "wrapperFrameId": "123:456" },
  "nodes": {
    "screen/Homepage": { "id": "12:34", "type": "FRAME", "name": "Homepage" }
  }
}
```

If filesystem writes aren’t appropriate, return the full ledger in chat output and treat it as the source of truth.

## Workflow

### Step 1: Initialize or load ledger

- If `.cursor/figma/state.json` exists, read it and reuse its `runId`.
- Otherwise create a new `runId` and initialize the file.

### Step 2: Rehydrate (find nodes again without relying on chat memory)

Before modifying:

- Run a read-only `use_figma` scan for nodes tagged with:
  - `sharedPluginData('cursor','run_id') === runId`
  - and/or matching deterministic names

Rebuild the `{ logical_key -> id }` map from tags.

### Step 3: Idempotent create/update rule

When creating `logical_key = "screen/Homepage/Header"`:

- If ledger has an ID for that key and the node exists → update
- If ledger has ID but node missing → re-create and update ledger
- If ledger has no ID → create, tag, and write ledger

### Step 4: Safe cleanup

When asked to undo:

- Delete only nodes tagged with `run_id === runId` and `owner === 'agent'`
- Delete deepest-first to avoid orphan frames
- Never delete untagged nodes

### Step 5: Resume protocol

To resume later:

- Share the `runId`
- Point to `.cursor/figma/state.json`
- Start the next session by rehydrating (Step 2), then continue

## Stop conditions

Stop and do not mutate the file if:

- You cannot find the wrapper/root node deterministically
- Tags are missing and names are ambiguous (multiple “Homepage” frames)
- The user asks for destructive deletion beyond tagged nodes

