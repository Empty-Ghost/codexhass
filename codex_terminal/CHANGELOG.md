# Changelog

## 0.2.0

- Updated the bundled OpenAI Codex CLI to stable version 0.144.5
- Switched to the pinned Home Assistant base image 3.24-2026.06.1
- Pinned shell framework and plugin sources instead of following moving branches
- Added Home Assistant image metadata for source builds
- Documented Home Assistant add-on updates and persistent in-terminal Codex updates

## 0.1.3

- Added `zsh`, `oh-my-zsh`, and `tmux`
- Started the terminal inside a persistent tmux session named `workspace`
- Added Linux-safe `zsh` and `tmux` defaults adapted from the owner's dotfiles

## 0.1.2

- Mapped Home Assistant config, share, and add-on config directories into `/data/workspace`
- Kept the add-on within Home Assistant's supported directory mapping model

## 0.1.1

- Fixed Home Assistant startup by disabling Docker init for the add-on
- Kept the Home Assistant base image init process as PID 1

## 0.1.0

- Initial release
- Added a `ttyd`-based Home Assistant terminal with persistent `/data` storage
- Added `npm`, `git`, `ripgrep`, and a pinned OpenAI Codex CLI
