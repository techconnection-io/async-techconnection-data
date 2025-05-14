---
slug: >-
  /talks/react-native-connection/react-native-connection-2025/mathieu-acthernoene-the-platform-abstraction-dilemma-designing-apis-for-a-multi-platform-world
date: '2025-04-02'
title: 'The platform abstraction dilemma: Designing APIs for a multi-platform world'
author:
  - Mathieu Acthernoene
video: L50gvZqGiSQ
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/L50gvZqGiSQ.jpg
slides: null
tags: []
year: 2025
conference: react-native-connection
edition: react-native-connection-2025
allow_ads: false
---
### Mathieu
  
Hi everyone and thanks for the intro. I'm Mathieu, I'm also known as Zuntech on GitHub, Blue Sky. I work at a company called Swan. We deliver a GraphQL API for banking stuff, you know, card payment, etc. I'm also a former podcast host at Putain de Code, which tells you how French I am if my accent wasn't enough. As you are all using React Native, you might be familiar with a few of my libraries. So React Native Permission, Localize, Boot Splash, and lately Edge2Edge. Out of curiosity, if I don't see the crowd very well, raising hands, are you using one of these? Yeah, more stress for me, thank you. Back to our topic. What does it mean to abstract platform and more importantly, why it matters? Ten years ago, Facebook introduced React Native, a new framework for building mobile applications. And the initial version only supported iOS as a target. And five months later, they added support for Android. Then a few months later, Nicolas added web support. Then Facebook added tvOS support. Initially, it was built-in React Native, but it later became its own package, maintained by Duke, by the way. It does a really good job keeping it up to date. Not that despite the package name, it also supports Android TV. Then Microsoft added support for operating system, desktop operating system, so Windows, macOS. And it seems that the list will only continue to grow over time. So what will be next? React Native fridge? I don't know. React Native ATM, maybe? We never know. What we will consider as a platform in two years, maybe? I mean, I'm not sure you heard of that, but a guy actually ran Doom within the TypeScript type system. So the core idea behind React Native is to provide a common declarative abstraction for any interface. But each platform has different IPIs and models, leading to different ways of representing things. Just look at OEMoji at different meanings, depending on the device you have. Think of it as you are not just writing code, you are a diplomat between platforms. You want to provide intuitive, flexible and future-proof API. You are a mediator making the call between iOS, Android, Windows, the web and so on. And for example, let's take Notify. It's a great example of a package that does that perfectly. Under the hood, iOS uses Apple push notification services, requiring device tokens, explicit user permissions, this kind of stuff, while Android uses Firebase, which works differently, has different requirements. To help you achieve the same goal, let me introduce to you the abstraction spectrum. I put all my design skills in this, so have a little. It's useful once you start wrapping more than one platform, of course. And as you can see, it goes from less to more abstraction. At the top left, you expose concepts and APIs from platforms directly to your users. You just take it and show it. And at the top right, it's more than a one-size-fits-all approach. You flatten the platform differences to the lowest possible common denominator. So let's focus first on the less side of the spectrum, which is less abstraction. Like I said, in this scenario, you expose API exactly as they are designed on the native side. If a native API is updated, for example, you update yours the same way because you act as a pass-through. Since it's only a binding, your library will be quick to develop, easy to maintain. But the drawback is that your user will have to understand the concept, API, option of each targeted platform. And this results in a poor developer experience. If a user app is only available on iOS, the day he will have to add Android support, for example, there will be extra work. And lastly, since developers will need to understand the underlying concept for each platform, it will take them longer to implement your library. A great example of following this logic is React Native Device Info. As device information differs across platforms, and if you try to unify the API, it will result either in like limit available functionality by only exposing the lowest common denominator, we don't want that, or confuse developer by providing an API that looks the same but behaves inconsistently across platforms. So in this particular example, avoiding abstraction makes sense. Now let's focus on the right side, which is more abstraction. In this scenario, you expose an API that could be like something totally different from like the platform API, or could align on one platform design. For example, this is a case of React Native Permission. or could align with a less capable platform design, for example, React-A-Fu Splash. This kind of API requires a design step. Even if you align to one platform API, you will have to perform an unification job on the other platform, meaning additional work and more time spent for you. And when the platform is updated, you will need to update your API for every platform. And this work, of course, falls on your side. But it's one of the key factors in improving the developer experience. And if you want to implement a library like that, your product manager will probably thank you because you will be faster in implementation. If you want good examples of this kind of library, there's React Native Gesture on there, or ReactDT Screen and other, you probably don't know how they work on the native side, but you don't care because you have a good, nice, unified API. To go a bit further, let's do a quick comparison between two packages that fulfill the same purpose but are at opposite ends of the spectrum. On one side, we have ExpoWebBrowser, a non-opinionated in-app browser package that offers a high level of granularity by exposing various methods and options for every platform. As you can see, the documentation reflects that. If we place it on the spectrum, I will say it's approximately here. And at Swan, so my company, our users have to implement this kind of package to embed our authentication into their app. And with ExpoWare Brother, they were a bit lost. Because at some time, we do a biometric check, and why the fuck it opened like in another app? Why the user leave my app for that? And how can I dismiss actually the in-app brother at the end of a flow? Because the method is only available on iOS. All of these questions could have been solved by giving them a specific set of options and educating them about the underlying concept. But we chose to take a different path and to publish another package with a different philosophy. Because of its position on the spectrum, our package API is very basic, but for 90% of the users, this fits their needs and it results in a significant time saving for them. If they have additional requirements and want to use specific options, they can. They can switch actually to explore their browser. But it's important to note that they will have to configure all the defaults that React Native Browser abstracts, first transferring the mental load to them. In the end, and after considering all these parameters and with a bit of practice, you will see that it's very easy to determine if a library is on the left or on the right of the spectrum. Let me show you how I personally apply all of this in my own library. First, with React Native Localize, at start it was only iOS and Android. At some time, I didn't like web support. But, for example, the get currency method doesn't exist on the web. There's no concept of currency on the internet. And I had two choices. Should I return null or should I somehow provide a result? And I chose the second option because I could do it. The abstraction cost was okay. And I just shipped like a big constant file using data from like Wikipedia. Next example, this is like the React Native Permission V1 API. So as you can see, it was like a permission matrix, like some permission available on both platforms, some on the Android, on the iOS. And underneath there was an issue. For example, the contact permission on iOS, using contact permission is using read and write access to contact. And on Android, it's not the same. You have two permissions, two distant permissions, read and write. Let's say you want to only ask for the write contact permission, which is less intrusive because your app will not have access to existing contact. You couldn't do that with the first API because it was aligned on the iOS one. The solution here was to reduce the level of abstraction. So instead of doing an abstraction, actually, I just expose every permission for every platform. And actually this new API flexibility allows me to add more platforms later, like Windows, new permissions, etc. very easily and without any breaking change. But sometimes I also move the cursor to the right. For example, on iOS, Android, and Windows, permission flow are different. So I add all this schema in my readme and exposing all of them, saying to people, "You can factor in this. fine-tune actually each behavior. And people just open issue saying, yeah, I don't understand why it's different on iOS Android, this kind of stuff. How can I architecture my code? So yeah, this was a bad idea. And I made the choice to say, hey, let's imagine like you have only one schema that abstracts all the platforms, all the supported platforms, and just implement it that way. No more extra conditions. This is the best way actually to implement it. So let's guide the user to do so. Okay. And the last and perhaps the most obvious example, it's React Native with Splash. Trust me, Splash screen is a really tricky topic. So to avoid users footing themselves, like shooting themselves in the foot, I aligned the behavior on the Android one. But if you open Xcode, you can do whatever you want, actually. So between these two sides, less and more abstraction, there's something we want to reach, a sweet spot. What it is? Well, the sweet spot is simple things are easy, complex things are doable. How can we reach it? You have to accept that actually, React Native Library are not just developers, they are product people. They have to think like, if all this platform has been designed at the same time together, what will be the API? Their job is balancing trade-offs, predict future platform quirks, and breaking change, etc. But maybe you are not writing React Native library. And that's okay. Most people don't. But let me plot twist. This talk is about API platform, API in general, and abstraction trade-off. Either you are wrapping operating system API, cloud services, third-party SDK, even libraries. So maybe you are not doing this on day to day, but you are probably doing this and it's the same rule. Design choices like this are everywhere. For example, a faucet can actually expose its technical constraints or give a user what they want. So I recommend this talk. It's really great. So when doing like this kind of work, ask yourself a question. Should your API reveal the underlying structure or should I spend time like developing an unified and consistent interface? How should I manage features that are not available for certain providers? Not using them, doing the abstraction on my side, this kind of stuff everywhere. When you build client-agnostic API, you are tackling the same challenge as a cross-platform developer. So finding the right balance between simplicity and flexibility. Again, this is a hard job, especially given that provider can be added, replaced, removed. It's okay to make mistakes, experiment. So first beta, 0.something version, collect feedback and use it to refine your API. Based on everything, let's define a few rules like a LinkedIn influencer would do. Depending on the situation, it might make sense to abstract or not. For example, we have query builder in SQL and ORM. and two solutions on opposite ends of the spectrum can be beneficial for the same user. It always depends on the context. Support developers in avoiding pitfalls. Design API with empathy. Developers need more than just an access to platform features. They also need guidance on best practices and usage. Don't forget that the API of your provider will change or have a shutdown if you are using Google products, for example. Plan for it. Future proofing is part of the job. And iterate, even React Native has refined itself over time. Module has been externalized for the core, some core API has changed, etc. you have to adapt to evolving usage context. For example, today, the web is a very significant target in React Native project. And that's all for me. Thank you for listening.

### Speaker 2
  
Thank you very much, Mathieu. Cool. Now, you know, speaking of Google killing products, there is one that I think they should consider. Kidding? Yeah, I can't think of one. Yeah, cool. Let's not get into that. Cool. I'm just starting with something completely unrelated. You climbed Mont Blanc. How was that?

### Mathieu
  
Yeah, that was me, like, this morning, when you made a joke about, like, the guy climbing a mountain. That was you, yeah.

### Speaker 2
  
Is that why you changed your fun facts?

### Mathieu
  
Yeah, exactly. Oh, my God, I'm sorry.

### Speaker 2
  
That was literally the only one that came to my mind at that moment.

### Mathieu
  
Yeah, it was not a fun fact, actually. But no, it is pretty fun.

### Speaker 2
  
Like, how was it climbing Mont Blanc?

### Mathieu
  
Exhausting.

### Speaker 2
  
Is it true what they say about like the oxygen?

### Mathieu
  
Yeah, yeah, truly. At some point I was just complaining and my guide was like, it's nothing. Just don't pretend.

### Speaker 2
  
Okay, you were being told off by your instructor for not being able to breathe.

### Mathieu
  
Exactly.

### Speaker 2
  
That's something, that's something. Okay, cool. Well, look, thank you for your talk. I think that like not everyone in here is a library maintainer, but I think what you were touching on is more architectural principles, which are very, very important. if you're actually building any project at scale that's beyond a side project. You need to make sure there's feature proof, that you're making the right abstractions in the right places. So I think talks like that are very important to think about the development process as a person who's leading a project. So I think that's very cool. I want to jump into audience questions. You obviously talked about the two different approaches, sort of the two polar opposites. What is your preferred approach that you take essentially?

### Mathieu
  
Yeah, mine is clearly like over-up section. I'm on the right side of spectrum, but it's because I like designing API in general and doing products. So yeah, this is more my philosophy actually.

### Speaker 2
  
Okay. Do you think that one of the two approaches you presented is better for backwards compatibility? And maybe you can link that to examples of if you've ever struggled with backwards compatibility in the libraries that you maintain.

### Mathieu
  
I think maybe doing less abstraction is better for backward compatibility. But yeah, actually, it's a huge topic, because on Android, we have to support maybe 10 versions of Android. So backward compatibility is like-- is always in our mind, I would say, because we have to test on a lot of devices over time.

### Speaker 2
  
I guess let's take a concrete example from that. So where is that? I know you've worked on Boot Splash, you've worked on Edge-to-Edge. What was the... Can you think of an example of where... maintaining backwards compatibility was quite important with those two specific libraries.

### Mathieu
  
For example, with BootSplash, I did like the extra mile because at start, BootSplash used like AndroidX, which is like a support library from Google. And they give us like a splash create API for older device. But it was special. So it missed like some features. And at some point, I said, OK, but it only targets maybe two or three versions of Android, a complete set of features, and it was not enough, given especially Android 4 never up to date. So yeah, for example, I implemented the brand image feature on my side. It's not in the polyfill, but for me it was important that everyone has this feature, even if you have an old phone, for example.

### Speaker 2
  
Makes sense. Are there any books or websites you would suggest to get familiar with API architecture and design? I can think of a few, but I'm going to let you jump in if you have any yourself.

### Mathieu
  
Yeah. I can't remember the name of one book, but sorry. I have one in mind especially, but I can't remember. So there's so many books about this that's been written. A lot of them were written in the 80s, which tells you how much this field is the same on different technologies. But there's the Software Craftsman, which I think is either Martin Fowler or Bob Martin, who is not the... Well, anyway, let's leave that aside. But there is that book. One of the best resources that you can look for in terms of architecture and patterns on architecture is the Martin Fowler blog. Martin Fowler is the chief scientist of ThoughtWorks and he's brilliant when it comes to architecture. But typically when you go in that camp, you start looking at very, very heavy architectures and it becomes a lot of abstractions on top of abstractions. So in the React world, take it with a pinch of salt. But it's very much geared towards this DDD-style approach of development. So yeah, those are just some resources in case anyone's looking for something more concrete. There's a question about edge-to-edge on iOS, which I don't think...

### Mathieu
  
Actually, by default, the package on iOS, there's no native site on this package.

### Speaker 2
  
Can you think of some libraries in your mind as like a person who's gone through a bunch of open source libraries that live in the wild that has great API design from like your perspective? Maybe excluding your own libraries just to...

### Mathieu
  
Yeah, of course. Actually, like I say, I'm not like an app developer anymore, so I know a few libraries, but not using them on day to day. But yeah, for example, like the Unistyle 3 API that we just saw is an example for me of a good API. Because you can iterate if you have a basic state sheet.

### Speaker 2
  
Yeah, that makes sense. I think it's what doesn't limit you right now and what doesn't limit you in the future and helps you move quickly now is probably the sweet spot, right?

### Mathieu
  
Yeah, and you can add support for, you know, fight by fight.

### Speaker 2
  
No, 100%. Awesome. Thank you so much, Mathieu, for your time and thank you for your talk. Really appreciate it. Please give him a massive round of applause.