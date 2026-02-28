# Does This Repo Use Convex `persistent-text-streaming`?

Short answer: **No, not as a separate component/package dependency.**

## What was checked

I checked for:

- dependency/package references to `persistent-text-streaming`,
- imports containing `persistent` + `streaming` component names,
- usage patterns that would indicate the standalone component.

No matches were found in:

- `package.json` / `package-lock.json`
- `src/`
- `example/`
- existing docs

## What this repo uses instead

This repository implements its own persistent streaming layer inside the Agent component:

- `streamingMessages` table tracks stream metadata and lifecycle state.
- `streamDeltas` table stores chunked delta payloads.
- `DeltaStreamer` writes and heartbeats deltas.
- `syncStreams` and message hooks rehydrate stream updates for clients.

So, behavior is conceptually similar to persistent text streaming, but implemented directly in `@convex-dev/agent` internals.
