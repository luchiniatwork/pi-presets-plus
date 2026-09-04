## Why

pi-ai 0.80.6 added a seventh thinking level, `"max"`, sitting above `"xhigh"`. The package hard-codes the six older levels, so a preset declaring `"max"` is rejected at load time, and models that support `"max"` but explicitly null `"xhigh"` (e.g. Fireworks' Kimi K3 routers) silently degrade: a preset asking for `"xhigh"` falls back to `"off"`, which pi-ai's `clampThinkingLevel` then rounds up to `"low"`.

## What Changes

- Add `"max"` to the accepted `thinkingLevel` set at load-time validation.
- Mirror pi-ai's `getSupportedThinkingLevels` for the new level: like `"xhigh"`, `"max"` is valid for a model only when `thinkingLevelMap` explicitly maps it to a non-null value.
- Extend the activation clamp, the editor thinking-level radio, and the picker card formatting to the seven-level set.
- Render the picker card's `"max"` value with the `thinkingMax` theme color, falling back to `thinkingXhigh` on Pi versions whose themes predate that color (Pi >= 0.80.6), matching Pi's own fallback.
- Bump the `@earendil-works/*` devDependencies to ^0.84.1 so current pi-ai types are visible to `tsc` (a convenience, not a requirement — the runtime floor for `"max"` is Pi 0.80.6).

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `preset-storage`: `thinkingLevel: "max"` is accepted at load-time validation.
- `preset-activation`: `"max"` follows the `"xhigh"` validity gate — valid only when `thinkingLevelMap` explicitly maps it non-null — and clamps to `"off"` otherwise.
- `preset-editor`: the thinking-level radio offers seven levels and applies the same explicit-mapping gate to `"max"` as to `"xhigh"`.
- `preset-picker`: the preset card displays `"Max"` with the `thinkingMax` theme color, falling back to `thinkingXhigh` on Pi versions without that theme color.

## Impact

Thinking-level validation, activation clamping, the editor radio row, and the picker card rendering change; the `preset-storage`, `preset-activation`, `preset-editor`, and `preset-picker` specifications change with them. Presets declaring any of the six older levels behave exactly as before. The devDependency bump changes no runtime behavior: the package ships source and Pi loads it with its own bundled pi-ai.
