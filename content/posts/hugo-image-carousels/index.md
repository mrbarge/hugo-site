---
title: "Reusable image carousels in Hugo"
date: 2025-03-11T20:45:14+10:00
draft: true
categories:
  - Coding
tags:
  - hugo
  - web
thumbnail: "/img/carousel-thumb.jpg"
images:
  - https://bargenqua.st/img/carousel-thumb.jpg
image: https://bargenqua.st/img/carousel-thumb.jpg
draft: false
---

I wanted to be able to display multiple different image carousels within a single Hugo blog. Here's a little hack I made to an existing Hugo image carousel implementation that let me achieve that.

<!--more-->

In searching around for a good image carousel implementations suitable for Hugo blogs, my searches frequently pointed back to [this site right here](https://hugocodex.org/add-ons/slider-carousel/). And it is indeed a good one, so kudos to the author! However, it had one main flaw that made it unsuitable for my purposes - I wanted multiple carousels, each with their own set of distinct images.

The [site's](https://hugocodex.org/add-ons/slider-carousel/) implementation had a hard dependency on a carousel yaml file named `carousel.yaml`, which is where all the carousel images are defined. I wanted to be able to have a Hugo shortcode that let me define the name of the carousel as a parameter, and then look up a yaml file named accordingly.

So if you've arrived here via searching for a similar thing, read on! Here's what I did.

My main change was to modify the `layouts/shortcodes/carousel.html` file to be this, instead:

```html
{{ .Scratch.Set "height" (.Get "height") }}
{{ .Scratch.Set "unit" (.Get "unit") }}
{{ .Scratch.Set "ordinal" .Ordinal }}
{{ .Scratch.Set "items" (.Get "items") }}

{{ $carouselName := (.Get "name") }} 
{{ $carouselData := index .Site.Data (print $carouselName) }}

<div id="carousel{{ .Ordinal }}" class="carousel" duration="{{ .Get `duration` }}">
    <ul>
      {{ range $index, $slide := $carouselData.images }}
        <li id="c{{ $.Scratch.Get "ordinal" }}_slide{{ add $index 1}}" style="min-width: calc(100%/{{ $.Scratch.Get "items" }}); padding-bottom: {{ $.Scratch.Get "height" }}{{ $.Scratch.Get "unit" }};">
          <img src="{{ $slide.image }}" alt="" />
          <div><div>{{ $slide.content_html }}</div></div>
        </li>
      {{ end }}
    </ul>
    <ol>
      {{ range $index, $page := $carouselData.images }}
        <li><a href="#c{{ $.Scratch.Get "ordinal" }}_slide{{ add $index 1 }}"></a></li>
      {{ end }}
    </ol>
    <div class="prev">&lsaquo;</div>
    <div class="next">&rsaquo;</div>
</div>
```

Notably, this part now uses a `name` parameter to load the data from a corresponding `<name>.yml` file into `carouselData`:

```html
{{ $carouselName := (.Get "name") }} 
{{ $carouselData := index .Site.Data (print $carouselName) }}
```

and then we iterate over `carouselData` in the main block:

```html
{{ range $index, $page := $carouselData.images }}
    <li><a href="#c{{ $.Scratch.Get "ordinal" }}_slide{{ add $index 1 }}"></a></li>
{{ end }}
```

Then, in the blog, I can use the shortcode like this:

```pre
<carousel name="my-carousel" ... >
```

and, based on the `name` parameter, Hugo will look for a `data/my-carousel.yml` file to define the images used in that carousel.

It's a small change, but it allowed me to feature multiple carousels on blogs such as [my previous one](../failed-game-dev-2/).

Hope this helps! And, of course, full credit to the original carousel author for their excellent work to pivot off.