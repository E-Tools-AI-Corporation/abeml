# Abe M/L — `abeml`

**`abeml`** (Abe‑LLM) is the **commercial full edition** of the compiler for the
[Abe](https://e-tools.ai) programming language (`.abe`). It compiles the **entire**
language — **Level 1** (general‑purpose application programming) **and Level 2
(machine learning)** — through LLVM to a single self‑contained native binary.

Level 2 is a complete, native ML toolchain with **no Python and no framework**:
tensors, neural `layer`s and `model`s, transformer blocks (attention, RoPE,
RMSNorm, SwiGLU, grouped‑query attention), autoregressive inference (KV‑cache,
sampling, `generate`), tokenization, safetensors/GGUF loading, training (`train`,
optimizers, autograd, LoRA), quantization (Q8_0/Q4_0), mixed precision (bf16/f16),
and an optional CUDA GPU backend. Your model **and** its serving compile into one
binary.

This repository distributes **documentation and a license‑gated build** — the
compiler source is not published here.

> **Commercial product.** `abeml` is a commercial product of **E‑Tools AI
> Corporation**. A downloaded build runs in a time‑limited **evaluation** mode and
> then requires a valid license for continued/production use. See
> [LICENSE](LICENSE) and the [EULA](EULA.md).

> **Status:** `1.0.0` · **platform: Linux x86-64** (glibc ≥ 2.34).

## Free vs. commercial

| | Compiler | Level 1 | Level 2 (ML) | License |
|---|---|---|---|---|
| **Free** | [`abepro`](https://github.com/E-Tools-AI-Corporation/abepro) | ✅ | ✕ (parses, rejects codegen) | free |
| **Commercial** | **`abeml`** | ✅ | ✅ | paid (evaluation available) |

If you only need Level 1 (general application programming), use the **free
[`abepro`](https://github.com/E-Tools-AI-Corporation/abepro)** edition. `abeml`
adds Level 2 (machine learning) and the full runtime.

## Evaluation quick start

Download the **bundle** — it contains the compiler *and* the full runtime it
links, so native compilation works out of the box:

```bash
# Download + unpack the evaluation bundle (compiler + full runtime)
curl -fsSL -O https://github.com/E-Tools-AI-Corporation/abeml/releases/latest/download/abeml-1.0.0-linux-x86_64.tar.gz
tar xzf abeml-1.0.0-linux-x86_64.tar.gz
cd abeml-1.0.0
./bin/abeml --version

printf 'function main(): i64 { console.log("Hello from Abe M/L"); return 0; }\n' > hello.abe
./bin/abeml hello.abe -o hello   # needs clang + llc on PATH; runtime auto-found in ./runtime
./hello
```

> **Note:** the standalone **bare** binary (`abeml-linux-x86_64`) has no runtime
> beside it, so native `-o` compilation needs the runtime — use the bundle, or
> set `ABE_RUNTIME_DIR=<path>/runtime`.

Unlicensed, `abeml` compiles during the evaluation window and prints an
`UNLICENSED EVALUATION` banner; after the window it requires a license. See
**[INSTALL.md](INSTALL.md)** for the self‑contained bundle (compiler + full
runtime) and license installation. Verify downloads against `SHA256SUMS`.

## Licensing

Use beyond evaluation requires a license. Install your license token any one way:

```bash
export ABEML_LICENSE="ABE1.…"        # best for CI / containers
# or:  export ABE_LICENSE_FILE=/path/to/license
# or:  write the token to ~/.abe/license
```

Licensing terms are the [Abe M/L Compiler EULA](EULA.md)
([PDF](Abeml-Compiler-EULA.pdf)); common questions are answered in the
[Licensing FAQ](LICENSING-FAQ.md) ([PDF](Abeml-Licensing-FAQ.pdf)). To purchase a
license or request an extended evaluation: **licensing@e-tools.ai**.

The **Abe runtime** that your programs link is licensed as follows: the free
Level‑1 runtime (shipped with `abepro`) is redistributable under the Abe Runtime
Redistribution License (ARRL); the **full runtime** (Level 1 + 2 / ML) that ships
with `abeml` is commercial and governed by the EULA.

## License & trademarks

- **This repository and the `abeml` build** — proprietary; see [LICENSE](LICENSE)
  and the [EULA](EULA.md). Not open source.
- **Trademarks** — *Abe*, *Abe Pro*, *Abe PeL*, *Abe Vibe*, and *Abe‑LLM* are
  trademarks of E‑Tools AI Corporation; see [TRADEMARK.md](TRADEMARK.md).
