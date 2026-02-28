# AI SDK Version and Usage in This Repository

## Version used here

This repository targets **Vercel AI SDK v6**.

- `ai` is pinned as `^6.0.35` in `devDependencies`.
- `ai` is also declared as a peer dependency (`^6.0.35`) so downstream users bring their own compatible AI SDK v6 installation.
- Provider utilities are aligned with the v6 ecosystem (`@ai-sdk/provider-utils` `^4.0.6`).

## AI SDK APIs used by this codebase

The main AI SDK entrypoints used by this package are:

- `generateText`
- `streamText`
- `generateObject`
- `streamObject`
- `stepCountIs`

The Convex Agent library wraps these APIs to:

1. Add thread/context handling.
2. Save prompts/responses as message records.
3. Optionally persist streaming deltas to Convex for resumable multi-client streaming.

## AI SDK result handling patterns used in repo

This repository uses AI SDK result objects in several ways:

- **HTTP streaming response pass-through** (e.g. `toUIMessageStreamResponse` / related stream response methods).
- **Async stream consumption** (`for await` on stream parts).
- **Step lifecycle handling** (`onStepFinish`, continue/stop behavior).
- **Tool-call orchestration** through AI SDK tool abstractions.

## Compatibility guidance

If you are integrating this package in another app:

1. Keep `ai` at a compatible v6 release.
2. Keep provider packages (`@ai-sdk/openai`, `@ai-sdk/anthropic`, etc.) on versions intended for AI SDK v6.
3. Validate any AI SDK breaking changes against this library's wrappers around stream/generation flows.

## Useful AI SDK docs to read (v6)

- AI SDK docs homepage: <https://ai-sdk.dev/docs>
- Core `streamText` reference: <https://ai-sdk.dev/docs/reference/ai-sdk-core/stream-text>
- Core `generateText` reference: <https://ai-sdk.dev/docs/reference/ai-sdk-core/generate-text>
- Tools overview: <https://ai-sdk.dev/docs/ai-sdk-core/tools-and-tool-calling>
- UI message streaming concepts: <https://ai-sdk.dev/docs/ai-sdk-ui/streaming-data>

> Note: This repository builds higher-level Convex persistence and thread semantics on top of those core AI SDK primitives.
