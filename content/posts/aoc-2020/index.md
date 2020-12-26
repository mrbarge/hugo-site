---
title: "Advent of Code 2020 reflections"
date: 2020-12-26T14:07:21+10:00
draft: false
categories:
  - Year In Review
  - Coding
tags:
  - advent of code
  - golang
thumbnail: "/img/aoc-2020.jpg"
images:
  - https://bargenqua.st/img/aoc-2020.jpg
---

[Advent of Code](https://adventofcode.com) has wrapped for another year, so I figured I’d write a companion piece to [last year’s blog](../aoc-2019-wrapup) about the same topic with some brief thoughts and reflections on 2020’s event.

## Overall feelings

I quite enjoyed this year’s collection of puzzles. Unlike last year’s [Intcode](https://esolangs.org/wiki/Intcode) theme - which spanned almost the entirety of the month - each puzzle this year was its own standalone thing. There were also no puzzles that I felt demanded much algorithmic knowledge, with nary a shortest-path problem to be seen - much to my relief, as they’ve historically always been the more challenging ones for me. So in many ways, this felt like one of the more approachable years in its history.

This was one of the first years where, on numerous occasions, I was able to write the solution and then immediately get the correct answer, with no hair-pulling hours of debugging required. I’m not sure if this is because this is one of the most coding-heavy years I’ve had in recent memory in my regular job, or if I’m just getting used to the types of “gotchas” that AoC problems tend to pull, but I was nonetheless really happy. I of course didn’t get anywhere close to a place on the public leaderboards, but I was happy enough to just be able to keep up with the problems day by day. As with all previous years, my solutions are [available on Github](https://github.com/mrbarge/aoc2020), although I do notice my code getting rougher and rougher with each successive day as December fatigue set in.

## Approaching problems

In last year’s blog I swore that I was not going to fall into the same trap as previous years, and was going to sit down and create a collection of reusable helper functions that could be used in many of the problems. So, I started my AoC month a day early by doing that - and I’m extremely glad I did, because it saved me a heck of a lot of time each day. I’d definitely recommend anyone commencing AoC to do the same if they’re considering tackling a whole month’s worth of problems. Helpers that benefited me the most were:

- File helpers to read a file in various formats (CSV, multi-line text, single-number-per-line)
- A 2D “Coordinate” type and helper functions to get the neighbours of a coordinate.
- Array helpers for finding elements and set intersections

Of course, depending on your implementation langauge of choice, some of these may already be part of the core language. 

## Recommended days

This year it felt like there were many days that required or benefited from a solution that embraced [recursion](https://en.wikipedia.org/wiki/Recursion_(computer_science)). Recursive programming is typically not something I’m do much of in my day-to-day job, so it was fun to exercise that part of my brain again and think about how to do that effectively.

In terms of memorable or recommended days for those getting started with AoC:
- [Day 3](https://adventofcode.com/2020/day/3) is a good warm-up for some of the later days where more advanced 2D (or 3D, or 4D!) grid traversal is required.
- [Day 4](https://adventofcode.com/2020/day/4) is not too hard, but is a good test of performing data validation.. and - if you're like me - will probably test just how much you pay attention to the requirements there-in.
- [Day 7](https://adventofcode.com/2020/day/7) is probably where things start getting tricky and where you can flex some of those recursive programming muscles.
- [Day 8](https://adventofcode.com/2020/day/8) is the classic AoC-style "write a parser for basic computer operations". It's a good jumping-off point for Aoc 2019 if the process of solving it appeals to you.

For anyone looking for a challenge, the day I think was the most enjoyable was [day 18](https://adventofcode.com/2020/day/18). This was a great problem because it’s easy to understand and can be solved in many different ways. I ended up solving it by getting the bright idea to pass the equations into Golang’s [parser](https://golang.org/pkg/go/parser/) (the same parser that parses Golang packages) and navigating the resulting Abstract Syntax Tree to calculate the sums and define a custom mathematical precedence. That was a tonne of fun and I learnt a new thing as a result.

My other favourite "hard" day was probably [day 20](https://adventofcode.com/2020/day/20), which I’d say is also the month’s overall hardest problem - though of course opinions on that may vary. This was one of those problems where you could probably short-cut your way through Part 1 and then be absolutely stuck on Part 2 as a result of that short-cut. I did Part 1 the long way (determining each tile’s correct placement in the grid), so Part 2 was pretty straightforward, albeit a bit laborious to work through. This was also one of the days where I wrote up the whole thing, compiled, ran, and got the correct answer straight away, so it was memorable from that angle.

[Day 23](https://adventofcode.com/2020/day/23) was a great day because it really drives home how much the data structure you use for a problem can impact the feasibility of solving it. An array-manipulation-based solution will be too slow for what Part 2 throws at you, but a linked-list approach will absolutely smash it. 

## Summing up

AoC is definitely becoming one of my favourite things about the end of the year, and if you’re reading this, I hope you’ll join us in 2021 (if it continues). Next year I’m going to try a new language. For some reason, I want to try Haskell, but we'll see.
