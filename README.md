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
ccbounce <target_user> /path/to/project
```

Claude will exit and automatically restart in the target directory, still attached to your terminal.

To exit normally, just quit Claude as usual (`/exit` or Ctrl+C). The wrapper exits cleanly.

## Multi-user

`cctg` and `ccbounce` can be run by different users. Each user gets their own bounce file (`/tmp/ccbounce_target_<user>`), so instances don't interfere.

To bounce another user's Claude session:

```bash
ccbounce alice /path/to/project
```

## How it works

- `cctg` runs Claude in a loop. After Claude exits, it checks for a per-user bounce file (`/tmp/ccbounce_target_$USER`). If found, it restarts Claude in the specified directory. Otherwise it exits.
- `ccbounce` writes the target directory to the target user's bounce file and kills their Claude process (scoped to that user via `pkill -u`).
