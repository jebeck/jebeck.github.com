---
layout: post
title: "infinite interactivity with Inquirer.js"
date: 2017-02-05
tags: [command line, Node]
---

## intro: …do *what* with Inquirer?

Last weekend I spent some time on a [silly side project](https://github.com/jebeck/narkissos "jebeck on GitHub: narkissos"), and I was working towards a minimum, proof-of-concept “port” of the famous[^1] [Rogerian therapist chatbot “Eliza”](http://www.masswerk.at/elizabot/ "Eliza (elizabot.js)") into the [generator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function* "MDN: generator function")-based chatbot framework I had already started putting together. I didn’t yet have any user input functionality in the UI for the project, so I wanted to test out my port in the simplest way possible: via interactive command line.

I’ve used [commander](https://github.com/tj/commander.js/ "GitHub: commander.js") before for making Node CLI tools, but I knew it wouldn’t provide the interactivity I was looking for—namely, being able to input text and test an Eliza instance’s responses, back-and-forth, *indefinitely*. So I went looking around for other Node CLI libraries and soon came across [Inquirer](https://github.com/SBoudrias/Inquirer.js/ "GitHub: Inquirer"), which looked like it might fit the bill.

**Spoiler:** it did…*eventually*.

Read on for a short story of hacking an interactive question/answer CLI library into a chatbot framework, including a tiny taste of [RxJS](https://github.com/Reactive-Extensions/RxJS "GitHub: RxJS") (😮!).

## prerequisites

This blog post assumes a moderate familiarity with:

- JavaScript/Node.js
- command-line interface (CLI) tools
- some ES2015 features:
  - arrow functions
  - destructuring assignment
  - template literals

If you’re interested in the material here but need help with some of these assumed concepts, please [reach out to me](http://janabeck.com/contact/ "Jana Beck: Contact info"), and I’ll try my best to help!

## Inquirer basics

After installing Inquirer with `npm install inquirer`, you can get up and running very quickly. A tool that asks the user to input their name and then choose their favorite from a list of ice cream flavors take only about 14 lines of code:

{% gist e72b8f43d0e35258d8f38aaf0e22ce63 %}

💣 NB: One thing that tripped *me* up initially with Inquirer was that fact that the examples I found from older blog posts employed a callback in the second argument to `inquirer.prompt` to retrieve the answers. Since full support for Promises came into Node with version 4.x+, `inquirer.prompt([questions])` has been [updated to return a Promise](https://github.com/SBoudrias/Inquirer.js/issues/452 "Inquirer on GitHub: Issue #452 'Callback method does not work after 0.12.0'").

## adding infinite interactivity with RxJS

In order to use Inquirer for the ✨∞ *infinite* ∞✨ back-and-forth interactivity that you need to have an open-ended conversation with a chatbot, you need to be able to dynamically add new prompts. Since Inquirer already uses [RxJS](https://github.com/Reactive-Extensions/RxJS "GitHub: RxJS") under the hood, you can use RxJS in your Node script to achieve infinite interactivity.

Start by installing the same version of RxJS that Inquirer depends on—as of this writing, that’s `rx` 4.x[^2], so `npm install rx`.

Then after `require`ing Rx in addition to Inquirer, we can create a [`Subject`](http://xgrommx.github.io/rx-book/content/subjects/subject/index.html "RxJS Book: Subject"):

```javascript
const inquirer = require('inquirer');
const Rx = require('rx');

const prompts = new Rx.Subject();
```

Instead of initializing `inquirer.prompt` with an array of JavaScript objects, each encoding a question to be asked the user, we instead pass `inquirer.prompt` the new Rx `Subject` constant `prompts` we’ve just created. Then we access the callbacks we’ll need for a reactive interface with `ui.process.subscribe`:

```javascript
inquirer.prompt(prompts).ui.process.subscribe(
 onEachAnswer,
 onError,
 onCompleted,
);
```

The `onEachAnswer` callback receives an object representing the answer with two properties: `name` (= the `name` property in the prompt) and `answer` (= the user’s input). It’s in the `onEachAnswer` callback that we have the opportunity to dynamically create a new prompt and surface it in the user’s current session using the Rx `Subject`’s `onNext` function:

```
// onEachAnswer callback
({ answer }) => {
 prompts.onNext(makePrompt(`This is prompt \#${i}.`));
}
```

To create each question/prompt, we can define a simple `makePrompt` function:

```
function makePrompt(msg) {
 return {
   type: 'input',
   name: `userInput-${i}`,
   message: `${msg || 'Say something to start chatting!'}\n\n`,
 };
}
```

We kick off the chat with a simple call to `prompts.onNext` (passing in the default prompt resulting from `makePrompt()`) at the end of the file: `prompts.onNext(makePrompt())`.

Altogether, the simplest infinitely interactive Inquirer script with dynamically generated prompts looks something like this:

{% gist 1ca224af150767a25ecefc020d29bbd0 %}

[^1]: Or notorious?

[^2]: RxJS has released a new 5.x version which is available on `npm` under the package name `rxjs`. I can verify (from having tried myself) that only the 4.x version still published on npm under `rx` works with Inquirer.
