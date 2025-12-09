# UdonSharpCE Custom Agents

This directory contains custom agent configurations for the UdonSharpCE project. Each agent is specialized for specific tasks within the codebase.

## Available Agents

| Agent | File | Description |
|-------|------|-------------|
| `@ce-runtime` | [ce-runtime.md](ce-runtime.md) | Develops CE runtime libraries (Collections, ECS, Async, etc.) |
| `@ce-editor` | [ce-editor.md](ce-editor.md) | Creates Unity Editor tools and Roslyn analyzers |
| `@ce-docs` | [ce-docs.md](ce-docs.md) | Writes documentation and technical guides |
| `@ce-test` | [ce-test.md](ce-test.md) | Writes unit and integration tests |
| `@ce-compiler` | [ce-compiler.md](ce-compiler.md) | Works on compiler extensions and optimizations |

## Usage

Reference an agent by name when working with GitHub Copilot or compatible AI assistants:

```
@ce-runtime help me implement a new collection type
@ce-editor create a bandwidth analyzer window
@ce-docs write documentation for the CEPool API
@ce-test write tests for the tombstone deletion fix
@ce-compiler implement a peephole optimization pass
```

## Agent Selection Guide

| Task | Agent |
|------|-------|
| Writing CE runtime libraries | `@ce-runtime` |
| Creating editor windows/tools | `@ce-editor` |
| Writing Roslyn analyzers | `@ce-editor` |
| Documentation and guides | `@ce-docs` |
| Unit and integration tests | `@ce-test` |
| Compiler optimizations | `@ce-compiler` |

## Common Commands

```bash
# Compile (Unity)
# Open Unity - files recompile on change

# Run tests (Unity)
# Window > General > Test Runner

# Validate world (Unity)
# CE Tools > World Validator

# Build documentation
cd Tools/Docusaurus && npm run build

# Preview documentation
cd Tools/Docusaurus && npm run start
```

## Key Abstraction: Pure C# Development

UdonSharpCE provides a **pure C# development experience**. Developers never interact with:
- Udon programs or UdonProgram assets
- UASM (Udon Assembly)
- UdonBehaviour components (hidden by CE inspector)
- Low-level VRChat networking primitives

The compiler and editor scripts handle all Udon translation automatically:
- **On script change** → Compiler regenerates Udon programs
- **On add component** → Editor creates hidden UdonBehaviour
- **On build** → Final programs bundled for VRChat

**Only `@ce-compiler` works with Udon internals** — all other agents write and document pure C#.

## Agent Design Principles

All agents follow these principles from [GitHub's agents.md guidelines](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/):

1. **Clear Persona** — Each agent has a specific expertise area
2. **Project Knowledge** — Tech stack and file structure context
3. **Executable Commands** — Tools that validate work
4. **Code Examples** — ✅ Good and ❌ Bad patterns
5. **Explicit Boundaries** — Always / Ask First / Never rules
6. **Abstraction-Aware** — Most agents work with C#; only `@ce-compiler` touches Udon internals
