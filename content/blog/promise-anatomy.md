---
title: "Anatomy of the Promise Organism - DRAFT"
date: 2024-01-30
draft: true
tags:
  - Technical Notes
---

## Anatomy of the Promise Organism

Promises are organisms that can show up in many ecosystems but are found in abundance in JavaScript. In just a few years these species went from being a mere idea to conquering vast areas of the web and feeding on copious amounts of data.

In this article, we will explore the evolution of the Callback groupings into Promise colonies, and attempt to shine a light onto their beautiful —if intricate and possibly confusing— anatomy.

It must be noted that Promises are a genus, not a species. I will focus on the simplest, earliest species that arose in the JS ecosystem but keep in mind that it's a diverse family.

Still, this article should provide a basic understanding of the anatomy, from which the more complex organs and features of more sophisticated species can start to be understood.

## Callback: Ancestor to Promises

### Scratchpad
Blog post on the anatomy of Promises.

* Are they colonial organisms, or individuals?
* What parts do they contain?
	* State
	* value
	* handlers stack
* How do Promises link together to form colonies, or strings of Promises?
* Promise ranching
	* Cultivation methods for promises, including .all(), .each()
	* Promisifying of regular functions with async and await

The Then and other callback-receiving channels
The State

Hm. I would like to get a preview but apparently that is not possible with GH.

## Reference Material:
- Simplest implementation: https://www.promisejs.org/implementing/
- Bluebird promise code: https://github.com/petkaantonov/bluebird/blob/master/src/promise.js
- Promises explanation by Q promise library: https://github.com/kriskowal/q/blob/v1/design/README.md
- V8 Promise implementation (closed the tab; not very useful as I don't understand the context)
- Promises in the ECMASCRIPT specification: https://tc39.es/ecma262/multipage/control-abstraction-objects.html#sec-promise-objects

```ruby
def foo
  puts 'foo'
end
```
