# Codex host

The `attribution` skill and hook are host-agnostic. Claude Code loads them as a
plugin (see repo root). Codex consumes the same two pieces a little differently,
because Codex hooks live in a global `~/.codex/hooks.json` rather than inside the
plugin.

## What Codex needs

1. **Skill** — make the skill discoverable to Codex. Either drop it under a Codex
   plugin you already sync, or copy it directly:

   ```bash
   mkdir -p ~/.codex/plugins/attribution/skills/attribution ~/.codex/plugins/attribution/.codex-plugin
   cp plugins/attribution/skills/attribution/SKILL.md \
      ~/.codex/plugins/attribution/skills/attribution/SKILL.md
   # minimal Codex plugin manifest
   cat > ~/.codex/plugins/attribution/.codex-plugin/plugin.json <<'JSON'
   { "name": "attribution", "version": "0.1.0",
     "description": "Disclose auto-used skills / MCP tools / hooks as a footer line." }
   JSON
   ```

2. **Hook** — the same `reminder.py`, wired into Codex's global hooks:

   ```bash
   cp plugins/attribution/hooks/reminder.py ~/.codex/hooks/attribution_reminder.py
   ```

   Then merge the `UserPromptSubmit` entry from
   [`hooks.fragment.json`](./hooks.fragment.json) into `~/.codex/hooks.json`.

3. Restart Codex. Approve the global hook trust prompt on first run.

## Notes

- `reminder.py` is identical to the Claude hook script — it only reads env config
  and prints a reminder to stdout, which Codex adds to the prompt context.
- Configuration env vars (`AGENT_ATTRIBUTION_LABEL`, `AGENT_ATTRIBUTION_LOCALE`,
  `AGENT_ATTRIBUTION_DISABLE`) work the same on both hosts.
- Codex hooks reference an absolute path (`$HOME/.codex/hooks/...`) instead of
  Claude's `${CLAUDE_PLUGIN_ROOT}`, since the hook lives outside the plugin dir.
