# Installing Abe M/L (`abeml`) — evaluation

Prebuilt for **Linux x86-64** (glibc ≥ 2.34). You also need **`clang`** and
**`llc`** on your `PATH` to produce native binaries.

`abeml` is commercial software: a downloaded build evaluates for a limited window
and then requires a license (see **Licensing** below and the [EULA](EULA.md)).

## Option A — the bundle (recommended)

The bundle ships the compiler and the full runtime together; `abeml` finds the
runtime automatically.

```bash
VER=1.0.0
curl -fsSL -O https://github.com/E-Tools-AI-Corporation/abeml/releases/latest/download/abeml-$VER-linux-x86_64.tar.gz
curl -fsSL -O https://github.com/E-Tools-AI-Corporation/abeml/releases/latest/download/SHA256SUMS
sha256sum -c SHA256SUMS 2>/dev/null | grep abeml-$VER   # verify

tar xzf abeml-$VER-linux-x86_64.tar.gz
cd abeml-$VER
./bin/abeml --version
echo 'function main(): i64 { console.log("Hello from Abe M/L"); return 0; }' > hello.abe
./bin/abeml hello.abe -o hello && ./hello
```

Layout:

```
abeml-1.0.0/
  bin/abeml                 the compiler (Level 1 + 2 / ML)
  bin/abepel                the PeL compiler
  runtime/                  the full Abe runtime (found automatically as ../runtime)
  Abeml-Compiler-EULA.pdf   the governing license
  README.txt
```

To run from anywhere, add `bin/` to your `PATH`, or set
`ABE_RUNTIME_DIR=<this dir>/runtime`.

## Option B — the bare compiler

```bash
curl -fsSL -o abeml https://github.com/E-Tools-AI-Corporation/abeml/releases/latest/download/abeml-linux-x86_64
chmod +x abeml
```

## System libraries

Programs that use the runtime's networked/persistent modules also need the
matching system libraries installed:

| Abe feature   | needs                       |
|---------------|-----------------------------|
| http / net    | `libcurl`                   |
| database      | `libpq` (PostgreSQL client) |
| cache         | `hiredis`                   |
| crypto / auth | `libssl`, `libargon2`       |
| GPU (optional)| CUDA runtime (`libcudart`, `libcublas`) |

On Debian/Ubuntu:

```bash
sudo apt-get install -y clang llvm libcurl4 libpq5 libhiredis0.14 libssl3 libargon2-1
```

## Licensing

Unlicensed, `abeml` compiles during the evaluation window and prints an
`UNLICENSED EVALUATION` banner; after the window it requires a license. Install
your license token any one of these ways (precedence in this order):

```bash
export ABEML_LICENSE="ABE1.…"          # best for CI / containers
export ABE_LICENSE_FILE=/path/to/license
printf '%s\n' 'ABE1.…' > ~/.abe/license
```

`abeml --version` always works without a license. To purchase a license or
request an extended evaluation, contact **licensing@e-tools.ai**. Terms: the
[Abe M/L Compiler EULA](EULA.md) and [Licensing FAQ](LICENSING-FAQ.md).

## Only need Level 1?

If you don't need machine learning, the **free** [`abepro`](https://github.com/E-Tools-AI-Corporation/abepro)
edition compiles Level 1 with no license.
