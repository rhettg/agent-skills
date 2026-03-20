# agent-skills

Small shell tool for managing pinned agent skills from GitHub and syncing them into common local skill directories.

## Files

- `bin/agent-skills`: main command
- `.agent-skills`: sample manifest

## Manifest

The default manifest path is `~/.agent-skills`.

Format:

```text
github.com/OWNER/REPO//PATH@REV
```

Examples:

```text
github.com/openai/skills//skills/.curated/doc@dc48aff8208131776c9937326002bd60cf572ab6
github.com/TheGreatGildo/nerv-ui@c2c890b023e7d7b6d9498b67b82ffb3a3c92340f
```

## Commands

```bash
agent-skills add https://github.com/openai/skills/tree/main/skills/.curated/doc
agent-skills add --no-sync https://github.com/TheGreatGildo/nerv-ui
agent-skills sync
agent-skills status
```

`add` snapshots the current commit and writes a pinned entry to the manifest. By default it also syncs the skill immediately.

## Install

One simple setup:

```bash
mkdir -p ~/.local/bin
ln -sf "$PWD/bin/agent-skills" ~/.local/bin/agent-skills
chmod +x "$PWD/bin/agent-skills"
ln -sf "$PWD/.agent-skills" ~/.agent-skills
```

Make sure `~/.local/bin` is on your `PATH`.

## Targets

`sync` installs symlinks into:

- `~/.agent/skills`
- `~/.agents/skills`
- `~/.codex/skills`
- `~/.claude/skills`
- `~/.copilot/skills`

Removing a line from `~/.agent-skills` and rerunning `agent-skills sync` removes only symlinks managed by this tool.
