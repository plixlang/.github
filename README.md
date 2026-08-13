# Plix

Write like a small scripting language. Run it now. Compile it when you care about speed.

Plix is gradually typed: start without annotations, add types where they pay off. The same program runs in an interpreter (`plix run`) and as a native binary (`plix build`) with the same semantics. Ownership is opt-in — use `own`, `&`, and `&mut` when you want stricter memory discipline.

```
plix run app.px          # try it in seconds
plix build app.px -o app # same code, native (Cranelift)
plix exec app.px         # compile and run
```

**v0.10.1** · files end in **`.px`** · toolchain in **Rust**.

<p>
  <a href="https://github.com/plixlang/plix"><img alt="plixlang/plix" src="https://img.shields.io/badge/repo-plixlang%2Fplix-111827?style=flat-square" /></a>
  <a href="https://github.com/plixlang/plix/releases"><img alt="releases" src="https://img.shields.io/github/v/release/plixlang/plix?style=flat-square&label=release" /></a>
  <a href="https://hub.docker.com/r/plixlang/plix"><img alt="docker" src="https://img.shields.io/badge/docker-plixlang%2Fplix-2496ED?style=flat-square&logo=docker&logoColor=white" /></a>
  <a href="https://github.com/plixlang/plix/blob/main/LICENSE"><img alt="MIT" src="https://img.shields.io/badge/license-MIT-2ea44f?style=flat-square" /></a>
</p>

## Try it

Install from [Releases](https://github.com/plixlang/plix/releases), use Docker [`plixlang/plix`](https://hub.docker.com/r/plixlang/plix), or build from source:

```sh
git clone https://github.com/plixlang/plix.git
cd plix
cargo build --release --locked
./target/release/plix --version
./target/release/plix run examples/typed.px
```

Start without annotations:

```plix
func greet(name) {
    say("Hello, ${name}!");
}

greet("Plix");
```

Add types where they pay off:

```plix
func fib(n: int) -> int {
    if (n <= 1) { return n; }
    return fib(n - 1) + fib(n - 2);
}

struct Vec2 { x: float, y: float }
impl Vec2 {
    func norm2(&self) -> float { return self.x * self.x + self.y * self.y; }
}

say("fib(20) = ${fib(20)}");
say("norm² = ${Vec2 { x: 3.0, y: 4.0 }.norm2()}");
```

## Why Plix

| You want… | Plix does… |
|---|---|
| Scripting speed of thought | Interpreter, REPL, readable errors |
| A real binary later | Cranelift native backend, same language |
| Types when useful | Gradual typing; native path specializes proven types |
| Memory discipline without a wall | `own`, `&`, `&mut` only where you ask |
| Python libraries | `import py "numpy" as np;` |
| Behavior you can test | Interpreter/native parity, fuzzing, frozen API/ABI |

Everyday language: functions, closures, arrays, objects, `struct` / `impl` / `trait`, match, modules, interpolation, slicing, errors. No data inheritance.

| Command | Role |
|---|---|
| `plix run` | Interpret |
| `plix build` / `plix exec` | Native compile |
| `plix check` | Parse, types, ownership |
| `plix test` · `fmt` · `lint` · `repl` | Everyday tooling |

Docs in the main tree: [install](https://github.com/plixlang/plix/blob/main/docs/install.md) · [grammar](https://github.com/plixlang/plix/blob/main/docs/grammar.md) · [typing](https://github.com/plixlang/plix/blob/main/docs/typing.md) · [stdlib](https://github.com/plixlang/plix/blob/main/docs/stdlib.md) · [testing](https://github.com/plixlang/plix/blob/main/docs/testing.md) · [roadmap](https://github.com/plixlang/plix/blob/main/plix_roadmap_1_0_0.md).

The language, compiler, runtime, examples, and test suite all live in **[plixlang/plix](https://github.com/plixlang/plix)**. That is the project.

## Project history

This organization and the public `plix` repository are **new**. Most of Plix was designed and implemented locally, and much of that work was never part of a public remote repository. GitHub is the published tree, not a full day-by-day chronicle of every earlier edit.

AI was used to translate documentation from Persian to English and occasionally to assist with debugging and explaining test failures. The language design, compiler, runtime, tooling, and implementation were developed by the project author.

## Follow the main repo

**[plixlang/plix](https://github.com/plixlang/plix)** is the canonical repository and the best place to follow Plix’s development toward v1.0.0.

If you find Plix interesting, consider [starring the repository](https://github.com/plixlang/plix) to follow its development.

MIT. See [`CONTRIBUTING.md`](https://github.com/plixlang/plix/blob/main/CONTRIBUTING.md) and [`SECURITY.md`](https://github.com/plixlang/plix/blob/main/SECURITY.md).
