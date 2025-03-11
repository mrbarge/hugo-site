---
title: "Can AI write a sequel to my old QBASIC games?"
date: 2025-03-02T15:24:52+10:00
categories:
  - Coding
tags:
  - retro
  - ai
thumbnail: "/img/bargosoft-ai-logo-thumb.jpg"
images:
  - https://bargenqua.st/img/bargosoft-ai-logo-thumb.jpg
image: https://bargenqua.st/img/bargosoft-ai-logo-thumb.jpg
draft: true
---

We've learned through my [last blog](../failed-game-dev-2/) that game programming was never going to be the career for me. But if I feed AI my old games, can it do a better job of writing one? Let's find out.

After [reading the tale](https://www.reddit.com/r/ClaudeAI/comments/1iyumpf/i_uploaded_a_27yearold_exe_file_to_claude_37_and/) of someone who uploaded their old Visual Basic application to [Claude.ai](https://claude.ai) with surprising results, I knew what I had to do - feed it all the old **Grod** QBasic games that myself and my friend Tony had written, and ask it to write me a sequel. In QBasic.

And that's exactly what happened.

One by one I uploaded the Grod QBasic files, and then read the interpretive summary that Claude created:

{{< figure src="/img/ai-game-sequel/ai-game-sequel-1.png" link="/img/ai-game-sequel/ai-game-sequel-1.png" width="500x">}}

I then asked it to write me a new game in the series, with the following constraints:

- It had to be written in QBasic.
- It had to have multiple paths and endings.
- It should be set 30 years after the last game, but reference pop culture elements of the 90s.
- It should have graphics and sound, and end credits.

It then beavered away for a minute or two writing me a `GROD6.BAS`.

I encountered some problems initially. Firstly, Claude's output messages have a maximum size, and that meant the program just cut off abruptly. You can ask Claude to `continue` (the UI even suggests you do this), but when I tried it Claude would just rewrite the entire program from scratch and do the same thing again. I ultimately added an additional constraint that the game needs to fit within Claude's maximum message size to take care of that problem.

There were also a couple of minor syntax errors to fix up. At the end of the game it prompts if you want to replay. If you type `Y` the code would `GOTO 1`, except Claude the `1` label was missing. Likewise if you typed `N` it would `GOTO 900`, and `900` did not exist. These were easily fixed by me, and then.. I played Grod 6..

{{< carousel name="grod6-carousel" items="1" height="500" unit="px" duration="7000" >}}

Some observations:

- Apparently Bargosoft's successor is **Neurosoft** and its tagline is now `The future of retro entertainment`, which is quite cute, 
- The **Bargosoft** logo was shorted to just "BARGO".
- The general presentation felt authentic to the previous games, what with occasionally changing the colour of the text.
- There were indeed branching paths and multiple endings. However, there were no 'game overs' that I could find, which was definitely a hallmark of my terrible games. I found this quite interesting in that you're always steered towards eventual success. Which, in a very roundabout way, is an evolution that feels in line with modern adventure games.
- I am kind of impressed by the 'face' graphic. Everything else was a bit scuffed though. There was also PC speaker sound.
- The writing just.. well.. as expected, it feels very bland and AI to me. Almost too predictable.

Still.. it blew my mind that it could assemble this. It's ultimately not a very tricky thing, I suppose - the old games were very text-heavy and the logic very simple, so it doesn't feel like a difficult thing to interpret and recreate. But, yes.. kind of impressive, all the same.

I then decided to push things a little further, and ask Claude to write me a QBasic game based on/inspired by the previous Grod games, but in an entirely different genre like an arcade game.

Again, I had to do some minor tweaks - it named variables with underscores, which caused loading corruption in the original QBasic. Once I figured that out, it whipped me up a simple shoot-em-up game that - whilst very, very crude and buggy - still fundamentally sort-of worked.

{{< video src="/video/grod7-1.mp4" type="video/mp4" preload="auto" >}}

That's Grod up the top, and he's raining down little pixies for you to either shoot or avoid whilst you try and concentrate your fire on him. 

Were it not for the fact that it redrew the entire screen every frame, causing laggy input and a constantly flickering screen, it would genuinely be rather playable.

Actually.. why don't I ask Claude to try and fix that right now?

{{< video src="/video/grod7-2.mp4" type="video/mp4" preload="auto" >}}

Well, it.. sort-of did it. Which, to its credit, is genuinely kind of awesome.

Ultimately, it's been genuinely entertaining and fascinating to see how an LLM performed here. The actual content it produced, however, still reeks with the same AI stench that most LLM-produced material does. None of the game content really surprised me.. and I guess that's to be expected, because it's essentially doing predictive text. It's hard to be surprised when it's engineered to write the least surprising things.

{{<disqus>}}