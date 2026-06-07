# Jupyter Notebook — Basics & Shortcuts

This document collects beginner-friendly Jupyter Notebook basics and the most useful keyboard shortcuts for Classic Notebook, JupyterLab, and VS Code notebooks.

## Quick Start

- Start server: `jupyter notebook` or `jupyter lab` in your project folder.
- Open or create a notebook (`.ipynb`) file.
- Two modes: **Command mode** (blue border) and **Edit mode** (green border).
  - Command mode: keyboard shortcuts for whole-notebook actions.
  - Edit mode: typing and editing cell content.

## Cell Types

- Code cell: runs Python code and shows outputs.
- Markdown cell: write formatted text, lists, headers, math (LaTeX), images.
- Raw cell: output not processed by the notebook.

## Running Cells

- Run current cell and move to next: `Shift + Enter`
- Run current cell and stay: `Ctrl + Enter` (Cmd on mac)
- Run current cell and insert new below: `Alt + Enter`

## Create / Delete / Move Cells

- Insert cell below: `B` (Command mode)
- Insert cell above: `A` (Command mode)
- Delete cell: `D, D` (press `D` twice in Command mode)
- Merge selected cells: `Shift + M`
- Split cell at cursor: `Ctrl + Shift + -`
- Move cell up/down: `K`/`J` or use arrow + `Shift` depending on environment

## Change Cell Type

- Convert to Code: `Y` (Command mode)
- Convert to Markdown: `M` (Command mode)
- Convert to Raw: `R` (Command mode)

## Saving / Checkpoint / Kernel

- Save notebook: `Ctrl + S` (Cmd + S on mac)
- Restart kernel: Kernel menu → `Restart` (or in Command Palette)
- Interrupt kernel: `I, I` (press `I` twice in Command mode) or use the stop button
- Clear outputs: `Cell → All Output → Clear` or `Edit` menu options

## Useful Shortcuts (Classic Notebook / JupyterLab)

Command mode (press `Esc` to enter):
- `A` — Insert cell above
- `B` — Insert cell below
- `C` — Copy cell
- `V` — Paste cell below
- `X` — Cut cell
- `D, D` — Delete cell
- `Z` — Undo cell deletion
- `M` — Change to Markdown
- `Y` — Change to Code
- `1..6` — Set markdown header level (in Markdown mode after `M`)
- `Shift + Enter` — Run cell, select below
- `Ctrl + Enter` — Run cell, stay
- `Alt + Enter` — Run cell, insert below

Edit mode (press `Enter` on a cell to edit):
- `Ctrl + /` — Toggle comment on selection
- `Tab` — Indent or trigger completion
- `Shift + Tab` — Tooltip / parameter help (press multiple times for more info)
- `Ctrl + ]` / `Ctrl + [` — Indent/outdent selection

## VS Code Notebook Shortcuts (useful inside VS Code)

- Run cell: `Shift + Enter`
- Run cell and advance: `Shift + Enter` (same behavior)
- Run all cells: Command Palette → `Notebook: Run All Cells`
- Add code cell: `+ Code` button or `Insert Cell Below` from the toolbar
- Toggle output: Right-click cell → `Collapse Outputs`
- Restart kernel: Command Palette → `Python: Restart Kernel`

## Markdown Tips

- Headers: `# H1`, `## H2`, `### H3`
- Bold / italic: `**bold**`, `*italic*`
- Code: inline: `` `code` ``, block: triple backticks ```
- Math (LaTeX): inline `$x^2$`, block `$$E=mc^2$$`
- Images: `![alt](path/to/image.png)` — use workspace-relative paths

## Magic Commands (IPython)

- `%time` — time a single statement
- `%timeit` — run timing multiple times
- `%matplotlib inline` or `%matplotlib notebook` — control plotting inline behavior
- `%run script.py` — run an external script
- `%load filename` — load code into the cell
- `%pwd`, `%ls`, `%cd` — filesystem shortcuts
- `%%bash` or `%%bash -x` — run a whole cell in bash

## Common Workflows

- Restart kernel + run all: Useful after package installs or major code changes.
- Save frequently and use version control: Commit `.ipynb` carefully (consider `nbstripout` for large outputs).
- Use checkpoints: `File → Revert to Checkpoint` if needed.

## Tips for Reproducible Notebooks

- Keep long-running data downloads in separate scripts.
- Avoid storing large outputs or datasets inside the notebook JSON.
- Use `requirements.txt` or `environment.yml` to pin dependencies.
- Consider converting notebooks to scripts (`jupyter nbconvert --to script`) for production code.

## Troubleshooting

- If the browser token page doesn't load, check port forwarding and server logs.
- If kernel is disconnected, restart kernel and re-run cells from top.
- To remove output noise before committing, clear all outputs (`Cell → All Output → Clear`) and save.

## Quick Cheat Sheet (Most-used)

- Run cell: `Shift + Enter`
- New cell below: `B`
- New cell above: `A`
- Delete cell: `D, D`
- Save: `Ctrl + S`
- Toggle cell to Markdown: `M`
- Toggle cell to Code: `Y`
- Restart kernel: Kernel → Restart


---

Update: file created in `machine_learning/basics/jupyter_note_basic.md`. Feel free to ask to add VS Code-specific keymaps or a printable one-page cheatsheet.