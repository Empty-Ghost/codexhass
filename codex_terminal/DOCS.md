# Codex Terminal

`Codex Terminal` adds a lightweight browser terminal to Home Assistant using ingress.

## Included tools

- `zsh` with `oh-my-zsh`
- `tmux`
- `npm`
- `git`
- `ripgrep`
- `codex`

## Persistence

The add-on uses Home Assistant's persistent add-on data volume:

- home directory: `/data/home`
- workspace directory: `/data/workspace`

This keeps the following between restarts:

- Codex authentication data
- npm cache
- shell history
- cloned repositories and other files saved under `/data`
- tmux sessions while the add-on stays running

## Mapped Home Assistant directories

The terminal also exposes these Home Assistant directories inside the workspace:

- `/data/workspace/homeassistant`
- `/data/workspace/share`
- `/data/workspace/addon_configs`

These mounts are writable.

## Shell experience

The add-on starts in a persistent tmux session called `workspace`.

- close the browser tab and reconnect later to resume the same tmux session
- `Ctrl-A` is the tmux prefix
- `zsh` uses an `oh-my-zsh` setup derived from the owner's dotfiles
- user-edited `~/.zshrc` and `~/.tmux.conf` are preserved after first run

## First Run

1. Start the add-on.
2. Open the terminal from the sidebar.
3. Run `codex login`.
4. Work inside `/data/workspace` if you want your files to persist.

## Updating

Home Assistant offers an update after the repository publishes a higher add-on version.
Updating replaces the container image but preserves `/data`, including authentication,
shell configuration, npm-installed tools, and workspace files.

To update Codex independently and keep that version across add-on updates, run:

```bash
npm install -g @openai/codex@latest
codex --version
```

The persistent install takes precedence over the image copy. Run
`npm uninstall -g @openai/codex` to use the version shipped with the add-on again.

## Notes

- This add-on is intentionally source-built by Home Assistant from this repository.
- Supported architectures are `amd64` and `aarch64`.
- Access is intended through Home Assistant ingress.
