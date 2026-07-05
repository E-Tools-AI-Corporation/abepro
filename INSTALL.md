# Installing Abe Pro (`abepro`)

Prebuilt for **Linux x86-64** (glibc ≥ 2.34). You also need **`clang`** and
**`llc`** on your `PATH` to produce native binaries (`abepro` emits LLVM IR and
hands off to them).

## Option A — the bundle (recommended)

The bundle ships the compiler and the free runtime together; `abepro` finds the
runtime automatically.

```bash
VER=1.0.0
curl -fsSL -O https://github.com/E-Tools-AI-Corporation/abepro/releases/latest/download/abepro-$VER-linux-x86_64.tar.gz
curl -fsSL -O https://github.com/E-Tools-AI-Corporation/abepro/releases/latest/download/SHA256SUMS
sha256sum -c SHA256SUMS 2>/dev/null | grep abepro-$VER   # verify

tar xzf abepro-$VER-linux-x86_64.tar.gz
cd abepro-$VER
./bin/abepro --version
echo 'function main(): i64 { console.log("Hello from Abe Pro"); return 0; }' > hello.abe
./bin/abepro hello.abe -o hello && ./hello
```

Layout:

```
abepro-1.0.0/
  bin/abepro        the compiler (free edition)
  bin/abepel        the PeL compiler
  runtime/          the free Abe runtime (found automatically as ../runtime)
  README.txt
```

To run from anywhere, add `bin/` to your `PATH`, or set
`ABE_RUNTIME_DIR=<this dir>/runtime`.

## Option B — the bare compiler + standalone runtime

```bash
VER=1.0.0
# compiler
curl -fsSL -o abepro https://github.com/E-Tools-AI-Corporation/abepro/releases/latest/download/abepro-linux-x86_64
chmod +x abepro
# free runtime
curl -fsSL -O https://github.com/E-Tools-AI-Corporation/abepro/releases/latest/download/abe-runtime-$VER-linux-x86_64.tar.gz
tar xzf abe-runtime-$VER-linux-x86_64.tar.gz     # -> runtime/
ABE_RUNTIME_DIR="$PWD/runtime" ./abepro hello.abe -o hello
```

The PeL compiler is published the same way as `abepel-linux-x86_64`.

## System libraries

Programs that use the runtime's networked/persistent modules also need the
matching system libraries installed:

| Abe feature      | needs            |
|------------------|------------------|
| http / net       | `libcurl`        |
| database         | `libpq` (PostgreSQL client) |
| cache            | `hiredis`        |
| crypto / auth    | `libssl`, `libargon2` |

On Debian/Ubuntu:

```bash
sudo apt-get install -y clang llvm libcurl4 libpq5 libhiredis0.14 libssl3 libargon2-1
```

## Level 2 / ML

`abepro` type-checks Level-2 (ML) syntax but does not compile it — that's the
commercial `abeml` (Abe-LLM) edition. Contact **licensing@e-tools.ai**.
