---
title: "I was a failed teenage game developer (part 2)"
date: 2025-02-24T19:00:00+10:00
draft: false
categories:
  - Coding
tags:
  - retro
thumbnail: "/img/failed-game-dev-2-thmb.png"
images:
  - https://bargenqua.st/img/failed-game-dev-2-thmb.png
image: https://bargenqua.st/img/failed-game-dev-2-thmb.png

---

> _This blog first appeared in 2008 as a guest article for a friend’s (long since removed) website. To consolidate some of my previous writing in the one place, it has been re-posted with permission, with some edits and lots of additional media added. Think of it like the HD remaster of an old videogame, except it’s a videogame no-one played because it wasn’t very good._
>
> _Also be sure to read [part one](../failed-game-dev-1/) first!_

## Apathy vs puberty

It had always been a distant dream of mine to be a game programmer. At the time, of course, it was possible for young coders to whip up popular games in their own garage and flog them off as shareware. This shut-in, computer-chained lifestyle seemed like the sort of one I wanted to lead.

My bedroom had cut-out magazine pictures of my gaming heroes.. a PC Gamer interview with iD Software back in the Doom days, a Commodore 64 magazine piece on [Jeff Minter](https://en.wikipedia.org/wiki/Jeff_Minter), a shoddily self-drawn [System 3 logo](https://www.c64-wiki.com/wiki/File:System3_logo.jpg).. I'd gaze up at them almost daily, pinned on my little cork bulletin board.

{{< figure src="images/idsoftware.png" link="images/idsoftware.png" caption="This bunch of nerds was the first thing I saw every day." width="400x">}}

I tried somewhat half-heartedly to achieve that dream. After saving months worth of allowance money, I finally managed to gather enough dough to purchase Andre LaMothe's enormous book [Tricks of the Game Programming Gurus](https://doomwiki.org/wiki/Tricks_of_the_Game-Programming_Gurus), hoping that it would bless me with its game development knowledge. It was littered with code snippets showing how to write an engine, perform graphical tricks, play sound, and so on. It also weighed in at a rather imposing 700+ pages, giving it definite blugeoning potential. I think it may actually feature as a murder weapon in some editions of _Cluedo_.

The sheer intimidation factor alone left me unimpressed, and it turns out that doing graphics usually requires you to be competent at _maths_ (shudder), so I quickly returned back to the familiar comforts of my QBasic world.

During the last two years of high school, I also kept a running diary about how I was going to create a 3D SWAT-based game. I used pages upon pages to lay out the game design and describe how it would work. Looking back on it, some of it was rather cool, even though Sierra have since made a game franchise that was pretty much exactly what I had in mind. Here's my crazy mind at work in the diary's debut entry:

```
Had a good idea while I was in the shower this morning - I'm going to write
a 3D game! So now I'm left with a problem - what will I write about?
It has to be original (which is tough these days as a lot of ideas are
taken), has to be multiplayer (my rule of game programming no 2 - games 
MUST be multiplayer!), has to be extremely atmospheric, and has to be
absolutely awesome! It took me a while, but I've finally thought of
something. You know how on that "Cops" show the SWAT guys break into
buildings in an attempt to kill or arrest some villian who is inside?
This would be the most awesome opportunity for a multiplayer game...
```

In retrospect, I'm intrigued by these "rules of game programming" that I've apparently established.. but I'm even more intrigued by whatever-the-heck this episode of _Cops_ is that I'm referring to.

The entry continues, describing the sound design:

```
Sound will be a high priority, I want, no, I need
headphones/mics for the game. This would make for
interesting conversations between the players..

"RED ONE, THE PERPERTRAITOR IS IN THE SOUTH
BLOCK, LEVEL 12E. OVER"
"COPY THAT, RED THREE. I'M THERE. GET BACKUP."
"ROGER RED ONE. WE'RE COMING. OVER..."

and stuff like that. You could have conversations during
the game!! And you could chose which person to talk to as
well. No music - that would spoil the atmosphere. Cool.
```

Sure, it seemed like a good idea at the time, but as any _Call of Duty_ player can attest, the only thing microphones have brought to gaming is the ability for anonymous twelve-year-olds to call me a variety of slurs I simply can't repeat here.

Just like the Hindenburg, so too did the plans for "SWAT" begin to slowly crash and burn, with my interest waning and the diary transforming into an often-cringeworthy fest of teenage angst.

```
Seriously though, would I read this diary 20 years on and find it
funny, or would I be disturbed by it? Think I wouldn't even be alive
in 20 f^cking years time to read this baby. Really.
Man, me at 37. Now there's a thought. Would I be married? Hardly. Who
would marry me? And where would I meet them? So what would I be doing? 
Working in the IT industry? Somehow I have my doubts bout that. Can't 
rely on my parents for ever. My life is just a waste. NO.
```

Hah-hah, _JOKE'S ON YOU_ 17-year-old me!

...

...... well, shit.

It wasn't all lost dreams and skipped opportunites, mind you. Oh no. I did make some games. Five of them, in fact. And after looking back on them, well, maybe it was for the best that I didn't end up in the business after all.

## The Grod saga

My first three games were all terrible text adventures based upon a pre-existing Commodore 64 game named [Grod the Demented Pixie](https://www.youtube.com/watch?v=RygiuANd50o). Actually, calling them _text adventures_ might be a stretch.. they all largely involved a series of picking random action choices (A, B or C), one of which was going to be the correct answer, with the other two leading to **GAME OVER**. No clues were given as to the correct answer, and most of the time it was just things that a 14-year-old would find cool or funny. As in the following examples taken from **Grod 3**:

{{< carousel name="grod3-carousel" items="1" height="500" unit="px" duration="7000" >}}

Take note of that `I came up with everything else in all the Grod games` bit in one of the screenshots.. we'll be returning to that shortly.

At the time I was pretty proud of my creations, crude as they were. But one fateful day at school, Tony - my good friend and coding rival from [part one](../failed-game-dev-1/), operating under his "company" persona of  **BISHTRONICS** - gave me a disk containing a solitary file. When I got home, I inserted the disk and inspected the contents. It was that moment that the world changed.

```
C:\> DIR A:\

Volume in drive A is QBASIC
 Volume Serial Number is 1234-5678

 Directory of A:\

GROD4    BAS       49,345  10-15-94  12:34p

        1 file(s)     49,345 bytes
        1 dir(s)      1,280,720 bytes free
```

**GROD4.BAS**...

Tony had gone and written an unofficial sequel to my precious babies.

I loaded it up, and my jaw dropped. It featured something the other Grod games didn't.. actual animated graphics and sound!

{{< carousel name="grod4-carousel" items="1" height="500" unit="px" duration="7000" >}}

At the time, this was the most amazing thing I'd ever seen. Yes, even more amazing than _Robocop_. My mind was blown. I _should_ have been flattered. In hindsight, I absolutely am. But this was _such_ a step up from my own dismal creations that, in the moment, I couldn't see it as anything but a reinforcement of my perceived lack of technical prowess.

I stewed over it before landing upon my response - to spend the next few weeks tirelessly writing what I hoped would be the ultimate Grod game, **Grod 5**. A returned volley; one that would be game-set-match **BARGOSOFT**.

At this point, though, I would like to take a brief tangent. We need to talk about drawing graphics in QBasic with the `DRAW` function. It's one of the most mind-numbing things one can ever hope to do. It's full of statements like:

```
DRAW "BL200 bd100 r50 u60 r300 l250 g50 e50 r250 u20 ....."
```

that draw each line pixel by pixel. I couldn't even tell you what the above does anymore, but I vividly recall the endless repetition of tweaking `DRAW` statements, running code to see if it looked alright (it wouldn't), rinse and repeat. But hell, it was a sacrifice worth making: my reputation - **BARGOSOFT'S** reputation - was on the line here, so if it meant nights of sitting there manually creating terribly simple graphics line-by-line, then so be it.

Suffice to say, Grod 5, like all the other games, pretty much sucked. Although it featured such gameplay additions as secret rooms (_during "A,B,C" prompts, you needed to type a phrase that no-one in their right mind would type without looking at the code itself_), and non-linear progression (_you can go via the left door.... or the right door..!_), it was still the same crusty old Grod underneath. So bad, in fact, that when replaying it for this blog and dying for the umpteenth time, I gave up on trying to beat it at all.

{{< carousel name="grod5-carousel" items="1" height="500" unit="px" duration="7000" >}}

As 1994 began to draw to a close so too did my three-year career in QBasic programming, taking with it my desire and patience to write these terrible games. And so, during the warm summer months, I authored my last hurrah: _Snake Stone : Death of a Galaxy_.

## The apex of creation

Spanning around 2500 lines of code split into three separate files, _Snake Stone_ (yes, a parody of [Blake Stone](https://en.wikipedia.org/wiki/Blake_Stone:_Aliens_of_Gold)) was the Grod-style of "A,B or C" text adventure gaming pushed to its limits. Or at least, the limits of my patience. A long introduction sequence, frequent graphical interludes.. I spent far, far too much time on this baby.

And yeah, it still pretty much sucked.

{{< carousel name="snake1-carousel" items="1" height="500" unit="px" duration="7000" >}}

There was also a _Snake Stone 2_ planned, but I only managed to write the introduction sequence and the first "A, B, C" question:

{{< carousel name="snake2-carousel" items="1" height="500" unit="px" duration="7000" >}}

I think once I got to that point, I realized that it was about time I invested my efforts in something other than giving a piece of crap a new coat of paint.. like, playing _Duke Nukem 3D_ for instance. 

Yeah. 

That'd do just fine.

And on that note, this two-part epic on 90s teenage nerddom draws to a close.

## Epilogue

Before BISHTRONICS and BARGOSOFT eventually crumbled into nothingness, a third competitor emerged. Word had spread through the nerd playground that Todd - the IT teacher's son - had written games the likes of which no-one had ever seen anyone write before.

We were immediately skeptical, and begged to see what these games were. When he finally showed us, our jaws dropped. He'd written an air hockey game with actual VGA graphics, smooth animation and SoundBlaster sound. I imagine we were feeling something akin to what the developers of [Awesome Possum](https://en.wikipedia.org/wiki/Awesome_Possum..._Kicks_Dr._Machino%27s_Butt) must have felt after seeing _Sonic the Hedgehog 2_. 

Or.. y'know.. how I felt seeing `GROD4.BAS`.

Convinced that he couldn't have made it himself, when we next were over at Todd's house for a party, both BISHTRONICS and BARGOSOFT decided to join forces to launch a corporate espionage attempt at finding out our new rival's secrets. When the moments presented themselves, we hunted for anything that might clue us in. Source code, software, you name it.

I don't honestly know if Tony saw it, but in my mind I can still clearly recall the moment that I did.

What did I spot, brooding hulkingly in his bedroom?

A copy of Andre LaMothe's _Tricks of the Game Programming Gurus_.

Why hello there, palms! Please meet my face. Repeatedly.

The end.

## Epilogue of the epilogue, and a tease of what's to come

As I tidy up this blog for republishing on my personal site, almost thirty years have passed since those wild QBasic days. That in itself seems unfathomable.

I do, however, continue to see echoes of the silliness myself and Tony got up to in the modern day. There's an endless flood of indie trash uploaded to Steam every month written by teenagers who figured out how to do something creative with their PC, stuffed it full of inside jokes, and decided to upload it for shits'n'giggles. So it'd seem some things will never change.

Republishing this blog has been worth it for at least one reason beyond simply huddling under comfortable blanket of nostalgia. Tony, whom I'd fallen out of contact with since high school ended, somehow stumbled upon Part 1 of this blog a couple of years ago and reached out. He took it all in good humour, and hopefully he'll do so with this one as well. So that's cool!

I'm also pleased to note that **Grod's** adventures didn't end in 1995 after all. What exactly does that mean? I guess you'll have to wait until the next part to find out.. and hopefully not quite as long.

{{<disqus>}}