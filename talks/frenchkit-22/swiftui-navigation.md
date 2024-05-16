---
slug: /talks/frenchkit-2022/luis-ascorbe-swiftui-navigation
date: "2022-09-29"
title: SwiftUI Navigation
author:
  - Luis Ascorbe
video: jhO9gfVg6_U
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/jhO9gfVg6_U.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/frenchkit-2022/luis-ascorbe-swiftui-navigation/slides.pdf
tags:
  - SwiftUI
  - Architecture
year: 2022
conference: frenchkit
edition: "2022"
allow_ads: true
---

0:02:54.8 Luis Ascorbe: Bonsoir, bonsoir, everyone, comment ça va. Thank you so much, Simone, for that great introduction, it's really, really nice to be here on this stage, is my first time at FrenchKit. I've always wanted to come, it's great to have conferences in Europe. I would like to go to all of them but it's also super hard because also my conference happens the same month, it was two weeks ago. So yeah, they've been doing a great, great job doing this conference, and I just want to ask for a big round of applause for Simone, Julien, Julien and Greg and the rest of the team.

[applause]

0:03:38.6 LA: Okay, so we don't have a lot of time, let's start SwiftUI navigation. So as we all know, Apple always do like great things, everything is perfect, everything can be decoupled and it works out of the box through all the platforms. Well, they always talk about the promised land but it is not always the case. Sometimes the reality is very different from what we have to work with. I am Luis Ascorbe, I'm a software engineer at Ultimate Money, and I also organize a conference in Spain called NSSpain. So what are we going to see today? I said, "We don't have much time," so I try to do like a broad topic on how we can navigate with SwiftUI. So we have navigation with UIKit, actually, but working with SwiftUI, we have navigation with SwiftUI, and I'm going to say like my take on which one you can use, depending on your situation because insofar, it depends always. So Swift navigation with UIKit because SwiftUI is great, You've seen it with Thomas. Right? If you try SwiftUI every time you start a new view, you just want to use the out-of-the-box. It's read, it is super fast, "It is a joy," as Thomas said. And I totally agree, it's a great, great tool, but you have to really know how to take one way or the other.

0:05:28.8 LA: So if we want to go the UIKit route for navigation, we have to know about `UIHostingController`, which is something you already saw on... Done install before. But I am going to explain it real quick. So imagine you have like a SwiftUI view and then if you want to use it from UIKit, you will just pass it as parameter to the uihostingcontroller and then you can present it from UIKit. Now, let's say you want to recouple your logic from your view, it's quite easy with observe object and the UI will look something like this, so it conforms to observable object, and then you can use Publish Properties to inform the view that something has changed, and then the view is going to redraw itself. So the theory is that SwiftUI is smart enough to make a diff between the different models that it has to present and it won't redraw the parts that didn't change. Let's see a real case, a real-life use case.

0:06:52.1 LA: I worked at... Before Ultimate, I worked at Beams FM. We were trying to build a social network, but like a new concept of audio. So we were trying to create a platform where you will post your voice and then people will just hear you. So it was like micro podcasting, it was like this concept that was coming out and with the wave of Clubhouse and all this stuff. So at some point we saw that... We had this assumption that if the content is more active, then people will be driven to listen more. So we switched the UI, the player, the main player, to have like a TikTok-like experience to see if that will make people listen to more content and discover more within the app. And I actually built this view. And so what we see on this view is a `UITabBarController`, which is the main root component. Then the navigation controller, which is the first controller of the tab. I have plain `UIViewController` that is the first view controller of the navigation controller, which has a wrapper because you can switch between the 4U and the following on the view, and then two page-view controllers, so you can switch between two of them to scroll up and down and see more content. And then each one of them will have the child views that are actually UI-hosting controllers which use SwiftUI view inside.

0:08:53.9 LA: So in this view, everything you are seeing, except the back button and the tab bar, is SwiftUI, because all interaction or everything that we show on a screen was made with SwiftUI because it was just way easier, has like dynamic captions here on the left and all the interaction, all these buttons, all these tab and animations was much, much easier to build with SwiftUI. Why would we choose this approach? Why we choose UIKit? The thing is that on our app, everything was already built with UIKit, so it was a way to start using SwiftUI without having to rebuild everything or, "Just throw everything and then I start from zero." There is no vertical page view on SwiftUI. We have to build our own, and even though we actually tried using a scroll view for this, we had some performance issues and it was like a lot of code that we have to write, and so we decide to go through the UIKit approach not only for navigation, but also for the scrolling component, and it worked really well.

0:10:18.2 LA: And well, SwiftUI is a joy to work with. I have to say this important point here, that if you're using `UIHostingController`, it has a small problem, which is the intrinsic content size has a bug, so it doesn't calculate correctly, sometimes it adds these margins around it. And the way to fix this is like a small... This is a small tip. So you have to subclass `UIHostingController` and ask for updates of the constraints. But I'm glad to say this was solved on iOS 16, so you only have to do this on iOS 15 if you support it.

0:11:06.1 LA: So, on SwiftUI, we have many APIs. We have like a `.navigationDestination`, `NavigationSplitView`, `NavigationStack`, which are all the new things and all the other modalViews and `NavigationView` and `NavigationLink`. So if we skip the new APIs for a second and we also like skip the modal APIs, which are like more straightforward to work with, we are left with `NavigationView` and `NavigationLink`. And this year, `NavigationView` was actually replicated, so we are left with `NavigationLink` to start with.

0:12:05.3 LA: Let's go with `NavigationLink`, so the way you would use it is very straightforward. You will put it on your view inside navigation stack or navigation view, and then whenever someone like taps on it, you will go to the SwiftUI view you have there. So it is really easy to work with but you have to have something important in mind, which is, in SwiftUI, your views have to be really lightweight, so your `init` will have the minimum code possible because, for example, this code is going to print `init` whenever `FrenchView` is presented on the screen, not even `BonjourView`, so you have to be really mindful of this, it is a way of thinking SwiftUI, that you have to take into consideration. It doesn't happen with model views, but the SwiftUI team recommends that you take care of having that really, really lightweight `init` on your view. And the thing is that this code is great if your app is small, but it's hard to decouple.

0:13:30.2 LA: I tried it. With the SwiftUI version, I tried this concept of using coordinators to strike all the logic of the views, and it worked but as soon as SwiftUI with iOS 14, I think, was out, it stopped working. And it's actually not meant to work with SwiftUI. Right? SwiftUI has another way of... Like more reactive. So please don't use MVP with SwiftUI, it has other architecture which is more meant for SwiftUI. Talking about architecture, let us jump onto the new APIs. Architecture is such a big topic that Apple decided to rewrite the whole navigation to be able to decouple things, so they presented this year, `NavigationStack` with `.navigationDestination`. So now you can actually have navigation links, and then you just pass the value and then you navigate there through navigation destination.

0:14:55.1 LA: So yeah, you will have navigation link, which you can pass the value, in this case, you can say "bonjour" and then through navigation destination, you get the value you want to go, and then present the view you want to get on a screen. Very, very nice, is a good way to decouple the interaction with the actual value that you want to use, and the part of the path, which is actually also an interesting topic to talk about because it's very, very broad, is quite easy to get through. You can actually use any kind of type or object you want to with the path, and it will work almost out of the way.

0:15:53.3 LA: I don't have more time to dig into the new APIs but I'm going to say I don't have to because two weeks ago, I'm sorry for the shameless promo, but Brandon Williams two weeks ago did a great talk at NSSpain, which is SwiftUI navigation with URL routing. And in here, he really goes through, What's navigation? How it works, and how to work around the actual APIs and the new APIs, and he even implemented with a few demos, how to delink and use URL routing in it. I just published the videos like, I don't know, 20 minutes ago, so it was available already before my talk, and yeah, you have the link here at the bottom if you want to check it out, it's a really good talk, so shout out to Brandon.

0:16:56.5 LA: And yeah, talking about Brandon, The Composable Architecture: I don't know if you all know it, but Brandon works as part of the PointFree team with Steve and Felix, and between them and the community they created this library, which by their definition is, "A library for building application in a consistent and understandable way with composition testing and economics in mind." It can be used in SwiftUI, UIKit and more, and on any Apple platform, iOS, macOS, tvOS, and watchOS So if you don't know about it, I will totally encourage you to try it out. It's great.

0:17:47.3 LA: Actually, now comes another real-life use case, which is the company I'm working at right now, which is Ultimate Money, so we are creating a non-custodial crypto wallet on the Sona blockchain. So this app is all built with SwiftUI, with The Composable Architecture, and everything is reactive and, yeah, it's actually a joy to work with both of them, SwiftUI, and the Composable Architecture. At the beginning, you have to get your way around how things work and how to know, how to work around all the signals, but as soon as you get used to, it is a game changer.

0:18:38.9 LA: Now, which one to choose. And it is not mainly like which one to choose, but which one you should consider. So I would say that if you want to use SwiftUI in your project, you want to consider UIKit [Navigation] if:

- you have already a project in which you are working on, and it is using UIKit
- you want to decouple navigation logic from the views because in SwiftUI, that's actually pretty hard right now. Maybe with the new APIs but if you have to support previous iOS versions, it is still a bit of a nightmare
- You want to try SwiftUI, and you cannot switch your architecture right now because that's a big one.

Then I would say that you can consider navigation with SwiftUI if:

- your deployment target is iOS 14+
- you are trying something out
- you want to play with the Composable Architecture, things like that.

I have to say that in this app we are working on right now, we still haven't worked our way around the new APIs, so we are still using the old ones. So yeah, it's a big, big change if you want to start using SwiftUI navigation compared to UIKit if you already used to it.

Merci.

[applause]

0:20:58.0 Simone: So thank you very much. The first question is - I won't ask if SwiftUI is production-ready because I think I understood what you meant - but it's kind of a same thing. Would you actually make the same statement that Apple did at the WWDC, that SwiftUI is absolutely the way to go and there is no going back?"

0:21:27.4 Thomas: When making new project... I would not make a new project in UIKit these days, but it's also dependant of what you're building. We have part in the app in UIKit but that we don't plan to change right now because we don't have the SwiftUI API for that, so it's really dependant of what you would build. But if you start a new project today, you should really like consider SwiftUI unless you have some specific feature that you know that you can't build with it.

0:21:56.5 LA: Well, I saw two real-case scenarios, so for me SwiftUI is totally ready for production.

0:22:06.0 Simone: If you had to go back and just pick one mistake you wouldn't do again on SwiftUI, what would that be?

[laughter]

0:22:20.1 LA: Use SwiftUI navigation.

[laughter]

0:22:22.9 S3: Yeah, I have big SwiftUI project, I will never rewrite using the new navigation, just to make change right now, but maybe also using it during iOS 13, I guess, and 14. I mean iOS 14 minimum target is great right now, below that, I think it was a bit of... Maybe too early because we had to test it a lot on devices to be sure that it was running the same as on the simulator.

0:22:55.8 Greg: Okay, so we have people writing SwiftUI for several years now, and even among those people, people who haven't written UIKit before; do you think we will make like all that jokes soon, like, "Oh remember UIKit as we say, remember Objective-C nowadays?"

0:23:17.7 LA: Yeah, for sure. [chuckle] Actually, I was talking before, during the coffee break, with Samuel and Leonard, and we were talking about how things seem to be all the time broken now, but the reality was that, and this was someone's point, the reality has been always like that, there is always like a new API and then you cannot use it because you have to wait two years to use it because you have to support previous versions. And it happened with everything Apple releases, and for sure, this is case, the problem is that navigation in a specific is so coupled to what you're doing that it is really hard to work around it. If you are using correlator, you can use "write a wrapper" on and put it away, and then use "rerun" or whatever you want, but navigation is not really an option.

0:24:17.4 Simone: Yeah. Another interesting question was, "Is anybody you find using introspection towards workaround things?"

0:24:28.0 S3: So we use it only at minimum, we use it only for testing, because we test like the final value inside text, for example or inside images, that's how we do test with introspect, but we don't want to use it in in production because any iOS version could break it if you changed the underlying like... And actually, since UI 16, more and more component don't choose like UIKit and underlying component, so yeah.

0:24:52.3 LA: Yeah, same, actually we were using a few things with introspection too because it is really hard to customize some things in SwiftUI because at the end, it works with UIKit behind the hood. So if the SwiftUI API doesn't give you access to that, then you have to use UIKit. And then you have to use appearance with UIKit, and then some appearance does work and some appearance does not work, so you have to introspect the view to change whatever you want. And at the end, some of these changes were so cumbersome that we decided to just go with what the system was delivering. In this case... I mean, for example, there was a... So I think if you use a searchable modifier from iOS 15 and you want to change the appearance of the font of the search box, it doesn't work. If you do it with the appearance on UIKit, it works. On SwiftUI, it doesn't. So you can introspect and then change it, which sometimes also doesn't work, but yeah, we decided to just go with the system form in this case.

0:26:08.2 Simone: Speaking about SwiftUI, something that SwiftUI finally brought to the Apple ecosystem is that we are finally actually using real components and getting ourself more and more close to the possibility of doing real atomic design. Do you do that in your app? Do you actually apply atomic design? And in case you do, do you have any feedback or any advices for people who want it to be full atomic?

0:26:39.4 LA: We do not like really like atomic, we don't have like molecules and atoms, it doesn't scale up with a lot of things, but we do use it with buttons, for example, and we heavily use button styles. So all our buttons are decomposed on button styles and you have just to say, "Okay, this button style is this." And then it will take that form. And it's pretty nice I have to say.

0:27:08.9 S3: In the medium, we had a design system that we use for UIKit, both Objective-C code, and also modern SwiftUI kit. We do a lot of view modifier on top of existing view, we create a lot of components but I would not say we're not fully atomic. We do a lot of customization, like with one modifier we can apply a whole system design rules on components, that's how we do it. Eessentially we wrap and create our own custom components. And we should use a better configuration but for now, [inaudible], they don't like that.

0:27:42.9 LA: It's very powerful, I have to say.

0:27:46.9 Simone: We would love to have more questions but we are a bit under time constraints sadly, so we will wrap things up now. Thank you, guys, for your answers.

0:27:56.0 S3: Thank you very much.

0:27:56.8 LA: Thank you.
