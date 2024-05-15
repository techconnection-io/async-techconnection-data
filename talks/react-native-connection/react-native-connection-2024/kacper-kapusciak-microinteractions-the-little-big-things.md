---
slug: >-
  /talks/react-native-connection/react-native-connection-2024/kacper-kapusciak-microinteractions-the-little-big-things
date: '2024-04-23'
title: 'Microinteractions: The Little Big Things'
author: Kacper Kapuściak
video: 6wU3FJMfdhI
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/6wU3FJMfdhI.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: react-native-connection-2024
allow_ads: false
---
[Kacper]
So, for example, if you have a banking app that would look like this, your users would have to, like, think a couple of times before sending money to it. It doesn't look like a banking app. So I'm not a designer myself, but I have a big passion for one thing and design.

These are the microinteractions. These seemingly small things can be very, very important and can make a huge difference for a finished product. So, well, I'm Kasper.

I work at Software Mansion in the React Native team. As Mo mentioned, I maintain some of the libraries. I help maintain reanimated, gesture handler, and screens.

Currently, I'm working on a new tool called React Native IDE, a VS Code extension for debugging React Native apps. That's about me. So let's get back to the content.

What are the microinteractions, anyway? So I want you to think about a car. Any car is fine.

You have something in mind? Yeah? Okay, cool.

So Dan Suffer, in his book about microinteractions, splits the interaction design into two. So it splits to macro interactions and microinteractions. And macro interactions are the main feature of something, of a product.

So you have a car in mind? Right. So the main feature of a car is to get you from point A to point B.

Main feature of a vacuum cleaner is to, well, vacuum, right? And microinteractions is everything else. So, for example, the feel of the steering wheel.

Is it made of leather? Is it made of rubber, plastic? How it feels?

The way a dial clicks when you adjust the volume on the radio. It can be very satisfying. The sound the door makes when you close it, right?

So you can't tell me this is not important. The microinteractions aren't important. Because when they add up, they can make a huge difference.

And there's a difference between an S-Class Mercedes and a Peugeot, right? Sorry for those two. I knew it.

I knew it. And this microinteractions can create something called a signature moment in your app. So like an iconic moment for your application or for your product.

So we are mobile developers. Most of us are. So, for example, on Instagram, you have a double tap to like a very iconic interaction.

On Tinder, you have swipe, which is now like copied on Slack. Even for swiping through messages. You have a swipe up on TikTok.

And it's copied also to YouTube Shorts and Instagram Reels. Very, very signature moment for this application. And microinteractions have a structure.

So Dan Stafford created his book and says, these are the structure of microinteractions. And there's a pure coincidence that this is exactly the chapters of my presentation. So you have triggers, rules, feedback, loops, and modes.

So let's maybe start with triggers. Triggers is what starts an interaction. So this is the entry point for any interaction.

And we have manual triggers and automatic triggers. So when you have manual triggers, I want you to think about more like buttons. We'll get to that.

And automatic is more like system-based. So a notification, for example. So manual triggers is everything that the user has to interact with by clicking, tapping, so buttons, switches, also checkboxes, et cetera.

And triggers can also be invisible. Remember our example from TikTok from swiping? There is no button for swiping.

The whole screen is a trigger. So these invisible triggers, OK. In React Native, there is, for example, shake to debug.

It's also an invisible trigger. These triggers need to be learnable. So at TikTok, they thought, OK, the first time a person uses the app, let's show an animation.

Hey, you can swipe up for more, which is brilliant. And triggers should initiate the same action every time. It's a frustrating experience, but I have a great example about that.

There is this app, the official national app for looking for train connections in Poland. Connections. And it has this refresh button in the bottom corner.

And this refresh button works differently when you tap it first and when you tap it the second time. So when you tap it first, it refreshes the feed. Fine, perfect.

But if you refresh again, it will block your app. You did something wrong. How could you refresh the app?

So this is such a frustrating experience. Why would you do that? A much better way to deal with this, because this is probably some legacy reason to add that, probably.

Just to not do that and create a simple text like, you're already up to date. That would be way better. Way simpler as well.

So we have manual triggers. We also had automatic triggers. So, for example, you have something based on time and dates.

A reminder or, yeah, something like an event in your calendar. This is based on the time. You have errors.

Something went wrong with the system. You need to show it to the user. The triggers can also be triggered by other people.

So someone sends you a message, or your Uber is at your door. And based on location. So, for example, the app can work differently when you're at home or at work, right?

A different location. This is called geofencing. So an example of time and date interaction is on Slack, you have a happy anniversary on your profile.

Cool. I guess. So we had triggers.

We have rules. So the rules govern the interaction. So how should the interaction work?

And what I'm trying to say here is that your users probably come with some established mental model about your app. So they know exactly how should this play button work. Like, they've used smartphones for a decade now.

They know how it should behave. So try not to break the established model of the user. So the play button here should just, the user taps the button, it starts playing the music, and it changes to pause.

If you break that established model, it will lead to confusion. A great tip about building interactions is to just create user stories, like a short sentence. If you can explain your interaction with a short sentence, where the noun, so the play button is a noun, is the trigger, you're doing great.

If it's a couple of sentences, you should split the interaction into smaller interactions. That's a pro tip for you. And about the rules, each platform has its rules.

We are cross-platform developers. So for example, there is a native model used on the left, where there is someone created a model from scratch, and it doesn't look right. It doesn't behave like a model from iOS.

If you can, try using the native components. So for example, here is just a model from React Native. You don't have to re-implement that.

Feedback. So feedback emphasizes the rules. So you kind of get what feedback is just from life, just getting feedback to someone.

And in our previous example with Azure, there is a progress bar when the song is playing, that yes, indeed, the song is playing. It's a way of conveying feedback. And there are different ways to convey feedback.

So for example, we have animations. And the animations should be very, very smooth, very fast. And what I'm trying to say is they shouldn't block the user from interacting with your app.

Even if you have the most beautiful loading animation, just skip it if you can. Just the animation, the app should be as interactive as possible, as soon as possible. We have animations.

We have messages. This is all the microcopy you have in your designs. So labels on forms and error messages, they should be concise.

Haptics, which is pretty cool. Just don't overdo it. Very cool way of conveying feedback.

And we have audio. Everyone has their phone silenced either way. Unless you're building a language-learning app like Duolingo.

But yeah, no one uses audio anymore. About animations, the default presets for React Native, at least to me, that's my opinion, are too slow. So the default here would be at 300 milliseconds.

It should be OK to just use 150 or 200 milliseconds. And even not using withTiming, you often use withSpring instead, which is based on physics rather than time and easings. It can lead to more natural results.

But also the default preset is a great starting point, I would say. But it needs some adjustments for your animations. So loops and modes.

You're all programmers or kind of get what programming is, I hope. So you can know what loops are. And loops are something that is either while loop or for loop.

So while until some time in the future or based on count. I'll get to that. So for example, remind me in 10 minutes is a time-based loop for interaction.

Or do something every 30 seconds. Or try to reconnect three times and then, I don't know, fail, do something a couple of times. These are loops.

We also have modes. Generally speaking, you should be avoiding modes. Modes can be pretty confusing to users.

So for example, we have a microwave that just have a one dial for inputting the power and for the time. And it can lead to confusion for people. For example, caps lock also can be confusing.

It changes the way your computer works. You are not inputting lowercase letters, but uppercase letters. And how many times have you tried to input the password and it didn't work because of caps lock?

So if not avoided, they should be well communicated. So your phone does a really well job of communicating if it is in a different mode. So we have do not disturb mode displayed at all times as a notification or in the bottom of your phone, which is really cool.

So let's observe the practice part of this presentation. I have some animation. Good.

I have prepared three animations for you that you can use right now in your application. And these are also made with, you guessed it, reanimated. And these are very, very easy and very short to add.

So you have a explore icon that rotates by 100% 180 degrees on top, right? Pretty cool, pretty simple. You do it by having an icon, SVG icon, that has some React state passed to it.

And this state changes whenever the icon is, well, active. It's a Boolean from true to false. Based on that state, we can use the right value hook, which you can use the React state inside of it to create a shared value.

A shared value is the driving factor for all animations in reanimated. And you can create it with use shared value hook or use the right value. And whenever the React state changes, it will change from 0 to 180 with spring animation.

We can use that rotation shared value and then use animated style hook to create animated styles that listens to the change of a shared value. So here we have transform.rotate, and it changes from 0 degrees to 180 degrees. It listens to the changes of a shared value.

It is the same shared value we had in a previous step, yeah. To make it work, to make it animating, we need to wrap our SVG with an animated view and pass that animated style to it. This animated style right here.

And that's it. So wrapping the SVG is way easier than animating SVGs, but it is also possible to just implement it in the SVG layer if you want. Yes, okay, next, next, next, yeah.

So we have that animation of rotating icon on click. Pretty satisfying. Next one, I have a staggering effect.

So animation that shows views one after the other as they appear. And this is implemented using the layout animations also from reanimated. And this is very, very easy to do with layout animations.

So yeah, let's do it. So we have a data array coming from props, and you just map over it and render some views and text. Pretty standard stuff for React developers.

We need to change those views and texts to an animated components. So animated.view. And we pass to that animated components entering props. So we have, for example, fade in right or sliding down.

We have many presets coming from reanimated, like fades, zoom, bouncing, zoom in, all the good stuff. So you can just use them. You don't have to implement them yourself.

And to implement the staggering effect, you just do a dot delay right here. And this is pretty smart when you didn't know about it. But if you know, it's obvious.

The index of an array starts from 0. So the first one is 0 times 150 milliseconds, the delay. And then it's 1 times, 3 times, 150 milliseconds.

They will appear one after the other thanks to this. Pretty cool, pretty simple few lines of code. Yep.

Cool. And last but not least, we have animating elements between the navigation screens. So we call it shared element transitions.

This is very satisfying to do and very, very, very simple. So shared element transitions are currently in experimental phase, more like beta phase. But we will very shortly, in like two or three months, make them stable.

We are working on this. And you implement this by having a screen with an animated view and some styles. So any layout styles work like width, heights, and borders work out of the box.

You have a different animated view on a different screen. Keep in mind that it only works in native stack. It also works in XProwder.

That's the same React navigation native stack, but it has to be native stack. We are working on bottom tab support. But yeah, native stack for now.

We have these two components on two different screens. And we need to connect them via shared element tag on both of the screens. And that's it.

That's it. It just works. So this talk was based on a book about microinteractions from Dan Saffer.

It was a speed run, as you've said, as you've seen. I highly recommend you checking the full book, because it's really great. It's about data.

The examples are data. But the base is still there. And I also highly recommend checking out Design Spells, which is a database for looking out for interactions which other people have made.

And thank you.

[Mo]
Thank you very much, Kasper. Please come along and we'll do a very quick Q&A. Come here, pal.

He's been looking forward to this. I love Q&As. Cool.

So first question is, what do you have against Peugeot? Against what? Against Peugeot.

Peugeot? Ah, no. It's fine.

[Kacper]
It's fine.

[Mo]
You chose the wrong audience to do that joke. I did that on purpose. Oh, yeah.

You like controversy, don't you? All right. So first question that I want to jump in with is your three examples are really cool.

Beautifully animated, as expected. For the first two examples, I want you to kind of talk me through the advantages that you see of using reanimated in those simpler transitions, because none of them are using gestures or anything. So they're not live animations.

They're more just static animations that happen on a trigger. What's the benefit of using reanimated over just using the animated or layout animation APIs from React Native directly with a native handler? And are there any performance benefits of using reanimated?

[Kacper]
Perfect. So in these two examples, they are very, very simple. Besides the layout animations, which are kind of experimental in the animated part, they don't work really well.

But we have a better API. Like the declarative approach is much better, much modern API, rather than just animated. That's one of the benefits.

And we support 120 FPS out of the box. So that's also better for the user. But these are the two examples I can think of right now.

[Mo]
Cool. All right. I'm going to just quickfire.

So answer these as quickly as you can. And we'll get back to the, we'll go back afterwards. So just quickfire.

Did you consider starting a new app from scratch? No. Sorry.

This is the wrong questions. Oh, no. I've messed up.

Well, all right. I'll try my best here.

[Kacper]
All right.

[Mo]
Software mansion slides look wonderful.

[Kacper]
Thank you.

[Mo]
That's the first thing that I'm seeing here. Please explain to the world why we shouldn't use React Native's animated API. So now you've done the pitch for reanimated.

Now do the anti-pitch for animated.

[Kacper]
No. So for most of the cases, it's fine to just use animated. Like the base, the core is fine, especially the native drivers.

But it has some limitations that reanimated doesn't have. So animated layout props, layout styles on native, use native driver doesn't work really well in animated. And without native driver, you have them on a JS thread.

If your app is doing a lot of animations, it doesn't work. Like it can have an ANR, application not responding, because of the animations.

[Mo]
And then the other thing, one other question was, if I use ExpoRouter, what's the alternative for shared element transitions?

[Kacper]
It's the same. It works exactly the same. So you just use the shared element tag.

And it works the same, because ExpoRouter uses React navigation native stack underneath. You don't have to do another configure or anything.

[Mo]
Does reanimated work in TV apps? You may not know. The answer to this is yes for certain platforms and no for other platforms.

A lot of TV OSs are web-based. And it's, yeah.

[Kacper]
So for example, for Windows support, we only do on the JS thread. So it's a web implementation working in JS. And on TV, it's the same.

[Mo]
And I wouldn't recommend that, just because of how low the web implementations on how low the resources are. Someone who's a web developer is terribly jealous of these animation possibilities for layout-based ones. And they are crying.

So my condolences. Lastly, final one, any updates on the React Native IDE?

[Kacper]
Any updates? Yeah. So people seem to know exactly what we do.

So today, we are having a private beta announcement on Twitter in a couple of hours.

[Mo]
That's not so private anymore, I guess.

[Kacper]
Well, the announcement is public. But the beta is private. So you need a form for having it.

[Mo]
That's just mean.

[Kacper]
Sorry.

[Mo]
Cool. All right. Thank you so much, Casper.

And great to have you with us. Cheers. Thanks.