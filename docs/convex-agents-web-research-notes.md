# Convex Agents Web Research Notes (docs.convex.dev/agents)

This note records the requested research step for `https://docs.convex.dev/agents/**/**`.

## Target pages checked

I attempted to fetch these pages directly:

- `https://docs.convex.dev/agents`
- `https://docs.convex.dev/agents/agent-usage`
- `https://docs.convex.dev/agents/threads`
- `https://docs.convex.dev/agents/messages`
- `https://docs.convex.dev/agents/streaming`
- `https://docs.convex.dev/agents/context`
- `https://docs.convex.dev/agents/tools`
- `https://docs.convex.dev/agents/rag`
- `https://docs.convex.dev/agents/workflows`

## Environment limitation

In this environment, outbound requests to `docs.convex.dev` return HTTP 403, so I
could not directly ingest the live website pages.

## Fallback context used (repo-local mirrors)

This repository already contains the corresponding agent docs content in
`docs/*.mdx`. I used those as the effective context source:

- `docs/agent-usage.mdx`
- `docs/threads.mdx`
- `docs/messages.mdx`
- `docs/streaming.mdx`
- `docs/context.mdx`
- `docs/tools.mdx`
- `docs/rag.mdx`
- `docs/workflows.mdx`

## Why this is still useful

Those files are the canonical documentation shipped with this repo and align
with the implementation and examples under:

- `src/client/*`
- `src/component/*`
- `example/convex/*`
- `example/ui/*`

So the integration guidance in the other docs in this folder is grounded in the
actual code you will copy from when porting to another repository.
