# AGENTS.md

Guidance for AI coding agents working in this repository.

## Repo identity

- This is my personal Neovim config, originally based on `kickstart.nvim`.
- Optimize for maintainability and usefulness in this setup, not for preserving the repo as a pristine template.
- Prefer small, understandable changes over unnecessary churn.

## Important files and directories

- `init.lua` — main entrypoint and primary config file.
- `lua/custom/plugins/init.lua` — add custom plugin specs here.
- `lazy-lock.json` — plugin lockfile; only update it when the task intentionally changes plugins or plugin versions.
- `.stylua.toml` — Lua formatting config.
- `README.md` — helpful general context, but this repo should be treated as my evolving personal config.

## Plugin and structure conventions

- When adding custom Neovim plugins for this config, add them in `lua/custom/plugins/init.lua`.
- Do not add new custom plugin specs in `init.lua` unless explicitly requested.
- If custom plugins are being used, ensure the corresponding `custom.plugins` import in `init.lua` is enabled.
- Follow existing patterns before introducing new structure.
- Modularization is allowed when it clearly improves the config.
- Avoid unrelated refactors or broad cleanup during focused tasks.

## Editing expectations

- Keep changes targeted and easy to review.
- Preserve useful comments and documentation; update or remove stale comments when behavior changes.
- When changing keymaps, plugin setup, or editor behavior, check nearby config for related settings that may also need adjustment.
- If a change affects documented workflow, structure, conventions, important commands, or agent expectations, update `AGENTS.md` as part of the same workload.

## Validation

- After Lua or config changes, run lightweight validation when practical.
- Preferred checks include:
  - `stylua init.lua lua/`
  - `nvim --headless "+qa"`
- Do not run heavyweight plugin install/update/sync commands unless the task requires them.
- In your final summary, mention what you changed and what validation you ran.
