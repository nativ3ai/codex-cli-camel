## Installing & building (codex-cli-camel)

This page is for the **fork** at `nativ3ai/codex-cli-camel`.

### One-line npm install (global)

```bash
npm install -g codex-camel
codex --version
codex-camel --version
```

If your system already has another `codex` binary earlier in `PATH`, use `codex-camel` directly.

### System requirements

| Requirement                 | Details                                                          |
| --------------------------- | ---------------------------------------------------------------- |
| Operating systems           | macOS 12+, Ubuntu 20.04+/Debian 10+, or Windows 11 via WSL2     |
| Git (optional, recommended) | 2.23+                                                            |
| RAM                         | 4 GB minimum (8 GB recommended)                                  |

### Build from source

```bash
git clone https://github.com/nativ3ai/codex-cli-camel.git
cd codex-cli-camel/codex-rs

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
source "$HOME/.cargo/env"
rustup component add rustfmt clippy

cargo build -p codex-cli
cargo run -p codex-cli -- --help
```

### Optional install as local `codex` binary

```bash
cd codex-rs
cargo install --path cli --force
codex --help
```

### CaMeL quickstart

```bash
codex camel monitor --threshold 6
codex camel status
codex camel compare
```

### Tracing / verbose logging

```bash
tail -F ~/.codex/log/codex-tui.log
```

For custom log filters:

```bash
RUST_LOG=codex_core=debug,codex_tui=info codex
```
