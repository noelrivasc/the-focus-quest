---
title: Clojure and ClojureScript are not identical
date: 2025-04-04
description: While most of the Clojure reference applies to cljs, not _all_ of it does
---

## Take away

```clojurescript
(not (== ClojureScript Clojure))
```

- ClojureScript is not identical to Clojure.
- Most of the time they are compatible but, when in doubt, check the specific API reference.
- The CheatSheet may not have the full picture; check the actual docs.

As I tackle my first project with Clojure(Script), I have had [the CheatSheet](https://clojure.org/api/cheatsheet) open most of the time for the past few weeks. Note that it's the _Clojure_ cheatsheet, not the _ClojureScript_ cheatsheet.

Today, I was following up on an implementation that uses walk (some form of it which I haven't quite figured out yet) to apply Tailwind classes to a hiccup structure. I wasn't getting the results I needed, `prewalk` leading to _too much recursion_ errors, and `postwalk` leading to transformation of structures I didn't want to touch.

So, I saw `postwalk-demo` in the cheatsheet and wrote a simple test to run through the REPL, but got an error: _clojure.walk.postwalk_demo is undefined_. I thought I may be doing something wrong with the import, and wrestled with it for a bit.

I visited the [ClojureScript API Documentation](https://cljs.github.io/api/) and then I found that while the walk functions are implemented, the `-demo` ones are not.

Also, note that the [ClojureScript CheatSheet](https://cljs.info/cheatsheet/) makes no mention of the `walk` functions, even though they are part of the language.

On the bright side, I love how accessible the documentation is, and how easy it was to clear up this confusion.
