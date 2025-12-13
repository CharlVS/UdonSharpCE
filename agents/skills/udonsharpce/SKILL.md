---
name: udonsharpce
description: Repo-wide expert guidance for working in the UdonSharpCE codebase (Unity/VRChat/UdonSharp). Use this for general project context, conventions, and choosing the right specialized CE skill.
license: MIT
metadata:
  repo: UdonSharpCE
---

UdonSharpCE is a custom fork of UdonSharp maintained by us. As the developers, we can make changes to the compiler and tooling as needed.

## Priorities

- **Developer Experience (DevEx)**: Prioritize clean, intuitive APIs and helpful error messages
- **C# Parity**: Provide a simple, abstracted experience that stays close to standard C# conventions and patterns
- **Maintainability**: We own this fork—prefer proper fixes over workarounds

## Key Abstraction: Pure C# Development

UdonSharpCE provides a **pure C# development experience**. Developers should not have to interact with:
- Udon programs or UdonProgram assets
- UASM (Udon Assembly)
- UdonBehaviour components (hidden by CE inspector)
- Low-level VRChat networking primitives

The compiler and editor scripts handle all Udon translation automatically:
- **On script change** → Compiler regenerates Udon programs
- **On add component** → Editor creates hidden UdonBehaviour
- **On build** → Final programs bundled for VRChat

Only the `ce-compiler` skill should modify Udon internals. Runtime/editor/docs/tests should stay at the pure C# abstraction layer.

## Skill Selection Guide

- Runtime libraries (Collections/ECS/Async/Net/etc.) → `ce-runtime`
- Editor tools, inspectors, analyzers → `ce-editor`
- Compiler pipeline, Roslyn transforms, UASM output, optimizations → `ce-compiler`
- Documentation and technical guides → `ce-docs`
- Unit/integration tests (Unity Test Framework) → `ce-test`

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

## Boundaries

- ✅ **Always:** Preserve the pure C# abstraction, prioritize DevEx, keep changes maintainable
- ⚠️ **Ask first:** Large refactors, new public APIs/modules, changes that affect many packages
- 🚫 **Never:** Leak Udon internals into user-facing docs/APIs unless explicitly requested

