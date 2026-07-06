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

```bash
# Download the latest Linux x86-64 evaluation build
curl -fsSL -o abeml \
  https://github.com/E-Tools-AI-Corporation/abeml/releases/latest/download/abeml-linux-x86_64
chmod +x abeml
./abeml --version

printf 'function main(): i64 { console.log("Hello from Abe M/L"); return 0; }\n' > hello.abe
./abeml hello.abe -o hello   # needs clang + llc on PATH
./hello
```

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
