<hr>

<p align="center"><img src="assets/yocrow-logo.svg" alt="Yocrow" width="320"></p>

# Yocrow agent skills

Agent skills that teach AI coding agents how to use [Yocrow](https://yocrow.dev),
which connects your agent to the official MCP servers of the providers you use.

| Skill | What it teaches |
| --- | --- |
| [`yocrow`](skills/yocrow/SKILL.md) | Finding, inspecting and running provider actions through the three Yocrow tools |

## Install

The Yocrow CLI offers to install these skills the first time you run it. You can
also install them at any time.

```bash
yocrow skills install
```

This copies each skill into `~/.agents/skills`, which Codex, Cursor, Gemini CLI,
GitHub Copilot, OpenCode and other agents read. It also copies them into
`~/.claude/skills` and `~/.kiro/skills` when Claude Code or Kiro is installed.

To install by hand, copy a skill folder such as `skills/yocrow` into your
agent's skills directory.

## Format

Each skill is a folder containing a `SKILL.md` file that follows the
[Agent Skills](https://agentskills.io) format, with a `name` and `description` in
its frontmatter.

## License

[MIT](LICENSE)
