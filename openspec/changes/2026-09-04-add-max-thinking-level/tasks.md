## 1. Extend the thinking-level set

- [x] 1.1 Add `"max"` to the accepted `thinkingLevel` values in `src/types.ts` and to load-time validation in `src/store/validate.ts`; verify a preset declaring `"max"` loads and an out-of-set value is still skipped with a warning.
- [x] 1.2 Add `"max"` to `ALL_THINKING_LEVELS` in `src/activation/thinking.ts` and extend the explicit-mapping gate so `"max"`, like `"xhigh"`, is valid only when `thinkingLevelMap` maps it to a non-null value; keep the defensive optional-chained read for pi-ai versions predating `thinkingLevelMap`.

## 2. Apply and editor behavior

- [x] 2.1 Verify activation clamps `"max"` to `"off"` unless explicitly mapped, and honors `"max"` when `thinkingLevelMap: { "max": <non-null> }`; cover both paths in `tests/activation/apply-clear.test.ts` and `tests/activation/thinking.test.ts`.
- [x] 2.2 Add `"max"` to the editor's thinking-level radio in `src/ui/editor/rows/thinking.ts`; verify validity dimming, auto-snap, and the dimmed-levels hint reuse the shared `validThinkingLevels` rule unchanged.

## 3. Picker rendering

- [x] 3.1 Format `"max"` as `"Max"` in `formatThinkingLevel` and map it to the `thinkingMax` theme color in `src/ui/widgets.ts`.
- [x] 3.2 Fall back to the `thinkingXhigh` color when the active Pi theme has no `thinkingMax` color (Pi < 0.80.6), scoped so only the `"max"` render path can trigger the fallback; cover both the native-color and fallback paths in `tests/ui/widgets.test.ts`.

## 4. Packaging

- [x] 4.1 Bump the `@earendil-works/*` devDependencies to ^0.84.1 and regenerate `pnpm-lock.yaml` from the current lockfile without downgrading unrelated packages.
- [x] 4.2 Add a `CHANGELOG.md` entry under the next release describing the `"max"` support and the theme-color fallback.

## 5. Validate the change

- [x] 5.1 Run the format check, `tsc --noEmit`, biome/eslint, and the full vitest suite; verify all pass.
- [ ] 5.2 Run `openspec validate "add-max-thinking-level" --type change --strict` and verify the planning artifacts satisfy the schema.
