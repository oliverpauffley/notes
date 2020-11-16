# Tmux
A terminal mutliplexer. Useful for running multiple terminal windows at the same time.

Prefix: `ctrl + b`

## Sessions
- New session `tmux new -s <name>`
- Detach `d`
- Attach `tmux attach -t <name>`
- Switch `tmux switch -t <name>` or `s`

## Windows (tabs)
- New `c`
- Move `0-9`
- Rename `,`

## Panes
- Split horizontal: `"`
- Split vertical: `%`
- Drop pane: `ctrl + d`
- Move: with arrow keys or ghjk.
- Zoom/unzoom: `z`

## Scrolling
- Start scroll mode `[` then you can use normal vim bindings to move around.