# Abe Pro — `abepro`

**`abepro`** is the **free edition** of the compiler for the
[Abe](https://e-tools.ai) programming language (`.abe`) — a typed, memory-safe
systems language with built-in concurrency (ARC + cycle collector, actors,
structured concurrency), compiled through LLVM to native code.

`abepro` compiles **Level 1** of Abe — the general-purpose application language.
It **parses the entire language**, but Level 2 (the machine-learning layer —
tensors, `layer`/`model`, `train`/`infer`, GPU) is serviced only by the
commercial **`abeml`** edition (Abe-LLM). Feed `abepro` a Level-2 program and it
reports a clean diagnostic pointing you at `abeml`.

This repository distributes **prebuilt binaries and documentation** — the
compiler source is not published here. The free Abe **runtime** is a separately
licensed, freely-redistributable library (ARRL) and is published with the
[releases](https://github.com/E-Tools-AI-Corporation/abepro/releases/latest).

> **Status:** `0.2.0` · **platform: Linux x86-64** (glibc ≥ 2.34). macOS,
> Windows, and ARM builds are not published yet.

## What you get

- **`abepro`** — the Abe compiler, free edition (Level 1 → native).
- **`abepel`** — the [PeL](https://e-tools.ai) ("Plain English Language")
  compiler: PeL → Abe → native.
- **the free Abe runtime** — the Level-1 module set (core, strings, collections,
  regex, templates, dialog, async, crypto, db, cache, http/net, prompt, metrics),
  redistributable under the [Abe Runtime Redistribution License](ABE-RUNTIME-REDISTRIBUTION-LICENSE.md).

## Quick start

```bash
# Download the latest Linux x86-64 build
curl -fsSL -o abepro \
  https://github.com/E-Tools-AI-Corporation/abepro/releases/latest/download/abepro-linux-x86_64
chmod +x abepro
./abepro --version

# Type-check and compile Abe source
printf 'function main(): i64 { console.log("Hello from Abe Pro"); return 0; }\n' > hello.abe
./abepro --check   hello.abe
./abepro           hello.abe -o hello   # needs clang + llc on PATH
./hello
```

For a self-contained bundle (compiler + the free runtime it finds automatically),
download `abepro-0.2.0-linux-x86_64.tar.gz` from the
[latest release](https://github.com/E-Tools-AI-Corporation/abepro/releases/latest);
the free runtime is also published standalone as
`abe-runtime-0.2.0-linux-x86_64.tar.gz`. See **[INSTALL.md](INSTALL.md)**, and
verify downloads against `SHA256SUMS`.

## Hello, Abe

```abe
function main(): i64 {
    console.log("Hello from Abe Pro");
    return 0;
}
```

## Documentation

- **[Abe Pro Programming Manual](pdf/ABE-Pro-Programming-Manual-1.0.0.pdf)** — the
  language reference. (Level-2 / ML chapters describe features serviced by the
  `abeml` edition.)
- **[Abe Pro User Manual](pdf/ABE-Pro-User-Manual-1.0.0.pdf)** — using the compiler.

## Level 2 / ML — the `abeml` edition

Abe's machine-learning layer (native tensors, neural `layer`/`model`, transformer
blocks, KV-cache inference + `generate`, tokenization, `train` with autograd,
quantization, and an optional CUDA backend) is part of the commercial **`abeml`**
(Abe-LLM) edition, together with the full runtime. `abepro` accepts the syntax so
your code type-checks, but emits Level-2 code only under `abeml`.

Licensing & the ML edition: **licensing@e-tools.ai**

## License

This repository distributes prebuilt binaries and documentation — **no source
code**.

- **This repository** (docs, manuals) and the distributed **binaries** (`abepro`,
  `abepel`) — the [Abe Pro Distribution & Documentation License](LICENSE): free to
  use (incl. commercially), verbatim redistribution permitted; not open source.
- **The Abe runtime** — [Abe Runtime Redistribution License](ABE-RUNTIME-REDISTRIBUTION-LICENSE.md) (royalty-free redistribution).
- **Trademarks** — *Abe*, *Abe Pro*, *Abe PeL*, *Abe Vibe*, and *Abe-LLM* are
  trademarks of E-Tools AI Corporation; see [TRADEMARK.md](TRADEMARK.md). The
  license covers copyright/use only, not trademark rights.
