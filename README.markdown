
# Template Haskell and QuasiQuotes

Slides for a short [talk at the Brisbane Functional Programming Group] [BFPG],
June 2012.

[BFPG]: http://www.bfpg.org/events/67067762/

These are probably only useful if you need to jog your memory about something I
said at the talk.  If you really want to learn Template Haskell and
QuasiQuotes, you should probably just head straight to the [Template Haskell
wiki page][TH], and start following links from there.

[TH]: http://www.haskell.org/haskellwiki/Template_Haskell

Learning Template Haskell does require some detective work. Those resources
which are up-to-date, namely the [relevant section of the GHC user manual]
[manual] and the [Template Haskell library API documentation] [API], are not
intended as tutorials. And many of the resources which are useful for learning
Template Haskell are either not altogether comprehensive, or somewhat out of
date. But you're clever, so I'm sure you'll work it out!

[manual]: http://www.haskell.org/ghc/docs/latest/html/users_guide/template-haskell.html
[API]: http://hackage.haskell.org/package/template-haskell

## Questions asked at the talk

A couple of questions came up which I didn't really address properly.

### Quoting names

[Nick][] asked whether quoting a name that is not in scope is an error. Indeed
this is an error. TH quotes are lexically scoped, so a quoted name always
refers to the name in scope at the point of the quotation, whether that name is
itself lexically scoped, or a qualified global name.  Global names add some
subtleties, because they might not be imported in the scope where the quote is
spliced. But the TH authors have thought about these things, and TH generally
works as you'd expect it to.

It is possible to create a quoted AST with a "free variable" that can be
captured by whatever name happens to be in scope at the point of splicing, but
you have to go out of your way to do that explicitly. See the [TH paper][] for
the details.

[TH paper]: http://research.microsoft.com/~simonpj/papers/meta-haskell/
[Nick]: http://twitter.com/nkpart

### Applications

[Sanj][] asked what applications make use of Template Haskell and QuasiQuotes.
I mentioned [Yesod][], since [Ben][]'s Yesod talk was up next, but here are a
few more.

[Derive][]: A library and tool for automatically deriving type-class instances.
Uses reification to inspect the data type whose instances are to be derived,
and provides ready-to-splice quoted declarations for the derived instances.

[Data Accessor][]: A library for defining composable accessors for fields of
data types. Comes with a [Data Accessor Template][] package which uses
reification to generate the accessors for a data type. The [Lenses][] package
provides similar capabilities, also using Template Haskell.

[Boomerang][]: A library for defining invertible parsers. Uses Template Haskell
to automatically derive some parser and pretty-printer combinators for a give
data type.

For more examples, you can fetch the [Hackage index][] and grep for
"TemplateHaskell" and "QuasiQuotes" (to find uses of the language extensions),
or grep for "template-haskell" to find dependencies on the support libraries.

[Yesod]: http://www.yesodweb.com/
[Derive]: http://hackage.haskell.org/package/derive
[Data Accessor]: http://hackage.haskell.org/package/data-accessor
[Data Accessor Template]: http://hackage.haskell.org/package/data-accessor-template
[Lenses]: http://hackage.haskell.org/package/lenses
[Boomerang]: http://hackage.haskell.org/package/boomerang

[Ben]: http://twitter.com/benkolera
[Sanj]: http://twitter.com/ssanj

