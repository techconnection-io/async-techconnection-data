---
slug: >-
  /talks/frenchkit/swift-connection-2024/melisa-de-la-garza-kmp-a-hands-on-perspective
date: '2024-09-23'
title: 'KMP: A Hands-On Perspective'
author:
  - Melisa De la Garza
video: 0AvHyr6e0_s
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/0AvHyr6e0_s.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Melisa
Hello, everyone. My name is Melissa, and today, I want to tell you about my experience with Kotlin multiplatform. Please don't kill me, okay?

First of all, how dare I? I know, I'm sorry. This is a Swift conference, not KotlinConf.

You're in the right place, okay? But I'm excited to tell you about my experience. I think it's worth exploring this technology.

Just think about it as another tool in your toolkit. Just try to keep an open mind. It's not the holy grail that Android developers say it is, but it's also not going to fail, I think.

So story time. This was the tale as old as time. It was a small iOS team with a slightly larger Android team, and we were working at an eCommerce company, so we were always coming into the same issues, sort of having the similar bugs, but not quite the same.

We were sort of put it against each other in a reluctant competition, and we were already sort of redesigning and refactoring the app once and again and again. This was a couple of years of work. So we needed something fresh, and COVID had just happened, so we needed something energizing, and then KMM came into our focus, and we were like, hmm, this looks interesting.

We might hate it, but, you know, let's read about it. So this is what we know, right? Kotlin Multiplatform has a lot of promises.

It allows us to share code between both platforms. It reduces the amount of code you have to write because of that. It will lead later on to faster development cycles, and it will have consistent behaviour across both platforms.

So that is a lot of good promises, right? But that also means a lot of unknowns. How are we going to get there?

So our manager, who was great, he managed to carve out some time for us to just experiment and do our own thing, which was great, paid to experiment. So we started small. We decided to start with a small feature that was isolated from the rest of the app so that in case it didn't work out, we can just throw it in the trash.

So, first, decisions, decisions, decisions. First of all, Monorepo, this was already two old apps with their own repositories, so how are we going to work together? So I decided to keep both worlds and add the Android repo as a submodule for the iOS so we can have their code but without being in each other's ways, and then do we want to integrate that as Cocoapods or SPM?

Well, SPM is, of course, way more elegant, but unfortunately, KMM was not ready for that in that moment, so we went with Cocoapods. That's OK. Then what will be shared?

We want to share code, but how much of it, right? So we decided let's go with basics, just the network layer, and some business logic here and there. OK, so far, so good.

Let's move on. Then setting it up. Has anybody seen Java Home before?

Exactly. So, yes, first thing first, something is failing because of some Java Home? What is that?

So we needed to set up environment variables which then, you know, company-managed machines will delete after some time, so that was a pain, you know. But OK, let's move on. If you haven't seen that, count yourself lucky.

And then this circus act. OK, well, what happens when you try to run a network call and then update the UI in the main thread? It's probably going to crash, right?

So that happened to us. Great. And then how do we fix that?

So coroutines came into the light, but what are those? These are lightweight threads that allow you to write asynchronous code with non-blocking code. So, OK, what does that mean?

That at the moment we were blocking our operations, we had poor UX, and the main thread was overloaded, so crash, even if it was a very small feature with one network call. It was a mess. But it turned out that coroutines could not be implemented in that moment for our Android project, so we had to do a little digging and they had to refactor some code, sorry, not sorry, and then we got there.

So with coroutines, we had smoother performance, better UX, and the thread management was done for us, so yay. But then the pain point started. Yeah, that's not pretty, right?

That is trying to serialize one single model from our data manually for our tests. That's a lot, right? That's one single model.

How are we going to maintain all of our unit tests? So if you're out there, I'm so sorry, but we had to turn off our unit test. In the meantime, while we figure it out, we thought, okay, let's not focus on unit tests right now.

The same unit tests are being run on Kotlin. Let's trust on those for a while, but also keep an eye on that. And then the architecture.

Yeah, what is going on? It's just saying failed. So this was kind of cryptic because we couldn't find out why it wasn't working.

We were explicitly saying we need to transpile this into both architectures for iOS simulator and iOS devices, but still we were keeping these errors. So it turns out that the Kotlin version that the Android project was using was not compatible with that plugin so that we could get the right architecture, so again, they had to refactor some code and, well, tough. Another pain point, and this was kind of a funny one.

I don't know if you've ever gotten bugs that you don't really understand, but this is a really funny one. They were using description as a variable in their models, but then that's also a reserved keyword on Swift, so we couldn't find out where the problem was because Swift wasn't finding any problem. Description is there, but it's not the description we actually wanted.

So, again, we needed to use an underscore. Who would have thought? Anyway, easy refactor, right?

And then the most known pain point of KMM is that it transpiles into Objective-C headers, which look like that, and if you're old like me, you might see that and your heart is warm. It's like, oh, yeah, Objective-C. How cute is that?

But if you're not and you don't like that, then it might be confusing and it might be a problem. The part below is the way that the project looks, the code looks on Kotlin, which is fairly familiar, so if you wanted to change something instead of going and changing on Xcode the code that you needed, you need to go to Android Studio or whatever you use and then change it there and then build it there and then bring it to iOS, but, you know, it works. Okay.

So let's do a recap. So far, we had no decoding, so that meant, sorry, testing for a while, and we had clashing naming, so we had to do a little refactoring here and there. Our CI-CD was not working because of that thing I told you about, that either it works on simulator or it works on device, so yeah, that meant manual releases.

Ouch. And the libraries and plugins became sort of a balancing act. You had to find a little fine-tuning here and there so that it would work the way we wanted it to work.

So this is what the project looked like. We found this from the declarative UI and Kotlin multi-platform architecture pattern. That's a mouthful.

Sorry. So we used this as our guiding structure. This is the technologies he was suggesting and what the future would look like, and this is the architecture that we had.

We didn't want to disrupt our MVVM, so that didn't mean a lot of refactor for our project, and this is what we started with the first feature, so we had the shared module that was just having the network layer with the rest in GraphQL network calls, but then this evolved later to this, so our view models were also included in the repository so that operations could be all the business logic could be in one single place, and then the API was ready for iOS to use it, but, of course, we had input during everything. So not everything was gloom and doom, okay? Otherwise, I wouldn't be here, of course.

So there were good technical findings. There was, indeed, reduced and unified business logic. It was fairly scalable because we could modularise this.

We had a single source of truth. We ensured stable performance as much as we could with the tooling available, and we were keeping our same architecture, our enums and generics, and after doing a lot of testing, we involved our QA, and he also did a lot of testing, but in any case, we added our feature flag just in case something went wrong and we didn't want to do an emergency rollback or something. So, okay.

Some other good findings but more soft skills were the team communication. We were so good communicating now. Yes, call it trauma bonding or friendship, whatever, but we were talking more and more to each other.

We were sharing all of our knowledge, both tips and tricks about Android Studio or Xcode, so, you know, they were new to Xcode. What is code signing? Well, we had to bring them in.

Also meant flexible capacity so that if one of us was out on holiday, maybe the Android team could step in and help out. We were flexible to changes and we only had to fix it once. So, of course, the product owner was super happy.

So we shipped it. In Thank you. So, of course, I am the girl with the list because I have to make lists about everything.

So the pros. We were code sharing, as I mentioned. We were very efficient in our work.

We had interoperability so we could communicate our code with each other, and we were delivering faster. What? I mean, yeah, it worked.

But on the downside, there was a learning curve, of course. We needed to learn Kotlin. They needed to learn Swift a little.

The tooling maturity is not quite there yet. I know it's been working, and JetBrains is working hard to make it easier for Swift developers. I don't work at JetBrains.

I'm not selling it. Don't worry. If you hate them, hate them.

The dependencies and configuration, as I mentioned, was a very delicate balance, so we needed to work on that, and the set-up on existing large projects is hell. So is it worth it? Consider this another tool in your toolkit.

As I said, it's not a silver bullet and it's not a one-size-fits-all. Would I do it again in this sort of project that is quite big and with a lot of legacy code? Maybe not.

But if you have a smaller project or if you want to do it on the side or if it's just like a pet project or whatever, go for it. It's super fun. I guarantee you're going to have fun banging your head against the wall, figuring out why it doesn't work, but when it works, it's so rewarding.

And I guess this will help us bridge the gap between mobile engineering and, I don't know, we can just be friends with those Android guys. Thank you. So I leave you with this quote.

Technology is nothing. What's important is that you have faith in people and that they're basically good and smart, and if you give them tools, they'll do wonderful things with them. And this was by our lord and savior, Steve Jobs.

Thank you.

### Zino
Thank you, Melissa. You're welcome. So through all the pain points and the problems and stuff, it seems that the major reason why you kept going was because of fun.

### Melisa
Yeah, definitely.

### Zino
Do you consider that a huge part of the development process? Should developers have fun?

### Melisa
Definitely. I think it can be a soul-numbing job if you're not having fun, because you're basically just talking to the computer all day, every day. So you at least should have fun with what you're doing, and that's it.

### Zino
And bashing your brain against cupboards is fun.

### Melisa
Exactly. It's fun. Try it.

### Robin
Well, I've got a question for you. You were talking about potentially befriending these Android developers that we like to push away. Since KMM is coming from an Android language, has that ever made you think, oh, maybe I could develop for both?

### Melisa
Yeah, definitely. That was sort of the initial thought behind it. Maybe we could do both.

Have you seen that be a point of both? I actually have a very good example. When we were starting the project, of course, it was like a senior task to back their heads against the wall, and the junior devs were just kept to a distance so that they would just learn from our mistakes, and one of the junior Android devs actually started growing with the company, and he got very excited about learning about Swift as well, and two years later, he's doing both really well, really exciting to see how he's even good at Swift UI now, and he's super excited with it and he's doing both, and I think it's great.

Oh, wow, that is great to see that kind of enthusiasm. Yeah, exactly. And know that it's possible to do both.

Yeah, definitely. I mean, they're so similar that why not? Yeah.

Yeah.

### Zino
I have more of a technical question based because, you know, I'm a data kind of guy, so the problem with transpiling and having multiple platforms is usually performance-based. Did you notice any performance hits?

### Melisa
At the beginning, when we were trying to figure it out, definitely. Some of them. Some functions were recommended to help with that, like the freeze function in Android.

I don't know. Stuff like that. But thankfully with the coroutines, it helped a lot handling of the threat management to the GCD, so, yeah, after we did that setup correctly, it went very well, very fine.

I mean, the only problem might be the build time for developers, but performance-wise for the users was fine.

### Zino
Performance is always great on Objective-C.

### Melisa
Yeah.

### Robin
Famously. Well, I've got a question for you that's coming from the audience. In your project setup, is it possible that you can put a break point into the Kotlin code, or is that just a black box that we can't get to?

### Melisa
Yeah. Unfortunately, it's a black box. It's just an API for Swift developers.

But in any case, you have to have both projects there, so you can read the code over there and sort of have a break point in which function it's crashing or just stopping and then go to the Android Studio and look at it there and see what's going on.

### Zino
All right. I don't have any more questions.

### Robin
I've just got one more question for you, and this is a personal one. Since you've added this into your project, has that had any effect on the hiring process on your team?

### Melisa
Yeah, that's a good question. It has. Unfortunately, whenever we were trying to hire some iOS developers and we mentioned that our project was already having this part ingrained in the project, some of them were not really excited about it and also not willing to learn Kotlin.

But that also meant that for us, maybe they didn't have sort of the fun mindset and the challenge mindset. It was a challenge, but I mean, we got there. OK.

### Robin
Good. Well, thank you. Do you have any more questions, Zina?

### Zino
I do not.

### Robin
No? Well, another round of applause for Melissa.

### Zino
Thank you, Melissa.

### Robin
Thank you. Thank you so much.