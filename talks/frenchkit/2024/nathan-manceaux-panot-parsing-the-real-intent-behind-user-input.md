---
slug: >-
  /talks/frenchkit/2024/nathan-manceaux-panot-parsing-the-real-intent-behind-user-input
date: '2024-09-23'
title: Parsing the real intent behind user input
author:
  - Nathan Manceaux-Panot
video: riK8aL_yZGw
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/riK8aL_yZGw.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: '2024'
allow_ads: false
---
### Nathan
So I'm Nathan, although I'm only the first Nathan you'll see today, there's a second one later on, and watch this space, he's much better. But I am a macOS developer, independent macOS developer. My slides will show up quite quickly, I hope.

If we could, Melissa, please change the, thank you very much. So, yeah, macOS developer, these days I'm working on retcon, which is a git client for rewriting git history really, really fast, like, before pushing your personal branch and opening a pro request, for instance. So you can say reorder commits just by drag and dropping, and like that's done, no step two, drag, drop, you're finished.

You can also rename commits just by typing in a new name, and no step two either. And you can even use command Z to undo almost anything. It completely changes the experience of rewriting history.

However, I'm not here to talk about retcon today, and instead, I'd like to tell you all about, well, the concept of parsing the real intent behind user input. Now, what does that mean? Well, it's about looking at raw input data, and from that, trying to understand, what did the user intend on doing?

So not just looking at what the user does, but trying to understand, what did they want to do? What did they want to happen? Now, that's still quite abstract, so let's jump right into a demo where I'll show you a simple app I've made for this occasion that actually does user intent parsing really, really badly, so we'll have to improve on it.

So as you can see, it's actually trying to emulate the home screen of the iPhone. So I have pages, and I can swipe between them just by dragging. And already, you can probably see there's something a little wrong here, right?

It's letting us just stop in between pages. That's no good. As a user, you know, I probably just want the page to be nicely framed up big on the screen, but it's letting me stop in there, which is not great.

Now, when you think about it, what the app is doing is actually technically correct. I mean, it's when my finger moves 300 pixels to the right, the pages move 300 pixels to the right. It's technically correct, but it's taking my input at face value.

That's the problem here. It's being too literal about my input. So let's change that, and let's have it try and understand better what I'm trying to do, which is go from one page to the next.

I don't care about the margin. So let's go to version 2 of the app, which has snapping. Now, when I release my finger, it'll snap to the closest page, which looks like this.

And already this is so much better, such a nicer experience. Like I release my finger, and I get a nice page. Now, this, well, I guess you can see the next issue here, right?

Which, yeah, when I do this short swipe, it doesn't seem to go to the next page. That's weird. Well, all right, once again, technically it makes sense when you think about it.

I drag, and when my finger's here, yeah, nearest page is still page number 2. So when I release, we're on page number 2. Bummer.

But you, you the audience, as humans, most part, I think, you can see me do the gesture, and you know I'm trying to get to the next page, even though my app doesn't. Why? What's cluing you in?

Well, you're not just looking at the location of my finger. You're actually looking at its velocity as well. You're looking at the speed at which I'm moving through the screen, and that tells you I'm desperately trying to get to the next page.

So let's go to version 3 of the app, which has a new edition, and now when I release my finger, it doesn't just look at the location of my track. It also looks at the velocity. If it's positive, we go to next page.

If it's negative, we go to the previous page, and this is so nice. This is so much nicer than before. And not just that, but this is on an iPhone.

Imagine this on a wide landscape iPad. You would have to drag your finger the whole way across the whole width of the screen just to get one page forward, and here, one centimeter of a swipe, and we're done. So I think this is a nice illustration of the idea of intent parsing, where you don't just look at what the user is actually mechanically doing, because that's a miserable experience.

No, you actually try to understand what they wanted to do, and this is what you act on. So that gives us a good idea of the value of user intent parsing for touch interfaces, but today, I'd like to show you the same concept in action across a variety of input devices, and so let's start with the next closest one, which is more precise. It's the mouse.

So the mouse is precise. It's one pinpoint cursor, pinpoint precision cursor, instead of ten wiggly sausages just moving about, and yet there's still room to understand, to interpret what the user is trying to do, and so I'm going to jump into a second demo, because I like to live dangerously, but this time, I didn't make the app myself. It's called macOS, and we're going to look at window resizing, which I swear is cool.

Here's a window which we could resize. Let's try that now. All right, this is what it looks like.

Nothing to see here, all right? Well, here's the idea. When you try to resize a window, what do you aim for?

Where do you try to click? I think most people, they will aim for the boundary between the window itself and the outside of the window. They will aim for the edge.

The problem with that is that, well, by definition, if you try and click the edge, well, 50% of the time, you will click outside the window, and does that mean you fail at resizing the window? That would be a bummer to fail at resizing windows half the time. Well, you don't, and so why?

Well, look at this. I get my mouse really close to the window, and I click, and I resize, and it works. I am clicking outside the window, and yet, well, most of the time, it does resize the window.

What's going on here? Well, the hitbox for the interaction, the area in which you're allowed to click, is not confined to the window. It's allowed to go outside a little bit, just a little bit, but it's allowed to go outside, and this way, the hitbox can actually be centered on the edge.

So if I click a bit to the left, it does resize the window. If I click a bit to the right, it does resize the window because the hitbox can exceed the visual boundary of the view. And that's, I think, our first lesson from Apple here.

Don't constrain necessarily your hitbox to the visual bounds. You can be creative. That can help.

And so this was only the first one of two cool things about window resizing. I told you it was awesome because the second thing happened at the top. So if you try to resize the window at the top, we can.

There's this affordance right here. And there's the title bar as well, which I can use to move the window around. Now what happens if I try and move the window to the right, but I click in the resize area?

Good grief, it moves the window, but I thought this was the resize? What is this witchcraft? Well, as far as I can tell, it is not witchcraft, but instead it's the application of something we've seen before.

When I begin my click, macOS does not take that click location at face value. I mean, I click in the resize area. It's quite clear.

The cursor tells us that. But macOS waits to see the motion of our cursor. So look at it.

As it moves to the left and to the right, nothing happens until a few pixels, and boop, it snaps in my hand because it saw that my motion was horizontal and moved to translate mode accordingly. Conversely, if I move to the top a little bit, at some point it will snap, and yeah, we're in resize mode. So one area, two potential interactions.

And this way, well, when I want to move my window, even if I miss a little bit, most of the time it'll work because macOS does not take our click location at face value once again. And so these two things together, the idea of distinguishing between the two interactions and having a hitbox extend outside the window, these two things together, they really make window resizing on macOS that much nicer. And actually, if you've used a different operating system at some point, which does not necessarily have the same refinements, then you will have felt firsthand how much more frustrating it is to try and resize a window that does not have this sort of thinking behind it.

Windows today. Okay, so now, well, let's keep going with the tour. So we've talked about touch, we've talked about the mouse.

What would be a more precise input device there? I can think of the keyboard, but the keyboard? I mean, the keyboard, you press a key, you get the letter, right?

There's nothing special about that. Unless, well, that depends on the key. If you press the double quote key, for instance, well, you can get different curly quotes opening or closing based on where you are in a word.

And actually, you'll get different quotes based on where you are in the world since if you're typing in French, you'll get French quotes. And not just that, you'll get the spaces associated with them because that is what French typography calls for. So yeah, two characters for the price of one.

We have this one key that can do many things based on context. And we actually have many examples for the keyboard. For instance, well, there's autocorrect, famously, where you type one word and you get an entirely different word, for better or worse.

And debouncing, where you're typing in a search field and actually the search field waits for you to stop typing for a while before it sends the network request in order to save resources. And, well, we should keep going. What's after the keyboard?

What's simpler? Well, that would be a single key, like a button. Can you do intent parsing with a button?

Well, I'd say yes. Think about your iPhone lock button. It will lock your iPhone, sure, if you click it once.

But click it twice and you will get Apple Pay. Click it three times and that's the accessibility menu, and long press it and you get everyone's favorite assistant. So four actions on a single button.

And I mean a button, that's like the two-state thing, the simplest possible input device I can think of right now on stage, which doesn't mean much, but that's still something. So intent parsing, it really applies across the whole spectrum of the input devices we've talked about today, from the simpler one to the richer one, from buttons to touch. And sometimes it's to add more actions onto a single simple input device, and other times it's almost the opposite.

It's about having a few actions, like go to the next page, go to the previous page, but distinguishing between these actions more reliably, using the richness of, say, touch input. And so all of this ultimately allows your app to better understand what is the user trying to do, to better respond to user input, which means that all of this obviously is in service of one of the noblest goals of all, an excellent user experience. Thank you very much.

And the last thing is, we have some resources. The QR code will stay visible during the Q&A, so don't panic. And yeah, there's the code for the demo itself, the sample code, and also a few resources from Apple themselves, both on the design side, it's fascinating, honestly, and on the implementation side.

You have my personal links, and you have a link to Redcon, which is a good client to rewrite history really pretty fast. Thank you.

### Rob
I feel like maybe there could be some kind of guidelines, like about human interfaces. That sounds like a good idea. If only someone had that.

But let's be serious. You talk about things like the hitbox. So famously we had the old 44-pixel hitbox.

Is there something for mice and for other types of things, or do you just kind of play with it, or like how far people should swipe or things like that, or do you just need to play with it?

### Nathan
So I don't know of guidelines about that specifically, but there might very well be. However, yeah, I think the main advice would be to play with it. Like for all these interactions, it's about you try it first.

You saw the first version of my sample app, and it was miserable to use. But also, as I said, it was technically correct. Like it's the most naive version you can build.

But you have to build that version first before you can then improve on it and try to find a better version of it. So it's really by using the thing that you realize, hey, this doesn't feel right. And sometimes you have a model to guide you.

Like in the case of my demo, you know, I uploaded the home screen, so I could just copy them. And we're far from having copied them in that sample. And sometimes you don't have a guide, but you do have a guide.

You have your own gut, which is real. Like it exists. I saw it.

And you can actually just try it. And as long as you're frustrated with it, yeah, you can keep going. And so a lot of that would be the fine-tuning, like find the right constant, the right threshold, the right area size.

That's something you can test for yourself, and that you can test on users. You can give the app to users and see, you know, how long they tolerate it.

### Rob
So you say, I mean, you pulled this from App Home, but App Home does go even more. I mean, how do you avoid... One of the things I'm worried about would be false positives, when you start having these little swipes, or people start to pull and then come back.

I mean, does the code get more and more and more complicated, or does it turn out that there's some simple things that work for almost all the cases?

### Nathan
Right. I don't think there's a simple silver bullet. Implementation-wise, I mean, once again, I reinvented the wheel here, so that's not a great example, but, like, well, there's, in the resources, you have something guides around that, like, doing gestures, and, like, Apple has amazing APIs for that, like, where you can really combine gestures, define them, and say, like, oh, this gesture actually waits for that other gesture to fail, to be like, oh, I can't be activated, so we really have good stuff around that. But then, yeah, once again, it's about, like, you know, rejecting palm input.

That's something you can notice in using, and then you can, all right, try and find strategies around it, but it's always going to be, like, creating coding. This is creating coding. You have to be like, okay, yeah, how can I distinguish between an intentional touch and a non-intentional touch?

And the user is not going to tell you. You're going to have a separate button that they click when they're like, I would like to interact with the iPhone. That'd be a lot easier, but you don't have that.

So you have to look at, try and find the minute differences in between the two things, like, oh, this is a mistake, this is not. And ultimately, your thing isn't going to be perfect, but that's okay. You just have to do your best effort at trying to guess at the intent of the user.

### Rob
Fantastic. Thank you so much.

### Nathan
Yeah, thank you very much.