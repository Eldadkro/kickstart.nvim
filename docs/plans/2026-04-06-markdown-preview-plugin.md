# Markdown Preview Plugin Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan iteratively. Steps use checkbox (`- [ ]`) syntax for tracking so work can resume cleanly after context resets.

**Goal:** Add `iamcco/markdown-preview.nvim` as a custom lazy.nvim plugin using npm-based installation and markdown-only lazy loading.

**Architecture:** Keep the change isolated to the existing custom plugin entrypoint at `lua/custom/plugins/init.lua`, following this repo's convention for personal plugin additions. Configure the plugin to install its web assets via `npm install`, load only for markdown buffers and markdown preview commands, and leave the main `init.lua` and lockfile untouched unless validation requires otherwise.

**Tech Stack:** Neovim Lua config, lazy.nvim plugin specs, npm

---

## File structure

- Modify: `lua/custom/plugins/init.lua` — existing home for custom plugin specs in this repo; add the markdown preview plugin alongside the existing VimTeX spec.
- Create: none
- Test/validate via commands: `stylua init.lua lua/` and `nvim --headless "+qa"`

### Step 1: Add the markdown preview custom plugin spec

**Files:**
- Modify: `lua/custom/plugins/init.lua`

**Why this step matters:** This adds the requested plugin in the repo's established custom plugin location without affecting unrelated plugin configuration.

**Before editing, re-read:**
- `AGENTS.md`
- `lua/custom/plugins/init.lua`
- `init.lua`

- [x] **Implement the plugin spec change**

Add this plugin table inside the returned lazy spec list in `lua/custom/plugins/init.lua`:

```lua
  {
    'iamcco/markdown-preview.nvim',
    cmd = { 'MarkdownPreviewToggle', 'MarkdownPreview', 'MarkdownPreviewStop' },
    build = 'cd app && npm install',
    init = function()
      vim.g.mkdp_filetypes = { 'markdown' }
    end,
    ft = { 'markdown' },
  },
```

Place it as a sibling entry next to the existing VimTeX plugin so the file remains a single small custom plugin list.

- [ ] **Run formatting verification** *(blocked: `stylua` not installed in this environment)*

Run: `stylua init.lua lua/`
Expected: command exits successfully with no errors.

- [x] **Run headless Neovim validation**

Run: `nvim --headless "+qa"`
Expected: command exits successfully.

- [ ] **Commit checkpoint**

```bash
git add lua/custom/plugins/init.lua docs/plans/2026-04-06-markdown-preview-plugin.md
git commit -m "feat: add markdown preview plugin"
```

**Resume note:** After a context reset, re-read this plan plus `AGENTS.md` and `lua/custom/plugins/init.lua`, check whether the markdown preview spec is already present, then continue from the first unchecked item in Step 1.
