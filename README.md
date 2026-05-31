# kdo — Workspace Manager for AI Agents

**kdo** is a Rust-based polyglot workspace manager built for AI coding agents. It compiles your monorepo into an agent-readable representation, serves it over MCP, enforces token budgets, and prevents context loops — so your agent stops wasting tokens and starts solving problems.

---

## Requirements

- **Rust** 1.75 or higher
- **Cargo** (comes with Rust)

Install Rust from [https://rustup.rs](https://rustup.rs)

---

## Installation

### From crates.io

```bash
cargo install kdo --version "0.2.0-alpha.1"
```

### From source

```bash
git clone https://github.com/shubhamxcode/Kdo.git
cd Kdo
cargo install --path crates/kdo-cli
```

### Using the install script

```bash
curl -fsSL https://shubhamxcode.github.io/kdo/install.sh | bash
```

---

## Quick Start

```bash
# Step 1 — go to your project/monorepo
cd your-project

# Step 2 — initialize kdo
kdo init

# Step 3 — check everything is healthy
kdo doctor

# Step 4 — see all discovered projects
kdo list

# Step 5 — wire into your AI agent (Claude Code)
kdo setup claude
```

---

## Running & Building Locally

```bash
# Build the project
cargo build

# Run in dev mode
cargo run -- --help

# Run a specific command
cargo run -- list
cargo run -- graph
cargo run -- doctor

# Run with the sample fixture
cd fixtures/sample-monorepo
../../target/debug/kdo list
../../target/debug/kdo graph
../../target/debug/kdo doctor
```

---

## All Commands

| Command | Description |
|---|---|
| `kdo init` | Initialize workspace — scaffolds template or adopts existing repo |
| `kdo new <name>` | Create a new project interactively |
| `kdo list` | List all projects in the workspace |
| `kdo graph` | Show the dependency graph |
| `kdo context <project>` | Generate token-budgeted context bundle |
| `kdo run <task>` | Run a task across all projects |
| `kdo exec <cmd>` | Run a shell command in each project directory |
| `kdo affected` | List projects changed since a git ref |
| `kdo doctor` | Validate workspace health |
| `kdo serve` | Start the MCP server |
| `kdo setup <agent>` | Wire kdo into Claude Code or OpenClaw |
| `kdo similar <project>` | Find structurally similar projects |
| `kdo source <symbol>` | Look up a symbol definition across the workspace |
| `kdo bench` | Benchmark token usage: filesystem vs kdo MCP |
| `kdo upgrade` | Upgrade kdo to the latest release |
| `kdo completions <shell>` | Generate shell completions |

---

## MCP Server (for AI Agents)

Start the MCP server so your agent can use workspace tools:

```bash
kdo serve --transport stdio
```

With an agent profile:

```bash
kdo serve --agent claude
kdo serve --agent openclaw
```

Available MCP tools agents get access to:

| Tool | What it does |
|---|---|
| `kdo_list_projects` | Lists all projects with name, language, deps |
| `kdo_get_context` | Token-budgeted context bundle for a project |
| `kdo_read_symbol` | Read a specific function/struct/class body |
| `kdo_dep_graph` | Dependency graph for a project |
| `kdo_affected` | Projects changed since a git ref |
| `kdo_search_code` | Search a pattern across all source files |

---

## Development

```bash
# Full CI — format check + lint + tests + docs
make ci

# Demo on the sample monorepo fixture
make fixture

# Build and install to /usr/local/bin
make install

# Run tests only
cargo test

# Run linter
cargo clippy --all-targets -- -D warnings

# Format code
cargo fmt --all
```

---

## Project Structure

```
kdo/
├── crates/
│   ├── kdo-core       # Types, errors, token estimator
│   ├── kdo-resolver   # Manifest parsers (Cargo, Node, Python, Anchor)
│   ├── kdo-graph      # Workspace dependency graph
│   ├── kdo-context    # Tree-sitter extraction, context generation
│   ├── kdo-mcp        # MCP server
│   └── kdo-cli        # CLI entry point
├── fixtures/
│   └── sample-monorepo  # Test fixture (Anchor + TS + Python)
└── web/
    └── site             # Landing page
```

---

## Supported Languages

| Language | Manifest |
|---|---|
| Rust | `Cargo.toml` |
| TypeScript / JavaScript | `package.json` |
| Python | `pyproject.toml` |
| Solana Anchor | `Anchor.toml` |

---

## GitHub

[https://github.com/shubhamxcode/Kdo](https://github.com/shubhamxcode/Kdo)
