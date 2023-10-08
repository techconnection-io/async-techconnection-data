---
slug: /talks/frenchkit-2022/robin-kanatzar-testing-for-accessibility
date: '2022-09-30'
title: Testing for Accessibility
author: Robin Kanatzar
video: 59uLAKVB-d4
thumbnail: https:/async-assets.s3.eu-west-3.amazonaws.com/thumbnails/59uLAKVB-d4.jpg
slides: >-
  https:/async-assets.s3.eu-west-3.amazonaws.com/slides/talks/frenchkit-2022/robin-kanatzar-testing-for-accessibility/slides.pdf
tags:
  - Accessibility
year: 2022
conference: frenchkit
edition: '2022'
allow_ads: true
---

Hi everyone, I'm Robin, I'm an iOS and Android engineer and I love building accessible applications.
Today I'm talking about testing for accessibility. The idea is to give you a few things, the information to get started with testing for accessibility to do that.
I'll start by breaking down what we actually can test with the machine when it comes to accessibility and then I'll present a few free tools so you can get started right away if you want before you get too excited about automating absolutely everything.

Accessibility is kind of special. It's all about the user experience. So testing with real people who use assistive technology is always better than testing with the machine. The machine testing we're talking about today is really to automate the easiest simplest checks: we can get that out of the way so we can spend more time talking about the more complex facets of accessibility with the real users of assistive tech.

So what are these easy things that we can ask a machine to do for us?
Firstly, a machine can check and tell us if the color contrast ratio between a text and its background is good enough. If it meets the recommendations, it can also tell us if any of our interactive elements are too small: we want them to be bigger than the minimum recommended touch target. A machine can also tell us if we have any elements with overlapping frames. The problem here being unwanted behavior in that overlap zone and a machine can also tell us if any of our elements have accessibility traits that shouldn't be paired together. This could cause confusion or even unwanted behavior for someone using your app with assistive technology. A machine can help us with a few more things but it needs a little bit of human help.

A machine can help us test our app to see if it supports dynamic type. Well, imagine taking a UI test running it on the smallest device that you support but making the font the biggest accessibility font size. If your test still passes, you could say this part of your application supports dynamic type. Well, it's functional but for dynamic type we also need a human to go in and check that we haven't lost any critical information, that nothing too important got truncated when you enlarge the font. Similarly, we could have a UI test run in portrait and landscape orientation to make sure that our app is functional in both. But again, we want a human to make sure that nothing in terms of context was lost.

When we rotated the device, a machine can also prompt us to to ignore elements that are considered decorative from assistive technology. So if they really don't add value, sometimes we can hide an element from voiceover, for example, but only a human can tell you is this element critical or not.

And finally, a machine can help us help tell us if we have good accessibility labels on our elements. It can check, first of all, that all of our elements have an accessibility label and then because it has access to that label, it can tell us if it matches some of the formatting recommendations; tell us if it starts with a capital letter; warn us if there's a special symbol or special character within the string, which we don't want. Things like that. But again, a human needs to come in after the fact and make sure that the word itself that we chose for the accessibility label is clear and really speaks to the context of the element in the application.

To see it all grouped on one slide, we have the things that a machine can do for us with no human help. And then the ones that we have to do human and machine together to test, but this is only a small fraction of what would make our app accessible.

There's a whole other category of things that we can't test with the machine. Right now, we have to rely on the real people who use assistive tech. And an example of this would be grouping your elements into semantic groups. It's a good practice to help in understanding a screen to take elements in to take elements group them together. So assistive technology will read them as one instead of each individual one. But you can imagine a machine can't tell you which ones should or shouldn't be grouped together.

So now that we know what to test, let's talk about the how there's a lot of tools out there. But for today for timing, we're only talking about the free ones.

The first free tool is simply the UI testing framework provided by Apple. If you didn't already know, whenever you make a UI test, you're using the accessibility tree under the hood. It's what you use to find your elements on the screen. It's what you use to navigate from page to page from within the UI test. You have access to things like the accessibility label, the accessibility traits, the frame, you can change the orientation, enlarge the font, all of the things I mentioned before. So UI tests are your best friend when it comes to accessibility testing and they're also the easiest way to get started. If you take away one thing from the talk, go write some strategic UI tests and it'll help with your accessibility testing.

If you don't want to do that all on your own, you can use this testing extension made by Rob Whitaker. [(This QR code will send you to the GitHub repo)](https://github.com/rwapp/A11yUITests). He has done this for you and um you can run all of the almost all of the checks that for the issues that we talked about a few slides before. And the great thing about his repo is you can select which ones which checks you want to run and you can sprinkle some of them into existing UI tests that you have or you can create new UI tests only for accessibility using this extension.

If we step away from the UI testing for a minute and think about the actual development process, when you have your hands in the code, you have Xcode open, you have a tool called Accessibility Inspector. You can launch it from the developer tools in Xcode and with this tool you can run an audit on the current screen of your application. The inspector will analyze what's on the screen and give you a big list of warnings if you have things wrong: like a color contrast is too low, the touch target is too small. Just like up here. The good thing about this tool during development - I tend to think of running it every time, I think of launching my unit tests - whenever you feel the need to touch base and make sure you haven't broken anything yet. It would be a good idea to run this one too to make sure you aren't introducing more accessibility issues as you're building a new feature.

Good one: SwiftLint. Everyone probably already has it in your project. But did you know that there is a linting rule for accessibility? I f you're using SwiftUI you can activate accessibility label for image and this will give you a warning if you include an image that is missing a label and you haven't explicitly marked it as a decorative image. So it basically tells you: either give it a label or ignore it from assistive technology.

The last tool I talked about is from a company called [Evinced](https://www.evinced.com/products/auto-test-sdks). It runs an audit on your app very similar to what we saw in accessibility inspector. But I love this one for QA because you don't need to be in Xcode. You don't need to own the code base. You can run an app on your phone, have it plugged in. Use this Mac application that you download from Evinced. It takes your screenshots, analyzes the screens and it'll give you a much more user friendly report if there's any issues and they also link to their knowledge base to give you suggestions on how to fix it. So this is great either for you to use as a QA or to ask your QA to download.

If we take a look at it, all of the tools that I talked about here on one slide: you have your UI tests with or without the extension. Those could be running on your CI hands off before you release a new version or before you merge something. Then during development every time you think of launching your unit tests you could run some audits with accessibility inspector and during QA you can add this extra layer and use the events to mobile flow analyzer to check again and make sure nothing has slipped through the cracks.

And with all of this together you're in a really good place for fixing an accessibility issue once and preventing the regression from popping up again at least with the issues that we talked about here.

So, to wrap it up we showed you a little bit of what you can test with the machine in the world of accessibility and I showed you the free tools available to you and I hope this has at least piqued your interest. So you go out and do a little bit of your own research and hopefully add more accessibility and start adding accessibility testing to your app.

Thank you so much for your attention.

Simone: So you mentioned that there are paid utilities. Do they provide significant added value?

Robin: Yeah, I think so, there was the company Evinced that has the flow analyzer there. They also do almost the same thing as an SDK and it's paid. I don't know how much it is but it's a lot faster than the open source one I showed so I think it could be worth it.

Greg: Do they work on Web views?

Robin: Yeah that's actually um or at least Evinced on their analyzer. That's one of the things that sets them apart from their competition that they can analyze into Web views: if you have a Web view heavy application.

Smone: And uh that's just um an advice for those implementing accessibility for the first time in their apps with no accessibility at all. What would you start with?

Robin: I think I would start with the accessibility labels. It's the most frustrating thing to just hear from voice over that you're about to select a button but you have no idea what the button is. So if you labeled everything in your app, it may not be the most efficient for someone using assistive technology but at least they know what they're doing.

Simone: And what about images? Like how can you provide automatic tags for some kind of images you might have?

A: That is a good question. I think there was something that came out with iOS 14 where Apple tries to give you a description of the image but I would I would need to check on that one. I haven't used it yet.

Thank you!
