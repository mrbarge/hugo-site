---
title: "Advent of Code 2019: personal wrap-up"
date: 2019-12-29T09:52:59+10:00
categories:
  - Year In Review
  - Coding
tags:
  - advent of code
  - golang
thumbnail: "/img/solar-system.jpg"
draft: false
---
In the [previous blog](https://bargenqua.st/posts/aoc-2019/) I described why [*Advent of Code*](https://adventofcode.com) is an awesome and creative way to exercise your programming skills. A few days ago I wrapped up 2019's problems, although I must admit I needed some serious help (read: reading someone else's solution) to do Day 22 Part 2.

This year was also the first year that I managed to convince some work colleagues to join me on the AoC train, which made for some fun watercooler discussions in the morning where we could talk about the ways we solved (or got stuck) on the previous day's problem.

## Introducing the intcode

Previous years of AoC have rarely had problems that were dependent upon solving a previous day's problem - they've all been independent and required . This year's AoC was a marked departure from previous years due to its inclusion of *intcode*, a simple computer which you begin to develop in [Day 2](https://adventofcode.com/2019/day/2), then extend in [Day 5](https://adventofcode.com/2019/day/5) and [Day 7](https://adventofcode.com/2019/day/7), until it is functionally complete in [Day 9](https://adventofcode.com/2019/day/9). *intcode* computers receives instructions as a series of comma-separated integers:

```
3,12,6,12,15,1,13,14,13,4,13,99
```

which instruct the computer to perform operations such as logic comparisons, addition, multiplication or register storage. 

When AoC 2019 began, I fore-warned my colleagues to expect a problem similar to intcode - previous years have involved engineering [similar](https://adventofcode.com/2017/day/18) [concepts](https://adventofcode.com/2018/day/16) - and once Day 2 arrived, I even recommended they solve it in a way that might be extendable for future problems. In no way could I have imagined that it would be taken in the direction that AoC 2019 went..

## Wait, is this program *Breakout*?

Once the intcode VM was complete in Day 9, AoC 2019 followed a predictable cycle: one day would be a problem requiring your intcode, the next day would be something that didn't, and repeat. 

Whilst this led to some incredibly cool problems, it often felt like the Intcode days followed a similar theme of just figuring out what inputs you needed to feed to your Intcode VM in order to run the supplied program correctly. This is a purely subjective thing, but I never really felt the same pride or satisfaction in solving the Intcode puzzles that I usually did with solving the non-Intcode ones (the feeling of finally solving 2018's [Day 17](https://adventofcode.com/2018/day/17) still lingers in me).

The variety in those Intcode programs, though, was pretty awesome. In one day you're writing the AI so that the Intcode program [plays a game of *Breakout* correctly](https://adventofcode.com/2019/day/13). Then you're [guiding a droid through a spaceship](https://adventofcode.com/2019/day/15) to find an oxygen system. Later on you're feeding a buggy inputs in a [*Moon Patrol*-like excursion](https://adventofcode.com/2019/day/21) across an asteroid's surface. This culminated in the very rewarding [final day](https://adventofcode.com/2019/day/25) where - once you've wired up your Intcode computer to receive interactive keyboard input - you find that you're playing a Zork style adventure game and in order to solve the day's problem you need to beat the game. 

## Community contributions

Half the fun of AoC is jumping onto the [subreddit](https://www.reddit.com/r/adventofcode/) after completing the day's problem and seeing how other people have either solved the problem (in Excel, even!), or gone the extra mile to contribute some visualizations of the solution. For example, here's someone's Intcode VM [playing the aforementioned *Breakout*](https://www.reddit.com/r/adventofcode/comments/ea01zn/2019_day_13_beating_intcode_breakout/). Plus, there's always the obligatory [solving something in *Minecraft*](https://www.reddit.com/r/adventofcode/comments/e7ylwd/i_solved_day_8_entirely_in_minecraft/).

With the inclusion of Intcode into 2019, people even began writing their own custom Intcode programs, such as [this Mandelbrot generator](https://www.reddit.com/r/adventofcode/comments/eeqb2g/mandelbrot_generator_written_in_intcode/), or an [Intcode computer written in Intcode](https://www.reddit.com/r/adventofcode/comments/e7wml1/2019_intcode_computer_in_intcode/). Some even began solving [previous AoC problems in intcode](https://www.reddit.com/r/adventofcode/comments/e6f5sk/2019_day1_implementation_using_intcode/)! The AoC community is filled with a bunch of incredibly talented folks, and this year that really shone.

## Personal takeaways from 2019

This has been the first year where I didn't manage to complete all 25 days by Christmas, which was disappointing but inevitable given that I've had a bit of a turbulent and time-consuming month (changing jobs, moving house, getting a dog). I enjoyed the Intcode twist on things, but didn't really encounter many problems that really required me to sit down and puzzle something out (and I don't think that's because I've suddenly gotten smarter in twelve months either). I would've liked to have gotten more time to genericize my Intcode code to be more re-usable across different problems; as it stands, with each Intcode problem I found myself teetering on a tightrope of imminent technical debt. Still, the highs of AoC 2019 were very high indeed, and I'm certainly glad I gave it my time and attention again this year.

Personal favourite days were probably [Day 13](https://adventofcode.com/2019/day/13) and [Day 15](https://adventofcode.com/2019/day/15) for Intcode, and [Day 14](https://adventofcode.com/2019/day/14) and [Day 10](https://adventofcode.com/2019/day/10) for non-Intocde. The hardest day for me is probably [Day 18](https://adventofcode.com/2019/day/18) because it's the only one that I haven't completed Part 1 of yet!

Here's my personal list of things to do before AoC 2020 to make one's life easier.

### Get a project template going

If you're thinking of tackling an AoC year, it's a good idea to structure your code so that you can potentially re-use classes or methods written in previous days. If previous years are anything to go by, it's almost assured that there'll be plenty of opportunities to re-use previous code. For next year I'm going to build up my project structure ahead of time, creating some basic stubs for each day which just run, read a file into memory, and then quit. 

That brings me to a very related topic..

### Build up a toolbox of helper methods

In solving AoC you're going to end up doing a lot of the same sorts of things. Things like handling X/Y coordinates on a 2D grid and finding neighbouring coordinates. Various array and dictionary manipulations. Reading CSV files, or files that would map to coordinates of a 2D grid. Graph traversal searches and shortest-path algorithms.

Depending on your programming language of choice, you may have support for some of these in the core library (Python in particular is a *very* AoC-friendly language). Otherwise, it's good to go in prepared. This is something I've been meaning to do for the last two AoCs and have regretted not doing it each time. There will not be a third time!

### Resist the leaderboard temptation (unless you know you're good enough)

I've tried in previous years to get on the leaderboard, but I'm just not fast enough. Australia is blessed to be in a time-zone which is pretty friendly towards leaderboard attempts (each problem appears at 3PM AEST), but I think I'm going to just take it easy from now on and not make leaderboard attempts. If nothing else, it's because my solutions easily suffer from the rush of getting to an answer as quickly as possibly in lieu of writing decent code.

### Get others involved

The real fun of AoC is not solving problems, but discussing with others how you solved them. With the day-by-day nature of the event, it makes for some great daily chats over morning coffee. Rope in some friends or colleagues to join you, and maybe even set up a private leaderboard.
