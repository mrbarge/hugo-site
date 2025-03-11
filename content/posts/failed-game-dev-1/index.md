---
title: "I was a failed teenage game developer (part 1)"
date: 2022-11-19T12:49:48+10:00
draft: false
categories:
  - Coding
tags:
  - retro
thumbnail: "/img/game-dev-logo-1.png"
images:
  - https://bargenqua.st/img/game-dev-logo-1.png
image: https://bargenqua.st/img/game-dev-logo-1.png

---

> _This blog first appeared in 2008 as a guest article for a friend’s (long since removed) website. To consolidate some of my previous writing in the one place, it has been re-posted with permission, with some edits and lots of additional media added. Think of it like the HD remaster of an old videogame, except it’s a videogame no-one played because it wasn’t very good._

I was a failed teenage game developer. 

But that’s not really what this story is about. It’s just the bait to lure you in.

Sure, there’s going to be a bit of video-game talk. But I could have just as easily titled it “_I was a failed teenage sous chef_”.

You see, this is ultimately the tale of healthy rivalry fought by two friends in the halls and classrooms of a sleepy, country-town high-school during the mid-1990s. 

But before we get there, let's wind back the clock just a few years prior to that.


## Chapter 1: 10 PRINT "THE BEGINNING"

My passion for programming started at a young age, right around the time that my parents introduced a 286 PC into the family. I’d just reached double-digits in age and had somehow stumbled upon the [GW-BASIC](https://en.wikipedia.org/wiki/GW-BASIC) interpreter that came with MS-DOS, allowing me to flex my [10 PRINT BOOBS / 20 GOTO 10](https://www.youtube.com/watch?v=JbnjusltDHk) Commodore 64 programming muscle on a device with an eminently more usable keyboard. Learning the input, output and logic constructs of BASIC naturally led me down the path to creating a text adventure game, one that would be loosely based around a freeware Commodore 64 game I was a fan of named [Grod The Demented Pixie](https://www.youtube.com/watch?v=RygiuANd50o).

The game itself was quite terrible, and only barely qualified as being a text adventure in the strictest possible sense. It (i) contained text, and (ii) at the time, probably did seem like quite the ‘adventure’

The thing I remember most about this game, however, is that it contained a secret. If the player typed in a particular phrase at the input prompt (probably something like `ATARI LYNX RULEZ`) they would be treated to a special hidden message. 

I would come back day after day to pour more words into this secret message, transforming it from a simple "hello everyone this is a secret message!" into pages upon pages representing an epic diary of my simple little 10-year-old life at that point. Some kids kept their personal thoughts and secrets hidden in a diary secured by lock and key; mine would be kept safe in a.. well, a plaintext BASIC file. Sadly, I no longer have the game itself, but for your benefit, I have written what I believe would be a 90%-accurate recreation of what it would've likely contained in one of its many paragraphs.

> _I have been playing Double Dragon 2 a lot today and it is really hard.  If you press punch and kick at the same time Billy does a really cool jump kick it is awesome. It gets really hard at the farm level though and I can't get past it because of all the punk girls with the chains.  Luke says that when you complete it you get a picture of a naked woman which is pretty weird
and I hope my mum does not find out. Anyway it is a good game and I give it 95.7 out of 100 and I hope that they make Double Dragon 3 because that will be even better._

{{< figure src="images/letter-from-tony.jpg" link="images/letter-from-tony.jpg" caption="When I moved towns, my friends and I would exchange letters like this that largely summarized games we'd played." width="400x">}}

A handful of years pass. Our family moved from one town to another, and MS-DOS meanwhile moved from GW-BASIC to [QBASIC](https://en.wikipedia.org/wiki/QBasic). My interests followed suit, if only because QBASIC included the famous `GORILLAS.BAS`, which allowed for surreptitious gaming on the school classroom computers. Now in Year 9 of high-school, I had befriended a guy named Tony after discovering that we held a mutual interest in both computers and the [ABC D-Generation](https://www.youtube.com/watch?v=n42lNEoP5zE). As far as high-school friendships go, ours would grow to be a fairly competitive one. Not out on the track, however.  Ours was a friendship fueled by the fury of QBASIC programming and burgeoning adolescent nerd ego. As the two kids in a small-town high school who seemingly were the only ones that held any interest in programming whatsoever, it was easy for us to convince ourselves that we were _The Best_ at programming as a result. This self-aggrandizing even led us to execute a daring and likely suspension-worthy raid of the teachers’ office at dawn to illicitly acquire some source code - but that’s assuredly a story best saved for another time.

I had just finished reading about billion-dollar maverick Bill Gates' founding of Microsoft, and now had a burning passion to create my own software company offering quality, QBASIC-written wares to.. well, no-one really. The lack of a target audience was hardly a concern. Thus, **BARGOSOFT** was formed on one dreary winter's day in June of 1993. Tony, meanwhile, had created his own 'company', **BISHTRONICS**, founded on much the same principles.

The following months would generate some healthy and fun competition between the pair of us. Each day we would arrive at school, our bags overflowing with boxes of 3.5" disks containing our latest software creations for the other to drool and be jealous over. What started as simple prompt-based applications would gradually evolve to imitate the look and feel of professional, ASCII menu-driven programs like DOSSHELL, LapLink or Microsoft Works.

{{< figure src="images/basic-disk.jpg" link="images/basic-disk.jpg" caption="This repurposed _PC Zone Magazine_ coverdisk from June 1993 contained the only surviving copies of any of my old code, and is largely the reason why this blog can exist at all." width="300x">}}

I still vividly remember the day that Tony had finally figured out how to implement an arrow-key-driven menuing system, complete with highlight bar and drop shadow on the menus. When he showed it to me, I couldn’t believe it was possible in mere QBASIC. All through that day’s lunch-hour I was sitting in stunned silence, trying to figure out how it could possibly be done, whilst bitterly disappointed at myself for having not been the first to figure it out. 

Our competitiveness soon blossomed into all-out war.  We started conducting early-morning assaults upon the classroom computers, unleashing our home built DOSShell replacements upon them, hoping to hear the positive swoons of the teacher when they next turned on the computer - knowing full well how much it would torment the other.

## Chapter 2: The shovelware cometh

The terrible software I invented during that period came thick and fast. There was **Bargosoft Quik-Ad Micro**, which proposed to do the following:

> _Ever wanted to display your own ads for software? This program will create your ad with a touch of colour and style.
Just type in your message after you choose to write your ad. Unfortunately I haven't figured out what to do after that so
you will have to write that section by yourself. Anyway, have fun!_

So ultimately if you typed in your advertisement text, it would display it in the middle of the screen surrounded by flashing, rotating ASCII asterisks. Who needs expensive PR departments when you can harness the raw power of Bargosoft Quik-Ad Micro FOR FREE?

{{< video src="/video/quik-ad-micro.mp4" type="video/mp4" preload="auto" >}}

There was also **Bargosoft Music Manager**, which prompted the user to enter in an octave, tempo, and notes that they wanted played through the PC speaker. The most amusing thing in retrospect about this and many of the other applications is that they all featured huge video-game like introduction sequences, featuring flashy logos and overbearing PC speaker music. If you can imagine being presented with the “20th Century Fox” intro logo every time you started a web browser, you’re close to understanding what the experience was like.

{{< video src="/video/bargosoft-music-manager.mp4" type="video/mp4" preload="auto" >}}

Music Manager itself was quite a stand-out, because not only did it feature the aforementioned logo presentations for an entire _minute_, it also featured a tonne of fake magazine quotes (from equally fake magazines) praising it before it even got to the main menu:

* _A powerhouse achivement!_ - Computer Utility Magazine
* _The best QBASIC utility we have seen so far!_ - PD Monthly
* _Definetly Bargosoft\Heatwave's best effort yet_ - PC Domain
* _Another winner for Bargosoft!_ - PC Upgrading

Then there was also the ill-conceived **Bargosoft Homework Manager**. This thing would ask you what subject the homework was for, what the homework was about, the due date, and any other "relevant information" you might have to offer. What might the program do next, you might wonder? Well, it sure as hell doesn't do the homework for you. In fact, all it does is send the following to the printer:

```
--------------------------------------------------------
**THE BARGOSOFT\HEATWAVE HOMEWORK MANAGER VERSION 1.0**
--------------------------------------------------------
Subject: <...>
Assignment: <...>
Due Date: <...>
Relevant information: <...>
--------------------------------------------------------
Copyright 1994. Bargosoft\Heatwave.
```

How useful! Surely such a program would be the wildest dream of any overworked student looking for assistance in their studies!

{{< video src="/video/bargosoft-homework-manager.mp4" type="video/mp4" preload="auto" >}}
> Content Warning: Contains rapidly flashing colours at the end!

It should come to no surprise that I myself did not use the **Bargosoft Homework Manager** despite having invented it.

There was also the almighty **Number Guess**, which.. well, you probably could figure it out from the title, but you'd not be anticipating the 45-second introduction sequence nor the repeated assertion of how amazing Pink Floyd is.

{{< video src="/video/number-guess.mp4" type="video/mp4" preload="auto">}}
> Content Warning: Contains rapidly flashing colours at the start!

Some of these applications even carried a splash screen containing the inspiring  _Bargosoft Mission Statement_..
 
{{< figure src="images/bargosoft.jpg" link="images/bargosoft.jpg" caption="The 'EDITED FOR SAFETY REASONS' bit was already there. I guess even as a fourteen year old I was paranoid of crazy internet people" width="550x">}}

Anybody willing to send me "a sample of their QBASIC skills" can still feel free to do so, and make me feel even more embarrassed about myself.

Now, the observant amongst you would've noticed the rather curious "BARGOSOFT\HEATWAVE" in some of the earlier screenshots. What's that all about, you might wonder? Well, things are about to get even more delusional from here, so strap yourselves in..

## Chapter 3: The imaginary demoscene

At around the same time that I was churning out shovelware like Quik-Ad Micro, I was beginning to take a healthy interest in the [PC demoscene](https://www.scene.org/).  Mind you, the only exposure I'd had to the demo scene was a collection of MOD files contained on a PC magazine CD-ROM, something I’ve written about in [a prior article](../mods-2). So the only thing I actually understood about the demoscene was that you needed to have a truly awesome name for your 'group'. Therefore, if I wanted Bargosoft to be a QBASIC-powered force to be reckoned with in the elite world of "the 'scene", I would need to give it a suitably awesome 'scene name.

I pulled out a dictionary and started scouring the pages, looking for the perfect word. Something to rival Fairlight.. Future Crew.. Triton..  and so eventually I settled upon the rather dubious title of "HEATWAVE". It didn't take me long to realise that 'HEATWAVE' is a pretty bland name for a demoscene group, so the search resumed for something cooler. For a brief period I decided upon **OPTICAL ILLUSIONS**, but since that was too many letters for me to bother rendering in QBASIC code, I changed it to **ENTROPY**.

{{< figure src="images/entropy.jpg" link="images/entropy.jpg" caption="A cool name deserves a cool logo." width="550x">}}

Of course, what's a demoscene group without demos? With the name taken care of, I then proceeded to spend weeks producing awful, horrid demos, leading to what would be known as the Imphobia series. “Wait a minute!”, a select handful of you might suddenly be crying, “Wasn’t Imphobia the name of an [actual demoscene disk-mag](https://www.pouet.net/prod.php?which=8877)?”. And yes, you’d be right! I don’t even remember what led me to this unsanctioned co-opting of the name; at a guess, it was probably the same sort of motivations that led me to write terrible fan-fiction sequels to *Aliens* and *Child's Play* at around the same time..

{{< figure src="images/aliens-earth-war.jpg" link="images/aliens-earth-war.jpg" caption="I shall spare you the remaining seven pages of this story." width="400x">}}

Before the Imphobia series, however, were some humble beginnings in wannabe QBASIC graphical experiments. The first, GROOVY3.BAS, consisted of an seizure-inducing flashing background whilst the words 'PINK FLOYD' scrolled down the screen in alternating colours. In fact, just about everything I've ever written contains a section where the screen flashes random colours in a blinding manner. Perhaps it shall ultimately be my trademark as an artist once I've passed on.

{{< video src="/video/groovy3.mp4" type="video/mp4" preload="auto" >}}
> The early fruits of my labour. Do I even _need_ to keep on giving the 'flashing colours' content warning at this point?

With my skills sharpened, it was time to move onto a real demo. Rewatching them  now, of course, they almost seem like parodies of what a demo should really be. The first Imphobia consisted of silly, mostly-random PC speaker music that played whilst the screen filled with basic ANSI graphics. Actually that's a half-truth: those two things didn't happen at the same time, since I had no idea how to do any sort of threading like that. So the music would play first, then the screen would fill with ASCII, then another piece of music would play, then something else would happen, and so on. The grand finale was the display of the Bargosoft and Heatwave logos, followed by some embarassing spiel about how awesome public domain software is.

{{< video src="/video/imphobia-1.mp4" type="video/mp4" preload="auto" >}}
> Imphobia #1. A landmark in.. something. 


The next three demos in the Imphobia series weren't much better, just featuring more elaborate graphics. In one of them I even introduced some goofy political point about how religion and nazism leads to nuclear war or something. Who the hell knows what I was thinking; to be honest, the biggest tragedy I can remember from my highschool years was the day I accidentally taped over my VHS copy of _Fraternity Vacation_ with the _Oprah Winfrey_ show.

{{< video src="/video/imphobia-3.mp4" type="video/mp4" preload="auto" >}}
> Imphobia #3. It really should've been called Imphobia 3-D.

{{< video src="/video/imphobia-4.mp4" type="video/mp4" preload="auto" >}}
> Imphobia #4. In 1994, Future Crew released the legendary "Second Reality".  I released.. this.

## In the next part..

Bargosoft Game Studios is founded, but Bishtronics deals it an early crippling blow. Meanwhile, a third competitor - as-yet-unknown to both - arrives to disrupt the local gamedev scene.

{{<disqus>}}