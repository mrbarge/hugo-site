---
title: "To BRBEATLP.958 and beyond (part 2): Learning the family tree"
date: 2020-08-09T16:51:52+10:00
draft: false
categories:
  - Coding
tags:
  - retro
thumbnail: "/img/mods2thumb.png"
resources:
- name: header
  src: images/soundtracker.png
- name: usenet
  src: mods-2/mods2usenet.png
images:
  - https://bargenqua.st/img/mods2thumb.png
image: https://bargenqua.st/img/aoc-2019.png
---

## The big four

One of the fascinating aspects of tracker music is the way in which it has evolved over the last three decades. A whole ecosystem of music creation tools grew from the homebrew efforts of talented programmers and musicians. Composition programs were born, forked, cloned, abandoned and reborn. File formats, too, were devised and revised - and sometimes even documented. Composers migrated from tool to tool as successive programs presented them with more sophisticated abilities to realize the music in their head. 

To say that one is a fan of 'tracker music' becomes a hard thing to clarify when there's such diversity about what that could represent. It extends beyond the music itself to the way it is constructed and presented to the listener. An MP3 may hold many minutes of great music, but offers no insight into how that music came to be. A tracker module lays its proverbial heart on its sleeve and bares those secrets for all to study and learn from. The listener of a tracker song is not only presented with the very notes and articulations that construct a song, but may choose to do so with the very instrument from which it was born. 

The open-source nature of this music therefore made it very amenable to satisfying the curiosity itch that I held about sampling (see [Part 1](../mods-1/) for more about that) - whilst simultaneously making that task quite challenging. There are plentiful file formats which collectively form "tracker music", and not all of them are what I'd personally call _rigorously documented_. And whilst several open-source solutions already exist for parsing them, part of my motivation for this task was to peek behind the curtain and learn more about these formats I'd held dear. I'd long held a desire to write my own module player one day, and whilst I'm now old enough and busily-employed enough to know that dream will likely never become a reality, I still wanted to at least get _partly_ there by writing any of the code I'd need to pluck the samples from these files.

For this task, I therefore selected the four formats that I felt were the most representative of the collective tracking library, and which coincidentally aligned with my own personal history as a listener:

- MOD files 
- S3M (ScreamTracker) files
- XM (FastTracker) files
- IT (ImpulseTracker) files

Why these four formats? Well, before we get into the journey about writing parsers for them, I felt it was worthy to go on a trip down memory lane and reminisce about how they came to be.

## Thunderstruck

It may be a bit ludicrous to believe that a freak lightning strike may be responsible for the birth of an entire subculture. Nevertheless, it was indeed a storm's fury that fried the circuits of German programmer/composer [Karsten Obarski's](http://www.vgmpf.com/Wiki/index.php?title=Karsten_Obarski) Commodore 64 one evening in the mid-to-late 1980s - an event that led him to purchase an [Amiga 1000](https://en.wikipedia.org/wiki/Amiga_1000) as a replacement computer.

Frustrated by the way in which many Amiga games would present their music as just a few long samples (here's a [looped 6 seconds of "Bad Cat" music](https://www.youtube.com/watch?v=9HflG8CZDxo) as evidence), Obarski set about trying to improve matters. He devised a means by which he could score longer musical themes without blowing the system's disk or memory constraints by sequencing smaller individual instrument samples instead. This system would ultimately form his tool [Soundtracker](https://trackerbase.blogspot.com/2014/01/ultimate-soundtracker.html), which birthed the concept of tracker music (and ".MOD" files) as we know it today. Looking at _Soundtracker_ now, three decades removed, you immediately recognize some of the hallmarks of just about every tracker interface to emerge since its release. Most notable among those features is its quintessential piano-roll presentation of sound channels and notes programmed into those channels, which any tracker musician will feel right at home with. 

{{< figure src="images/soundtracker.png" link="images/soundtracker.png" caption="The most charming part is the 'LENGHT' typo" width="300x">}}

What happens from there is something of a blur. The [Wikipedia entry](https://en.wikipedia.org/wiki/Ultimate_Soundtracker) states that Obarski gave or sold the rights of _Soundtracker_ to a software company named EAS, where it would be later commercially released. Many articles, including the Wikipedia page for _Soundtracker_, glean their history from [this retrospective](http://www.textfiles.com/artscene/music/information/karstenobarski.html) written in 1998 and readily available on [textfiles.com](https://www.textfiles.com). In doing my research, it was certainly one of the first pages I found, and I took it as fact. I later stumbled upon [a plea by the article's author](http://eab.abime.net/showthread.php?t=70465), made some sixteen years later, admitting that the article contained major factual errors - a regrettable circumstance, given that so many other sources now cite it as an authoritative piece on the topic. There's even doubt thrown on the claim that the software was commercially released at all. And yet, several years later still and on the very same forum, someone [presented photographic evidence](http://eab.abime.net/showthread.php?t=83343&styleid=4) that retail copies did indeed exist..

{{< figure src="images/soundtrackerbox.jpg" link="images/soundtrackerbox.jpg" caption="A SoundTracker box, in the wild." width="300x">}}

What we _do_ know is that Soundtracker was almost immediately cloned, cracked and distributed in various different guises, with [this timeline](https://www.exotica.org.uk/wiki/Soundtracker_History) giving an indication of just how splintered the program became. These sibling versions would receive their own feature additions and bug-fixes, becoming a mainstay for music players in the burgeoning Amiga demoscene. And whilst the commercial _Soundtracker_'s development would eventually cease in 1990, the pace of tracker development by scene groups marched on. The coming two years would see the birth of several other attempts by hobbyist scene developers to create their own trackers, including three notable titans of the early Amiga tracking scene: NoiseTracker, ProTracker and OctaMED. 

To document the evolution of those programs and their featuresets would be an article in itself, and one I'm not equipped to do a capable job of, having not 'been there' to witness it. I instead would highlight [this Usenet post](https://groups.google.com/d/msg/comp.sys.amiga.audio/SKcZed7isZ4/rVfq7XsGYeAJ) I found on `comp.sys.amiga.audio`, which provides at least one tracker's personal perspective on the state of things circa 1991. Whilst mining Usenet for these sort of posts, it was also fun to find the occasional early forms of "tracker wars" as posters argued about eachother's preference in programs. At least in 1991 people were a tiny bit more polite when compared to the Twitter threads of today.

{{< figure src="images/mods2usenet.png" link="images/mods2usenet.png" caption="Usenet threads: a more civilized argument, for a more civilized age.." width="300x">}}

## The PC era arrives

At this juncture, it is perhaps a fitting moment to introduce the sterling work of the [Tracker History Graphing Project](http://helllabs.org/tracker-history/), which has catalogued and visualized the evolution of every iteration of tracker software since _Soundtracker_'s very beginnings. Take a deep breath and prepare your mouse scroll wheel before you gaze upon [the almighty timeline graph](http://helllabs.org/tracker-history/trackers.svg). The years of 1988 to 1990 suddenly seem positively _plain_ compared to what was to come.

{{< figure src="images/trackerhistory.png" link="images/trackerhistory.png" caption="This is just years 1990 and 1991 in tracker history, alone!" width="300x">}}

As the PC demoscene began to usurp the Amiga's, tracker software would similarly make the architectural leap. _Scream Tracker_, developed by Sami Tammilehto of the legendary demogroup [Future Crew](https://en.wikipedia.org/wiki/Future_Crew), would become an early PC tracking staple by 1992. "Rival" scene group Triton would soon follow with _FastTracker II_ in 1993. Towards the end of 1995, Australian developer Jeffrey Lim would release _Impulse Tracker_, and its familiar user interface meant that many trackers who'd spent years working with _Scream Tracker_ could migrate over in the blink of an eye.

{{< figure src="images/impulsetracker.png" link="images/impulsetracker.png" caption="I can't contemplate how many hours I've started at this interface." width="300x">}}

The release of _Impulse Tracker_, in particular its v2.x branch, makes for some interesting observations about its initial acceptance within the community. _Impulse Tracker_ introduced numerous features that made it an incredibly powerful tracker, and one of them was the inclusion of a feature called [New Note Actions](https://wiki.openmpt.org/Manual:_Instruments#New_Note_Action). This allowed composers to determine what happened to existing playing notes when a new note in the channel occurred - a very appealing feature that could allow notes to fade out gracefully (delegated to a background channel) without needing to dedicate a whole channel to managing it. 

This new ability [sparked some debate](https://groups.google.com/d/msg/comp.sys.ibm.pc.demos/L7cQA1kvXPY/Y5BSSkFN60QJ) in the community. Whilst some were happy that such a commercial-quality feature had come to a free utility, and were excited about the ways in which they could integrate it into their music, others had concerns. Some were worried about the performance impact this would have on the hardware at the time. The [Gravis Ultrasound](https://en.wikipedia.org/wiki/Gravis_Ultrasound) sound card - once considered _the_ card for tracking - was going to struggle with New Note Actions - and this meant that composers couldn't be assured that their song would be heard 'correctly' by its listeners. Some argued that the feature even made for "wasteful" and "lazy" tracking, as the skill in juggling a constrained number of channels was less of an issue when you suddenly had 128 at your fingertips. 

That subject of "technique" would generate its own separate debate when tracker archive sites like [hornet.org](https://hornet.org) and [Trax in Space](https://www.traxinspace.com/) began to offer the community to publically rate tracker songs. Discussion stirred around what constituted the 'worthiness' of a high ratings. Should an amazing song with average technique be considered at the same 5-star level as a song with incredibly demonstrated tracking skill? Or should it just be all about the music? You might think, twenty-five years removed, that it's not a big deal. But at the time, such debates raged for months in weekly newsletters such as [TraxWeekly](https://resources.openmpt.org/traxweekly/). 

These three programs largely ruled the PC tracking scene through the decade, though the arrival of Windows 95/98 saw several other projects try to bring tracking to Microsoft's new graphical OS - [Psycle](https://trackerbase.blogspot.com/2014/02/psycle.html), [MadTracker](https://trackerbase.blogspot.com/2014/02/madtracker.html) and [Noisetrekker](https://trackerbase.blogspot.com/2014/02/noisetrekker.html), to name but a few. However, it would be remiss not to highlight [Jeskola Buzz](https://en.wikipedia.org/wiki/Jeskola_Buzz) in the late 90s, a tracker that took a markedly different approach to composition, one that seems more akin to the way modern DAWs will chain together effects and instrument plugins. The buzz around Buzz steadily grew, but in October 2000 updates to the program abruptly ended - the developer had suffered a hard disk crash and lost the entire source code. An [attempt to create Buzz 2](http://web.archive.org/web/20010208103601/http://www.jeskola.com/nettest/) languished to eventual abandonment, and as far as everyone was concerned, Buzz was dead. That is, of course, until the developer suddenly and unexpectedly reappeared with a new version six years later in June 2008. Though it's seen no further updates since 2016, there are many composers who swear by Buzz.

{{< figure src="images/jeskolabuzz.png" link="images/jeskolabuzz.png" caption="Jeskola Buzz allowed for complex routing between different sound generators and effects." width="300x">}}


It is important to remember that the vast majority of all of these programs were free* and in the public domain. Not only that, they were exceptionally _usable_ - certainly enough for a young kid like me to figure out how to make a song with no tutorials or documentation. Even now, FastTracker II just looks [plain gorgeous](https://en.wikipedia.org/wiki/FastTracker_2#/media/File:FastTracker_2_screenshot.png). But one would probably expect nothing less from demoscene coders who worked hard to extract every ounce of capability from home computers. It's a pretty potent recipe: pride in one's work, fueled by the scene's competitive one-up-manship, with just a hint of bravado and arrogance thrown in for good measure.

> *FastTracker II politely asked that you mail $20 to register a copy and be officially recorded as a contributor. Add whilst Impulse Tracker was offered for free, users could donate money to purchase a plugin that would allow it to output .WAV files in stereo. Neither program was crippled by not paying.

## The modern era

Nowadays, [Renoise](https://www.renoise.com/) and [OpenMPT](https://openmpt.org/) carry the torch for modern trackers authorship, but they're by no means alone in the field. There's also specialized branches of trackers such as [FamiTracker](http://famitracker.com/), that target the specific hardware sound engines of old systems. 
We're even about to see a hardware-based tracker in the form of the [Polyend Tracker](https://polyend.com/tracker/), something which I have to continue to talk myself out of pre-ordering every single day.

{{< figure src="images/polyendtracker.png" link="images/polyendtracker.png" caption="The Polyend Tracker, looking ridiculously cool." width="300x">}}

Music-wise, [ModArchive](https://modarchive.org/) and [Scene.Org](https://files.scene.org/browse/music) remain a massive repository of tracker music, with the former still seeing near-daily uploads. The recent PC FPS throwback title _Ion Fury_ committed to its retro aesthetic by offering a soundtrack [composed in a FastTracker II clone](https://3drealms.com/devblog/dev-blog-4-music-ion-maiden/). And last year, one of my favourite tracker musicians from the 90s, [Hunz](https://hunz.bandcamp.com/), streamed his [entire process of recording an album](https://www.youtube.com/c/Hunzmusic/videos) using Renoise. 

{{< figure src="images/renoise.png" link="images/renoise.png" caption="The modern day Renoise, some 30+ years after SoundTracker." width="300x">}}

So why are people still tracking? I guess, for one, there's something about the artificial constraints that tracker music imposes that can attract modern composers. Far from the limitless boundaries of DAWs like _Ableton_ and _Logic Pro_, the four-channel construct of a classic MOD tracker forces a composer to be brutally economical; to make every tick of every pattern in every precious channel count. The challenge is daunting, but the results when they come together are all the more impressive for it. 

For some, the simplicity of the format is a boon as well. To the unknowing bystander, the scrolling patterns of a tracker piano roll may look like the [cascading symbols of Matrix code](https://geekprank.com/matrix-code-rain/) as they flow by, but a tracker will instantly be able to intuit what everything means. I recently enjoyed [The Retro Hour](https://theretrohour.com/) podcast's [recent interview](https://www.youtube.com/watch?v=5Amt23x9rYc) with chiptune author cTrix, who lightheartedly noted the following about modern DAWs:

> _"To me it looks like you're in absolute noodle-land when you've got VSTs all over the place. I'm like, how do you work like that when you can't just see everything that's happening within five centimetres of your screen?"_

As we've seen, the tracker scene has been defined by the passion and talent of so many individual efforts. And yet, one may still wonder what Karsten Obarski may think about everything that has transpired since he first built _Soundtracker_ back in 1987. Truthfully, we might never really know. As best I can tell, Obarski has long since left the scene he helped to create, and his Internet presence is next to non-existent. In one of the [last public interviews](http://www.bitfellas.org/e107_plugins/content/content.php?content.211) with him that I could find, he had the following advice for the programmers of trackers in his wake:

> "_Just try to find new ways by yourself, and do not spend so much time making the same things others have done before you._"

## Next time

In the next part of this series, we get down to the business of fingerprinting the samples of every tracker file in existence - but not before learning what the heck a "parapointer" is through the aid of old 90s text files.

## Resources

Credit goes to the following resources which helped me learn or remember some of this history:

- [Interview with Karsten Obarski (1992)](http://www.bitfellas.org/e107_plugins/content/content.php?content.211) 
- [SoundTracker history](https://www.exotica.org.uk/wiki/Soundtracker_History)
- [The Tracker History Graphing Project](http://helllabs.org/tracker-history/)
- [A Guide to Soundtracker and Clones](https://groups.google.com/d/msg/comp.sys.amiga.audio/SKcZed7isZ4/rVfq7XsGYeAJ)
- The [comp.sys.ibm.pc.demos](https://groups.google.com/forum/#!forum/comp.sys.ibm.pc.demos), [comp.sys.amiga.audio](https://groups.google.com/forum/#!forum/comp.sys.amiga.audio) and [alt.music.mods](https://groups.google.com/forum/#!forum/alt.music.mods) newsgroups.
