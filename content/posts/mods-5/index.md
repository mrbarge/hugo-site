---
title: "To BRBEATLP.958 and beyond (Epilogue)"
date: 2021-02-10T20:22:00+10:00
draft: false
categories:
  - Coding
tags:
  - retro
thumbnail: "/img/mods5thumb.png"
images:
  - https://bargenqua.st/img/mods5thumb.png
---

## The story so far

In order to explore the origins and prevalence of a personally-beloved drum loop sample named `BRBEATLP.958`, I fingerprinted and catalogued every sample of every MOD/S3M/XM/IT file in the Mod Archive so that I could hunt it down amidst tens of thousands of different songs. Now that we've solved that mystery, let's wrap this up with an excursion through that data! 

Disclaimer: I've done the best I can to clean the data I gathered and ensure its accuracy, but I'm not going to stake any rigorous claims of perfection against it. So, you know, just take all of this for what it's worth!

- [Part one](../mods-1)
- [Part two](../mods-2)
- [Part three](../mods-3)
- [Part four](../mods-4)

## What were the ten most-used samples?

Across all IT, XM, MOD and S3M files in the [ModArchive](http://modarchive.org) torrents:

**Number 10** is a tom drum, known in many sample names as `Dr_Tom`.

{{< audio wav="./audio/10.wav" >}}

**Number 9** is a closed hi-hat, most commonly named `C-HIHAT.1`.

{{< audio wav="./audio/9.wav" >}}

**Number 8** is a cymbal crash! No real clues as to the origin of this one.

{{< audio wav="./audio/8.wav" >}}

**Number 7** is `POPSNARE2` from the `ST-01` sample pack.

{{< audio wav="./audio/7.wav" >}}

**Number 6** is another cymbal crash! Again no clues here. Its most common name is `CYMBAL.9`.

{{< audio wav="./audio/6.wav" >}}

**Number 5**, coming in at 126 bytes, is a simple chip lead.

{{< audio wav="./audio/5.wav" >}}

**Number 4** is the staple of many tracks, the open hi-hat. Its most common samplename is `O-HIHAT.1`, so I'm guessing it's the sibling of our #9 entry.

{{< audio wav="./audio/4.wav" >}}

**Number 3** is a bassier chip lead, a paltry 48 bytes long. 

{{< audio wav="./audio/3.wav" >}}

**Number 2** is a closed hi-hat, which many samplenames point to as `HiHat2` in the `ST-01` SoundTracker sample pack.

{{< audio wav="./audio/2.wav" >}}

And the **most popular** sample, used in 1,592 different modules - and which I would have _never, ever_ guessed - is the quintessential ingredient to many musical transitions: the reverse cymbal!

{{< audio wav="./audio/1.wav" >}}

## What were the biggest samples?

The biggest sample I found in a mod was [Falseheart](http://modarchive.org/index.php?request=view_by_moduleid&query=149416), although it's reasons are fairly explainable, as it's a large vocal track that accompanies the music.

The song with the next largest sample, and definitely the more gratuitous of the two, was [ggbb.xm](http://modarchive.org/index.php?request=view_by_moduleid&query=177472), which has a sample consisting of the *entire* 3 minutes of the 1994 Finnish Eurovision Song Contest entry, ["Bye Bye Baby"](https://www.youtube.com/watch?v=XOT4BGgktAc) by *CatCat*. And then proceeds to only use the first 20 seconds of it!  Which is, I guess, better than [zedfox_-_classic.xm](http://modarchive.org/index.php?request=view_by_moduleid&query=179699), a remix of [Megalovania](https://www.youtube.com/watch?v=c5daGZ96QGU) which contains a huge portion of [Dragster 5k](https://www.youtube.com/watch?v=zhsQ3gnck_c) and proceeds to not use it at all.

## Purple Motion or Skaven?

Which of these two legendary [Future Crew](https://en.wikipedia.org/wiki/Future_Crew) alumni are mentioned the most in sample texts?

Well, the results are so close that I think we're going to have to just call it even:

Skaven: 415 times.

Purple Motion: 400 times

(and yes I did include skipping the space, as well as their real names)

## What's the most common sample name?

The most common sample name - with 7,429 matches - was rather the confusing ` ntitled` (including the space).

Initially I was thinking this must have been a bug in my extraction code, but after not finding that phrase anywhere in my code - and verifying the presence of it in mod files with a hex editor - I was left a bit bewildered and started looking for an explanation.

It turns out this was very likely the result of a bug in the OpenMPT tracker which had an Impulse Tracker handling bug [fixed in v1.19](https://openmpt.org/release_notes/History.txt):

```
Garbage characters in sample / instrument / song names should be gone now. 
This should e.g. avoid sample names like " ntitled" turning up in modules 
after deleting sample names.
```

So, if we ignore that entry, what's the next most common sample name? With 4,783 matches, that would be, err.. `NoName`!

Now, whilst my suspicions are high that it's a similar situation of a program inserting that value as a default, I couldn't find a culprit. So if we take a look further down the list, our third most popular sample name is... *cue drum roll*... the very same instrument responsible for the drum roll! That's right, it's `SNARE`.

## The obligatory word cloud

So above we were considering unique sample names as the content of the entire field. What do we get if we run a word cloud generator over every individual word found in the sample texts? Well, you get something like this:

{{< figure src="images/wordcloud.png" link="images/wordcloud.png" >}}

I guess bass rules the world, and I'm all for it.

## The "album art"

The sample text space lets some trackers get a bit creative with their visually artistic side, so it's not uncommon to find a few fun displays of ASCII art flair. So to sum up this epilogue, let's celebrate a sprinkling of what I found whilst perusing the sample texts.

{{< gallery-slider dir="/img/mods-5/asciiart/" width="400px" height="750px" >}}

Will there be more to come after this? Well, probably not, unless I get some other bright ideas of what to do with this data (let me know if you've got some of your own!). I've certainly had a lot of fun with this series and I hope it was equally as enjoyable to read.