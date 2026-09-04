## Decisions

- **Mirror pi-ai's level semantics exactly.** `validThinkingLevels` re-implements `getSupportedThinkingLevels` rather than importing it, because Pi loads the package with its own bundled pi-ai and the exported helper is not part of the extension surface. `"max"` therefore joins the existing explicit-mapping gate alongside `"xhigh"`: a level is invalid when `thinkingLevelMap` maps it to `null`, and the two highest levels are additionally invalid when their key is absent.

- **Defensive reads for older Pi.** `thinkingLevelMap` is read optional-chained so Pi bundles predating the field degrade to the legacy rule (levels through `"high"` valid, `"xhigh"`/`"max"` gated off) instead of throwing.

- **Theme fallback at the render site.** The `thinkingMax` theme color exists only in Pi >= 0.80.6, and `theme.fg` throws `Unknown theme color` for unknown colors inside the picker's render path — a crash, not a notification. The card catches that specific throw for the `"max"` level only and re-renders with `thinkingXhigh`, matching Pi's documented fallback. The catch is deliberately scoped to `"max"` so it cannot mask unrelated theme errors.

- **devDependency bump is a convenience.** The runtime floor for `"max"` is Pi 0.80.6 (where the level and theme color shipped); the `^0.84.1` devDependency floor only keeps the bundled type definitions current for `tsc`. The peer dependency range stays `*`.
