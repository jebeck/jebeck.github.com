---
layout: post
title: "Beeminding Diabetes"
date: 2012-11-05
tags: [diabetes, Beeminder, Quantified Self, continuous glucose monitoring]
---

*[Beeminder](https://www.beeminder.com/ "Beeminder.com") is an online webapp that helps you track and commit to goals. I've been using it to track and commit myself to some of my blood glucose goals off and on since last January. It turns out that today is a particularly good day for me to write about Beeminder and my diabetes goals because I failed on one of my goals yesterday, and now I have to pay Beeminder $10.*

## What is Beeminder?

Beeminder is a web-based service where you can track any goal that has a quantitative component (weight, miles run, pages read, words written, etc.) and a quantitatively-defined target (target weight, a certain number of miles run/pages read/words written per week, etc.). You can start to track any goal for free, but if you fail to make adequate progress (as defined by the target and deadline set when you started), then in order to restart and continue tracking the same goal, you have to pledge money against the possibility that you'll fail again. The pledges start at $5, but each time you fail on the same goal, it is suggested that you increase the amount of money that you pledge according to the schedule:

| Try  |  Amount |
|------|---------|
| 1    |  Free   |
| 2    |  $5     |
| 3    |  $10    |
| 4    |  $30    |
| 5    |  $90    |
| 6    |  $270   |
| 7    |  $810   |


The ideas behind this fee schedule are that the threat of having to pay out your own hard-earned cash upon failure is quite motivating (see also: [loss aversion](http://en.wikipedia.org/wiki/Loss_aversion "Wikipedia on loss aversion")) and that by the time you've reached a certain fee level, you *haven't* already accumulated that much money in losses[^a].

### Beeminding Natural Phenomena

In my opinion, Beeminder is *particularly well-designed* when it comes to tracking goals that are not completely within one's conscious control---weight, for example. With any Beeminder goal you set, the goal is to stay on a "yellow brick road," the width of which is determined by the rate of your goal.

<figure class="right">
  <img alt="close-up of Beeminder's yellow brick road" src="/images/beeminder/Beeminder_road_width.png">
  <figcaption>Beeminder's yellow brick road</figcaption>
</figure>

So, if your goal is to read 10 pages a day, then the road will be 20 pages wide, with your target in the center. You always have at least a day's worth of buffer if you start at the center of your road or above. If you start in the center of your road (blue dot in the image to the right), then you can do nothing that day and be at the bottom edge (but not off) your yellow brick road the next day (orange dot).

The really clever bit has to do with how Beeminder deals with goals that involve random fluctuation (basically, anything to do with some sort of natural or biological phenomenon would qualify, I think). What's brilliant is that all the user has to remember is the exact same thing as in the simple fixed-rate case: if you're in the center of your road or somewhere further to the right side of the road today, it's impossible to lose tomorrow. Essentially the idea is that you're never punished for a single terrible day, but two horrible days in a row could send you off your yellow brick road. How Beeminder actually accomplishes this is described further [on their blog post about road width](http://blog.beeminder.com/roadwidth/ "Beeminder Blog: The Magical Widening Yellow Brick Road").

## Beeminding Diabetes

When I first heard about Beeminder (via [a post on the QuantifiedSelf blog](http://quantifiedself.com/2011/12/toolmaker-talk-bethany-soule-daniel-reeves-beeminder/ "QuantifiedSelf Toolmaker Talk: Beeminder"), I thought it sounded like a particularly good way to track and commit to diabetes-related goals because of its ability to deal with random fluctuation in the data.

<figure class="center">
  <img alt="blood glucose goal graph from Beeminder" src="/images/beeminder/Beeminder_BG_screenshot.png" />
  <figcaption>My Beeminder daily average blood glucose goal</figcaption>
</figure>

In my opinion, blood glucose management is not quite as simple as just tracking your daily average blood glucose, so I decided to track and commit to goals for three separate indicators of my blood glucose management, getting the data for all of them from my [Dexcom continuous monitor](http://www.dexcom.com/ "Dexcom website")[^b]. The three indicators I track are:

- [my daily average blood glucose](https://www.beeminder.com/janabeck/goals/bg "My Beeminder: Daily Average Blood Glucose")

 - [the daily standard deviation of my blood glucose](https://www.beeminder.com/janabeck/goals/sd "My Beeminder: Daily Standard Deviation of My Blood Glucose")

- [the percentage of my blood glucose readings per day that fall into the hypoglycemic range (< 65 mg/dL)](https://www.beeminder.com/janabeck/goals/hypos "My Beeminder: Percentage of Hypoglycemic Readings")

The graph from my recent Beeminder off-road adventure is a perfect illustration of exactly why I like Beeminder for tracking and committing to diabetes-related goals:

<figure class="center">
  <img alt="screenshot from Beeminder derailment with crucial data points indicated with arrows" src="/images/beeminder/Beeminder_offroad_screenshot.png" />
  <figcaption>My recent Beeminder off-road adventure</figcaption>
</figure>

In this screenshot from the Beeminder website, the pink arrow points at one terrible day where I went off the yellow brick road, but since my previous data point (white arrow) and my next data point (orange arrow) were both well under the center line of my road, that one terrible day wasn't punished. In contrast, the green arrow points to where I just went off the road. But here my previous data point (blue arrow) was above the center line of my road, so I wasn't safe from losing, and that's why this terrible day resulted in my having to pay $10 for failing on my goal.

### Beeminder's Fee Schedule and Indefinite Goals

I first started tracking my diabetes-related goals at the beginning of January, 2012, but I stopped tracking for a while in August because I started to question whether Beeminder was really the best way to motivate myself with respect to my blood glucose management goals. The problem was that on two out of my three goals, I'd already derailed a couple of times: one more derailment, and I'd be committing myself to pay out $30 if I derailed again. For me, $30 is where the money starts to feel a bit scary[^c], and the problem with diabetes is that it *never* goes away. I have this thing for life, and there are *always* going to be times when my blood glucose management is less than ideal, and I fall short of my goals. So I just couldn't see myself continuing up Beeminder's payment ladder.

**However**, one thing that Beeminder has changed relatively recently is that they no longer force you to stay on the $5 → $10 → $30 → $90... fee schedule. Instead when you fail on a goal you can choose to stay at the same amount of money that you just paid out for failing[^d]. This is the sole reason that I started tracking my blood glucose management goals again---because I think that for lifelong goals that are inevitably going to involve failure now and again, the ever-escalating fee schedule just does not make sense psychologically. Self-forgiveness is a big part of successful diabetes management. When you fall short[^e] of your goals---whether it's one blood glucose reading that's not where you'd like it to be or a disappointing A1C reflecting the last 2--3 months of your diabetes management[^f]---you have to be able to accept that and regroup without beating yourself up about it.

> **tl;dr**: [Beeminder](https://www.beeminder.com/ "Beeminder.com") is great. I recommend giving it a try if you want or need an extra kick in the pants to help you track and commit to any diabetes-related or other goals.

* * * * *

[^a]: That is, this is the argument for not just doubling your pledge with each new attempt at your goal. See [the Beeminder pricing FAQ](https://www.beeminder.com/money "Beeminder FAQ: Pricing") for more.

[^b]: More about the Dexcom in [my post about analyzing my Dexcom data](/blog/2012/10/12/lessons-learned-from-100/ "Lessons Learned from 100,000+ Blood Glucose Readings").

[^c]: Although I have paid out that much, on two separate goals.

[^d]: So this means that on [my goal to run a certain number of miles per week](https://www.beeminder.com/janabeck/goals/runs "My Beeminder running goal"), where I've already paid out $30 and committed to a new contract valued at $90, I'm now permanently stuck at that $90 commitment level or higher. I don't really mind that with my running goal, as it's the one that I've had the most success with in terms of Beeminder motivating me effectively.

[^e]: I didn't even want to use the word "fail" in this sentence.

[^f]: [There are no "bad" numbers in diabetes.](http://forecast.diabetes.org/words-aug2012 "Diabetes Forecast: 9 Diabetes Terms We Can Do Without")