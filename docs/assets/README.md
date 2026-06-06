# Assets

## demo.gif

The README hero embeds `docs/assets/demo.gif`. Until you record it, the image
link in the README shows a broken-image placeholder — that's expected.

### What to record (~5 seconds, 720px wide)

1. Open a fresh agent session (Claude Code, Codex, or Cursor) with reply-trace
   installed.
2. Ask something that triggers automation, e.g. *"search the Anthropic docs for
   prompt caching"* (forces an MCP call) or *"review my diff"* (a skill/subagent).
3. Let the reply finish so the **last line** shows the footer:
   `Auto-used — MCP: anthropicDocs/search_docs; ...`
4. Highlight / zoom the footer line for the last beat.

### Recording tips

- Record at 2x scale, then downscale to 720px wide for crispness.
- Keep it under ~2 MB so it loads fast on GitHub and Pages. Tools: `Kap`,
  `LICEcap`, `ffmpeg`/`gifski` (`ffmpeg -i in.mov -vf "fps=12,scale=720:-1" -c:v gif out.gif`
  or pipe to `gifski` for smaller files).
- A "before → after" cut (reply without vs with the footer) reads best.

Save the result here as `demo.gif`. No README change needed.
