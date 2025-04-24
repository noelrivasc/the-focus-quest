---
title: Careful work is faster —and way more enjoyable
date: 2024-07-11
description: Start with understanding; don't waste time to trying things in haste.
tags: Focus Quest
---

I spent about three hours chasing a bug today. You've been there: following up the trail of some mysterious failure; trying to repeat what you did before to replicate the error. Failing, trying again, narrowing down the possibilities. Getting a small hit of dopamine each time you confirm a part of the problem.

— The `WHATEVER` variable is `undefined` here. The .env is not being loaded.

— Oh wait... but this other one is there. So... it's being overwritten.

...and on and on, until you get to the culprit and are able to replicate a solution, and find yourself immersed in a mix of exhaustion and contentment.

**The problem with today's bug is: I could have solved it in 5 minutes** (PR description included), had I read the code carefully.

See, a colleague removed a dependency, but he also removed the use of the module in a configuration file. I added the dependency back but things weren't working, so I started testing and trying things that weren't working, until I was flailing around frantically. 

Hours later, I found one missing configuration line. It was right there, red, highlighted in the diff.

In my attempt to be quick, I wasted hours.

Had I worked slowly, diagnosed carefully and with full presence of mind, I would have saved lots of time and frustration.
