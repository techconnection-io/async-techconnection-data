---
slug: "/talks/frenchkit-2022/audrey-sobgou-zebaze-the-journey-of-widgets-begins-with-one-step"
date: "2022-09-30"
title: "The Journey of Widgets Begins With One Step…"
author: "Audrey Sobgou Zebaze"
video: XRMcdUUA0HU
thumbnail: thumbnails/audrey.jpg
slides:
tags: ["WidgetKit", "SwiftUI"]
year: 2022
conference: frenchkit
edition: "2022"
allow_ads: true
---

0:00:29.3 Audrey: Hi, everyone. Thank you for having me this afternoon. So there are two presentations left, so please bear with us. My name is Audrey and I have two goals today. Try to improve my Memoji first and the second one trying to encourage women to just do some talks here, right? Mathilde, do you hear me? So I'm coming from a country where we know how to spell correctly, like, a footballer's name Kylian Mbappé. And another one where actually we eat cheese, charcuterie. I had too much yesterday, but also where we can eat croissant and pain au chocolat.

0:01:25.6 Audrey: Jerome is gonna kick me out of Swift's Baguette Channel. I'm working at Proton, and specifically on the Proton Drive, previously Proton Mail, but now I'm working on that application, which is gonna be released next month. So we're gonna talk about widgets. Widgets were introduced in iOS 14 and later on iOS 16. So what is a widget? So the definition is, widget is an element of graphical user interface that display information or provides a specific way for user to interact with the application system, operating system, or application, according to TechTarget. So on Larousse, sorry about the reference, because they have "boboization" in the dictionary this year, which is a process of gentrification. So widget are from window, fenêtre, and gadget. It's a gadget. So we should know that widgets are not mini apps. They should display content. So it's all about content. So today we're gonna have three concepts to try... To learn about. I'm gonna call it with an acronym you all know it's gonna be GDPR. It's not about GDPR legislation, sorry about that. But I display four letters instead of three. Yeah, well... I was hacky so just for you to remember it, but basically it's GPR. So the widget is gonna be about glanceable, personalized and relevant design or development, you can choose whatever you want.

0:03:17.9 Audrey: So the first one is about having information at a **glance**, so quickly. So for that we're gonna have... We're gonna use timeline provider protocol to do that, and with that timeline we're gonna have a placeholder, which is gonna be like placeholder of the view of your widget basically, and also snapshot, which is the current state of your widget, but also a timeline. So if you had a specific time you provide considering your data.

About **personalized**, so it's gonna be about the size, the count, the kind and the configuration.

And **relevance**. Relevance is gonna be about time. You can have an event, like a calendar, a presentation, like having a calendar displaying the number of event the day before, and the actual information, detailed information on the specific day and location where you can have weather and you can use directly from the widget, the location where you want the widget to be displayed. So for that, basically it is simple. So you get a timeline provider, you provide content with snapshot placeholders or other entries, and you display the content inside a view. So quickly just to get into it, you have to use the widget extension and if you want to have customization or dynamic stuff, you can use also intents, we'll get back to it.

0:04:58.7 Audrey: So if we want to use custom intents, I can implement something like events widget calendar by using a display identifier, it is just a string inside the widget. So using that specific intents extension, and I can have the configuration: so it's gonna be static information where I have that provider, common provider; conforming to `TimelineProvider`, I have the entries, the view; I can have the display name, the description, and the supported families. But also the `IntentConfiguration` where you can basically use your custom intent and having the same, well, the same class basically. You can also use multiple widgets. Just look at the Datadog one. So you can have multiple widgets like they have, and in different kinds.

0:06:07.4 Audrey: But you can also take care about the privacy. The fact that if you are in the banking application, you want to display content when the device is unlocked, to not display content when the device is unlocked, but also display it when it could be... When it's... When it's locked, and when it will be unlocked by using the privacy sensitive function. So in iOS 15 came Widget suggestions, those Widget suggestions are directly inside the Widget screen and you can add them, but they're using something called Intents also, but recommendation on Intents, and SiriKit is really good at that, at reading all those. So, basic code, if I want to display specific character using recommendation, I just have to conform to use an intent recommendation and display like a specific Hero I want to use. So that's really basic code.

So when iOS 16 came up, something you already know about: live activities. But also you can have what you had with watch... WatchKit and ClockKit. You can port it directly by using WidgetKit, all the computation directly while using the WidgetKit framework.

0:07:42.4 Audrey: So live activities lock screen widget, what is it about? Simple to same, simple to use, first you have to have the add `NSSupportLiveActivities` to your info.plist and display information. That information can directly come to remote notifications, to have live data and dynamic data directly and to process every information directly into the widget.

So, for that, we use activity attributes. And the object is basically... The concept is to add an activity, update an activity, and end the activity, because it lasts a certain time. We will get back to it. So a common example is gonna be about adding an activity. Right now I'm gonna order famous dishes. I like food, you guessed that, something like, famous Senegalese food which is called Ceebu Jen. But also for that I'm gonna try to update my activity with ordering and process of ordering. So I'm gonna use order attributes coming from activity, onforming to activity attributes and add, just now an image and a text. So requesting the attributes, updating them by using the activity that update task, that function with the task, and basically ending the activity.

0:09:25.0 Audrey: So this can be displayed as... In activity lock screen as something which is really sensible and which is really relevant. So the order is received, order is in progress and I can eat. What about the new thing? The new iPhone we have, it's Dynamic Island. On Dynamic Island it's just a small piece of screens. Sometimes you don't... You don't even see it because you get used to not seeing the notch, but it's really nice. And with that you can just... Trying to replace text, informational text, relevant one. On the right I just... The example is all about just replacing the image on the right. So basically it's working with having a region in the Dynamic Island. We have the leading, the trailing , the center, and the bottom.

So if I want to build Dynamic Island, also simple, I have a context. The context is the order of my command. So I have a status of the command. So by switching to all the layouts of the Dynamic Island, I can just get the image and replace it according to the status.

0:11:02.4 Audrey: So we have expanded region (it's a big piece of code) and basically you are gonna have the Dynamic Island where you have everything you want to display inside the views with all the leading, trailing, center, bottom, and the expanded one, and everything related to come back at this place, like leading... Also leading, trailing, and minimal one, the one I showed you before, and with some background because they're in black as a default value. So Dynamic Island, live activities, WidgetKit, by using WidgetKit, ActivityKit, that's basically it. So what I want to show you is just a small start of having all those widgets, and... By respecting some concepts.

So to summarize, please make it GDPR compliant - GPR. Live activity can use remote notifications and they are not there forever. They last up to eight hours. So we can cook now, right? Everything is okay. So please start with a small step, one, and maybe you're gonna have multiple widgets. Thank you. Merci.

0:12:45.0 Greg: Thank Audrey.

SimoneSo just as a quick note: so on Wednesday evening we have speakers dinners with all the speakers, and we were talking with Audrey about Dynamic Island and she said "Oh, I didn't put that in the slides," and today it's there. So it's massive work and you can guess that speakers work until the very last minute to update slides and their talks to bring awesome content on stage. So, well, that was great and thank you.

[applause]

0:13:30.5 Greg: So what... On how many widgets did you work?

0:13:34.7 Audrey: I'm working right now. I'm trying to work on all the widgets from all the products, basically mail, calendar, drive and VPN. So different kinds of interactions. So on the VPN, you're gonna maybe have to directly have access to the latest country you want on events. Well, everything related to calendar, on drive, maybe the progress status on the livestream activity lock screen and on mail, well, kind of same last as the calendar. So displaying mail in a relevant way.

0:14:14.8 Simone: What about the limitation of live widget appearing on the lock screen? You talked about GDPR and... Is there any that you are prevented to do by the OS or by the framework to avoid you displaying sensitive data?

0:14:33.6 Audrey: So I talked about the private sensitive stuff, but the activity lock screen well, it doesn't display all those. We can use basically the attributes also on the live activity. But you should kind of take care of the fact that yeah, maybe don't use it too much because that's not the goal. The goal is to basically display stuff and not to hide everything every time.

0:15:02.5 Greg: Yeah. Apart from the widgets you are working on, what are your favorite widgets?

0:15:10.4 Audrey: The DataDog one! Or basically the weather, the one on weather calendar. I use it lot. I'm using the Spark Calendar, the Mail calendar it depends, and the music one. Sometimes the photos, well, a lot of them.

0:15:31.3 Simone: Actually, were widgets for you an opportunity to get into SwiftUI, or you knew SwiftUI before doing widgets?

0:15:39.4 Audrey: Well, I've used SwiftUI since its first version in 2020, with my colleagues at Aircall. So yeah, so we use it and basically, I choose to present widget because it was kind of like the first framework basically only on SwiftUI, so that people can start fresh trying to just have a piece of code, to just isolated piece of code because it's in an extension. So that we can play around like small views, not too much logic. And that's why I wanted to just present it, to give opportunity to people just doing UI Kit these days, which is not bad to at least know, get a sensation of something new.

0:16:28.5 Greg: Thank you Audrey.

0:16:29.9 Audrey: Thank you.
