---
layout: post
title: "Generating SVG fonts for use with @font-face in TideSDK"
date: 2013-07-25
tags: [CSS3, SVG, TideSDK, fonts, web typography, hacks]
---

*What's inside: how to convert .ttf and .otf fonts to .svg for use with `@font-face` (in older versions of WebKit). Also: the story of why the hell this is a problem I recently had to solve.*

## The Why

In the last few weeks, I've started building a desktop application to display some more useful visualizations of the data generated from my various diabetes devices, particularly the data from my Dexcom continuous glucose monitor. Since I'm building the visualizations with the JavaScript data visualization library [D3](http://d3js.org/ 'D3.js: Data-Driven Documents')[^Demo], I've chosen to build my desktop application with [TideSDK](http://www.tidesdk.org/ 'TideSDK') <span class="aside">[JEB, 2016: TideSDK was supposed to become TideKit until it didn't... ([some discussion of TideKit's dissolution on GitHub](https://github.com/reduxframework/redux-news/issues/59 'GitHub: TideKit discussion')) 😞]</span>, which is a framework for creating multi-platform desktop apps using web development tools---i.e., HTML5, CSS3, and JavaScript.[^Python]

## The Problem

TideSDK is now an open-source project (and an Affiliate Project of [Software in the Public Interest](http://www.spi-inc.org/ 'Software in the Public Interest (SPI) Inc.')), after having been discontinued as a commercial product alongside [Titanium SDK](http://www.appcelerator.com/platform/titanium-sdk/ 'Titanium SDK') from [Appcelerator](http://www.appcelerator.com/ 'Appcelerator Inc.'). One result of this split is that updates have been rather sparse, and so the current version of TideSDK is using a rather old version of WebKit, a version that only supports SVG fonts for loading via the CSS3 `@font-face` at-rule.[^source]

This is a problem because it seems to be quite rare to find SVG fonts for download, at least in the realm of free fonts. [Google Fonts](http://www.google.com/fonts/ 'Google Fonts') doesn't include SVG downloads, and neither does [Font Squirrel](http://www.fontsquirrel.com/ 'Font Squirrel'). So if you don't want to use only the most basic fonts that you can assume are installed on any potential user's system, what can you do?

## The Solution

It's not *that* hard, as it turns out, to convert .ttf or .otf fonts to .svg. A quick Googling brought me to [FreeFontConverter](http://www.freefontconverter.com/ 'FreeFontConverter'), which will transform a font from almost any format you can imagine to a wide variety of output formats, including .svg.

However, after I'd converted a couple of fonts to .svg---one each from Google and from Font Squirrel; one .otf, one .ttf---neither of them worked in TideSDK. At first. It turns out there are two sticky points when it comes to including SVG fonts via `@font-face`.

1. First: The opening `<svg>` tag in the document *must* include the `xmlns` attribute: `xmlns="http://www.w3.org/2000/svg"`. The SVG fonts I generated from other formats using the FreeFontConverter tool didn't include this attribute in the output .svg file. It wasn't until I finally scrounged up one native SVG font file to test load that I noticed this attribute was missing in the converted files.

2. Second: Even if there is only one font defined in the .svg file named (for the sake of example) *file.svg*, the `id` attribute of the `<font>` element must be specified in the `@font-face` at-rule like so:

```css
  @font-face {
    font-family: 'MyFont';
    src: url('../fonts/file.svg#myFont') format('svg');
  }
```

Where the `id` attribute on the `<font>` element in *file.svg* is `id="myFont"`.

That's it! Not *hard*, by any means, but still enough to have caused me a couple of hours of frustration and endless Googling until I figured out these fixes, so I thought I'd share my newfound knowledge for anyone else out there who might run into the same problem(s).

**Next up:** more blood, sweat, tears, and endless Googling in my quest to get TideSDK's Python plug-in working.

* * * * *

[^Demo]: Here's a [demo](http://janabeck.com/iPancreas-archive/examples/html/dexcom-week-by-week.html 'D3 Demo: Dexcom Data Week-by-Week') of one of the visualizations I plan to include in this application.

[^Python]: There are also plug-ins for using PHP, Ruby, and Python in your application's "back end." I'm using the Python plug-in since all my diabetes data-wrangling tools are Python modules.

[^source]: According to [this Stack Overflow discussion](http://stackoverflow.com/questions/14404352/google-webfonts-with-tidesdk 'Google Webfonts with TideSDK'), but confirmed in my attempts to load .ttf and .otf fonts, which worked just fine if I served up my app in Chrome, but failed in TideSDK.