# SymPyCall

[![Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://jverzani.github.io/SymPyCall.jl/stable)
[![Dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://jverzani.github.io/SymPyCall.jl/dev)
[![Build Status](https://github.com/jverzani/SymPyCall.jl/actions/workflows/CI.yml/badge.svg?branch=main)](https://github.com/jverzani/SymPyCall.jl/actions/workflows/CI.yml?query=branch%3Amain)
[![Coverage](https://codecov.io/gh/jverzani/SymPyCall.jl/branch/main/graph/badge.svg)](https://codecov.io/gh/jverzani/SymPyCall.jl)


This is a sketch of what is needed to use `PythonCall` instead of `PyCall` for `SymPy.jl`. At the moment, the expectation is that *if* that change proves desirable, this would become `SymPy` (that is `SymPyCall` is not going to be registered).

Along the way, some small design decisions might be adjusted and are reflected here:

There would be a few deprecations:
* `@vars` would be deprecated; use `@syms` only
* `Base.show` isn't *currently* using pretty priting
* `elements` for sets would be removed (convert to a `Set` by default)
* Would `Q` be ported? (Use `\itQ` for now)
* What to do with matrices? Using `Matrix{Sym}` with no `SymMatrix` type expected
* `sympy.poly` *not* `sympy.Poly`, though `sympy.Poly` does work for now via a hacky thing to manage `ManagedProperties`,
* would we export `CommonEq` symboles?
* `limit(ex, x, c)` deprecated; use `limit(ex, x=>c)` or `sympy.limit`
* no new special functions exported, just the ones in SpecialFunctions.jl


## Installing `sympy`,

To install `sympy` in `PythonCall` isn't hard; below shows how it may be done. If this were to become registered, automating this would be very desirable.

```
using PythonCall
]
conda add python sympy
conda resolve
[delete key]
sympy = pyimport("sympy")
```
