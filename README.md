# SNEK is Not an Acronym


## About

This library is specifically written to be useful for a broad range of ways in
which I create art using various generative algorithms.

![head](img/cells.lisp.png?raw=true "ex")

In short `snek` is three things:

1. A simple (graph) data structure for working with vertices and edges The
   structure is named `snek`; the name is explained below. This structure is
   combined with a programming pattern for applying changes to the structure.
   The pattern relies on `alterations`, see below.

2. A tool for drawing things called `sandpaint`. `sandpaint` uses random
   sampling to draw it's primitives. This creates a fairly distinct and gritty
   look in many cases.

3. A series of useful data structures and tools. E.g. a 2D vector `vec` and a
   package for generating different kinds of random numbers: `rnd`.

![head](img/spline-script.lisp.png?raw=true "ex")


### About the Name

A while back someone on twitter suggested that if Python 3 was named "snek" it
would avoid naming confusion. I found that amusing at the time, and picked snek
as the placeholder name for this project. I've been looking for a better name,
but I haven't found one yet.


## Alterations

The pattern depends on the concept of `alterations`. In short: an `alteration`
is a change that will be applied to the structure at the end of a given
context. `alterations` are further described in
http://inconvergent.net/snek-is-not-an-acronym/.

I have also written about things related to `snek` at

  - http://inconvergent.net/a-propensity-for-mistakes/ (indirectly about `snek`)
  - http://inconvergent.net/a-method-for-mistakes/
  - http://inconvergent.net/arbitrary-alterations/
  - http://inconvergent.net/grains-of-sand/ (about "sandpainting", see `src/sandpaint.lisp`)

Here is and example of manipulating a `snek` instance called `snk` using
`alterations`. Alteration constructors are postfixed with `?`.

```lisp
; context start
(snek:with (snk)
  ; iterate vertices
  (snek:itr-verts (snk v)
    ; move alteration
    (snek:move-vert? v (rnd:in-circ 1d0))
    ; w will be an arbitrary
    ; vertex in snk
    (snek:with-rnd-vert (snk w)
      ; join v and w if they are closer than d
      (if (< (snek:edge-length snk (list v w)) d)
        ; join vertices alteration
        (snek:join-verts? v w))))
; context end
; alterations have been applied
```


### Custom alterations

You can define your own arbitrary alterations. There is an example of this in
`ex/custom-alt.lisp`. I have also written about it here:
http://inconvergent.net/arbitrary-alterations/


## Examples

There are some examples included. All examples are in the `examples` folder.

If you don't provide a filename (with full or relative path) as the first
argument, the resulting file will be named `./tmp.png`.


## Usage

Among other places, `snek` is used in

  - http://moment.inconvergent.net/
  - https://twitter.com/sandpaintbot
  - https://twitter.com/scratchpaintbot
  - https://twitter.com/cronianrings
  - https://twitter.com/rndshep

![lines](img/lines.lisp.png?raw=true "ex")

![lines](img/grid-bz-walk.lisp.png?raw=true "ex")

I also use it to create mechanical plotter drawings:

 - http://inconvergent.net/mechanical-plotter-drawings/
 - http://inconvergent.net/mechanical-plotter-drawings/3/
 - http://inconvergent.net/spline-script/plots/


## Dependencies

This code requires `Quicklisp` and `zpng`. The path to quicklisp must be set in
`src/load`. `zpng` is automatically installed via `quicklisp`.

 - http://www.xach.com/lisp/zpng/
 - https://www.quicklisp.org/beta/


## Tests

There are some tests included, see the `test` folder.


## Stability, Changes and Versioning

This code is highly experimental on my part. It is likely to change with no
warning or explanation. I will keep a note of the version number in
`src/load.lisp`.


## On Use and Contributions

This code is a tool that I have written for my own use. I release it publicly
in case people find it useful. It is not however intended as a
collaboration/Open Source project. As such I am unlikely to accept PRs, reply
to issues, or take requests.


## Planned Changes

 - Randomized order of alteration apply
 - test parallel zmap implementation


## Bugs

 - bzspl has lower sample density near the edges in some cases.


## Thanks

I would like to thank

  - https://twitter.com/RainerJoswig
  - https://twitter.com/paulg
  - https://twitter.com/jackrusher

Who have provided me with useful hints and code feedback.

