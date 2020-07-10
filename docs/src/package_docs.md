# Sample Documentation
```@meta
CurrentModule = JuliaTemplateRepo
```

This page shows how to pull in the doc strings in your code.

The first thing to do is insert
````markdown
```@meta
CurrentModule = JuliaTemplateRepo  # your package name here
```
````

which sets the module to your package so you don't have to prepend the methods with your
package.

## Pulling in some docstrings
First, let's pull in the docstrings for `vec_add!` and `vec_sub!`, which we can do using
````markdown
```@docs
vec_add!
vec_sub!
```
````

This inserts the following into our markdown file:

```@docs
vec_add!
vec_sub!
```

Notice how in the `vec_add!` docstring we included both signatures in a single docstring,
but `vec_sub!` had two separate docstrings. We can select only one of the docstrings by
filtering with the input signature:
````markdown
```@docs
vec_sub!(::VecPair)
norm(::VecPair)
```
````

which inserts only one docstring,
```@docs
vec_sub!(::VecPair)
```

## Linking Docstrings
We can link to the docstring for [`vec_add!`](@ref) using the `[`vec_add!`](@ref)` syntax.
Note the tick marks around the method, inside the square brackets. We can also do this
inside the docstring themselves, like we do in the docstring for [`VecPair`](@ref):

```@docs
VecPair
```

For illustration, we also show in this docstring how to include ``\LaTeX`` math inside the
docstring. For reference, we've copied the raw docstring below:

```julia
"""
    VecPair{V}

Holds two vectors of the same length and type.

The vectors can be retrieved using `v.a` and `v.b` or `v[1]` and `v[2]`.
Supports [`vec_add!`](@ref) and [`vec_sub!`](@ref).

Here is some ``\\LaTeX`` for you:
```math
    \\sum_{i=1}^N x_k^T Q_k x_k
```

# Constructors
    VecPair{V}(a,b)
    VecPair(a::V, b::V)
    VecPair(a::StaticVector, b::StaticVector)

"""
```

## Writing Docstrings
As stated in the [Julia manual](https://docs.julialang.org/en/v1/manual/documentation/),
start the docstring with the signature, which is indented with 4 spaces so it prints as
Julia code. You can use normal markdown syntax, such as headings, to make your docstrings
look since and stay organized. See the above example and the
[Documenter.jl docs](https://juliadocs.github.io/Documenter.jl/stable/man/latex/) on how
to include ``\LaTeX`` math into the docstrings.



## Building documentation locally
You can build the documentation locally by only running the `makedocs` function, and
disabling `prettyurls`. It's common to update docstrings in your code and want these
changes reflected in your build. After making a change to the docstring, you need to
"rebuild" the docstrings by executing the whole file, easily done with `CTRL-SHIFT-RETURN`
in Juno. You can then rebuild the the docs (using `CTRL-RETURN` in Juno) and the docstrings
will be updated.
