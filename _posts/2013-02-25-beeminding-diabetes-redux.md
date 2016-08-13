---
layout: post
title: "Beeminding Diabetes: Redux"
date: 2013-02-25
tags: [diabetes, Beeminder, Quantified Self, continuous glucose monitoring]
---

*A short story about paying---literally---for my mulishness.*

*See also: [My first post](/blog/2012/11/05/beeminding-diabetes/ "Beeminding Diabetes") on Beeminding diabetes.*

Over the course of three days this past week, I managed to derail *all three* of my Beeminder diabetes goals. On February 21st, I derailed on my mean blood glucose and standard deviation goals. On the 20th, I was on the wrong side of the yellow brick road for both goals, although I was just barely over the centerline on my standard deviation goal. Then on the 21st I indulged in some unwise[^a] midnight snacking that sent my blood glucose through the roof:

<figure class="center">
  <img alt="graph of blood glucose showing a very high spike in the early morning" src="/images/R/feb21.png" style="width: 600px;" />
  <figcaption>My blood glucose: 21 February 2013</figcaption>
</figure>

This spike ruined both my mean blood glucose and standard deviation for the day, and since I wasn't on the right side of the road to start with, the road didn't auto-widen, and I derailed.

But that's not the real story here. What's remarkable is how even though I'd just taken a $10 hit from derailing on those goals (paying out $5 for each), I also derailed on my goal tracking the percentage of my readings in the hypoglycemic range two days later.

There's a sense in which this almost makes sense since an increase in hypoglycemia is always a risk when you're trying to improve your blood glucose control. In fact, derailing on my mean and standard deviation goals *did* provide the kick in the pants to get me to focus on getting back to the "tight" blood glucose control that I try my best to maintain. On the 22nd, I recorded a very good mean and standard deviation:

<figure class="center">
  <img alt="graph of blood glucose showing early morning and early evening lows" src="/images/R/feb22.png" style="width: 600px;" />
  <figcaption>My blood glucose: 22 February 2013</figcaption>
</figure>

This tight control continued into the 23rd, and I actually started clinging to the low end of my target range. Since the 23rd was a Saturday, I didn't set an alarm and slept late, waking up around 11:20 a.m. to my Dexcom showing several hours of readings hugging or sitting just below the 70 mg/dL line[^b]. (My meter read 76 mg/dL when I tested upon waking.)

I'm not much of a breakfast eater, so after waking up I just settled in front my computer and started working on a project. Over the next several *hours*, my blood sugar drifted down and down, and even though my Dexcom (still in "Vibrate" mode) was buzzing at me every five minutes, I mulishly persisted in ignoring it because I was so engrossed in my project[^c].

<figure class="center">
  <img alt="graph of blood glucose showing two lows, first annotated with 'excusable: still sleeping' and second with 'me being a stubborn idiot'" src="/images/R/feb23_anno.png" style="width: 600px;" />
  <figcaption>My blood glucose: 23 February 2013</figcaption>
</figure>

**And here's the kicker:** the percentage of my readings under 65 mg/dL on the 23rd ended up being 27%, which is exactly one percentage point higher than the day before. Since my road auto-widened the day before to accommodate the sudden spike in low readings[^d], I would have been fine as long as I stayed at the same level or had a lower percentage of low readings. The fact that I derailed by one percentage point might have been frustrating if it weren't for the blatant and obvious fact that I could have easily prevented the derailment if I hadn't been such a stubborn idiot, happily hacking away (with a lovely hypoglycemia-induced headache brewing at the base of my neck) and ignoring my Dexcom. So, in the end, I am absolutely happy to have paid [Beeminder](https://www.beeminder.com/ "Beeminder") another $5: I utterly and completely deserved to be punished for such idiotic behavior[^e].

* * * * *

[^a]: I was going to say that such midnight snacking was atypical for me, but then I took a look at the sparkline for my #snack hashtag where I track my carbohydrate consumption on [your.flowingdata.com](http://your.flowingdata.com/ "your.flowingdata Twitter-based self-tracking app"), and it made a liar out of me, as it's clear that my most frequent carb snacking time is between 9-11 p.m.:
    <img alt="bar graph showing frequency of snacking concentrated in evening and nighttime hours" src="/images/R/snack_sparkline.png" style="max-width: 100%;" />
 (Alas, self-tracking is a double-edged sword, with not all truths about ourselves discovered thereby being truths we'd actually like to believe about ourselves...)

[^b]: This means that my Dexcom had been alarming off and on for several hours before I woke up. I didn't hear it because I accidentally left my alert profile on the "Vibrate" program. (Audible alerts *always* kick in below 55 mg/dL, but I wasn't that low.) The ability to program different alert programs for different times of day is a design feature I am *desperately* hoping that Dexcom integrates into their next generation system because I like to use the discreet "Vibrate" or "Soft" profiles most of the time, but I would love to have the "Attentive" program come on automatically every day at midnight.

[^c]: I was f---ing around with [this AppleScript](http://complexpoint.macmate.me/Site/Kindle_Notes_to_DEVONthink_2.html "Kindle notes to DEVONthink 2") <span class="aside">[JEB, 2016: Resource behind link has disappeared 😢]</span> to import my Kindle Highlights into [DEVONthink](http://www.devontechnologies.com/products/devonthink/overview.html "DEVONthink: Information management reinvented"). I don't actually know AppleScript, and the script didn't do exactly what I wanted "out of the box," so it quickly became that kind of half-frustrating, half-fun and completely addictively engaging task that I'm sure many other hacker types are well-acquainted with. (And eventually: I gave up and started writing my own Python script to do what I actually want to do.)

[^d]: The spike in low readings on the 22nd was partly due to the fact that several hours of data were missing that day because I had to <del>insert a new Dexcom sensor</del> reboot my Dexcom sensor.

[^e]: And I've written the whole story up here for a little extra public shaming.