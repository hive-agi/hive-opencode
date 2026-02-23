# hive-opencode

Terminal bridge for [OpenCode](https://github.com/opencode-ai/opencode) in the [hive](https://github.com/hive-agi) ecosystem. Spawns and manages OpenCode sessions inside Emacs vterm buffers (or any terminal host) with hive-mcp wired in as an MCP server.

## What it does

- **Bridge** — Spawn OpenCode processes in vterm buffers, manage lifecycle (spawn/kill/send/status)
- **Config** — Generate per-session `.opencode.json` with hive-mcp and custom MCP servers wired in
- **Tools** — Emacs-native tools exposed to OpenCode (buffer inspection, elisp eval, window layout, project files, git status)
- **Swarm integration** — API entry point compatible with hive-mcp swarm spawn conventions

## Architecture

Written in [ClojureElisp (cljel)](https://github.com/lages/clojure-elisp) — Clojure syntax compiled to Emacs Lisp.

```
src/cljel/opencode_emacs/
  bridge.cljel  — Core spawn/kill/send/status + swarm API
  config.cljel  — .opencode.json generation with hive-mcp wiring
  tools.cljel   — Buffer, eval, window, project, git tools
```

Compiled output lands in `out/`.

## Build

```bash
make compile    # Compile cljel -> elisp
make watch      # Watch mode
make clean      # Remove compiled output
```

Requires the `clel` CLI from [clojure-elisp](https://github.com/lages/clojure-elisp).

## Why "hive-opencode" not "opencode-emacs"?

OpenCode supports `opencode serve` + `opencode attach` which works over any terminal (tmux, kitty, etc.). The cljel files are the Emacs-specific implementation, but the project scope is broader than just Emacs.

## License

Copyright (c) 2024-2026 hive-agi contributors

EPL-2.0 OR GPL-2.0-or-later WITH Classpath-exception-2.0. See [LICENSE](LICENSE).
