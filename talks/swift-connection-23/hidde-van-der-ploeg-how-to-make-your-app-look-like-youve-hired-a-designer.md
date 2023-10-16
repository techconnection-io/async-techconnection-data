---
slug: >-
  /talks/swift-connection/2023/hidde-van-der-ploeg-how-to-make-your-app-look-like-youve-hired-a-designer
date: "2023-09-21"
title: How to Make Your App Look Like You've Hired a Designer
author: Hidde van der Ploeg
video: tlk9BRvIbq4
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/tlk9BRvIbq4.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/477c5b8208ac40f3bae075e1d74080f9/slides.pdf
tags:
  - Design
year: 2023
conference: swift-connection
edition: "2023"
allow_ads: false
---

First of all, thank you Swift Connection for having me.

I'm happy to talk about design.

My name is Hidde, it's pronounced hidden without the N.

This is a very common mistake.

I'm a Dutch designer turned full-time indie dev since a few years.

Basically, I taught myself how to program because I didn't want to find a developer that was just as enthusiastic about my apps that I was.

Today, I have six apps in the App Store.

They're all very different.

Almost all multi-platform, definitely all watch-wise.

Yay, team watch-wise.

I've been designing apps for about 15 years now.

And if you look back, these things were cool.

You had gradients everywhere, textures everywhere, gloss was everywhere.

I mean, I can't believe we couldn't use the phone without sunglasses on.

But that's enough about me.

I only have 15 minutes, so we're gonna make this fast.

First of all, when you talk about design, you think about these two tools, right?

The enemy of Xcode, basically.

Well, the good thing is to do better design, to become better at design.

You don't really need these.

It helps.

It helps definitely when you create visuals.

But visual is a whole other talk.

So I'm going to give three main pointers.

I think it says three, but actually it's like 12 or 16.

I don't know.

But I thought three was better.

So we started with the first thing.

You open Xcode.

You start a new app.

You have found a cool name through chatDpt or whatever.

You're creative.

So you start with style definition, right?

This is the first blank canvas that you face.

So you start with defining a clear brand and defining clear brand is super important.

Even if it's just a tint color.

I mean, every project comes with a default tint color.

I think it's blue, but that's why, maybe that's why so many apps are blue.

And how do you do this?

How do you pick the right color?

So for me, and I think for a lot of designers, picking a color is the most difficult thing to do.

But luckily enough, inspiration can come from anywhere.

It doesn't have to come from other apps.

It doesn't have to come from other colors you like.

It could be your favorite color, as long as it fits the thing.

So when I say everywhere, I literally mean everywhere.

This is something I do.

I, if I see a picture of, or an image or something,

I think like, oh, I like those colors, could be an octopus apparently.

Then I save them and I get some colors from the slides.

So basically you can turn any image into a color palette.

So in this case, I would like the blue because as I said, blue is very popular.

So you have your base color based on an image, right?

And then these HSB sliders, hue, saturation, brightness sliders, sometimes it's L for lightness, I don't know, people can't agree on things, are your best friend.

So you keep the same saturation brightness, you change the hue all the way to the right, you have a danger color, or if you're from China, probably the positive color.

You change the brightness and you have like a different tone of your color.

This is a very easy way to create a bigger color palette for your app.

So then this is the base thing that everyone always thinks, like, oh, design is just how it looks like.

Well, it's actually how it feels like.

And to give you an example, let's start with, hitter is following you.

This is neutral on its own.

It's a bit as basic as it gets.

But if we make it red and with a hard line, no rounded corners, this becomes dangerous.

I think this hitter guy sounds like a stalker in this case.

So what did we do?

We make it more round, we change the color to blue.

This already looks friendly.

We add a context, a little icon.

Now it's clearly for some social network.

And if you compare this with a few steps, it's a completely different message.

And to give an example how I applied that to one of my apps, this is an app called Gola, which is your bigger goal tracking app.

I always had the idea, OK, goal tracking is very personal, and what do you do with things that are personal?

You write those things down, you make little drawings.

So I was like, that's gonna be the branding.

So for every single part in the app, even like tutorials, like you can see here with tab here and add here,

I try to make it feel a bit more human, feel a bit more organic, just while keeping the sterility of seriousness of like making progress.

So in a way, you have to decide what feeling fits your app the best.

And I know it's very difficult to listen to your feelings.

We can talk about it later.

I'm open at the bar later for feeling talk.

But honestly, it goes to like, OK, a bank should not feel like a game, right?

And a to-do list should not feel like a bank, in a way.

So honestly, get some part of feeling. write feelings down that you want your app to convey, and then you can find inspiration around those feelings.

Then we get to point number two, consistency.

Consistency is difficult. But consistency is very important.

Consistency helps users recognize UI patterns.

So a good example is if you use the default UI kit or Swift UI, all the components from Apple, it immediately is easier to use because they're familiar.

They don't have to think about it.

And they don't have to, it's clear right away what they need to do.

How do you achieve consistency while still customizing, centralizing?

And this is not a design system talk because you can go to any design conference for that.

This is still a developer's talk-ish.

So you start with Swift.

All my code examples are Swift UI, just to be clear.

You start with an extension of color just to define, to make it clear, like this color is used as, like the CTA button.

Right now I use this MP tint dark, but if I feel like I need to change the CTA colors,

I at least have to change the one spot and everything is still consistent when there's one main action to do.

You can go as far as what it is for GOLA by going like completely nuts,

'cause yeah, I'm still a designer and I like colors.

So I made a tint, a background, car background, bottom, gradients and shadow.

But by defining those on one spot, I had the structure for a team and I could easily change the color to whatever I feel like.

And to this day, even when I find a new image, like the octopus, then I can create a team out of it and it's just changing a few variables and there's a taste for everyone.

Luckily, with the new app structure from SwiftUI, it's also very easy to stay consistent in your fonts or in your tint color.

So if you only change like the tint or the font design, in this case the rounded, this would make sure that every single label in the app is rounded.

Or every single tint and also basic UI control is in the right tint color.

Of course if you don't have theming, you don't really need the tint color here because you can put it in the asset catalog, but just to show you how easy it is to stay somewhat consistent at least, if you forget about it, it still looks and feels the same.

The same is for fonts.

Also just centralize it, even if it's just for the sake of having it on one spot and not be able to mess it up somehow, not be able to have custom fonts in the middle of nowhere.

A good rule of thumb is to try to keep the sizes very similar to the native sizes. because you can say relative to, but also because they're very familiar and they fit for most cases.

Like, there's a whole team of designers at Apple that came up with these sizes, so why challenge that?

By centralizing this, you literally reduce any risk of going nuts and going full custom for one specific view.

If you do, please keep an eye out for, like, hey, I'm doing something completely off the book.

Should I really do this or should I change the design to fit more with what I decided for earlier on?

A good rule of thumb, basically, is do not reinvent the wheel unless you're 99% certain.

A lot of the UI components, a lot of things have been thought of for years.

I mean, we're on iOS 17 now, that's 17 years of thinking.

You can try, but I hope -- I wish you good luck with the bug reports.

So then the last point I want to touch on is doing too many things all at once.

This is basically the most common problem I see in most UIs, where you get like a few

And as a developer, you build this new feature, so like where you put it, in the Home tab.

And another new feature, where?

Home tab.

Everything in the Home tab.

If you can't find it, put it in the Home tab.

User will find it.

That's not good practice.

The good practice is to keep focused.

Try to think about every view.

What is the purpose of this view?

What do I want the user to do here?

And one way to get focus is with hierarchy.

Hierarchy is a very difficult word to spell, but it's also very difficult to get right.

The reason why, there is no simple rule of thumb, this works everywhere, but hierarchy can be achieved in many different ways, especially with text.

You can have this, this has no hierarchy, but you can have different weights, you can have different sizes, different colors, different fonts, or mix up all of them.

This only shows like experiment with hierarchy in text.

See what fits best.

But please keep the hierarchy fixed to the one thing that that view needs to do.

And then once the hierarchy is good, give it some space to breathe.

It needs some space.

No, there's edges everywhere.

Give it some space.

And a really good tip to do this is we all know this.

So if you magically align these two, the padding with the corner radius, this is a secret trick, 99.9% it will look nice.

Even try to double the padding, and then if it's too much, go down to the minimum of the same as the corner radius,

'cause then basically it will always match nicely with the rounded corners, and it will all look fine.

Then just ask, again, I can't stress this enough, continuously ask yourself, why do people use this app?

What does this view need to do?

The why is super, super important.

Because when you focus on intention, it removes as much confusion to the user straight away.

And a good example is watchOS, again, TeamWatchOS.

This tiny screen, this is also why I'm such a fan of WatchOS platform, is because the tiny screen forces you to create focus.

You can basically only do one thing, because there's only like six buttons fitting in that tiny screen, max, that's already cramped.

So I think WatchOS 10 redesign really clearly shows how clear focus can be, and it just looks a lot nicer when there is good focus.

It's also really important to stress navigation,

But navigation is a whole bigger topic that I will not talk about too much, because it's all-- yeah, like I said, it's big.

There's a good talk about navigation from WWDC last year.

I really recommend to watch this, because they go into that, like, when to pick tapboard, when to go for modal, and when to do a push.

And they will also stress, like, please keep focus on doing one thing and not too much.

So now it's time for the bonus round.

This is where the secrets of the designers guild come to life.

First thing is we love to nitpick details.

I'll give you a small example.

This is not me Rickrolling you.

This is actually a screenshot from my app.

But what you'll notice is there's these tiny little icons.

I could have just put labels there saying, OK, won a Brit award.

There's some rich media involved. this is the release date.

Other than also seeing the hierarchy here again,

I went the extra mile and made icons for all genres and all types of information that I can find about a song.

Of course, I understand, I am a designer,

I can whip out an icon like that, but it brings me to a point that you can always find an icon pack somewhere or just use SF symbols, but try to go the extra mile to make things a bit more visual, make things a bit more fun.

And what also is fun is animations.

So animations is a really difficult thing to get right.

But luckily enough, there's plenty of good SwiftUI APIs, especially since this year, where even the spring value got to be the default. But please just add them and see if it feels right, because I think

It's easier to remove an animation again than to add, and use that same animation that you created for this one thing somewhere else.

But at least your app feels a bit more organic, a bit less still, a bit less stiff in a way, unless you're a bank app, then don't animate anything.

Another example of a new API that got introduced is for number values.

This is the default behavior, which is not that bad on a widget.

On an app, it just changes, right?

But with three lines of code, I think maybe even the identity transition could be removed, and the infallible content is only for widgets.

But with the numeric content transition, it looks so much nicer, and it costs you one minute-- no, I mean, come on.

If you write this in one minute, you're a professional typer.

Maybe five seconds.

But yeah, then again, animations are hard.

So luckily, there's things like pow from moving parts, where they basically have loads of nice transitions for you to use straight out of the box.

It's only $99, I think, for one-time purchase.

Honestly, it's a no-brainer if you just want to make your app look a bit nicer.

And then this one.

This, as a designer, this hurts the eyes the most.

The left one, where the inner view does not match the corner radius of the outer view, we get nightmares from this.

So if you want to become friends with more designers, just use this secret formula.

I mean, it's not secret, it just sounds cool.

But this formula, and it will look so much nicer.

SwiftUI has a thing called content-relative shape, which works fine in widgets, but gets to straight corners real fast.

And then we're back at this one, our favorite tool.

This is our design tool.

So the best part of designing with this tool is this shortcut.

Does anyone know what this shortcut does?

Yes, it opens this boy.

It's my favorite shortcut.

So whatever you do, after this talk, and if you have talked about your feelings to me, please just read the interface guidelines every now and then.

It updates fast, it's nice content, you don't have to listen to what they say, but at least you can say to your designer,

"No, the interface guideline says that this is the way."

It's fun, trust me.

I come from the other side, when I learned how to program, it was the best superpower to get.

Yeah, so that was my talk about design.

As I said, it was lightning, I tried to make it fast,

I'm all open book for the rest of the conference.

So most important thing, have fun building cool apps, please.

Thank you very much.
