# pi-google-google-search

[![ci](https://github.com/code-yeongyu/pi-google-google-search/actions/workflows/ci.yml/badge.svg)](https://github.com/code-yeongyu/pi-google-google-search/actions/workflows/ci.yml) [![license: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Google native search extension for the [pi coding agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent).

This package is the standalone extraction of senpi's former builtin `google-google-search` extension.

## Behavior

The extension does not register a new tool. It intercepts Google provider requests before they are sent and ensures a native `googleSearch` tool is present for `google-generative-ai` / `google-vertex` payloads when Google search is enabled (default-on).

| Case | Result |
|------|--------|
| API is `google-generative-ai` or `google-vertex`, `PI_GOOGLE_GOOGLE_SEARCH` is unset/empty/truthy, and no Tool object has a `googleSearch` key | injects a new Tool entry `{ googleSearch: {} }` |
| Existing Tool object already has `googleSearch` key (any value) | preserves caller payload without duplication or overwrite |
| Existing Tool object has only `functionDeclarations` | keeps that object and adds separate `{ googleSearch: {} }` entry |
| `PI_GOOGLE_GOOGLE_SEARCH` is falsy (`0`, `false`, `no`, `off`) | no-op |
| API is non-Google | no-op |

Truthy values for `PI_GOOGLE_GOOGLE_SEARCH` are: `1`, `true`, `yes`, `on` (case-insensitive, surrounding whitespace allowed). Unknown values fall back to enabled to preserve default-on behavior.

It also appends a system-prompt section for Google sessions indicating native `google_search` availability when enabled.

## Installation

The package targets the [`pi`](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) coding agent. Pi loads extensions from `~/.pi/agent/extensions/`, project `.pi/extensions/`, or via the `--extension` / `-e` CLI flag.

```bash
# From npm (once published)
pi install npm:pi-google-google-search

# From git
pi install git:github.com/code-yeongyu/pi-google-google-search

# Manual placement
git clone https://github.com/code-yeongyu/pi-google-google-search ~/.pi/agent/extensions/pi-google-google-search
cd ~/.pi/agent/extensions/pi-google-google-search && npm install

# Dev / one-shot test
pi -e /path/to/pi-google-google-search/src/index.ts
```

After installation, restart pi or run `/reload` inside an interactive session.

## Development

```bash
npm install
npm test
npm run typecheck
npm run check
pi -e ./src/index.ts
```

The test suite uses vitest. TypeScript is strict, Node-only, and uses ESM imports with `.js` suffixes.

## Origin

Ported from `packages/coding-agent/src/core/extensions/builtin/google-google-search/index.ts` in the senpi-mono fork of pi-mono.
