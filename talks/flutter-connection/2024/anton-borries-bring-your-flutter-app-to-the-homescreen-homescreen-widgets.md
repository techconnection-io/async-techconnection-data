---
slug: >-
  /talks/flutter-connection/2024/anton-borries-bring-your-flutter-app-to-the-homescreen-homescreen-widgets
date: '2024-04-24'
title: Bring your Flutter App to the HomeScreen - HomeScreen Widgets
author:
  - Anton Borries
video: gAjZsZmMTlc
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/gAjZsZmMTlc.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: '2024'
allow_ads: false
---
[Anton]
My name is Anton, I'm from Germany, I'm a software developer at 1,5 Grad and yeah, I'm talking about homescreen widgets today. And so we all kind of know what homescreen widgets are. You can see them on the screenshot already.

It's these little boxes that give you more information from your app. But to get on the same page, let's maybe first look at what the actual platforms say about homescreen widgets. So iOS and the human interface design guidelines describes them as a widget elevates and displays a small amount of timely relevant information from your app or game so people can see it at a glance in additional context.

So on iOS, we're talking about homescreen widgets, but actually the technology for the lockscreen widgets, as you can see at the bottom, is also the same. This is iOS, Android and the Android design for mobile guide, they are writing widgets are customizable homescreen elements that display a clear and actionable view of an app's content or actions. Widgets help users complete their goals more easily.

So with these definitions, why should you consider adding a homescreen widget to your app? So you can display information in additional context, so not only in your app, but also on the user's homescreens or lockscreens. And you can enable your users to really interact faster with your app, which is always great.

Then great argument to get to your product owners, you get more space for your app. Like on iOS, the smallest size for homescreen widgets is two by two. So you get four times the space.

The user sees your content, your branding. It's really beneficial. And it's also enabling and giving you a bigger canvas to play with your brand on the homescreen rather than just your app icon maybe.

So Duolingo is doing this really well, in my opinion. So they found out that half of the learners with the widget installed have a streak of at least six months. So you can really see that a streak in Duolingo means those people, they have all opened the app every day for at least six months, which is a lot.

And we all would like if our users would do this. And also you can see how well they use the space of the homescreen widgets to play with their brand and give you this brand experience. So enough of the green bird.

Let's talk about the blue bird because we all love the blue bird. So homescreen widgets with Flutter. When I first looked into it, how it can be done, I found out really quickly we can't just run normal Flutter because the operating systems, they are really limiting you how much you can do with that.

So for example, they limit you what kind of content you can display. Like on iOS, you can't scroll on homescreen widgets. And they also limit how often it can be updated.

And the reasoning behind this, and I can understand it, is they really have to optimize the homescreen for everybody, for battery life, et cetera, because imagining a massive Flutter engine on the homescreen, updating 60 times per second, your battery won't really like this. So you have to do a lot of native stuff. And I myself included, while having like a background in Android development, I'm always a bit, ooh, native stuff.

And so I thought, so how can I improve this so homescreen widgets with Flutter are as easy as possible? And so a couple of years ago, I started working on HomeWidget. So HomeWidget, you still have to write all of the widget configuration, like the views, registering it on the native site.

But HomeWidget really guides you through with the documentation. And there's also a Google code lab about it. It's a bit of work, because you have to open Xcode, and nobody likes opening Xcode.

But it's really easy. And so as I said, you still have to build your widget UIs using native features. However, massive shout out to Leah, because it was her idea to also add the render Flutter widget function.

And with that, you can pass just your regular Flutter widget. HomeWidget then takes a screenshot of that widget, saves that as an image, and then offers you documentation, how you can implement and add this widget to your native widgets. Which let's say you have a big hero image, or hero view that you built in your app, and you want to bring that to your home screen widgets.

With render Flutter widget, it works. There's some issues with it when you want to do this in the background, because of some limitations. But generally, it's a really, really good starting point.

So the other big thing about HomeWidget does, it does some abstractions of features. So how do I get the data from my Flutter app to the native widget? How do I update the widget?

How can I include interactivity, especially with iOS 17, where interactivity came to iOS? So how does it work under the hood inside of HomeWidget? So from your Flutter app, you call saveWidgetData or getWidgetData.

And HomeWidget then, underneath, talks with the user defaults on iOS, or the shared preferences on Android. And once again, on the native side, there is extensive documentation and help functions, especially on Android, to guide you how you can then get the data that you send to your native widgets into your native widgets. So great.

You have sent data to your widget. How do you update it? You call HomeWidget.updateWidget. And once again, HomeWidget does the work and reloads the widget center timeline on iOS and doing the update on the app widget manager on Android. And if you follow during the setup the documentation of HomeWidget, these updates then happen automatically. Another big thing, like I already mentioned, is interactive widget, because this is what really drives the goal achievement for your users. Let's say you have a to-do app and you want to have a to-do list and want to enable users to do the to-dos or our favorite app, not red as Luca's app, but still the right, our Flutter counter counting up.

And so you could do this on the native side. However, with HomeWidget, there's a way that you can do the counting in Dart. So what you're seeing here, both apps call the same Dart function updating this value.

So you only have to write the interactive code once. How does this work? You register an interactive callback, which is just your function.

And then on your widgets in the native side, you send an intent and yes, they both call it intent. It's I think the first time they got the naming the same. And then once again, HomeWidget handles all the rest for you, boots up a new Flutter engine if your app is killed and calls the callback that you have registered.

And that way you can achieve things like we just saw with the counting up. And so native code, I talked a lot about you have to write stuff in native. And I really want to point out that I want my, I want you to leave this talk with the feeling I can write native code.

So this, it fits on one slide, all the iOS configuration that you need to do in order to get interactive widgets going fits on one slide. So on the left, this is where you create your intent or define your intent. And you can see that's the HomeWidget background worker, which does all the heavy lifting.

And then on the right, you see how you can use that background intent into your button. So don't be afraid, all the native code for interactive widgets for iOS fits on one slide. And yes, it also fits on one slide for Android.

So once again, thankfully, HomeWidget now supports Jetpack Glance, which looks a lot more like dark or like Flutter code when building UIs, and it makes life simpler and it fits on one slide. So on the left, once again, the action callback where you define your intent coming from HomeWidget. And then on the right, adding that to your widget.

So it's not as daunting. So other, some cool features from HomeWidget. You can detect when a user started your app from your widgets.

For analytics, it's always great to know, does a user currently have a widget installed? If you might want to give them a benefit or just track it in your analytics. As mentioned, lock screen widgets on iOS are also supported.

And then my favorite feature is that on Android, it's not available on iOS yet. I'm not sure if at WWDC it will be added. You can pin widgets to the home screen directly from the app.

So a user can interact with your app and then drag the widget directly on their home screen, which really limits the burden it takes for your users to use your home screen widgets on the app. That's it. You can find HomeWidget on PubDev.

There are some articles linked there. I think it's quite close to 1,500 likes. So let's say if we hit the 1,500 likes, I have a dash lying in the back.

So if it hits 1,500 likes and you can show me that you've liked it on PubDev, the first person doing that will get a dash. If you're building home screen widgets, feel free to send them to me on Twitter. These are a couple of apps that are all in production using home screen widgets, built with HomeWidget.

And yeah, that was my talk. Thank you very much. Happy building.

[Thomas]
Thank you very much. Please come with us. You have a lot of questions.

[Simone]
Yeah. I'll start with a known Flutter one for once. So you contribute to this repository, which is, of course, used by many people now.

How do you find the balance between your contribution to this repository and your everyday work at 1,500?

[Anton]
It's a mixture. So what I notice is that it's always a bit in phases. When there's motivation, there's never time, let's be honest.

So it's really a matter of motivation. And so seeing and finding out how people are using it is really a big boost for motivation. And then also, it's now starting that there are more and more community contributions as well.

And that obviously helps seeing that it's well used. That helps. And then it's a matter of finding the time and not sleeping very much.

[Simone]
Yeah, exactly. I know the feeling.

[Thomas]
So maybe first questions with four votes. How does the updates work when my app is killed?

[Anton]
And so where you mean if you get, for example, a background, it should still work like you have to register the background callback same when you want to access like a database when your app is killed. It's then the same way that the plugin has to be booted up in the background. But I believe that that works.

[Thomas]
Okay. I think it's linked with the second one. It's the same person, I think, who talks about the permissions that the home widgets can have.

Like you said about background tasks. But do we have to specifically give permissions to the home widgets?

[Anton]
It depends a bit how you want to do it. So if you want to do the calls from the native side directly, then I'm not 100% sure. If you go back to the Dart side, I believe it's the normal permissions.

[Simone]
Yeah. By the way, as far as I understand, home widget is not magic. Basically, behind the scenes, they have the same limitations of the native APIs.

So depending on Android and iOS, the answer might be different. And of course, the permissions also might be different from the real Flutter app, because it's basically there in widgets. For instance, on iOS, you are on iOS land and you are...

[Anton]
On your own. On your own, okay.

[Thomas]
There is one, yeah, about background capability. So of course, that's a question that everyone had. Does it support different widget sizes?

I think so, because you can... Yes.

[Anton]
So that's the way the lock screen widgets work. For example, it's... So on iOS, they call the different sizes families.

So you have small, medium, large, and then extra large as well. And then the ones for the lock screen are called like peak small or something. I'm not exactly sure about the name, but yes.

And then on Android resizing, this is configuration you need to do on the native side. And there's a bit of Googling or like with SharedGPT to get help there. There's a lot of, as it's native stuff, native developers have contributed a lot how you can configure that to your needs as well.

[Thomas]
Okay, thank you. Another question is, I think it's related to what we talked about, the APIs and the fact that it is in native, but can we integrate some sorts of voice assistants with home screen widgets?

[Anton]
My guess is not directly from the widget, just because it's super limited, possibly on Android, because you can do more what feels like hacky stuff on the Android widgets. But generally, I don't think you can get like voice input on the widget itself.

[Simone]
Yeah, long story short, before the last iOS update, if I'm not wrong, it was so limited, you couldn't even tap on anything. It just, I mean, the whole widget was just a massive button and you could not interact. Since recent years, I guess, I mean, you can also have interactive elements on the widget.

Does HubWidget support that?

[Anton]
Yeah, this is what I meant earlier with the callbacks. You can do it in Dart. As I mentioned, iOS doesn't support scrolling, but one of the examples, it's an app called Enduco.

They do endurance training plans and they actually use an interactive button that sends Dart code that sets a variable, which then updates it to look like a second page. So you can do page switching that way. It's, I think, a lot of like the guy who did this Apollo Reddit app has like a massive, like fidget spinners as home screen widgets.

And I think they work in a similar manner.

[Simone]
Yeah, this is very much related to, I mean, how Apple implemented widgets, which is supposed to be something which is, it's not interactive to allow the widget to not to be calculated every time. So basically, it's, I mean, the implementation you chose for like a static image was super clever because it actually, kind dish of how it works really behind the scenes from the iOS side, because it was supposed to be static.

[Thomas]
Another question. Well, it's just, what's next for home widgets? Do you have a backlog of ideas?

[Anton]
Yes. So one of the big thing is that I want to improve the documentation and the structure of it. And the other thing, which it was on the brink of getting like as a one more thing in the talk itself is that I've played around with macOS support and macOS support will be coming soon.

[Thomas]
Awesome.

[Simone]
All right.

[Thomas]
It's an announcement at the Flutter Connection.

[Simone]
Very good. Thank you very much for your time and your talk. And so we are gonna for a break.

It's the last break of the day.