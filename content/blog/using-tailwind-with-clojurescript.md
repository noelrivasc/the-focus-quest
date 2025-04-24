---
title: Tailwind 4.x with ClojureScript
date: 2025-03-29
description: It's quite simple, actually
tags:
  - Technical Notes
  - Clojure
---

When I was figuring out how to integrate Tailwind with a re-frame project I'm working on, I found some instructions for Tailwind 3.x that didn't work with the newer version.

So, this post has notes on how to use Tailwind 4.x with clojurescript.

## The gist

- Create a CSS file with the `@import "tailwindcss";` directive
- Install the Tailwind CLI
- Run Tailwind in _watch_ mode

## Simpler than I thought (with one caveat)

I hadn't set up Tailwind before, so I was pleasantly surprised with how simple this turned out to be.

I thought that Tailwind had a way to parse the input files' syntax and get the classes from the right places (for example, the `class` attribute of HTML elements). Had that been true, I would have needed to find a way to make Tailwind compatible with the ClojureScript syntax.

Tailwind does not care about file syntax; it just scans text files for the text patterns (class names) it knows, and includes those classes in its output. So, in a CLJS project, one just needs to call the watch command and point it to the cljs files.

Caveat: if there's any string manipulation involved in generating the class names, they will not be picked up by Tailwind. If that's your case, you'll need to find a way to dump the class names to a file, or configure Tailwind to include them in another way. I have no help there (yet).

```clojure
; Example: this component's color will not be included
(defn card [color]
    (:div {:class [
        (str "bg-" color "-700") ; this concatenation does not match the bg-COLOR-700 that tw would expect
        ]}))
```

## Step by step

- Create a CSS file with the `@import "tailwindcss";` directive (`input.css` in this example).
- Install TW as a dev dependency `npm install -D @tailwindcss/cli`
- Run Tailwind in watch mode, and have it scan your CLJS files `npx @tailwindcss/cli -i ./some-path/css/input.css -o ./some-path/public/css/main.css --content './src/cljs/**/*.cljs' --watch`
- Include your CSS output (`./some-path/public/css/main.css` in this example) in your html.

## Usage example

Here's a simple example from a simple app I'm building:

```clojure
(defn v-main-panel []
  (let [factor-active (re-frame/subscribe [::subs/factor-active])]
    [:div.wsid-app
     [:main
      ; The BEM-style classes are just reference; not used for styling
      [:div.title__wrapper 
       [:h1.title 
        ; In attributes for readability
        ; They could be appended as h1.title.text-cyan-700.font-bold just as well
        {:class ["text-cyan-700" "font-bold" "italic" "text-6xl"]}
        "What Should I Do?"]]
      [:div.decision-container
       (v-factors-panel)
       (v-scenarios-panel)]
      (v-modal-dialog (not (nil? @factor-active)) v-factor-form)]]))
```
