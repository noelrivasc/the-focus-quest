---
title: In Lieu of Types
date: 2025-04-22
description: In TypeScript, types describe the shape of data; In Clojure, spec and examples can do the same.
tags:
  - Clojure
  - Technical Notes
---

After reading the whole re-frame documentation, I started working on a demo app to put those ideas in practice. This is the first non-trivial thing that I attempt to write in ClojureScript.

I set up my db, and started adding events and subs. Before long, there were some data structures in use but my default db still looked like this:

```clojure
(def default-db
  {:transient {:factor-active nil}
   :factors {:all []}})
```

... which tells me _nothing_ about the structure of the db.

Types are not a thing here, and I knew that just writing an example in comments was not going to cut it —the comments could quickly become obsolete and misleading, or maintaining them could be a hassle.

So, I learned the basics of spec, with the goal of using the spec as both live documentation and functional validation.

The db code is still a WIP and there's a good chance that I'm doing something horribly wrong, but at least there's some guide now, and run-time validation:

```clojure
; -- FACTORS ------------------------
(s/def :factor/id (s/or :empty (s/and string? #(= 0 (count %)))
                        :uuid (s/and string? #(= 36 (count %)))))
(s/def :factor/min (s/and int? #(<= -10 % 0)))
(s/def :factor/max (s/and int? #(<= 0 % 10)))
(s/def :factor/title (s/and string? #(<= 1 (count %) 50)))
(s/def :factor/description (s/and string? #(<= (count %) 120)))

; {
;  :id ""
;  :title ""
;  :description ""
;  :min -10
;  :max 10
;  :weight 0
;  }
(s/def ::factor (s/keys :req-un [:factor/title :factor/min :factor/max]
                       :opt-un [:factor/id :factor/description]))
(s/def ::factor-list (s/coll-of ::factor :kind vector?))

; -- SCENARIOS ----------------------

(def default-db
  {; Information that is used for procedures but that is
   ; not the resulting data that is the goal of the program
   :transient {; Just default values of factor form
               ; These do not change as form is edited
               :factor-edit-defaults nil

               ; The model that changes as input is made
               ; Goal of duplication: avoid re-renders or
               ; having local state in the component
               :factor-active nil
               :factor-active-validation {:is-valid nil}}
   :factors {:all []}})
```
