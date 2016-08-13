---
layout: post
title: "How to Use Python in TideSDK. No, <em>really</em>."
date: 2013-07-26
tags: [Python, TideSDK]
---

*Blood, sweat, tears, and endless Googling in my quest to use Python in the "back end" of my TideSDK desktop application.*

## The Backstory

In [my last post](http://janabeck.com/blog/2013/07/25/generating-svg-fonts-for-use-with-at-font-face-in-tidesdk/ 'Generating Fonts for Use with @font-face in TideSDK'), I introduced one of my current projects, which is to create a desktop application to display some more useful data visualizations of the data generated from my various diabetes devices, especially from my Dexcom continuous glucose monitor. I've chosen [TideSDK](http://www.tidesdk.org/ 'TideSDK') <span class="aside">[JEB, 2016: TideSDK was supposed to become TideKit until it didn't... ([some discussion of TideKit's dissolution on GitHub](https://github.com/reduxframework/redux-news/issues/59 'GitHub: TideKit discussion')) 😞]</span> as the platform for building this application.

TideSDK, a splinter project from [Appcelerator](http://www.appcelerator.com/ 'Appcelerator Inc.')'s [Titanium SDK](http://www.appcelerator.com/platform/titanium-sdk/ 'Titanium SDK') mobile development platform, is a framework for creating multi-platform desktop apps using web technologies such as HTML5, CSS3, and JavaScript, with the additional option to include PHP, Ruby, and/or Python in your application's "back end." I've chosen the framework because it seems like the ideal solution for integrating the work I've already been doing in Python to wrangle and analyze the data from my diabetes devices with the power of the JavaScript interactive data visualization library [D3](http://d3js.org/ 'D3.js: Data-Drive Documents').

Despite the fact that TideSDK is a community-driven open-source project with an uncertain future[^TideKit], it seems like a reasonably future-proof platform, in the sense that any code written for TideSDK can be ported to a web application with minimal effort. (In fact, I've been doing all of my development testing in Chrome as well as in TideSDK.) However, figuring out how to *actually* incorporate Python into my application has been quite a challenge, but I've finally succeeded, and so I'm writing this for anyone who may run into similar troubles.

[^TideKit]: [Recent events](https://twitter.com/tidesdk 'Twitter: @TideSDK') [on Twitter](https://twitter.com/tidekit 'Twitter: @TideKit') <span class="aside">[JEB, 2016: More broken links...]</span> have everyone confused, but seem to indicate that TideSDK will soon be taken over(?)/merged with(?)/rebranded as(?) [TideKit](http://www.tidekit.com/ 'TideKit') <span class="aside">[JEB, 2016: and again a borked link]</span>, a platform for simultaneous mobile, web, *and* desktop development.

## The Problem

The root of my difficulties incorporating Python into my application were not with TideSDK itself, but rather with its documentation[^docs]. According to [TideSDK's guide to including Python in your application](http://tidesdk.multipart.net/docs/user-dev/generated/#!/guide/using_python 'Using Python in TideSDK'), there are a couple of ways to incorporate Python code, after including the Python module in your app's manifest[^manifest]. First, according to the documentation, you can include Python using `Titanium.include("test.py");`. Unfortunately, this was the result: `ReferenceError: Can't find variable: Titanium`.

*OK,* I thought, *maybe this isn't so hard.* TideSDK is no longer Titanium Desktop since development was discontinued by Appcelerator. A quick peek at [the API documentation](http://tidesdk.multipart.net/docs/user-dev/generated/#!/api/Ti 'TideSDK API documentation') yielded the revelation that the `Titanium` global namespace was changed to `Ti` in TideSDK. Simple enough change, right? But `Ti.include("test.py");` was similarly unsuccessful, yielding `TypeError: Result of expression 'Ti.include' [undefined] is not a function`. Looking back at the API documentation, I found the `include()` method to be suspiciously absent from the `Ti` module. So things weren't looking good, and then [the release notes from the 1.3.1-beta release of TideSDK](https://github.com/TideSDK/TideSDK/blob/1.3.1-beta/CHANGES 'TideSDK 1.3.1-beta Release Notes') <span class="aside">[JEB, 2016: another broken link since TideSDK was deleted from GitHub in the TideKit attempt]</span> finally confirmed both the global namespace change and the removal of the `include()` method.

[^docs]: In addition to writing this, I would submit proposed changes to TideSDK's documentation, but given its uncertain future, I'm going to wait a bit to find out whether the project is still live before submitting a pull request.

[^manifest]: As these things go, several of my early failures were due to forgetting this essential step.

## The Solution

The situation at this point would have been bleak indeed, but for the fact that the documentation outlines *two* ways to include Python code in a TideSDK application. Method two is to embed Python in the DOM inside a `<script type="text/python">` block. I'd initially dismissed this, as I was planning to include several Python modules in my application, each involving several hundred lines of code, and that didn't seem appropriate for embedding in the DOM. So although I was successful getting `hello world` to work with this method of inclusion, I wasn't convinced it was the answer to my problem. Commence endless Googling[^vain].

Google, in the end, didn't reveal the ultimate solution to my problem, and---ironically enough, given its proven inaccuracy in other areas---the TideSDK documentation *did*. When I finally read down further in the guide to using Python in TideSDK, I happened upon this essential piece of information:

> Any class, function or variable that you want to pass from Python back to JavaScript must be declared in the `window` object.

Finally the `<script type="text/python">` method of inclusion started to make sense. In order to incorporate a Python module into your TideSDK application, all that's required is to import the module inside a `<script type="text/python">` block and then declare the desired class(es) and method(s) in the `window` object for use global use in your application. For example:

```html
<script type="text/python">
  import dexcom_to_JSON

  window.test_python = dexcom_to_JSON.test_python
</script>
```

This makes it possible to call `window.test_python();` anywhere in your JavaScript to fire the `test_python()` function from the `dexcom_to_JSON` module. Exactly what I needed, and it only took me hours of Googling and hair-pulling to figure out.

* * * * *

[^vain]: I probably would have arrived at the solution to this problem much faster had I not been convinced that there *had* to be a replacement for the `include()` method that just wasn't yet documented. The moral of the story here is probably something like: "Search for the solution, not what you want to find."