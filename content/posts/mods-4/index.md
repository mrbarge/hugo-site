---
title: "To BRBEATLP.958 and beyond (part 4): A mystery solved"
date: 2021-01-01T10:22:00+10:00
draft: false
categories:
  - Coding
tags:
  - retro
thumbnail: "/img/mods4thumb.png"
images:
  - https://bargenqua.st/img/mods4thumb.png
---

## The story so far

In order to explore the origins and prevalence of a personally-beloved drum loop sample named `BRBEATLP.958`, I've fingerprinted and catalogued every sample of every MOD/S3M/XM/IT file in the Mod Archive so that I can hunt it down amidst tens of thousands of different songs. Now it's time to see where this takes us.

- [Part one](../mods-1)
- [Part two](../mods-2)
- [Part three](../mods-3)

## How many songs used `BRBEATLP.958`?

I found fifty-four different songs which all used (or at least included) `BRBEATLP.958`, spread across all four file formats.

More interesting was actually seeing all the unique filenames that had been used to name the sample:

- `DL035.IFF`
- `DRUMLOOP.AIF`
- `RIFF11-1.SMP`
- `1.wav`
- `JUNGLE1.IFF`

to list but a few.

This then made me wonder..

## What was the earliest use of `BRBEATLP.958`?

I, and I'm sure many others, first heard this sample through the song [Point of Departure](https://modarchive.org/index.php?request=view_by_moduleid&query=55696) by [Necros](https://modarchive.org/member.php?69271), because it was a very popular tracker song during the PC scene era.

But, given that the sample had been used by more than fifty songs and with a variety of different filenames, it got me wondering: which module file might've been the first to use it?

_Point of Departure_ was released as part of the musicdisk _Progression_, which has a date of 22 July 1995 in its `file_id.diz`. So we'd be looking for modules written before then. 

Unfortunately, it's hard to pinpoint when many modules were released - especially `.MOD`s as they're typically the oldest. If there's nothing in the song's sample metadata, it's very difficult to ascertain a date unless a web search manages to provide any clue.

So, starting with the list of all .MOD files that used the `BRBEATLP.958` sample, I began to do some searching to see if I could find their individual release dates.

It was then that I discovered..

## Someone's done this already, more awesomely

Searching for the release date of one specific .MOD, I eventually stumbled upon the [.mod Sample Master](https://modsamplemaster.thegang.nu/) site, a fantastic resource where someone has catalogued each individual sample from the archive of .MOD files. We can indeed [find `BRBEATLP.958` on this site](https://modsamplemaster.thegang.nu/sample.php?sha1=4ddfbca0d8f77b30c6578351eb1a5f1bc183b368), under one of the alternate filenames of `DL035.IFF`, and through there we can see the list of `.MOD` files that use the same sample.

Finding this site was great, because it was further validation that my own efforts were correct (all the matches in my dataset were in this site's list!). And it didn't immediately render my existing efforts pointless, because the site is - presently, at least - solely focused on the `.MOD` format. But aside from all that, it also has one other fantastic feature - the _"Similar Samples"_ section. This, as you can imagine, links to other samples which have a close similarity to the one presently being browsed.

Through that feature, I was able to discover [a different sample](https://modsamplemaster.thegang.nu/sample.php?sha1=52ac3dd508b8688fabd7715620522e127d586ca1) - most commonly titled `sl2.brk.beat` - which was used in _many_ more mods than the `BRBEATLP.958` sample. It had roughly 300 bytes difference (out of ~29400), but sounded almost indistinguishable.

Suddenly my focus shifted to this new sample and what discoveries it might bring.

## The `sl2.brk.beat` connection

I immediately searched my dataset for any matches of the `sl2.brk.beat` sample hash. I found 56 additional modules that used that sample - 28 of which were non-`.MODs` - so now I was looking at more than 110 different songs that made use of _either_ sample.

My goal was still the same: to find the earliest use of that sample I possibly could - but more-so, to hopefully find out something about that sample's origins at the same time.

Finding a precursor to _Point of Departure_ came pretty quickly, with many of the `.MOD` files using the `sl2.brk.beat` sample having dates of 1993 or 1994 in their sample text.

Ultimately, the earliest use of the sample I could find was in the song "[Pandemonium](https://modarchive.org/index.php?request=view_by_moduleid&query=158504)" by **Yaz**, which several Internet sites pointed towards having a release date of 1992.

{{<youtube fejUAZ6fuwQ>}}

Later in this blog we'll cover some confirmation that this was indeed _the_ earliest use of this sample in a .MOD file. With that question finally answered, it was time to determine the origin of the sample itself.

## A sample-pack diversion

In my dataset, I'd noticed that a couple of modules named the sample as `ST-31 sl2 brk.beat`. Anyone with a decent interest in the Amiga demoscene will recognize the meaning of the `ST-XX` prefix - it indicates a particular SoundTracker sample pack, collections of which used to be distributed between Amiga tracking enthusiasts back in the day. The first, `ST-01`, was created by Karsten Obarski ([remember him?](../mods-2)) and came bundled with The Ultimate SoundTracker. There's a [nice article](https://chipflip.wordpress.com/2017/02/13/obarski/) I found on that. You can also download [the entire ST-XX collection](https://archive.org/details/AmigaSTXX) from Archive.org.

So, was `BRBEATLP.958`/`sl2.brk.beat` indeed a part of one of these sample packs, and could that be its origin?

Well, to be absolutely sure, I went and listened to every single sample with a filesize between 25000 and 35000 bytes in that Internet Archive mirror, and no.. it was not any of them. I will note, however, that doing this was such an incredible nostalgic flashback. Only with a true relic of the 1990s could you possibly experience the sonic dissonance of two seconds of an Iron Maiden guitar solo followed by a radio jingle for 'Stereo FM' followed by the sound of a laughing baby. I think it would be an _awesome_ project to build a new song nowadays using just the samples in these packs.

```bash
# Using sox/play to play every file in the archive in a certain file-size range..

find . -type f -size +25000c -size -35000c -exec play -r 8000 -b 8 -c 1 -e signed-integer -t raw {} \; -exec echo {} \;
```

This quest was beginning to look like a lost cause, and then, suddenly..

## The answer was right there

Searching on variations of the filename `sl2.brk.beat` eventually clued me in to the existence of a British breakbeat rave group whose name was.. would you believe it.. [SL2](https://en.wikipedia.org/wiki/SL2_(group)).

I spent an _extremely_ enjoyable half an hour listening through the SL2 discography circa 1989-1992 (which one of the group's members had only very recently [uploaded to YouTube](https://www.youtube.com/c/thedjslipmatt/videos)). I heard several breaks that _could_ have been `BRBEATLP.958`, but I wasn't completely sure until I landed upon the song "[The Noise](https://www.youtube.com/watch?v=cHT1KLE5gS4)"..

{{<youtube cHT1KLE5gS4>}}

.. and, right at the 1m11s mark, there it was. Undeniably the beat I'd been looking for this whole time. Attached to a thoroughly excellent tune, might I add.

As if I needed any other reassurance, I would later also find the StackExchange thread "[How did musicians acquire samples for tracker music?](https://retrocomputing.stackexchange.com/questions/15812/how-did-musicians-acquire-samples-for-tracker-music-mod-s3m-xm-and-the-like)" where none other than Yaz himself (creator of Pandemonium) [commented](https://retrocomputing.stackexchange.com/questions/15812/how-did-musicians-acquire-samples-for-tracker-music-mod-s3m-xm-and-the-like#comment53013_15814) on the origins of the samples for that track:

>  We swapped sample disks by post (not many folks had modems then apart from crackers/traders) or we sampled our own from synths or we used sounds from other mods. We also sampled from records from the time (I sampled from the b-side of an SL2 rave track for example for my Pandemonium mod)

So: the sample was created directly from the SL2 record by Yaz and used in his track _Pandemonium_, and subsequently spread out from there. The only unknown is how/why the sample slightly changed from `sl2.brk.beat` to `BRBEATLP.958` - it's entirely possible someone else may have re-sampled the same beat. For my part, I'm happy enough to leave that loose end hanging.

## Some thanks

This whole dumb endeavour wouldn't have been possible without:

- [The Mod Archive](https://modarchive.org/), for its part in digital preservation of tracking music.
- [OpenMPT](https://openmpt.org/) for helping keep the scene alive for musicians young and old, and doing so in an opensource way. I wouldn't have tackled the .IT format without it.
- [The Mod Sample Master](https://modsamplemaster.thegang.nu/), truly an awesome site, without which I may not have made the sample leap I needed to make. 
- [The Internet Archive](https://archive.org), which plays such a _vital_ role in preserving the history of an Internet which is so difficult to find anymore.

They all deserve a big, unknowing thank you. 

## Until next time..?

We've arrived at the end of this adventure, but there's room for at least one epilogue. Since I gathered data across all samples in the Mod Archive, we may as well use it for more than just `BRBEATLP`. In the concluding entry of this series, we'll take some fun excursions through the data and see what interesting things we can find. Like, for instance, what's the most frequently used sample of all time? What's the biggest sample used in a song? And just how many samples have the word 'poop' in their name? 

I don't know when I'll write up that entry, but I hope it won't take quite as long as this one. Until then, thank you for reading.
