---
layout: post
title: "how to publish data on npm"
date: 2016-11-20
tags: [open data, JSON, JSON Schema, npm]
---

Is your response to this title 🤔? Or worse yet, 🙄?

I haven’t (personally) seen many folks publishing data on npm, but I decided to [try it](https://www.npmjs.com/package/everest-data "npm registry: everest-data") recently for [a personal project](https://github.com/jebeck/dead-on-everest "GitHub: @jebeck/dead-on-everest"), and I thought it went so well that I’m writing this blog post to evangelize a bit about the process.

So give me just 3⃣ bullet points to convince you that **npm is a *great* place to publish an open dataset** because it has:

- built-in functionality for version control, including breaking vs. non-breaking changes via [semantic versioning](http://semver.org/ "Semantic Versioning")
- built-in functionality for updates
- easy-to-use hooks for quality control (via `test`, `prepublish`, etc.)

In addition, if you’re using [D3](https://d3js.org/ "D3: Data-Driven Documents") to visualize data, you’re already using JavaScript and perhaps (probably?) using npm as a JavaScript dependencies manager, so adding data to a project via `npm install` fits perfectly into your workflow.

If you’re convinced—or at least curious—please read on!

## [context [skippable]](#prerequisites "Skip to "prerequisites"")
I started drafting this blog post in October of 2016, back in the 🌞 days when [FiveThirtyEight](http://fivethirtyeight.com/ "FiveThirtyEight") (along with many other organizations) was predicting Hillary Clinton as the next President-elect of the United States. Now it’s mid-November, and we in the United States are facing the impeding reality of a President Donald Trump, who is—among other things—arguably [the least transparent Presidential candidate in history](https://www.washingtonpost.com/politics/even-with-new-details-trump-still-the-least-transparent-candidate-in-modern-times/2016/09/14/caaa0dba-7a92-11e6-ac8e-cf8e0dd91dc7_story.html "Washington Post: 
Despite gestures, Trump is still the least transparent U.S. presidential candidate in modern history"). Regardless of politics[^1], all evidence suggests that the gains made towards open and transparent government under the Obama administration may be lost entirely. As Steven Aftergood wrote in [an editorial for the Federation of American Scientists](http://fas.org/blogs/secrecy/2016/11/transparency-trump/ "FAS: Transparency Will Need a Reboot in the Trump Era"):

> It’s not that Trump has promised transparency and failed to deliver. He has promised nothing of the kind. Hypocrisy on this point would actually be a step forward.

In short: the world has changed, and as I’ve been working to finish this blog post, the dataset—Wikipedia’s [list of all the people who have died attempting to climb Mount Everest](https://en.wikipedia.org/wiki/List_of_people_who_died_climbing_Mount_Everest "Wikipedia: List of people who died climbing Mount Everest")—that I used when developing the workflow this blog post is about now seems out of touch with the times. It’s not even that this dataset doesn’t contain important facets: one of the main reasons I wanted to visualize the deaths on Everest data was to bring home the fact that a very large proportion of those who die on Everest are Nepali and Tibetan nationals, for whom climbing Everest is not a hobby but rather an economic livelihood.

Even so, the Everest data is narrow in subject and focus and literally—that is, geographically—disconnected from the things that feel most relevant to me today. So here I’ve paused, and I’m going to continue this blog post with a different Wikipedia-`<table>` sourced dataset that feels at least *slightly* more relevant to the current climate: [a list of denaturalized former citizens of the United States](https://en.wikipedia.org/wiki/List_of_denaturalized_former_citizens_of_the_United_States "Wikipedia: List of denaturalized former citizens of the United States").  Donald Trump has publicly announced his [intent to deport millions of immigrants](http://time.com/4569034/donald-trump-undocumented-immigrant-deportation/ "Time Magazine: Donald Trump Plans to Deport Up to 3 Million Immigrants") and has [threatened dissenters such as Harry Reid with legal action](https://origin-nyi.thehill.com/blogs/ballot-box/305786-reid-spokesman-trumps-threat-of-legal-action-should-worry-americans "The Hill: Reid spokesman: Trump's threats of legal action should worry Americans"). Imagining that he may progress to threats or actions to denaturalize immigrants who have become citizens and express political dissent against him is far from difficult. Thus, the historical context provided by the list available in Wikipedia may be at least potentially valuable in the years[^2] to come.

Even before this week’s election in the United States, the intent of this blog post was always to demonstrate a workflow for publishing high-quality datasets in the open and making them:

- easy to work with (as easy as `npm install`)
- easy to have confidence in (look at the schema and run the validation)
- and easy to contribute to (add new data, check that it passes the validation, and publish a new version)

In many cases, getting the data is the hardest problem; for example, aside from the threat of an opaque U.S. government under Donald Trump, consider the problem of [tracking people killed by the police in the United States](https://www.theguardian.com/us-news/2015/mar/18/police-killings-government-data-count "[The Guardian] The uncounted: why the US can't keep track of people killed by police"). Despite this—or, in other words, even knowing that *access* to data is a prerequisite challenge, having a workflow for making data that *is* accessible *maximally* accessible and useful is important, and I believe that the workflow I’m describing here may be a good place to start—comments welcome!

And finally: it may feel[^3] as though the election of Donald Trump as the 45th President of the United States is a sign that the wave of anti-intellectualism that has been cresting in American culture for decades has reached a tragic peak[^4], but I still believe that **a clear presentation of facts has the power to persuade**, and I’m choosing to fight anti-intellectualism in part by working to promote the accessibility of high-quality data so that data journalists of all stripes—professional and amateur—have it to analyze and present to media consumers.

# prerequisites
This blog post assumes a basic familiarity with:

- JSON as a data interchange format
- regular expressions
- `git` for version control
- [npm](https://www.npmjs.com/ "npm: node package manager") as a JavaScript package registry and repository

If you're interested in the material here but need help with some of these assumed concepts, please [reach out to me](mailto:jana.eliz.beck@gmail.com "My e-mail"), and I'll try my best to help!

# let’s do this 💪

## from `<table>` to JSON
I honestly don’t even know which HTML `<table>` to JSON converter I used: certainly [one of these](http://lmgtfy.com/?q=table+to+JSON+converter "Let me Google 'table to JSON converter' for you..."). [This one](http://convertjson.com/html-table-to-json.htm "Convert HTML Tables To JSON") looks familiar. In short: if your data originates in an HTML `<table>`, like mine did for this project, then this step should be one of the easiest. There are many tools available to convert between a `<table>` and JSON, and little cost to trying several to see which gives the best results in your particular case.[^5]

## sanitizing JSON: find-and-replace
No data extraction tool, like the HTML `<table>` to JSON converter I used, is going to yield perfect results, so data sanitization is an essential step. There may be problems in the data that jump out at you immediately *and* are easily fixable in a text editor with find-and-replace or [regular expression-based find-and-replace](http://docs.sublimetext.info/en/latest/search_and_replace/search_and_replace_overview.html#regular-expressions "SublimeText Unofficial Documentation: Regular expressions"). On the other hand, some issues in the data are subtle or rare but important to fix, and so using a tool other than the naked human 👁 to find these issues can be very helpful: we’ll talk about how to catch these cases using a JSON Schema in the next section.

As an example of the first type of problem, let’s look at how the “Denaturalization date” `<table>` column was transformed from Wikipedia’s [list of denaturalized former citizens of the United States](https://en.wikipedia.org/wiki/List_of_denaturalized_former_citizens_of_the_United_States "Wikipedia: List of denaturalized former citizens of the United States"). The result of the HTML to JSON transformation in this case was particularly messy, with many cells’ data coming through with bizarre formatting (e.g., `000000001984-03-02-0000March 2, 1984[12]`), including potential reference annotations at the end of the line. Initially, I was doubtful that I would be able to sanitize such a mess with find-and-replace, even with the help of regular expressions, but I decided to try anyway, and it turned out to be much easier than I initially guessed!

I matched the “Denaturalization date” in need of sanitization with the regular expression `"Denaturalization date": ".*([12]\d\d\d).*",`. I think one of the crucial pieces here to extract the *year* value was using `[12]` to restrict the first number in a sequence of four digits to only 1 or 2, thereby avoiding matching on the weird sequences of 0000s in the data. Aside from matching this target sequence of four digits starting with 1 or 2 in a capturing group (delineated with parentheses) to pull out the year, I used `.*` to allow anything (or nothing) to appear in the rest of the value string.

For the replacement text I used `"denaturalizationYear": "$1",` to accomplish two tasks at once:

1. replace the not terribly code friendly (because of the space) “Denaturalization date” property name with a spaceless (and stylistically idiomatic for JavaScript) name: `denaturalizationYear`
2. extract just the year of denaturalization from the mess of formatting[^6]

## sanitizing JSON: schema validation
To catch the more subtle issues in the data, I wrote a JSON Schema and put together a very simple command-line script to check the data against the schema and report on errors.

[JSON Schema](http://json-schema.org/ "JSON Schema"), currently in draft 4[^7], is a tool for validating JSON by defining a schema in JSON Schema’s own specification language, which is also JSON. There are a number of JavaScript libraries, as well as libraries in other programming languages, that [implement JSON Schema](http://json-schema.org/implementations.html "JSON Schema implementations") to provide validation as well as other tasks related to schemas, such as schema and documentation generation. The [tv4](http://geraintluff.github.io/tv4/ "Tiny Validator (for v4 JSON Schema)") JavaScript package[^8] provides an extraordinarily simple API for validating JSON with a JSON Schema:

```js
const tv4 = require('tv4');

const data = require(<path-to-data-file.json>);
const schema = require(<path-to-schema-file.json>);

tv4.validate(data, schema); // returns Boolean
```

The `validate` method returns a Boolean—`true` or `false`—indicating whether the validation passed. *If* validation failed, then information about the failure will be found in `tv4.error`.

### building a JSON Schema
To catch subtle errors in the data, I drafted my JSON Schema bit-by-bit, running validation frequently and correcting any errors as they arose either in the data or in the schema.

So I started with `{}` in my `schema.json` file: an empty object is the simplest JSON Schema possible and also a pointless schema, as it enforces no constraints! Continuing on the path of pointlessness temporarily, I added [two bits of JSON Schema metadata](https://spacetelescope.github.io/understanding-json-schema/basics.html "Understanding JSON Schema: The Basics"):

```json
{
  "$schema": "http://json-schema.org/schema#",
  "id": "https://github.com/jebeck/denaturalized"
}
```

Then came the first substantive piece of work, defining the `type` of the expected JSON data, which in this case was `array`: while each instance of denaturalization is a JSON *object*, the dataset as a whole is an array of such objects. At any level in a JSON Schema where the value of `array` is given for `type`, a sister property `items` may be used to define the “shape” of each item inside the array.

```json
{
  "type": "array",
  "items": {...}
}
```

The contents of the `items` property is just another JSON Schema with a `type` and other properties. In the case of the denaturalization dataset, the `type` for each of the items in the array is `object` and the key-value pairs that can appear on each object are specified under `properties` in yet another embedded JSON Schema!

I started just by listing the expected keys on each instance of denaturalization in my dataset, giving each an empty schema `{}` temporarily but also specifying `additionalProperties` (a sister to `properties`) as `false` to enforce the restriction that *only* the five properties specified were allowed to appear on each object:

```json
{
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "name": {},
      "reason": {},
      "reasonCategory": {},
      "denaturalizationYear": {},
      "status": {}
    },
    "additionalProperties": false
  }
}
```
 
The next step was adding the `type` to the schema for each property—`string` for all but `denaturalizationYear` which I specified as a `number` instead:

```json
  "properties": {
      "name": {
        "type": "string"
      },
      "reason": {
        "type": "string"
      },
      "reasonCategory": {
        "type": "string"
      },
      "denaturalizationYear": {
        "type": "number"
      },
      "status": {
        "type": "string"
      }
    },
```

Validating with this expanded schema immediately revealed a problem: all my `denaturalizationYear`s in the dataset were actually string values, even though logically they should be numbers, as specified in the schema. So I used regex-enabled find-and-replace again to fix this oversight. Fixing this oversight put into mind the fact that there’s also a clear minimum and maximum to the number values that should be allowed in the `denaturalizationYear` field: the year of first citizenship in the United States (1776) to the current year (2016), so I added [those constraints](https://spacetelescope.github.io/understanding-json-schema/reference/numeric.html#range "Understanding JSON Schema: numeric range") as well:

```json
    "denaturalizationYear": {
        "type": "number",
        "minimum": 1776,
        "maximum": 2016
      },
```

For the `reasonCategory`, which is a field I added by hand from the color-coding of the Wikipedia table, there were only three possible values, and so I specified these directly in the schema using [the `enum` property](https://spacetelescope.github.io/understanding-json-schema/reference/generic.html#enumerated-values "Understanding JSON Schema: enumerated values"):

```json
    "reasonCategory": {
        "type": "string",
        "enum": [
          "Hiding World War II crimes or association with Nazis",
          "Serious crimes, suspicion of spying for the communists, or association with terrorists",
          "All other reasons"
        ]
      },
```

Regular expression support in JSON Schema is difficult to get working for text-heavy fields due to the fact that using `.` to match any character is [not recommended](https://spacetelescope.github.io/understanding-json-schema/reference/regular_expressions.html "Understanding JSON Schema: regular expressions"), so I didn’t add any further validation beyond specifying a `string` type for `name`, `reason`, and `status`. However, I did add one last specification to the schema: listing all five object properties in a `required` array:

```json
{
"type": "object",
"properties": {
...
},
"additionalProperties": false,
"required": [
      "name",
      "reason",
      "reasonCategory",
      "denaturalizationYear",
      "status"
    ]
}
```

This revealed that there was no `status` information for some instances of denaturalization, and so—because this was a case of a too-strict schema rather than incorrect data—I removed that field from the `required` array.

## publishing the data to npm
The first step in publishing a package to npm is creating the package metadata, which is stored in a `package.json` at the top level of the repository. Creating this metadata is simple with the `npm init` command that runs an interactive “wizard” to walk you through the initial metadata creation (and avoid the fatal formatting mistakes that can come from attempting to manually write JSON).

Using an accurate `description` in the `package.json` is especially important for publishing data to help the resulting npm package registry page show up in search results. For the denaturalized citizens project, I put “JSON datasets of denaturalized (former) citizens by country, starting with the United States” as the `description`.

But even more important than using an accurate description is pointing the `entry` point for the package to the data. If you do this correctly, then anyone who installs the package with `npm install` will be able to load the data as a native JavaScript array using just `require('<package-name>')`—in the case of the denaturalization data, `require('denaturalized')`. The `npm init` wizard defaults the entry point to `index.js`, which is almost certainly **incorrect** when publishing data to `npm`, so be sure to watch for this during the package initialization or check later to be sure it’s correct.

During the wizard setup, I specified `node validate.js` as the `test` command since I wrote my tiny JSON Schema validation tool in a file named `validate.js`; later I also added it manually as the `prepublish` command in `scripts` in the `package.json`. This is also a very important step, particularly if you anticipate other people contributing to the dataset. With the validation specified as the `prepublish` command, it will be *impossible* for you (or anyone else you’ve granted publishing rights) to publish a new version of the data to the npm registry if the data fails the validation. The `prepublish` “hook” always runs on any attempt to `npm publish` and aborts the publishing attempt if the specified script exits on an error.

### pulling the trigger

Before issuing my first `npm publish` command for the denaturalization dataset, I did the following to prove to myself I was ready to publish:

- added basic instructions for how to use the package (via `npm install` and `require` for JavaScript projects and by downloading from GitHub for non-JavaScript projects) in the README
- on the `node` command line, `require`-d the JSON data file listed as my package `entry` and checked its `length` property and the first item in the array (i.e., at index `0`)
- committed my work and pushed it to my upstream GitHub remote repository
- turned on [Circle CI](https://circleci.com/ "CircleCI: Continuous Integration & Delivery")[^9] for the project to run the validation on a remote server with every push to GitHub to guard against some specific configuration on my machine allowing the validation to pass when it would fail otherwise
- waited for CircleCI to report success on the “build”
- tagged my latest commit as v0.1.0 and pushed the tag to the GitHub remote with `git push origin --tags`

Then, at long last, it was time to `npm publish`! 🎉

Feel free to use and/or reference either of the data projects mentioned in this post:

- (former) citizens denaturalized ([on GitHub](https://github.com/jebeck/denaturalized "@jebeck on GitHub: denaturalized")) ([on npm](https://www.npmjs.com/package/denaturalized "npm: denaturalized"))
- deaths on Everest ([on GitHub](https://github.com/jebeck/everest-data "@jebeck on GitHub: everest-data")) ([on npm](https://www.npmjs.com/package/everest-data "npm: everest-data"))

----

[^1]: Although I have little interest in being coy about mine: I am a liberal who values civil liberties and a maximally-inclusive social safety net provided by the federal government. I voted for Hillary Clinton, and I’m deeply troubled by the election of Donald Trump.

[^2]: I for one am hoping that they number only four.

[^3]: It certainly does to me.

[^4]: One hopes not just a local maximum!

[^5]: If your data originates in another non-machine readable format—a table in a PDF, for example—there are also tools for this, particularly several Python packages that I’ve heard discussed, although I won’t mention any in particular right here because I don’t have personal experience with any of them, and my knowledge is likely to be out of date.

[^6]: Extracting just the year of denaturalization was also a bit of an editorial decision. In many places, a date with month and day was available, but in some cases it wasn’t, and I made the judgment call to standardize based on the lowest common denominator of available information since it seemed to me that the finer-grained date information added little additional value. In my short experience with doing this kind of data sanitization, I can already say that similar editorial decisions come up frequently.

[^7]: Eventually the JSON Schema specification may be submitted as an RFC proposal to become an Internet Standard.

[^8]: “tv” here an abbreviation for “tiny validator.”

[^9]: The fact that CircleCI will run the `npm test` script without any configuration (normally done via a `circle.yml` file) makes it a particularly attractive CI option for a project like this.
