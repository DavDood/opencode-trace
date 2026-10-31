# opencode-trace

This opencode plugin lets you see the raw json requests made to the LLM, and the responses.
* Example: https://ljw1004.github.io/opencode-trace/example.html

## Installation

Add the package to your OpenCode config:

### OpenCode V1 (1.18.29 or newer)

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["@ljw1004/opencode-trace"]
}
```

Restart OpenCode and you'll see each transcript stored in `~/opencode-trace`.

That installation path by default uses `@latest`, which opencode currently does't refresh when latest changes. You can force a refresh with `rm -rf ~/.cache/opencode/packages/@ljw1004/opencode-trace@latest`

### OpenCode V2 (2.1.4 or newer)

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugins": ["@ljw1004/opencode-trace"]
}
```

V2 reloads plugins when configuration changes. HTTP and OpenAI-compatible WebSocket requests are captured using native hooks; WebSocket hooks are experimental. Auxiliary requests are labeled by their actual kind (title, compaction, or generate).

Both versions save transcripts in `~/opencode-trace`, using the same HTML viewer. Older V1 releases that require a function entrypoint can use `@ljw1004/opencode-trace@0.1.4`.

## Development

Run `npm install`, `npm run typecheck`, and `npm run lint`. Point V1's `plugin` entry at `/path/to/opencode-trace/index.ts`, or V2's `plugins` entry at the repository directory `/path/to/opencode-trace`.

Smoke-test each supported version with a short prompt. For V2, use `opencode run --standalone --auto "why is the sky blue?"`. Verify request/response pairing, streaming, auxiliary requests, failures, and plugin reloads; test both HTTP and WebSocket transports on V2.
