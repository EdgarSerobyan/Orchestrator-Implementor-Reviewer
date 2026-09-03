# Codex Orchestrator–Implementor–Reviewer setup

This repository contains Codex workflow guidance and a bounded implementor
configuration. `AGENTS.md` is the canonical workflow text, and
`implementor.toml` configures the implementation agent.

## Install

For a global installation, copy the files to your Codex home directory:

```text
AGENTS.md       -> $CODEX_HOME/AGENTS.md
implementor.toml -> $CODEX_HOME/agents/implementor.toml
```

If `CODEX_HOME` is not set, Codex normally uses `$HOME/.codex`, so the usual
destinations are:

```text
$HOME/.codex/AGENTS.md
$HOME/.codex/agents/implementor.toml
```

Create the `agents` directory if it does not already exist. Restart Codex after
copying the files so it discovers the custom implementor agent.

To enable the workflow for only one repository, place `AGENTS.md` in that
repository's root instead of in `CODEX_HOME`. The implementor configuration
still belongs at `$CODEX_HOME/agents/implementor.toml` because custom agent
definitions are stored in the Codex home directory.

If you use an AI coding agent, you do not need to copy the files manually. You
can simply ask it:

> Install the Orchestrator–Implementor–Reviewer architecture from this
> repository. Put `AGENTS.md` in my Codex home for a global installation (or
> in my repository root for a project-only installation), and put
> `implementor.toml` in the `agents` directory under my Codex home. Preserve
> any existing files and ask before replacing them.

The agent should verify the destination paths, create missing directories, and
avoid overwriting existing guidance or agent definitions without permission.

## License

MIT. See [LICENSE](LICENSE).
