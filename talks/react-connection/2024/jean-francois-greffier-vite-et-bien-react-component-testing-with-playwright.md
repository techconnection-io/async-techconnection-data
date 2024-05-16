---
slug: >-
  /talks/react-connection/2024/jean-francois-greffier-vite-et-bien-react-component-testing-with-playwright
date: '2024-04-22'
title: 'Vite et bien : React component testing with Playwright'
author:
  - Jean-François Greffier
video: 1dZMpyJlOiY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/1dZMpyJlOiY.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
[Jean-François]
I'm Jean-François Greffier, I'm from France, I'm from Rennes. I like software craft testing and I am a Playwright Ambassador. It basically means that I'm paid with stickers and merch by Microsoft.

So I bring some for you actually, if you want some merch, some stuff, I have some. So, first thing is, what is Playwright? Anyone using Playwright right now?

Yeah, not bad, yeah. Ever heard of it, if you're not using it? Okay, well that's much better than last year when I made my first talk about Playwright.

So, Playwright, it's open source, but it's mainly maintained and sponsored by Microsoft. It's rather new, it was created in 2020, but it's inherited from Puppeteer. The story behind it is that some people that were working on Puppeteer at Google left to create Playwright.

So Puppeteer, it's an automation tool, where Playwright, it's more a testing tool. So you can make automation, but it's really made towards testing. And testing not only Chrome and Chromium, but also Firefox and WebKit.

And it's maintained by a small but very capable team. Those people, they're really experienced. They worked on Puppeteer for some of them, or on the Chrome DevTools.

We also have guys work on the Chrome DevTools protocol. So a very capable team of brilliant people. Just a word on how it works.

So Playwright is a Node app. So today I will only talk about Node and TypeScript. But actually there are some bindings so that you can use Playwright with other languages.

Just like Java, Python, C Sharp. The idea is that you can use the tooling that makes sense for you. And so Playwright is driving different browsers from the outside through their debugging protocols.

And Playwright is coming with three browsers. Chromium, Firefox, and a browser that is made up of WebKit and JavaScript core. The idea behind this browser is that to have Safari, you need macOS.

To have macOS, you need a Mac. Not everyone is using a Mac. And your CI is probably not using a Mac.

So to have something that is very close, we have a browser that's made with the open source bricks that are behind Safari. So WebKit for the rendering and JavaScript core. But today I'm talking about component testing.

So I'll let a few seconds for you to read that test. And hopefully you should be quite familiar with the syntax. This is because the test framework that comes with Playwright, which is Playwright test, looks like very much just a VTest.

And the getByText or getByRule, it's inspired by a testing library. By the way, can see that it's also Playwright Ambassador. So it's not just by luck that it happened.

And you have expect that was literally just expect. Now they redevelop it because they don't want so many dependencies. So if you're already doing testing with Jest and testing library, you already know Playwright more or less.

Component testing is using VTest in the background. So you have your different components that will be on the test. Playwright will use VTest to bundle that in a simple app, write it to the file system.

And then VTest will serve it again for Playwright to test it. Because at first, Playwright was an end-to-end testing tool. So features.

Instead of making a list of features, I found that I should show you. So I hope everything goes well. So I prepared a small test and I'm developing a component, which is just a simple counter.

So the first thing I want to test is that it works. So you see the mount, it's pretty easy. It's what we call fixture in Playwright.

So you mount it and then you have your components, which is mount result. So you can do some stuff like reload stuff and all, but actually it's a locator behind. So it means that you can do your normal Playwright stuff behind.

So I will check if it's visible. Sorry. So I expect my component to be visible.

You can see here you have all kinds of expects. Some of them are basically the same than jest. Some of them are web-first assertions.

Something that makes sense for the DOM in an app. So you can have like for input, whether it's editable, whether it's empty, whether it has focus, these kind of things. So I will just check if it's visible.

Visible means it's in the DOM and it's rendering to the DOM. My race lint is not very happy because this is asynchronous. So asynchronous stuff, I don't know if any of you tried Cypress or this kind of.

In Cypress, they had their own syntax on asynchronous stuff. For Playwright, it's just a wait. It's just promise.

So let's run that. And it passed. Great.

So here I'm using the VS Code extension. But I will just do it with command line for the next test because I need some kind of watcher. Here we go.

So I have some other tests, so it will test everything. And I save. Okay, the watcher works.

By the way, I want to see my browser. I want to see my components. Oops.

Yeah. Okay. So I have my component.

I started working a bit on it, but this is not doing much. So next thing I want to develop is to increment. So let's make a new test.

So increment when I click or something like this. Okay, so first thing I want to do is to click on the button. So for that, I need a locator.

So it means a way to find my button. So I use my favorite query selector, which is getByRule. This is great because it kind of forces you to make semantic HTML.

A button should be a button, or if it's not a button, then you should use ARIA to tell the browser that it should act as a button. So I found my button. Sorry, I make a locator for my button, and then I will click on it.

And again, this is asynchronous. Okay, so I need to wait. Okay, cool.

It works. Sorry, all of that is a bit small. And my button is really early, so what I will add is some CSS.

So obviously, you can do it in your component. That's one thing, but maybe you have a global CSS in your app. So for that, you have access to some of the files that Playwright builds under the hood.

So you have this HTML and this TSX, and then you can import stuff. This is very handy to import global style or maybe to import some style that you need to force something just for your test, but maybe not in your component. Okay, much better.

Except that my test is not working anymore. You see it's red. I need to fix something.

It's not clickable anymore. Okay, so the last thing I touch is my CSS. And I'm really dumb because I made a mistake in the CSS.

You cannot catch this before the browser because you need the real rendering, the real deal to see this kind of. So sure, it's a bit artificial, but you still can have regression because of whether something is there, it's visible, it's on screen. And now it clicked, and then I want to check that my countering actually increments.

So what I will check is just text. So I check that in my component, it contains a text. So here we are, and then count is one.

Let's format a bit. Whatever. Okay, and it fails because I didn't implement it yet.

So let's go to my components. And yeah, I have my plus. I prepared some work, but I didn't actually make the counter itself.

It's good that I prepared the use state and all because I don't always remember. I made React. I was using React a long time ago, and then I did some Angular, and then now finally I'm back to React.

Okay, so set count, blah, blah, blah. And you see here, actually, you can see that Playwright rebuilt the bundle because I touched the, not the test, but I touched the components. And it's green.

Great. Cool. Okay, next test.

Oh, decrement? Okay. So obviously I need to click on some button and check the count.

So it should be minus one. And yeah, okay, but I need another button, and I need to specify what the button. For that, I will not only just get by row, it's not enough to get the right button.

I will also get this button by an accessible name, something like decrease or decrease button or something. Sorry? Okay, so I need my second button.

Okay, I'm not using Mac usually. Do you know where the shortcut for the emoji keyboard? Bottom left?

Yeah. Oh, great. Perfect.

Thank you. Okay. And yeah, I should change the label probably because, yeah, everything's red.

Actually, two of my tests are red. The increment one is broken as well. Why is that?

Because here, by default, Playwright works in strict mode with the locators. So we say that, okay, this is strict mode violation. What does it mean?

This locator resolves to two elements. I want a button. Actually, there are two buttons in this component.

So Playwright will not choose for you. It will just fail. So I need something more specific.

So name is Anna Puri. Need to change this as well. Oh, yeah.

Okay, how is it? Blah, blah, blah, blah, blah. Okay, I can click my element.

The first test for the plus is working. But the count is not minus one. Yeah, because I didn't implement it.

So I'm very dumb. I just copy-paste that thing. And I'm going to click two.

Why not? My goal here is to pass my test, which is red, which is not passing. So I just want to pass it.

And then it's green, and I'm happy. It's not. Yeah, I didn't change that.

Okay. So many code to change. Whoo, it's green.

It's quite ugly. Sorry, my shortcuts. So increase count a little.

Now I can refactor, because I know that my test is passing. And everything's fine. And whatever I'm doing, it's safe, as long as it has passed.

Anyone familiar with what I just did? Looks like TDD, kind of. Yeah.

Oh, my God. I'm late. So I've shown you web-first assertions, means assertions that make sense in the DOM.

Locators. So I'll just show you my favorite one, which is a testing library one. Auto-weighting means that what should be asynchronous is asynchronous.

And we have debugging in Trezor, but I will probably cut on Trezor. I will just show you really quickly what it is. Because the thing is that when your app is not working, it's probably in the CI.

It's not always on your machine. It works on my machine, but not on CI. So what you have with end-to-end and also with component testing is that you can have a trace.

Trace is like a time lapse. So you have a network issue. You should display something.

So you will have all of the steps of your test with here, a screenshot, and also actually a DOM snapshot. But I'm already running out of time. So I've shown you some nice stuff.

As you can see, I can use Playwright Component Testing as a workbench. It's nice, but to be honest, there are some drawbacks, some stuff that are not so nice. The first thing is that this feature, component testing, is still experimental.

It's been experimental since a while, since at least two years or something. The API is not changing much, but it can. Documentation is lacking, so we probably need some effort to have something better.

But it's also linked with the fact that it's experimental. And to my liking, it's not quite fast enough for TDD. It's not as fast as VTest.

That's for sure. It will never be. But yeah, it's not as fast as it can because of the way they do the bundling.

I wanted to talk about the alternatives very quickly. If you don't use Playwright or maybe the other way around, if you're already using Cypress, you should probably use the Cypress Component Testing. It's really nice.

It's kind of similar. If you're not already using Cypress, then you should check for other alternatives. Same with Storybook.

Storybook is great because Storybook allows you to isolate your components. Then they're quite easy to test. So either by using their own testing solution, by the way, it's Playwright behind the scenes, or by plugging your favorite end-to-end testing solution, like Cypress or Playwright or whatever.

So yeah, Playwright Component Testing, as you've seen, it's packed with features. I didn't have time to show you in more detail the Trezor, but it's really a game-changer. You should try it by yourself.

It's not perfect. It's not perfect. It's still rough, and it's experimental, and maybe in some case, with mocking, you will have some stuff that you will miss.

But I think it's a great workbench because it can help you to isolate your component and have your test, your code, and the rendering all at the same time. I didn't show you, but actually, I was running the test with Chromium, but you can run the test with all three browsers altogether, and then you can see the rendering right away. And since you have the browsers, you can also inspect what's happening in the browser.

So it's really cool, and I hope I convinced you to try it out. Thank you.

[Christophe]
Thank you, Jean-Francois. Please come and take a seat. There you go.

So we might create the questions a bit more and have a few less questions in order to sort of catch up a bit on the timeline, but absolutely go, Jean-Francois, for talking about Playwright during the breaks. Playwright's awesome. So really, even if you're over the Cypress persuasion, it's just you haven't seen the light yet.

So don't hesitate to come and talk to Jean-Francois after. Do you have any...

[Romain]
Yeah, especially that we have many questions about tests. Maybe I will try to take three questions, but in one question. When it comes to UI testing, you have unit testing, end-to-end testing, performance testing.

When would you recommend to use Playwright compared to other tools like Jest, RTL, and things like that?

[Jean-François]
First, you probably need Playwright for end-to-end testing to test at least your happy path because you need to test your app and not just your component and not just a set of components. At some point, you need to test the whole thing. So end-to-end also means the backend.

So for happy path, for example, if you are doing e-commerce website or something, you need to check that people, your client can actually check out and buy stuff. Otherwise, you don't have business.

[Christophe]
You want to test the entire story.

[Jean-François]
Yeah, that's for sure. For component testing, it's a bit more complicated because when do you want to test components with rendering? Then it depends on...

I guess you can do it when your components are reused several times. And even better, if you have a design system, you should test it, and you should probably make your image snapshot and this kind of...

[Christophe]
Yeah, and also if your component uses some web APIs that stuff like Happy DOM or JS DOM do not support, and you have to be in a browser anyway.

[Jean-François]
Yeah, exactly. Some stuff are not possible with a virtual DOM. Just like I wanted to show, I know it's a bit artificial, but I wanted to show with my button that doesn't work that the CSS have in Python the functionalities.

[Christophe]
Another question?

[Jean-François]
There are a lot of questions.

[Christophe]
It's on you. People can pass to you about not having picked their questions. Yeah.

[Romain]
So I will take the voted. How to make a full end-to-end test including the backend? Do you have any advice?

[Jean-François]
Small problem of environment. So you need to run your end-to-end test against something. So you can do it against your prod maybe with some service account or something.

I'm not sure many people do that. Or then you should have some pre-prod environment. Or if you can, just mount the whole in some Docker Compose or Kubernetes or whatever.

So it's more like a DevOps program. But yeah, it's interesting. The ideal thing is something that you can run also locally so that you can run your app with everything server and all on your machine.

But it's not always possible. So it depends.

[Christophe]
Yeah, it's really like either Docker or when the backend maintains up-to-date mocks that MSW can reuse so that you can actually have half end-to-end kind of thing.

[Jean-François]
Yeah, it's always hard to maintain the mocks and to have exactly something that reacts like the real thing. So it's about how realistic you want your test to be also. Degree of confidence.

[Christophe]
Okay, we'll have to cut that short. But please do come to Jean-Francois with all your questions during the breaks. Thank you very much, Jean-Francois.

Thank you. Thank you.