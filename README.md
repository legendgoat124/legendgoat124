<h1 align="center">legendgoat</h1>

<p align="center">
  <em>Small libraries that do one thing exactly right.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/TypeScript-3178c6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript">
  <img src="https://img.shields.io/badge/Python-3776ab?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Node.js-5fa04e?style=flat-square&logo=node.js&logoColor=white" alt="Node.js">
  <img src="https://img.shields.io/badge/dependencies-zero-brightgreen?style=flat-square" alt="Zero dependencies">
</p>

---

I build things with no dependencies, real test suites, and documentation
that explains the *why* rather than restating the signature.

A theme runs through all of them: the interesting part of a problem is usually
the part everyone else rounds off. A rate limiter is easy until the clock jumps
backwards. A filter language is easy until you ask what it can reach. A path
tracer is easy until the light is small enough that random rays never find it.

I also try to report the measurements that did **not** flatter the design,
because those are usually the ones worth reading.

## Projects

### 🔦 [photon](https://github.com/legendgoat124/photon) · TypeScript

A physically-based path tracer. BVH acceleration with a surface-area-heuristic
split, next-event estimation, glass with Schlick-approximated Fresnel, a
thin-lens camera, multithreaded rendering, and a PNG encoder written from the
chunk format up so the whole thing stays dependency-free.

![Cornell box](https://raw.githubusercontent.com/legendgoat124/photon/main/renders/cornell.png)

Every pixel is an average of 900 random light paths. The only light source is
the panel in the ceiling — everything else you can see arrived by bouncing,
which is why the white boxes pick up a faint red on one side and green on the
other.

The renderer is deterministic: a seed fixes the image byte for byte, no matter
how many threads produced it. There is a test asserting exactly that.

### ✨ [glint](https://github.com/legendgoat124/glint) · Python

A small dynamic language, implemented **twice** — once as a tree-walking
interpreter, once as a bytecode compiler and stack VM. The VM runs about **2×
faster**, and having both side by side shows precisely where that comes from.

Every program in the test suite runs on both backends and the transcripts must
match. That comparison caught three real bugs that neither implementation
revealed on its own.

The most interesting result was a failure: a top-level loop originally ran
*slower* under the VM, and the cause was not architectural at all — it was the
position of one opcode in a Python `elif` chain. Moving two branches took it
from 0.80× to 2.37×.

### ⏱️ [ratchet](https://github.com/legendgoat124/ratchet) · TypeScript

Five rate limiting algorithms behind one interface — token bucket, GCRA,
sliding window log and counter, fixed window.

Every limiter takes an injectable clock, so behaviour is a pure function of
elapsed time and the tests are exact rather than `setTimeout` plus a tolerance.
Composition never leaks budget: `all()` asks every limiter before charging any
of them.

### 🔍 [sift](https://github.com/legendgoat124/sift) · Python

A filter language for records — real lexer, real Pratt parser, tree-walking
evaluator. **Never `eval`.**

```python
sift.filter_records("age > 40 and 'code' in tags", people)
```

Paths resolve through mappings and sequences only; there is no `getattr`
fallback, and that omission is the entire security model.

### 📈 [brailleplot](https://github.com/legendgoat124/brailleplot) · TypeScript

Terminal charts drawn with Unicode braille. A braille cell is a 2×4 grid of
addressable dots, so one character carries eight pixels.

```
1000┤        ⡠⠒⠉⠑⢄                                  ⢀⠔⠉⠑⢄
    │   ⢠⠒⠉          ⠈⢆                        ⡠⠊⠁        ⡇
 750┤ ⡰⠁                  ⠘⡄                 ⢠⠃              ⠱⡀
    │⠊                        ⠘⢄           ⡜                    ⠈⢢
 500┤                            ⠘⡄    ⢠⠃                          ⠘⡄
    └───────────────────────────────────────────────────────────────
```

## How I work

- **Zero dependencies** where the problem does not genuinely need one.
- **Tests that assert behaviour**, not implementation — properties over golden
  strings, so a refactor that keeps the contract keeps the suite green.
- **Strict types**: `noUncheckedIndexedAccess` and `exactOptionalPropertyTypes`
  are on, because the bugs they catch are the ones that reach production.
- **Commit messages that explain the reasoning**, since the diff already shows
  the change.

## Stats

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=legendgoat124&show_icons=true&hide_border=true&theme=transparent&hide_title=true" alt="GitHub stats">
</p>

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=legendgoat124&layout=compact&hide_border=true&theme=transparent&hide_title=true" alt="Top languages">
</p>
