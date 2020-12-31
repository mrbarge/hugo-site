---
title: "To BRBEATLP.958 and beyond (part 3): Parsing ancient scriptures"
date: 2020-12-31T10:27:00+10:00
draft: false
categories:
  - Coding
tags:
  - retro
thumbnail: "/img/mods3thumb.jpg"
images:
  - https://bargenqua.st/img/mods3thumb.jpg
---

## The story so far

Obsessed with the muffled, 8KHz mono perfection of a drum-loop used in an old ScreamTracker III module, I aim to seek out how many other modules may have used the same sample.. but not before some hard nostalgia-blast reminiscing over the tracking subculture as a whole.

- [Part one](../mods-1)
- [Part two](../mods-2)

## Forming the battle plan

First thing's first: if I was to figure out how many other songs might've used `BRBEATLP.958` in them, I needed to get my hands on as many tracker songs as I possibly could.

Back in the day, [hornet.org](https://hornet.org) was _the_ place to go for this kind of thing. And it still exists now, as does [scene.org](https://files.scene.org/browse/music/). But the best place I found to get the most comprehensive snapshot of modules was [modarchive's torrent archives](http://tracker.modarchive.org/) - over 40GB worth of tracker music from the 90s up until today,  constituting well over 130,000 individual songs. The folks seeking those torrents deserve a tonne of thanks for helping to keep this amazing digital archive around and available.

With modules gathered, my next task was a bit more daunting. It wouldn't be enough to simply scan modules looking for samples with the matching name `BRBEATLP.958` - for one, some module formats didn't have a `filename` metadata field for their samples, and there would also be nothing to guarantee that a composer wouldn't have just renamed the sample to whatever they liked (and indeed, this did turn out to be the case.. but more on that later!)

I therefore figured that I'd get the most accurate results for my search by calculating a checksum of the sample, and then looking for any other samples that had a matching checksum. This wasn't going to catch cases where the sample had been converted into a different format or codec (thus altering the underlying data), but it'd be good enough to find the cases where someone had saved the raw sample off and imported it directly into their own song.

Now, the problem with _that_ approach was: how exactly was I going to get a checksum of every sample of every mod in order to figure that out? Well, in lieu of finding any existing ways to do that easily, the immediate answer that came to mind was - write it all myself.

## Adventures in parsing

As noted in part 2, I settled on the four most prevalent formats to work with: ProTracker, ScreamTracker, FastTracker and Impulse Tracker. Fortunately, my goals were somewhat simplified by the fact that I didn't need to write a fully feature-complete parser - I only needed to identify, extract and checksum the samples contained there-in. However, as I'll note later - this was easier said than done in some cases! 

The code for all of this is sitting in a [Github repo](https://github.com/mrbarge/go-mod) - I'm not quite sure it would be useful for anybody except me, but it is nevertheless there. 

### Protracker 

Writing a parser for ProTracker was by far the easiest of the four - and I actually wrote a relatively complete parser for this one, including parsing patterns. This was due in no small part to the format's relative simplicity and the prevalence of good documentation.

In fact, I'd written a good portion of the parsing code quite some years ago as my first foray into learning Golang. As a result, whilst the code was exceptionally terrible, it at least provided an easy jumping-off point for finding and processing the sample data and kickstarted this whole endeavour.

Fun parsing fact: we learned in part two that many tracker programs would extend the mod format in various ways - and one such way of identifying these variants is through four bytes at offset 1080. From one of the documentation specs about its potential values: 

> "The four letters "`M.K.`": these are the initials of Unknown/D.O.C. who changed the format so it could handle 31 samples (sorry.. they were not inserted by Mahoney & Kaktus [1]). Startrekker puts "`FLT4`" or "`FLT8`" here to indicate the # of channels. If there are more than 64 patterns, Protracker will put "`M!K!`" here. You might also find: "`6CHN`" or "`8CHN`" which indicate 6 or 8 channels respectively.
> 
> [1] Developers of [NoiseTracker](https://en.wikipedia.org/wiki/NoiseTracker).

One other gotcha with writing a ProTracker parser is to remember that [endianness](https://en.wikipedia.org/wiki/Endianness) matters - something I hadn't needed to consider since I stopped working on Solaris SPARCs decades ago! Given that the ProTracker format originated on the Amiga, which itself was a big-endian platform, reading multi-byte values had to be done with big-endianness in mind. Doing this gave me _way_ too many painful flashbacks to time spent debugging audio codec libraries as part of my job in the early 00s.

- [NoiseTracker/SoundTracker/ProTracker Module Format](https://www.aes.id.au/modformat.html)
- [mod-spec.txt](https://www.eblong.com/zarf/blorb/mod-spec.txt)

### ScreamTracker

Writing a parser for ScreamTracker III was also relatively straightforward. There's decent documentation and plenty of it. One brief hassle I had was understanding what a "parapointer" was, as they're referenced throughout the fileformat spec as an offset and weren't a traditional byte offset. Turns out that parapointers are offsets where each unit represents a span of 16 bytes - so, to transform it into a byte offset, you'd multiply the value by 16. As best I can tell, the term "parapointer" is one that's wholly unique to ScreamTracker 3 and not something used in wider computer science - but if it does, it must go by a different name. I'd genuinely love to know.

The other tricky bit about parsing this format is that we now have to potentially deal with signed and unsigned sample data. Whilst the data format supports both types, samples in ScreamTracker files are almost always stored unsigned. This will be of importance later.

- [Scream Tracker 3 module: format specification](https://formats.kaitai.io/s3m/index.html) (the block diagram was a great reference)
- [Scream Tracker 3 Module](https://wiki.multimedia.cx/index.php/Scream_Tracker_3_Module)

### FastTracker 2

FastTracker is an interesting format because it's the first one to deal with both instruments and samples. An instrument is like additional wrapping on top of samples which instructs how the samples are played (panning, vibrato, volume), whilst the sample is the same old raw audio data that we're used to.

Now, FastTracker can handle both 8-bit and 16-bit samples. I did write the ability to extract both types, and gathered data on both, but consciously decided to ignore 16-bit samples when searching for `BRBEATLP.958` matches - the original sample was 8-bit mono, so even though it was technically possible that someone might've converted it up to 16-bit when using it in a FastTracker song, I felt it was a pretty unlikely occurrence.

A lot of the challenge in writing the FastTracker parser was just getting the offsets correct. You have to jump around the file quite a bit based on the numbers and sizes of patterns, instruments and samples themselves, all of which can be variable, so it added a small extra layer of complication over the existing formats.

The other catch here was that FastTracker samples are _signed_. I was initially getting confused when FastTracker songs that I _knew_ used `BRBEATLP.958` were not producing the same checksums as their ScreamTracker cousins, and thought that my parser had a bug. In reality, it was because my ScreamTracker checksums were being generated based on _unsigned_ sample data. 

My workaround for this was to convert all ScreamTracker samples into 8-bit signed data before computing a checksum - that way I'd get matching checksums across both formats.

- [The UnOfficial XM File Format Specification](http://www.soma.pirate-server.com/projects/experiments/xm/XM_file_format.pdf)
- [The "Complete" XM module format specification](http://jss.sourceforge.net/moddoc/xm-form.txt)

### Impulse Tracker

Oh dear.. Here's where it got a bit headachy for me, and where I ended up pausing any work on this project at all for a couple of months.

It's not that Impulse Tracker documentation doesn't exist - [it does](https://github.com/schismtracker/schismtracker/wiki/ITTECH.TXT) - but it didn't contain all the information that I needed - and even when following it correctly, I found cases of offsets that were confusingly not in line with what the spec said should be happening (and whilst I'm sure my code could have bugs, I was verifying this by poring over the files through a hex editor). Adding to that, Impulse Tracker can optionally store samples in a compressed form. But details on how this compression scheme works are not in any specification I could find. 

There are other little gotchas as well, for instance, some .IT files may have been created using a FastTracker-to-Impulse Tracker conversion tool which writes some of the file metadata incorrectly. The file format also underwent several revisions as the software progressed, so depending on the file format version you may have to read the file differently.

Whilst many of these problems were probably surmountable, trying to decipher how to write the decompression code for samples was what really became a blocker with my very scarce amounts of free time. 

Since a lot of the hard work on parsing .IT files had already been done with the [OpenMPT player](https://openmpt.org/), I eventually got the bright idea to write a small C++ program that would use [openmpt's .IT parser](https://github.com/OpenMPT/openmpt/blob/553389d97cb61ea8e9acaa40c995e0dc411beb2d/soundlib/Load_it.cpp) to do all the hard work of loading the .IT file correctly, then I could grab and checksum the samples in memory. This worked really well and ended up being my solution here. 

- [ITTECH.TXT](https://github.com/schismtracker/schismtracker/wiki/ITTECH.TXT) - .IT format specification.

### Wait, hang on..

The realization was not lost on me that I could've used the same OpenMPT-based method for _all_ the different types of tracker formats. And yes indeed I could have - and probably would've been able to gather the data with much more accuracy and in less time than it took me via the Do-It-Yourself approach. But for me, this was as much of a learning exercise as it was simply a quest to find the family tree of `BRBEATLP.958`. When I was a teenager, I'd always wanted to write my own tracker audio player, but never found enough time and inspiration to do it. After the efforts spent above.. well, I sure as heck won't be writing one any time soon, but I'm satisfied that I probably got.. hmm.. at least 15% of the way there, let's say.

## In the next entry

All up, these efforts resulted in extracting and checksumming 2,147,369 different samples spread across 135,040 different tracker files.

Did all this result in any amazing insights? How many times was `BRBEATLP.958` used in tracker music? And could anyone except me possibly find any of that interesting?

Well.. I guess that'll all be a tale for the next (and final) blog! Until then - thanks for sticking around.

