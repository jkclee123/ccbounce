# ccbounce

Restart Claude Code in a different directory without losing your foreground terminal session.

## Setup

Both `cctg` and `ccbounce` should be in your `PATH` (e.g. `~/bin`).

## Usage

Start Claude with the wrapper instead of running `claude` directly:

```bash
cctg
```

To bounce Claude to a different directory (run from within Claude):

```bash
ccbounce /path/to/project
```

Claude will exit and automatically restart in the target directory, still attached to your terminal.

To exit normally, just quit Claude as usual (`/exit` or Ctrl+C). The wrapper exits cleanly.

## How it works

- `cctg` runs Claude in a loop. After Claude exits, it checks for a bounce file (`/tmp/ccbounce_target`). If found, it restarts Claude in the specified directory. Otherwise it exits.
- `ccbounce` writes the target directory to the bounce file and kills the current Claude process.
