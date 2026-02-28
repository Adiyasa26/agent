# Repository Flow (End-to-End)

This is the overall flow of how this repository is organized and how requests travel through it.

## Layered architecture

```mermaid
flowchart LR
  A[Consumer app] --> B[Convex functions in app/example]
  B --> C[@convex-dev/agent client layer src/client]
  C --> D[AI SDK core calls]
  C --> E[Component API calls src/component]
  E --> F[Convex DB tables]
  F --> G[Reactive queries/subscriptions]
  G --> H[React hooks src/react + example UI]
```

## Request lifecycle (typical chat streaming)

1. User sends a prompt from UI (`example/ui/chat/*`).
2. App calls Convex action (`example/convex/chat/streaming.ts`).
3. Action uses `Agent` wrapper from `src/client/index.ts`.
4. Wrapper prepares context/thread state, then calls AI SDK stream API.
5. Stream output is:
   - persisted as final messages,
   - optionally persisted incrementally as deltas.
6. Query (`listUIMessages` + `syncStreams`) returns message history + active deltas.
7. React hooks (`useUIMessages` / streaming helpers) render progressively.
8. Stream finalizes as `finished` or `aborted`; UI converges to final stored message.

## Repo areas and responsibilities

- `src/component/*`: Convex component schema + low-level table functions.
- `src/client/*`: agent abstractions, AI SDK wrappers, context/storage orchestration.
- `src/react/*`: frontend hooks/components for streaming message UX.
- `example/convex/*`: runnable backend examples.
- `example/ui/*`: runnable frontend examples.
- `docs/*`: usage and architecture documentation.

## Why this structure works

- Keeps AI provider logic and Convex persistence coordinated.
- Encapsulates durable streaming in one reusable package.
- Supports both backend-only automation and interactive UIs.
