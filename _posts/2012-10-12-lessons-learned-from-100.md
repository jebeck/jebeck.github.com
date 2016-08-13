---
layout: post
title: "Lessons Learned from 100,000+ Blood Glucose Readings: The Long Version"
date: 2012-10-12
tags: [diabetes, Quantified Self, continuous glucose monitoring, data visualization, statistical analysis of blood glucose data]
---

*It's been a few months since I posted the handout version of my Quantified Self talk analyzing a little over a year's worth of my blood glucose data from my Dexcom continuous glucose monitor. I kept meaning to write out a long-form version of my talk, since the handout/slides don't contain much exposition, and now I'm **finally** getting around to it.*

## Introduction

### Type 1 Diabetes

(You can skip this if you're a PWD. If you're just interested in my visualizations of Dexcom data, you can [jump to that section](#visualizing-change).)

[Type 1 diabetes](http://en.wikipedia.org/wiki/Type_1_diabetes "Wikipedia entry on type 1 diabetes") is an autoimmune disease (like lupus and rheumatoid arthritis). In type 1 diabetes, the body's immune system attacks and kills the insulin-producing [β-cells](http://en.wikipedia.org/wiki/Beta_cells "Wikipedia entry on beta cells") in the pancreas. This results in very little to no endogenous insulin production, which means that the person with diabetes (PWD) is dependent on synthetic insulin.

Today's synthetic insulins are produced via genetically-modified *E. coli* bacteria. The resultant biosynthetic insulin is delivered by injection or infusion (with an [insulin pump](http://en.wikipedia.org/wiki/Insulin_pump "Wikipedia entry on insulin pumps")) into the subcutaneous fat layer. It's important to note that this method of delivering the drug **does not** very effectively mimic the production of insulin in a non-PWD. Injection into subcutaneous fat is not a very fast method of drug delivery: even the fastest of the modern "fast-acting" insulin analogs (NovoLog, Humalog, Apidra) don't reach their peak action until around 45-90 minutes after they are introduced into the body.

#### Insulin Dosing

Insulin dosing is more of an art than a science. (Please excuse the total cliché.)

There are two types of insulin doses that everyone who doesn't produce their own (or enough of their own) insulin needs to survive and thrive: *basal* insulin and *bolus* insulin.

##### Basal Insulin

Basal insulin is the "background" insulin---the insulin needed by the human body just to carry out normal functioning. PWDs who use an insulin pump get their basal insulin via a constant, slow drip of insulin infused through the cannula that is embedded under the skin in the subcutaneous fat and that is the outlet of the infusion line connected to the reservoir of insulin inside the pump. PWDs who don't use an insulin pump take a once-daily injection of a delayed-release "long-acting" insulin (e.g., Lantus or Levemir).

##### Bolus Insulin

Bolus insulin is the insulin that a PWD takes on an as-needed basis to "cover" carbohydrates ingested as well as to bring down high blood glucose. PWDs who use an insulin pump can deliver a bolus of insulin at any time using the pump's controls. PWDs who don't use an insulin pump will inject bolus insulin using either syringes and a vial of insulin or an [insulin injector pen](http://en.wikipedia.org/wiki/Insulin_pen "Wikipedia entry on insulin pens"), a device with a helpful dial mechanism for drawing up precise doses of insulin.

When a PWD is taking insulin to cover carbohydrates s/he is intending to consume, s/he calculates how much insulin to take using an insulin-to-carb ratio---that is, a ratio defining how many units of insulin can be expected to cover a certain number of grams of carbohydrate. There is no universal insulin-to-carb ratio. Rather, every PWD must determine the insulin-to-carb ratio that works best, and this may even vary by time of day: many PWDs find that they need a larger insulin-to-carb ratio (i.e., more insulin required to cover fewer grams of carbohydrate) in the morning.

### My Type 1 Diabetes

I was diagnosed with type 1 diabetes in December of 2003 at age 19. I was quite lucky in that my diabetes was diagnosed without my going into diabetic ketoacidosis (DKA), a dangerous condition (sometimes resulting in coma or death) that arises from prolonged very high blood sugar and little or no insulin in the bloodstream. Perhaps because I was diagnosed before I was at the dangerous point where I wasn't producing a significant amount of my own insulin, my type 1 diabetes has always been somewhat mild, in comparison to others, likely because I am still producing small amounts of my own insulin. (At least as of November of 2006, this was confirmed by a non-zero result with a C-peptide assay. C-peptide is a by-product of insulin production, so a non-zero C-peptide implies non-zero insulin production.)

<figure class="right">
  <img alt="my Animas Ping insulin pump" src="/images/qs/ping.jpg" />
  <figcaption>My Animas Ping insulin pump</figcaption>
</figure>

#### My Insulin Pump(s)

Since December of 2006, I have been using an insulin pump. I started with a [Medtronic](http://www.medtronicdiabetes.com/ "Medtronic Diabetes website") Paradigm 522, but since January of 2011 I've been using an [Animas/OneTouch Ping pump](http://www.animas.com/animas-insulin-pumps/onetouch-ping "Meet the OneTouch Ping").

#### Continuous Glucose Monitoring

I started using a [Dexcom continuous glucose monitor](http://www.dexcom.com/seven-plus "Dexcom Seven+ continuous glucose monitor") in February of 2011. The Dexcom system involves a sensor wire embedded under the skin in the PWD's subcutaneous fat tissue. A transmitter snaps into the sensor wire's cradle and transmits a blood glucose reading to a separate, wireless receiver unit every five minutes.

Some visual aids:

<figure>
  <img alt="Dexcom sensor wire after sensor removal, demonstrating thinness, flexibility, and angled insertion" src="/images/qs/dexcom_wire.jpg" />
  <figcaption>The Dexcom sensor wire</figcaption>
</figure>

<figure>
  <img alt="Dexcom sensor cradle with transmitter, affixed to the back of my upper arm" src="/images/qs/dexcom_arm.jpg" />
  <figcaption>The Dexcom sensor cradle with transmitter attached, where I often wear it on the back of my arm</figcaption>
</figure>

<figure>
  <img alt="Dexcom receiver" src="/images/qs/dexcom_no_hitter.jpg" />
  <figcaption>The Dexcom receiver</figcaption>
</figure>

##### Features of the Dexcom

As well as providing an (approximate) blood glucose reading every five minutes, the Dexcom system includes several other useful features. There are seven possible different trend arrows that indicate the rate at which the PWD's blood glucose is changing: a steady arrow, three speeds of up arrow, and three speeds of down arrow.

<figure>
  <img alt="Dexcom showing slanted down trend arrow" src="/images/qs/dexcom_angle_down.jpg" />
  <figcaption>Down arrow #1: mildest downward trend</figcaption>
</figure>

<figure>
  <img alt="Dexcom showing double straight down arrows" src="/images/qs/dexcom_double_down.jpg" />
  <figcaption>Down arrow #3: the dreaded "double down" indicating a rapid drop in blood glucose</figcaption>
</figure>

<figure>
  <img alt="Dexcom showing double straight up arrows" src="/images/qs/dexcom_inaccurate.jpg" style="width: 300px" />
  <figcaption>Up arrow #3: the horrifying "double up" indicating a rapid spike in blood glucose</figcaption>
</figure>

The Dexcom is also user-programmable to provide audible and/or vibrating alerts when the PWD's blood glucose is above a certain threshold, below a certain threshold (and, for safety reasons, below a hard set 55 mg/dL), or changing very rapidly. The Dexcom system also comes with Windows-only software that allows the user to download his/her data in basic XML or tab-delimited formats.

##### Accuracy of the Dexcom

The main utility of the Dexcom system is not to replace fingerstick blood glucose monitoring but rather to provide a fuller picture of a PWD's blood glucose fluctuations. PWDs who use a Dexcom system are encouraged to continue fingerstick testing whenever making a treatment decision: at minimum, this means fingerstick testing before every meal (in order to determine the proper insulin dose), before exercise, and before going to sleep. In addition, the Dexcom system requires calibration with a fingerstick test approximately every twelve hours.

The Dexcom sensor wires are designed (and approved by the FDA) to be used for seven days, but many Dexcom users (including me!) will "reboot" a sensor after the initial seven days have passed and continue to wear the same sensor wire for up to 14 days. Accuracy of the system is greatly improved by doing this since the sensor is working from a greater number of calibration readings.

<figure>
  <img alt="Dexcom receiver and fingerstick blood glucose meter showing very different blood glucose values" src="/images/qs/dexcom_inaccurate.jpg" />
  <figcaption>An example of the Dexcom's occasional complete inaccuracy</figcaption>
</figure>

A corollary to this is that the accuracy of a sensor is often particularly low on the first day or two after the PWD has inserted a brand new sensor wire. Whenever a fingerstick reading differs by more than 20% from the Dexcom's reading (as in the picture to the left), entering the fingerstick reading as an additional calibration is recommended.

## My Experiment

### Introduction

#### Blood Glucose Management

Blood glucose levels in a non-PWD vary between 70--130 mg/dL and only reach the higher end of that range after high-carbohydrate meals.

[Many PWDs](http://www.diabetes.org/living-with-diabetes/treatment-and-care/blood-glucose-control/tight-diabetes-control.html "American Diabetes Assoc.'s definition of tight glucose control") aim for a target glucose range of 70--130 mg/dL before meals (i.e., fasting) and less than 180 mg/dL at the zenith of the post-meal spike. There is also [some evidence](http://www.dlife.com/diabetes/blood_sugar_management/trecroci_083107 "dLife article about Irl Hirsch's research into glycemic variability") that high glycemic variability (i.e., the standard deviation of blood glucose measurements) is an indicator of risk for diabetic complications independently of average blood glucose.

Accordingly, my blood glucose management goals (with respect to the data provided by the Dexcom system) are the following:

- as many readings in the target range of 70--130 mg/dL as possible

- keep the percentage of readings *below* 65 mg/dL to a minimum

- reduce the standard deviation (as measured on a day's worth of readings) of blood glucose readings

- reduce the daily mean of blood glucose readings

When I started using the Dexcom continuous glucose monitoring system, my first reaction was shock. Before using the Dexcom, I had been completely (and blissfully) unaware that my post-meal blood glucose spikes were regularly above 200 mg/dL and often in the 220--230 mg/dL range, especially in the morning.

The mere fact of having a reliable feedback mechanism in the form of the Dexcom monitor was not enough to effect an improvement in my post-meal blood glucose excursions. Months passed, and I only grew more and more frustrated with my seeming inability to control my post-meal blood glucose.

The first potential solution I attempted was to try supplementing my insulin regimen with a recently-approved new drug called [Symlin](https://symlin.com/ "Symlin website"), but that (as they say) is a story for another time: regular use of Symlin was somewhat useful in controlling my post-meal blood glucose excursions, but in the end the effect wasn't large enough to outweigh the considerable side effects of the drug.

#### A New Hypothesis

Finally, in the summer of 2011, I happened across another potential strategy for improving my blood glucose: a low-carbohydrate diet. I had been aware of the low-carb and Atkins diet fad(s), but I'd always dismissed it as nothing *but* a fad. It wasn't until I read Gary Taubes' *Good Calories, Bad Calories* that I really started to take a low-carbohydrate diet seriously as a viable option. Once I was convinced that carbohydrates aren't an essential component of a healthy diet and therefore that there wasn't any harm in trying a low-carbohydrate diet, I decided to test following a low-carbohydrate diet as a means to improving my blood glucose management.

> _**Hypothesis:**_ *Carbohydrate restriction is an effective way to improve blood glucose outcomes.*

The reasoning behind using a low-carbohydrate diet as a means to improving blood glucose outcomes is quite straightforward: the vast majority of a PWD's blood glucose excursions (assuming his/her basal insulin has been properly adjusted) are a direct consequence of carbohydrate consumption especially given that, as mentioned above, the delivery of insulin through subcutaneous fat tissue is only a pale imitation of the insulin response in a non-PWD.

> When I hear a physician saying to a type 1 diabetes patient, "Go ahead and eat whatever you want, just make sure you cover your glucose with insulin," it's like telling a firefighter, "Just go ahead and pour as much gasoline as you like on that fire you’re trying to put out, as long as you cover it with enough water." Completely circular and illogical.
> ---[low-carbohydrate advocate Peter Attia, M.D., in an interview on the diabetes blog A Sweet Life](http://asweetlife.org/feature/the-ketogenic-diet-and-peter-attias-war-on-insulin/ "Interview with Dr. Peter Attia on A Sweet Life")

#### The Nitty-Gritty Details

I decided to start following a carbohydrate-restricted diet at the beginning of January, 2012. Since I already had many months of blood glucose measurements from my Dexcom system when I wasn't following a low-carbohydrate diet, I already had the data for the control part of my experiment.

I used a variety of tools to analyze and compare the next several months of my Dexcom data, following my adoption of a carbohydrate-restricted diet:

- export files from the Dexcom software:
  - XML files, useful for manipulating in Python with [BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/ "I can't recommend this package enough!")
  - tab-delimited .csv files, useful for direct importing into R

- in [R](http://www.r-project.org/ "The R Project for Statistical Computing"):
  - built-in non-parametric statistical functions
  - built-in plotting functions: boxplot(), etc.
  - [ggplot2](http://ggplot2.org/ "ggplot2 website") for data visualization

### The Results

#### Statistical Significance

My first task after collecting several months worth of blood glucose data while following a carbohydrate-restricted diet was to assess whether this dietary change resulted in a statistically significant difference in blood glucose measurements. Because blood glucose data are not normally distributed (i.e., non-parametric), I used the Wilcoxon rank-sum test (similar to the more familiar Student's t-test used with parametric data) to test the null hypothesis that the data from before and after my dietary change could have been drawn from the same population. The result came out overwhelmingly in favor of rejecting this null hypothesis, with a *p*-value of `2.2e-16`.

I was also able to calculate an estimate of the median of the difference between a sample from my blood glucose measurements on a "normal" diet and a sample from my measurements on the carbohydrate-restricted diet, which turned out to be -19 mg/dL.

> _**Conclusion:**_ *My adoption of a carbohydrate-restricted diet resulted in significant (negative) change in blood glucose values.*

<a id="visualizing-change"></a>

#### Visualizing Change

Next I turned to the task of visualizing the change in my blood glucose outcomes.

<figure>
  <img alt="violin plots of blood glucose readings showing significantly less variability and lower center of blood glucose with a carb-restricted diet" src="/images/qs/dexcom_violin.jpg" style="width: 400px;" />
  <figcaption>Violin plot of Dexcom blood glucose readings</figcaption>
</figure>

A violin plot of my blood glucose measurements from my regular diet versus the carbohydrate-restricted diet gives quite a clear picture of both the improved, lower mean glucose I achieved with a carbohydrate-restricted diet as well as the concomitant reduction in glycemic variability.

I also wanted to look at my three sub-goals for improving my blood glucose management---reducing daily mean glucose, reducing daily standard deviation, and minimizing hypoglycemic readings---each on its own. In every case, the visualizations show improvement quite clearly:

<figure>
  <img alt="line graph of daily mean blood glucose with trend lines for regular and carb-restricted diet showing significant lower trend for the carb-restricted diet" src="/images/qs/mean_blood_glucose.jpg" style="width: 600px;" />
  <figcaption>Daily mean of Dexcom blood glucose readings showing significant improvement under carb-restriction</figcaption>
</figure>

<figure>
  <img alt="line graph of daily standard devication of blood glucose with trend lines for regular and carb-restricted diet showing significant lower trend for the carb-restricted diet" src="/images/qs/standard_deviation.jpg" style="width: 600px;" />
  <figcaption>Daily standard deviation of Dexcom blood glucose readings showing significant improvement under carb-restriction</figcaption>
</figure>

<figure>
  <img alt="line graph of daily percentage of blood glucose readings under 65 mg/dL with trend lines for regular and carb-restricted diet showing initial spike but eventual lower trend for the carb-restricted diet" src="/images/qs/daily_low.jpg" style="width: 600px;" />
  <figcaption>Daily percentage of blood glucose readings < 65 mg/dL showing initial spike but eventual improvement under carb-restriction</figcaption>
</figure>

There are a few patterns evident in these three graphs that reflect extra-dietary factors that had an effect on my blood glucose management. First, the rise in both mean blood glucose and standard deviation in March is a testament to the fact that I was traveling a great deal then and found it much more difficult to adhere to the same level of carbohydrate-restriction. Second, the dramatic increase in the percentage of readings below 65 mg/dL at the beginning of my carbohydrate-restricted diet are a reflection of the fact that as soon as I started to restrict my carbohydrates, my insulin needs (*basal* as well as bolus) dropped significantly---in fact, faster than I was able to adjust.

<figure>
  <img alt="smoothed trend line graph showing change in percentages of low, target, and high blood glucose over time, with low and high decreasing under carb-restriction and target increasing" src="/images/qs/percentages.jpg" style="width: 600px;" />
  <figcaption>Percentages of low, target, and high blood glucose readings over time</figcaption>
</figure>

I also put together a smoothed graph of the percentages of my blood glucose readings that were hypoglycemic, in my target range, or higher than my target range. Here the trend towards a reduction in high readings and an increase in target range readings upon the adoption of a carbohydrate-restricted diet is very clear.

Finally, using a single sample week from each of the test conditions, I produced a heatmap of my blood glucose readings by time of day.

<figure class="left">
  <img alt="heat map of blood glucose by time of day during regular diet showing wide blood glucose variability" src="/images/qs/oct.jpg" style="width: 320px;" />
  <figcaption class="img-width">Heatmap of blood glucose readings during a regular diet week</figcaption>
</figure>

<figure class="right">
  <img alt="heat map of blood gluocse by time of day during carb-restricted diet showing significantly less variability, especially in the morning" src="/images/qs/jan.jpg" style="width: 320px;" />
  <figcaption class="img-width">Heatmap of blood glucose readings during a carbohydrate-restricted diet week</figcaption>
</figure>

The heatmap from the regular diet week is on the left (or top), and the heatmap from the carbohydrate-restricted diet is on the right (or bottom). Although the difference between the two heatmaps is not extremely stark, it is fairly clear that glycemic variability was considerably higher on a regular diet versus a carbohydrate-restricted diet.

#### Looking for Patterns

##### By Day of the Week

<figure>
  <img alt="heat map of blood glucose readings by day of week showing no strong pattern" src="/images/qs/day_heatmap.jpg" style="width: 360px;" />
  <figcaption>Heatmap of blood glucose readings by day of the week</figcaption>
</figure>

I used heatmaps again to look for whether or not there was any pattern to my blood glucose readings by day of the week. Again there doesn't appear to be much of a pattern, although it does appear that weekends---when I'm sure I lapsed on my carbohydrate restriction more than I did during the week---show more variability than weekdays.

I also graphed my blood glucose readings for the different days of the week as box-and-whisker plots, but if anything, I think this visualization gives even less of an impression of a clear pattern of variance in my blood glucose readings by day of the week.

<figure>
  <img alt="box plot of blood glucose readings for every day of the week, again showing no strong pattern" src="/images/qs/day_boxplots.jpg" style="width: 600px;" />
  <figcaption>Box-and-whiskers plots of blood glucose readings by day of the week</figcaption>
</figure>

##### By Time of Day

<figure>
  <img alt="heat map of all blood glucose readings by time of day showing least variability in the early morning" src="/images/qs/all_heatmap.jpg" style="width: 360px;" />
  <figcaption>Heatmap of all blood glucose readings by time of day</figcaption>
</figure>

The heatmap for all my blood glucose readings by time of day is a bit more revealing. And in fact what I think this heatmap reveals most clearly is that I'm a very nocturnal graduate student! My blood glucose readings are consistently lowest between about 6 a.m. to 9 a.m., which would probably look odd to most PWDs, as many of us struggle in particular with higher blood glucose in the mornings: this is known as the "dawn phenomenon." It's not that I'm an unusual PWD who doesn't struggle with the dawn phenomenon; rather, my dawn phenomenon just happens a few hours later than usual, peaking in the early afternoon hours instead of the morning because of my habitual late nights and late mornings.