---
slug: >-
  /talks/flutter-connection/flutter-connection-2024/esra-kadah-from-touch-to-code-flutters-gesture-mechanics
date: '2024-04-24'
title: 'From Touch To Code: Flutter’s Gesture Mechanics'
author: Esra Kadah
video: grZRXGa_gRc
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/grZRXGa_gRc.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: flutter-connection-2024
allow_ads: false
---
[Esra]
I'm Esra, and today I'm going to talk about Flutter's gesture mechanics, and let me just check it out. Okay. We are fine.

So first of all, let's meet me. I'm one of the co-organizers of Flutteristas, and you can also see me actively talking in Flutter communities. I'm one of the ex-organizers of GDG WTM communities, and of course currently a full-time developer in Flutter and Dart.

And today we actually have a super short talk. It will be like ten minutes lightning, then we will have our coffees, and what we will talk about is we're going to go for touch screens, types, how they work, gestures, gesture detector, how does gesture in the gesture arena, small awareness movement which I really love related to user experiences, and, of course, conclusion and Q&A part. So, we are all here to answer this question, how does our swipes and taps are translated into the code?

And I just need your full attention, only for seven minutes, it will be pretty quick. Please do not try to grasp every single definition that I'm going to mention. It will be too fast to grab everything, and trust me, go with the flow.

So first we're going to start with two types of screens. One of them is resistive screens, and the second one is capacitive screens, and resistive ones are the ones that we always see in kiosks, ATMs, and so on, and the capacitive ones are the ones we use in our tablets, computer, actually, our smartphone, and, you know, when I say what's the difference between those, you can easily probably say sensitivity, and let's go what's happening behind the scenes.

So resistive touch screens are actually has two layers, and it's slathered with a conductive material, so when you actually have the mechanical touch, and a press, it actually sends the electricity to process in XY dimensions, like a plus sign, and then it can match up with registers and see whether it does anything, and in capacitive touch screens, we have four layers, the top layer is actually made by mostly, you know, gorilla glass and glasses, so beneath this glass, there is diamond-shaped grids that you can see it on the right, separated with a transparent insulator, normally it is not like red and blue, it is just for you to grasp the grid and diamond shape a little more, and the material called between is ITO, it is excellent electrical conductivity, it gives us, and then the bottom part keep the electrons in place, so that, actually, we have negative electric field at the bottom, and then positive electric field at the top, so once you actually click on screen, you are literally messing up with electrical field, and then it is just sending the signals, and processor can say, yeah, she touched here, it is like X 50, Y 100, it is very much more sensitive, because it can actually understand what is happening with the electric field change, then we will immediately go for, yes, this happens, when there is a water droplet, when you are using your gloves, you actually cannot mess with the electrical field much, and water droplet is just causing, it is just touching anywhere, now it is not like a regular touch, but it is just getting multiple touch points simultaneously, and it is causing confused behavior, that is why water droplet is not really a friend of it, and when we talk about gestures, of course, probably this is our, like, daily life gestures that we know, you know, swipes, pinches, zooms, swipe right, swipe left, double taps, and so on, and once we go for gestures, we always have gesture detector in our mind in Flutter, and it is just a widget that detects gestures, I think all of you had a little probably iterations with gesture detector already, let's see what is going on with the simple print, in global position, we can see, like, basic offsets as an XY dimensions, but what is going on behind the curtain is it actually has a gesture recognizer, and it has tap gesture recognizer, and it is actually calling our print function to see what is going on, but when we think about all the stuff and processors we mentioned before, this should be something going a little bit deeper, right? Like, this is just too simple for it. Actually, we have listener widget to see even more raw data about what is happening behind the touch, it has pointer event, and pointer event has position, time stamp, kind, device, and better ID, and even more, so once we just log this, it is just like simple rectangle for us to see, so now you can see offset, you can see time stamp, pointer device kind as mouse, and so on, this could be touch, mouse, trackpad, stylus, so now you can actually differentiate between device kinds, and you actually have at the end the embedder ID, in case you connected multiple devices to your main device, let's say, but we have actually another layer of complexity here, because as you can see, the event data there, like the logs, are actually stream of data, and this stream of events coming with its own complexity, it is starting from the first data received by the listener, so once I see this data, we actually don't know whether it is a tap, whether it is the beginning of a double tap, or maybe it is just first data of log press, I don't know, I cannot see the feature, it can't too, so what are we going to do next? This situation called gesture disambiguation, and we actually need to define what is happening behind the scene.

There is a gesture arena, and this resource provided by Flutter, it has recognizers, and it is going on like what is going on behind it, but we will just proceed with a small example to grasp what is going on with algorithms there. So, we have our gesture detector, we have tap gesture recognizer, double tap gesture recognizer, long press gesture recognizer, and we have a gesture arena. Now, they're going to start fighting with each other to see which one is winning.

And these are our gesture arena members. We have only two rules to decide who is going to win. First one is at any time, a recognizer can defeat, like declare defeat, and say, this is not me, I'm leaving, or any of them can say, yeah, it is definitely a double tap, I won this arena, and then we would say, okay, this is the double tap.

So, let's give it a start with a directly real-life example to see. So, we have gesture arena, we have our members, and we have recognizers, and there is a time span going on. Let's say our user had a small touch, now the fight has started.

Well, like three of them are waiting to see which one is going to win the next. But around 50 milliseconds, we just got a pointer up event received, which means the user just left a finger, and this will actually eliminate the long press recognizer. It will be like, nah, it's just too early for it.

Normally, long press recognizer would wait up to 500 milliseconds to say, yeah, it's definitely a long press. Now, it's just too short for it. It's leaving the arena.

Now, we have tap recognizer and double tap recognizer on the arena, and let's say nothing has happened until 300 milliseconds. Nothing is happening. So, let's see what's the result of it if nothing is happening.

Double tap recognizer will say, unfortunately, there is no other action, it's just going to leave, and it just admits defeats. We only have tap recognizer left, and, of course, once there is an only single member stay in arena, it will be tap recognizer winning, and your gesture detector will call on tap function now. And I want to just go for super small thinking out of our habits right now, because I want you to think about gestures we have daily.

Now we are actually scrolling through Instagram, and we are, like, you know, doing a lot of horizontal, vertical swipes, then we see lots of boring stories shared by an influencer. We are, like, okay, skip this, or just now we are swiping right or left to just ignore that content, or we are simply double tapping to a picture to like it, and it is actually, like, quite a habit of us now if I just when I tell you, you can easily simply imagine those gestures. And this is, like, how much our habits has evolved, and these gestures are not just simple actions, because now in 2024, these are really primary means of human interaction now, because we are literally living with our phones, and it's even evolving more with AR, VR machines and so on that we are just trying to understand what users are doing.

And for this talk, I wanted to just give you a little bit insight about what's going on behind the curtain, and I want you to, like, feel once you are using gesture detector again or your phone today, I really would like to have a moment to appreciate, like, the complexity behind of these, and as developers, we are defining these actions. These are getting a habit of users. So it could be even worse than this.

We have, like, we could have just, like, a picture with five tabs, or we would just swipe our Instagram with, I don't know, three fingers horizontally. This is actually totally possible to program also. And to just have a small going of what did we cover in the seven minutes, like, we go through, like, different type of screens, we see what's going on technically with electric field and so on, we connect it with the gestures, we connect it with Flutter and Flutter gestures, and then we went for how this algorithms are getting our gesture definition.

So this is quite quick one. You can ask me anything, and in this QR code, I actually have a Google form for you to fill it, because now I just raised the point that let's think about what these gestures could be differently, and I want you to send me with this Google form your outside of the box gesture ideas, and I'm planning to do them in our in my next talks, and definitely for some submissions, I have some swag, I have some dash, I have some, you know, small pins as a gift, and thank you for you. So thank you for listening to me, and hope it just clicks something in your mind, and now it's a little bit different. Thank you.

[Guillaume]
Thank you. Thank you very much, Ezra. Thank you.

Do you care to join me for a couple of questions?

[Esra]
Yes.

[Simone]
So please sit in the middle.

[Esra]
Of course.

[Simone]
All right. Let's see. Let's start with the basics.

Why are we replacing all the resistive screen with the capacitive ones?

[Esra]
Because actually the capacitive ones we use in the iPhones, in iPads, and so on, when you consider the ATM kiosk ones, the resistive screens are way much more durable. It's like less costful to maintain and so on, and is this one, this part is also getting recorded now?

[Simone]
Yeah, sure. Yeah.

[Esra]
Okay. Now I will just cut it a little bit slower. I wouldn't want to have a drunk person ordering a burger using my iPad that much, and it would be like causing me some trouble.

[Simone]
Yeah, sure.

[Esra]
So resistive screens are always a go-to to reduce effort, reduce maintaining, like they are more durable, and capacitive ones are more of personal and professional use, I would say. All right.

[Guillaume]
They're probably cheaper too.

[Esra]
Definitely.

[Guillaume]
Yeah. There's a technical question from somebody who's saying that the Google form needs permission.

[Esra]
Form access? Okay. I will just fix it out.

I will just tweet it.

[Guillaume]
Thanks, guys.

[Esra]
Thank you.

[Guillaume]
Yeah, one other question is, is there any documentation about the time attached just to needs, like for example, 300 milliseconds for double tap? Is it a standard or some arbitrary values set by the framework?

[Esra]
Like currently, as I know they are in framework, correct me if I'm wrong, because GM also has an amazing talk related to gestures, you can always check it out, but you can actually customize those. You can actually overwrite those values, you can overwrite that gesture detectors, or you can even have your own one, which he is actually talking about, if you want to just give a couple words related to that.

[Guillaume]
Yeah, so the value is a constant in the Flutter framework, but the value is also passed as parameter to gesture detectors and listeners and so on, so you can definitely overwrite it if you need to.

[Simone]
So like in modern phones, compared to the old ones, I don't know if you used old resistive screens, the interaction is much richer with gestures as the link to the typo screen we use.

[Esra]
Like actually, the gesture world is just started with 2007 first Apple iPhone release, and this is like, that's why it's also one of the revolutionary things, because like 2007 first iPhone release is like first ever capacitive screen successfully used in smartphones, then once we think about that, literally we just started to have gestures after 2007. So that's why I actually mentioned about our habits, these are shaped in last years, even almost like last 10-15 years, that these are like even normal right now. New generation and newborns, they are like in three years old, they are using those gestures now, but they weren't there before 2007, so that's actually something I would say always to be aware of and go for it, and that's why in resistive screens like ATM, kiosk and so on, you cannot touch the two points at once, like there is no zoom functionality, because it just can't, it just can't understand what's going on.

[Simone]
Fun fact, my mother sometimes is trying to zoom on ATM screens, but she can't.

[Esra]
And also like resistive screen stuff, when you have super huge light hit on that, of course you can't see it, and trust me, you will never be able to see it, it is technically impossible, so you will be always having this while you're trying to get the money.

[Simone]
There is something that made me curious, you said iPhone is like the first high-tech with the capacitive screen used successively, and then actually are there other companies that try to do capacitive screens on mass market?

[Esra]
To be honest, as I know, the invention of capacitive screen was before resistive screen, I think it's around 1960s, 1970s, they found capacitive screen and then for resistive screens, it just went for, not they say mistake, but it was like lab iteration that they get resistive, and they just proceed with that, then they started to successfully use the capacitive screen, so actually it started with capacitive first, but everybody kept using resistive, then with iPhone, then we switched to capacitive once back again.

[Simone]
Super interesting, thank you very much.

[Esra]
Yeah, like it is definitely something you need to watch, I wish I could squeeze it, but we just have super short time.

[Guillaume]
Maybe one last question, what's the most original gesture that you add to an application, like three finger swipe or double long press?

[Esra]
For me, like lately I'm always having fights to have the best user experience, so when there's an unusual thing, I'm always raising it, and I say not do it, because it looks like it is so fancy and good, like they mentioned in animation, but the user will not be able to find it, like when I wanted to come with new stuff, I wanted to actually have a form in next talks, probably the following ones, thanks to your feedback and ideas, for example, while you are filling a Google form, actually you could use sensors to swipe down, or I would just do like totally switching my phone and doing like totally different gestures than normal, because now we are swiping up and down, and let's put it to horizontal, you click once to a text field, let's make it a long tap, let's make it like three taps, and there is even more, much more than this, because in history, as we know, military always raising some stuff for us to improve, and when you think about military conditions, there are like totally different screens and gestures applied there.

Now I need to be able to use my glow, I need to be able to like working when it's wet, when there is raining, but it should be still sensitive and working as capacitive screens that they have actually PSAP, like projective capacitive screens, and there is even more, and you know they are not using simple fingers or swipes in some of them, they are using hand gestures, double hand gestures, so it's even very much more than this, and very much beyond than Flutter, so of course this gives you a little bit more awareness about the tools that we are using now.

[Guillaume]
Yeah, I think it's, you can start with the user's habits and the base for the gesture you implement, and then if you want to create new habits, or you have to make the gesture discoverable, and actually that's what TikTok is doing, because the other swipe is now becoming a habit, but it wasn't at the time, and they just created this small animation when you go to the page for the first time, just teaching you how to swipe up and down, so if you happen to implement some weird gesture, then you might want to make sure that it's discoverable to your user based on their habits. Totally, yes. Thank you very much Ezra.

[Esra]
Of course, thank you for having me.

[Guillaume]
Thank you very much.