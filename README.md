# Sublime Text config

`Packages/User` for Sublime Text 4 — set up to work as close to my
[Emacs config](https://github.com/christerso/emacs-config) as Sublime allows. Languages: Go, C, C++,
x86-64 assembly (NASM + GAS), Zig, Odin (ols), plus syntax highlighting for
Protocol Buffers, Cap'n Proto and CMake (Rust/Go/TOML/YAML ship built-in
with ST4).

## Restore on a new machine

1. Install Sublime Text 4 and [Package Control](https://packagecontrol.io/installation).
2. Clone this repo as `Packages/User`, at the OS-specific path:
   - Linux:   `~/.config/sublime-text/Packages/User`
   - macOS:   `~/Library/Application Support/Sublime Text/Packages/User`
   - Windows: `%APPDATA%\Sublime Text\Packages\User`
3. Start Sublime — Package Control installs everything in
   `Package Control.sublime-settings` automatically.

Language servers come from the system, not from Sublime, and are referenced by
bare command name so each OS just needs the binary on PATH:
`gopls` (`go install`), `clangd`, `asm-lsp`, `zls` (version-matched to zig),
`ols` (Odin LSP). Global server configs shared with Emacs/Neovim:
`~/.config/clangd/config.yaml`, `~/.config/asm-lsp/.asm-lsp.toml`.

### macOS notes

- Keys: the `Default (OSX)` map is **identical to Windows** — same literal
  `Ctrl` keys and `Ctrl+Space` leader. Two OS keys must be freed first:
  disable **System Settings › Keyboard › Keyboard Shortcuts › Input Sources ›
  "Select the previous input source"** (it steals `Ctrl+Space`); goto-definition
  on click is **`Cmd+Click`** (Ctrl+Click is the mac right-click).
- Tools via Homebrew: `brew install zig nasm asm-lsp zls ols` and
  `brew install --cask font-jetbrains-mono-nerd-font`. `gopls`/`clangd`/`cmake`
  as usual (`clangd` ships with the Xcode command-line tools).
- `odin` (built at `~/repos/Odin`) is symlinked into `~/.local/bin` so it is on
  PATH; `odin root` still resolves through the symlink.
- **Launch Sublime from a shell (`subl .`)** so it inherits your PATH — macOS
  GUI (Dock/Finder) launches get a minimal PATH that omits `/opt/homebrew/bin`
  and `~/go/bin`, so LSP servers and build systems won't be found otherwise.
- NASM builds emit x86-64 Mach-O and run under **Rosetta 2** on Apple Silicon
  (`softwareupdate --install-rosetta`); asm-lsp hover/completion needs no build.

## Keys (Emacs muscle memory)

`Ctrl+C` is the Emacs prefix — **plain Ctrl+C no longer copies**; use
`Ctrl+Shift+C` or `Ctrl+Insert`.

| Key | Does |
|-----|------|
| `Ctrl+C F F` | fuzzy find file (Goto Anything) |
| `Ctrl+C F G` | grep across the project |
| `Ctrl+C F S` | fuzzy LSP symbol, whole project |
| `Ctrl+C F J` / `F L` | fuzzy symbol / line in file |
| `Ctrl+C C` / `Ctrl+C Ctrl+C` | build (pick variant) / repeat last build |
| `Ctrl+C R` | build variant "Run" (Go: `go run .`, NASM: assemble+link+run, C: compile+run file) |
| `Ctrl+C T T` / `T P` | go test package / project |
| `Ctrl+C O` | switch source/header (clangd) |
| `Ctrl+C A` | LSP code actions |
| `Ctrl+C G N` / `G P` | next / prev git hunk |
| `Ctrl+.` / `Ctrl+,` / `Alt+,` | goto definition / references / jump back |
| `Ctrl+Alt+L` | LSP format document |

## Color schemes

Default is **Voidlight** (`Voidlight.sublime-color-scheme`) — the same
near-black + pearl palette as my Emacs/Neovim themes. Calm dark alternatives
installed: Catppuccin, Nord, ayu, Gruvbox Material. Switch via
`Ctrl+Shift+P → UI: Select Color Scheme`.
