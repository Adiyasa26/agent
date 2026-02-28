# How Convex Works in This Repository

This package is a **Convex Component** that provides reusable agent infrastructure.

## 1) Component packaging model

At the component layer (`src/component/*`), the repo defines:

- Convex component identity (`defineComponent("agent")`).
- Component schema tables (threads, messages, stream state, files, memories, vectors, api keys).
- Internal/public Convex functions to create/list/update thread and stream resources.

Applications include this component and then call its generated API through higher-level client helpers.

## 2) Data model overview

Core persisted entities:

- **threads**: conversation container + ownership/status metadata.
- **messages**: canonical persisted message records, tool/text metadata, usage.
- **streamingMessages**: active/finished/aborted stream registry.
- **streamDeltas**: chunked incremental outputs for realtime replay/resume.
- **memories / vectors**: retrieval context support.
- **files**: uploaded file metadata + refcount lifecycle.

This model lets Convex queries serve both:

- durable historical records,
- live stream updates to subscribed clients.

## 3) Runtime function model

The repo uses Convex function types according to job:

- **actions**: invoke LLM providers, run long/async operations.
- **mutations**: write tables, update stream heartbeats/status.
- **queries**: list messages/streams, power reactive UI subscriptions.
- **internalAction/internalMutation**: internal orchestration and safety boundaries.

## 4) Realtime + persistence strategy

Instead of only HTTP chunked streaming:

1. AI output is streamed.
2. Chunks are periodically persisted as deltas.
3. Clients subscribe to Convex queries.
4. UI merges stable messages + incoming deltas.

This supports:

- multi-client sync,
- reconnect resilience,
- async background generation where no HTTP stream is attached.

## 5) Practical references

- Convex component docs: <https://docs.convex.dev/components>
- Convex functions model: <https://docs.convex.dev/functions>
- Convex subscriptions/reactivity: <https://docs.convex.dev/realtime>
- Convex scheduling: <https://docs.convex.dev/scheduling/scheduled-functions>
- Agent docs for this component: <https://docs.convex.dev/agents>
