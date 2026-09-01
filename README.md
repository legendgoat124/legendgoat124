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

I build focused libraries with no dependencies, real test suites, and
documentation that explains the *why* rather than restating the signature.

A theme runs through all of them: the interesting part of a problem is usually
the edge case everyone else rounds off. A rate limiter is easy until you ask
what happens when the clock jumps backwards. A filter language is easy until
you ask what it can reach.

## Projects

### ⏱️ [ratchet](https://github.com/legendgoat124/ratchet) · TypeScript

Five rate limiting algorithms behind one small interface — token bucket, GCRA,
sliding window log and counter, fixed window.

Every limiter takes an injectable clock, so behaviour is a pure function of
elapsed time and the tests are exact instead of `setTimeout` plus a tolerance.
Composition never leaks budget: `all()` asks every limiter before charging any
of them, which is sound because these algorithms only ever *gain* budget as
time passes.

```ts
const limiter = new GCRA({ limit: 100, windowMs: 60_000 });
const { allowed, retryAfterMs } = limiter.consume();
```

### 🔍 [sift](https://github.com/legendgoat124/sift) · Python

A filter language for records — real lexer, real Pratt parser, tree-walking
evaluator. **Never `eval`.**

```python
sift.filter_records("age > 40 and 'code' in tags", people)
```

Paths resolve through mappings and sequences only; there is no `getattr`
fallback, and that omission is the entire security model. Filters can come
from a config file or a user, and the worst they can do is not match.

Ships with a `grep`-shaped CLI for JSON Lines.

### 📈 [brailleplot](https://github.com/legendgoat124/brailleplot) · TypeScript

Terminal charts drawn with Unicode braille. A braille cell is a 2×4 grid of
addressable dots, so one character carries eight pixels — an 80×20 terminal
becomes a 160×80 bitmap.

```
1000┤        ⡠⠒⠉⠑⢄                                  ⢀⠔⠉⠑⢄
    │   ⢠⠒⠉          ⠈⢆                        ⡠⠊⠁        ⡇
 750┤ ⡰⠁                  ⠘⡄                 ⢠⠃              ⠱⡀
    │⠊                        ⠘⢄           ⡜                    ⠈⢢
 500┤                            ⠘⡄    ⢠⠃                          ⠘⡄
    └───────────────────────────────────────────────────────────────
```

Line plots, scatter, sparklines, bars, and histograms.

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
