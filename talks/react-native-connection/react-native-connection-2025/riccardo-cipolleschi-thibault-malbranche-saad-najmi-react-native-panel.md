---
slug: >-
  /talks/react-native-connection/react-native-connection-2025/riccardo-cipolleschi-thibault-malbranche-saad-najmi-react-native-panel
date: '2025-04-02'
title: React Native Panel
author:
  - Riccardo Cipolleschi
  - Thibault Malbranche
  - Saad Najmi
video: DAM5c986RiY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/DAM5c986RiY.jpg
slides: null
tags: []
year: 2025
conference: react-native-connection
edition: react-native-connection-2025
allow_ads: false
---
### Mo
  
Cool. Well, folks, thank you so much for coming on board. Super excited for this. Hopefully, and also get some questions from the audience. So, Core Contributor Summit, let's start with that 'cause I think it's a really interesting concept and maybe, who's heard of the Core Contributor Summit here in this room? Okay, so a lot of people didn't know this existed. Do you feel left out now? Sorry. So last year was my first year at the Core Contributor Summit. It was quite interesting to see the depth of conversations that were going on and how many things you don't think about when you're like, I just want this new feature. And then you're like, oh, wow, there's so much to consider that I just absolutely did not clock onto before I was part of some of these conversations. But Thiebaud, you've been in the Core Contributors group for the longest out of any of us. So tell us about what it's been like over the last few years for you.

### Thibault
  
Basically, the Core Contributors Summit is whenever we get the chance to be in the same physical place at the same time, we try to get together and talk about all the issues we have asynchronously all the time. And I remember the first time I gave out with people was in the London office in 2019. And that's when we started implementing auto-linking, the thing that makes that you don't have to change your native files by hand. So that's how we discussed and we made a proposal during the summit and then we implemented it that came out of the core contributor summit.

### Mo
  
That's like as monumental of a shift in React Native's history as ever. So yeah, that's quite... I didn't know that story. Very cool. So we'll touch on... there were a few different... so the way that the core contributor summit was set up was there was a bunch of different sessions. And so there was a bunch of different topics that were discussed. And we're going to actually cover a lot of those points and kind of give you some knowledge as to what was talked about. Before we do that, though, I want to take a step back because this is actually one of the first conferences to be run and React Native conferences to be run since the launch of the new architecture. And so we want to really like reflect on the launch of the new architecture, especially for Ricardo as someone on the core team of React Native, and really talk about like what was the good, what was the bad and the ugly of the release and how you found it in practice.

### Riccardo
  
So yeah, we released the new architecture in October 26th, if I'm not mistaken. So it's now six, seven months, something like that. And I think it's going pretty well. Our usual process when we release something in the open source is that we first test it internally. And we have been testing the new architecture in the Facebook app since... quite a bit, like the development started in 2019. So it took some time to roll it out in the Facebook app and then to roll it out properly in the open source. Of course, the Facebook app is pretty big, but it's not... I mean, in the open source there are much more use cases. So at some point we decided we need to release it. We need to see how it behaves in the, in open source. And it's behaving pretty well, I'd say. We partnered with Expo to make sure that a lot of libraries were compatible and that a lot of people can jump on the new architecture with the least amount of issues. And right now, thanks to some data that Expo shared with us, it's going pretty well. And yeah, of course, there are some edge cases or some things that we need to figure out or iron out to make it even better. But yeah, I think it's going pretty well.

### Mo
  
I mean, none of these launches, like fundamentally changing the core of how you build apps is ever going to be like perfect. It's unheard of, you know, like if there's iOS developers in the room, you probably remember the launch of Storyboard. That wasn't great. Swift, when it first came out, was really, really challenging. And API stability was a nightmare. You had a story about build times with Swift.

### Thibault
  
Yeah. Actually, when I started my first internship, so I only made one year of school. I only saw C code before that. And I arrived in a company where we were transitioning from Objectivity to Swift. And a fun fact is we were trying out this new architecture called Viper. I don't know if you've already done Viper. But it's basically you have a lot of files that are not useful. And Swift was pretty slow when you had a lot of imports. And so what was happening is we would press compile every time we would change a single letter in a label. And we would just press compile on the MacBook Air and go play ping pong for like half an hour. And then we would come back and see that we made a typo and start again, basically. Really fast turnaround times there. Great.

### Mo
  
I'm pretty sure you got, I'm sure you got very good at ping pong. And then Swift UI performance, I guess as well was like another instance of it. So it's never going to be perfect, but you know, I think one of the things that stands out to me is like the amount of stuff that's now like coming out of the community, as a result of, of, you know, the new architecture, like legend lists, if you speak to Jay Meistrich, he said that it was because of the new architectures, synchronous paints and fabric as an example that that he got inspired to build it. And we're seeing some really cool stuff with the reanimated folks. So I think there's, there's so much there that is that is being unlocked because of the the new architecture. So I guess the question is, what's next after the new architecture? And that was one of the things that we discussed. Probably from a practical and housekeeping perspective, there's a conversation around how long does the old architecture get supported? So from Ricardo, I guess I'm interested to hear from like Meta's perspective, how long do you keep the old architecture chugging along? And from Thiebaud afterwards, I'd be keen to hear what does that mean from like community libraries in general?

### Riccardo
  
Yeah, so when we developed the new architecture, the plan was to develop something that was able to enable new features. Like, for example, as Louis was talking about all the concurrent rendering stuff from React, they needed a new architecture to work. And of course, the goal is to get rid of the old architecture at some point. We are finalizing internally a roadmap that is going to be shared at some point in the future, in the next future. So stay tuned for more precise information about that.

### Thibault
  
And regarding the library state, I remember, so I'm meeting WebView and I remember when they announced the new Arc, there was no Compact Layer at the beginning. So all the libraries had to make changes to be used on the new architecture. So most of the libraries already made those changes. And when the new Arc came out, the few that didn't would still work. So it was easy to migrate. Now I think it's time for the library author to slowly drop the support for paper because it's already painful to maintain an open source library, so maintaining twice as much code is not as good. I've had some side effects from having both architecture and web view and assumptions that wouldn't work so i know that's reanimated for once you put paper for example i think it's time to migrate to new architecture and for library to drop the older one and just for context i don't know maybe mentioned one of the talk about paper is the old version of you know the render so it's being replaced by fabric now with the new architecture just in case.

### Mo
  
Yeah, very much so. I think it's very clear that the entire ecosystem is going towards that direction. So I think it makes sense that library maintainers want to escape the shackles of having two different renders to manage as soon as possible. So... Yes, yeah. So one of the topics that we talked about when we said, okay, let's talk about, you know, what's next after the new architecture was about releases. You know, release cycles in React Native have evolved over time. And, you know, more recently, you might have noticed that there's been a lot more frequent releases coming in and a lot more incremental releases. And you know, you'll see on the Twitter or Blue Skyverse that it's significantly easier to do releases than it was maybe two years ago, three years ago. And so part of the discussion that we had was how can we make releases more incremental, maybe do something like six releases a year, which might scare app developers at first, but I think everyone's realizing that it's better for all parties involved. So, Ricardo, it'd be interesting to hear about what the motivation is behind those sort of six releases a year.

### Riccardo
  
Yeah. So, historically, in doing releases for React Native has been a bit painful because, like, the framework is pretty complex. There are a lot of details that need to be taken into account. And the idea of doing six releases is because we want to become faster and more efficient in doing releases. So we set ourselves goal to release more often to force ourselves to think deeply about how to improve it, how to improve the process, how to make it more automated and better. One of the reasons why it's complicated is also for the number of commits that we were shipping for every release. So doing more releases over the year means that we are releasing fewer commits per release. So that's a benefit in general because the release has, let's say, It's simpler to release, but also the update to the next version for everyone is easier to do. So overall, we thought that it was beneficial for both us and the ecosystem to have more releases. And of course, we highly encourage you to be on the latest version, stable version that we release. But if that doesn't work for you, you can always skip a version. Try not to skip more than one version because otherwise you fall back in the previous situation where you have to jump from like, I don't know, 72 to 76. And that's how you jump. But if you do 74, 76, it should not be that bad.

### Mo
  
Yeah. And, you know, we talked about the whole ecosystem. There's obviously app developers, there's library maintainers, meta. But, you know, there's also this less talked about category of people, which are the out of tree platform developers. And so Saad, and you've been silent so far, so I'm expecting a hell of an answer. But, you know, what's the effect of these more frequent releases for you as an out of tree platform maintainer?

### Speaker 5
  
In the beginning, it was quite scary because I think macOS historically was the slowest platform to release. We'd often be a couple of versions behind React Native Core, and that caused lots of problems because if you're a library developer and you're targeting macOS, now you're help yak. Thibaut was one of the people who told me, hey, can you please release faster because I can't update WebView? And I'm like, oh. Sorry about that. But so when more releases were proposed, I was initially scared. But as it turns out, it's not been that bad. Having each release have less commits means that I have less merge conflicts whenever I try to update React Native Mac OS, which has been a good thing. It also forced us to go and update our release process. And now releases are a lot more automatic. We went and we did a bunch of stuff. So I'm pretty happy about that. And then on the product side, because we also update React Native and Office, We kind of just keep on updating that at the same cadence. And if it's one version or two versions, we'll just pick it up. But so like we weren't forced to go. Now we have to update Office 50% faster. We still do like the number of updates that works for our team. Makes sense.

### Mo
  
So, Thibault, you were like on the release crew far before any of us. I mean, I've never been on the release crew, so, but you were, you were, you were, you were yet. Oh God. So, you were there from 2019. Is that right?

### Thibault
  
2020 for the release crew.

### Mo
  
2020. Okay, cool. So 2020 till now, I mean, we've gone through a pandemic, you know, a lot has changed. But how has the release process specifically changed? What's gotten better? What was it like back in the day?

### Thibault
  
So back in the day, 2020, I went to do more open source and I had no Macs. computer at home. So I decided to build my own because it was before the M1. And before the M1, you would buy a $4,000 machine that would be useless because it was too hot. And build time would be shitty. So I decided that I could build myself a gaming computer for half the price and pick components that would allow me to basically run Mac OS 2. And so I did with hackintosh back. Yeah with a hackintosh and I still have it and so back in the day I remember I I put like 12 core and 24 threads and I was like that's for work and That's what I told myself and as your company pay you to game. No, no, okay Well, I mean that's was on my own time with my own money. So it's yeah, it's okay and and so I did that and and Then they were looking for help with the releases. And I decided to see if I could test the releases because it was in 2020 a very manual process. And you had to pull everything, build everything, test everything, and building React Native back in 2020. If you had a MacBook would take like 30 minutes to one hour. So it was pretty bad. And with my HikenDash, it was like eight minutes. And so I was like, I can build faster than any one of the engineers at Meta. So that's pretty fun. And so that's why they liked having me in the release crew, because I could test really fast. And so they got a really fast feedback loop at that time. They just wanted you for your hardware, man. Yeah, exactly. Jeez. They used me. Just kidding. Cut that part out, please. And so it's been way better since then. Many things are automated and when I see the release cycle and the speed that these guys achieve right now it's it's crazy i'm i'm i've been in the past two release crew but the releases have been so fast every week there's a new release and it seems mostly automated now it seems like they tried to make to make a lot of releases so that they had to automate everything basically.

### Riccardo
  
Fun fact, yesterday I released 78.2 and it took like half a day basically.

### Mo
  
Nice. It's getting better. It's getting much better. Nice. Very, very cool. So another topic kind of moving away from releases, another topic that came up was specific to the sort of Apple ecosystem of devices that React Native supports, but was kind of just happened to happen because of CocoaPods getting deprecated. So there was a conversation around what happens now that CocoaPods is being deprecated. What does that mean for the world of React Native? So the way I want to tackle this is Saad came into that session apparently with some ideas and then the conversation went a different direction.

### Speaker 5
  
Sure. So, um, CocoaPods is getting deprecated. Everybody loves CocoaPods, so, you know, that made everybody sad. Very sad. But actually, CocoaPods does a lot of cool stuff, so I'm being half sarcastic. And Ricardo basically had a session where he asked... what should we use as a replacement? And we listed a bunch of options on the board. There's kind of the simple platform-specific ones like SPM, and then there are like the more complex build systems like Buck and Bazel. And I was all like, we should go use Buck or Bazel. We use a super cool, awesome thing written in Rust.

### Mo
  
In case people aren't familiar, can you just like give like a few lines on like, what are those super cool features that Buck and Bazel have?

### Speaker 5
  
Yeah, sure. Those are both build systems. They can handle multiple languages. They know the graph of all your dependencies very accurately across multiple languages. So you can have a very accurate build where you only touch one file and only the things affected by that one file happen. But the downside of that is you have a complex build system that you have to set up. And it's not what if you're just creating an iOS app. a standard iOS developer would use, which was pointed out at the Core Contributor Summit. And so it was kind of a, I think this is cool, but also it would probably be a bad idea for all the users of React Native to now have to learn how to use this new fancy thing that works at big companies, but maybe not on your MacBook.

### Mo
  
Yeah, no, that's very fair. And so I guess the conversation, maybe for Ricardo to pick up, where did that conversation go and what have you been doing since then off the back of the Core Contributors Summit to tackle this CocoaPods deprecation?

### Riccardo
  
Yeah, one of the main benefits of the Contributors Summit is that we sit all together in a room and we talk about a problem and we discuss alternatives, we discuss pros and cons of everything. The outcome was that we thought that Probably the best thing for the community is to use what is the simplest tool and what's closest to the actual platform that we are targeting. So in this case, it would be a Swiss package manager. Currently we are investigating and experimenting with it. So the idea is to try to be ready for WWDC with a prototype that is... can be kind of tested out by the community to see how it behaves. There are still some unknowns that we need to figure out. So that's why it's not advertised anywhere or, um, usable for, by everyone. Uh, but as soon as we figure out all the latest details, we are going to publish an, um, on RFC and we are going to also have the community with the migration from CocoaPods to SPM. Of course, CocoaPods, like the Reckonitive ecosystem is big. We have more than 1000 libraries in Reckonitive directory. So for a considerable amount of time, you're going to support both systems. To give library maintainers the time to properly migrate. So it's not that Cocoa Puffs is gonna be like dead in June. It's gonna leave a little bit more. But yeah, the plan is to move away from it because it's deprecated, it's going to be unmaintained and no more package is gonna be able to be added to their registry in December, I think. Or December next year, I don't really remember the date.

### Mo
  
Soon. Okay, cool. Now, I guess the last major topic that I think was discussed that we're going to cover today is around sort of the world of out-of-tree platforms, right? And so it's great that we've got Saad here as like an out-of-tree platform enthusiast to tell us a little bit more about those conversations. So I guess talk us through like one for the audience, people that might not be aware of what is an out-of-tree platform and what were some of the conversations you were having at the Core Contributor Summit about out-of-tree platforms?

### Speaker 5
  
Sure. So an out-of-tree platform for React Native is basically a platform that's not Android and iOS because Android and iOS are in the React Native repo. I'll call it React Native Core because that's easier. But stuff like React Native macOS, React Native Windows, React Native VisionOS, those are all out-of-tree because they're separate repos. Some are forks, some are doing some fun scripting to download the NPM source code. But it's basically a platform that you can use with React Native that is not in the official React Native repo.

### Mo
  
Okay, so that's namely web... Windows, Mac OS, tvOS.

### Thibault
  
Yeah, I feel like there's like weird ones like QT out there, but I don't know all of them.

### Mo
  
I did not know that was a thing, very interesting. Okay, so what were some of the conversations that you were having about out of street platforms? What were some of the things that come up? What are some of the challenges, I guess, you face on a day to day basis?

### Speaker 5
  
Yeah, so I think around that time, React Native Vision OS had just come out. And that was interesting because now Mac OS is not the only Apple platform out of tree. And so it kind of, we had to think about what are the rules that out of tree platform should follow? If there is an API in React Native that doesn't make sense for this platform, do we make a new API? Do we modify the API? If we modify it, how does that affect the whole stable API thing? 'Cause we'd like React Native to have a set of stable APIs. And also things like, if you do like something like import view from React Native, how do you make sure that if it's a macOS file, you import a view from React Native macOS? Like, can we come up with a set of rules that auditory platforms should follow so that they work well with standard React Native? Kind of the similar idea of the whole... React framework thing where a framework is this thing that follows a set of rules that works well with React. An out of tree platform is a thing that follows a set of rules that work well with React Native Core. So that was kind of an interesting one because up until then, I feel like we're doing that ourselves. And now there's more people and that's pretty cool.

### Mo
  
Very cool. It kind of ties in some capacity to the Frameworks RFC that you and Nico worked on last year or the year before, I guess. Do you want to talk a little about that and how it ties and how that Frameworks RFC can help this kind of conversation for other platforms?

### Riccardo
  
Sure. So yeah, it was mostly Nicola working on that. I just review it and give my two cents. But yeah, so we're trying to basically draw, we try to draw a line between what's our React Native core responsibilities and what are framework responsibilities. So core should be supposed to provide you with the primitives of how to build an app and frameworks should take care of basically everything else. So like navigation or providing a bunch of libraries that you can use to create your app. And we defined a bunch of rules. Some of them are more formal, like a framework should not redistribute binaries because the source of truth should be the binaries that we distribute as a Reconative core. And also there are some criteria for what we can do like promote framework to be official framework, let's say. For example, you can come up with a framework like tomorrow and pretend that to be on the React Native website because nobody's using it. So Expo is the React Native framework that we suggest because it's battle tested. A lot of people are using it. It works well. So we are confident that is a good solution for people to use it. And we think that those set of rules should help people that wants to create a framework to know what the expectations are, what do we want for them to work on and how to make it work. successful because at the end of the day competition is good um we want for people to come up with new ideas sometimes we also are able to upstream some of those changes inside core so that everyone will benefit from them um so overall it is basically a set of rules to like help people in the community develop what they want to.

### Mo
  
Makes sense. Cool. I'm going to move over to audience Q&As. Can you scan that QR code or is it blocked? Probably half the room can scan that QR code. But if you need to scan the QR code, get your questions in. The first thing that I'm going to address is someone's told me that my pronunciation of Thibaut's name is awful. So someone's pointed that out. So I will try my best to call you Thibaut. Nice. Is that better? Okay. Glad we've settled that one. The question with the most upvotes is, is there a plan to have React Native 1.0?

### Riccardo
  
I was expecting that. So let's say that 1.0 is the... the ideal, right? What we are working toward, but there is no concrete plan right now, meaning that we know that there are a bunch of stuff that needs to happen before we can promote React Native to 1.2 and we are not there yet. There are a lot of efforts going on right now. For example, you might have seen some comments related to stabilizing the JavaScript API. We probably are going to have some projects in the next half to stabilize the iOS and C++ APIs. This should help standardizing what React Native Core exposes to platforms and out of the platforms. So there are a bunch of stuff that need to happen before we can get there. So again, it might happen in the future, but we don't know when yet.

### Mo
  
Yeah, fair enough. Simon is asking, what should we do with unmaintained and incompatible libraries with the new architecture? Is there a good guide for migrating it ourselves, which has a lot more complexity if you want to? Are you talking patch it, take over it, or so on and so forth? But by and large, what is the escape hatch when there's a library that isn't compatible with the new architecture? Who wants to take this one?

### Thibault
  
Go for yeah i think you're probably best suited for it. Yeah i mean i'll try uh first i'm curious which library wouldn't support with the compact layer the new arc because i haven't encountered one uh and if there's a bug in the compact layer we could fix it um so that's my first point second point is uh yeah i mean if the library is unmaintained and you need it you should maintain it open source isn't free and uh if no one wants to take it It's no one's responsibility. So, I mean, as a maintainer of WebView, a library that I hate, because who wants to do WebView in React Native when you could have native components? I mean, someone has to do it, and in the end, if it's a maintainer, it's you.

### Mo
  
Yeah. Yeah, fair enough. Let's take a step back. I think someone's asked, so someone's mentioned, which library is your favorite library? And they've also done this as the emoji. So just want to recreate that for you. So you get a full visual of what the question is saying. So I guess what are your folks' favorite libraries? We can start from Saad.

### Speaker 5
  
Is it bad to say React Native Mac OS?

### Mo
  
No, I think that's very fair. There's going to be some level of bias with this question. But, you know, so that's your favorite library. What's your favorite library that you don't maintain?

### Speaker 5
  
So this is the problem of when you maintain the platform fork, you don't actually write a bunch of React Native code in product because you're not doing that. So I'm not sure I've used many. I know reanimated is cool, and I want to say reanimated, but I haven't used that outside of making test apps. So I'm going to go with that one, but there's a big asterisk over there.

### Thibault
  
I mean I could say that I hate and love WebView at the same time. Because that's how I got here. So WebView could be one of my answers, but I don't like it that much. Reanimated is super cool and I think it's changing a lot of things. And when I think of like one library that should be in every Reckonative project right now, it's probably this one. So that's going to be my go-to.

### Riccardo
  
As Saad was saying, I'm not writing a lot of React Native code, so I'd say that probably one of my favorites, but not for like the final result that it gets, but for the benefits that I get from trying things with that is probably Firebase. And that's like the reason is that Firebase is complex enough that if I make some change in the build system for iOS and it works with Firebase, I'm pretty confident that it will work for everyone else. So yeah.

### Mo
  
Oh god. I quite like a lot of the Expo libraries. I'm trying to think about ones. I really liked Expo AV as a user, and then I went into the source code to try to fix it, and then I didn't like it anymore. So that was an experience. Shout out to the team for Expo Video that they've been working on. I think it's the right path forward. There's quite a few of the Expo modules that I think are really good for just getting an idea up to scratch pretty quickly. Cool, we're done with the library fan fiction. I don't know. Is the Core Contributors Summit like the Avengers Gathering? No. Care to comment anyone else on that? No, it is not. Today, upgrading React Native versions of a project is quite complex. The CLI automatic upgrader rarely works. Is there a planned way to make... easier to upgrade. I'm going to start... If you're thinking today's difficult, where were you five years ago? Where were you? Or ten years ago, yeah. There's many people at Theodore Apps who have gray hairs now, and they might have something to do with a number of updates that they've done. But like... you have it easy now back in my days. Let me tell you about what it was like when I was a kid. No, it's gone significantly better. So I think that's worthwhile mentioning like it's night and day now, but what do you think are improvements that can be made still?

### Riccardo
  
Um, So one of the reasons why we are suggesting a framework like Expo is that it's supposed to help you with upgrades. So if you're not using Expo, maybe consider migrating to Expo to see if it makes it easier to upgrade. A couple of other things come to mind. we are stabilizing the APIs, and we are tracking the breaking changes that we are shipping for every new version of React Native. Doing so many releases, we are seeing the number of breaking changes decreasing. So that's another good thing that came out from the more frequent releases initiative that we have. So we have a bunch of projects basically that are supposed to make upgrades easier for everyone, even people not using Expo.

### Thibault
  
Yeah, just to comment on that, I think what's hard with upgrading Gradient Native is when it forces you to update your dependencies. your dependencies and your libraries that are unmaintained and that you have to change and then you have to change your product code. Upgrading React Native right now is mostly bumping just package.json and that's it. - Yeah, there's no like manual linking or anything like that. - But then if you have to change your weird dependencies that you made five years ago and the guy who did it in your company is gone, then you get into trouble. So if you have in-house code, don't forget to update it. And if you use open source libraries, don't forget to give money to people who maintain them. Maintain them, yeah.

### Mo
  
As if the new architecture wasn't painful enough, do you plan to rework the whole React architecture now to change the way the whole React tree, Shadow tree works in terms of rendering?

### Riccardo
  
Not that I'm aware of.

### Mo
  
Okay, cool. Someone's asking if anyone's working on the React Native CarPlay repository. That's not an out-of-tree platform that anyone I know supports. I think it's just like a library. So do you know anything about that?

### Speaker 5
  
I saw that library on GitHub in that I get a lot of notifications from GitHub and I saw somebody do something there, but I have not looked more into it.

### Mo
  
Cool. I echo Thibaut's sentiment about picking it up if you're looking for open source projects, because I think it's one of those that's abandoned. from what I remember could be wrong. Let's do one more which I'm just going to choose randomly. Are we ever going to get rid of Objective-C from React Native Core and we'll wrap it up there short answer, no.

### Riccardo
  
I mean, there is no really benefit in rewriting React Native. I mean, there are benefits, but they are not... Worth it. Worth it right now. what is more interesting for the community is to reach a point where you can use Zwift to write your native modules and native components. And that's something we are thinking about, something that we are looking into. it's basically top of my mind specifically on how to make it happen unfortunately there are different priorities that we need to balance um but yeah rewriting core in Zwift is challenging and not the top part it's challenging and there will not be very uh benefit for the community. I doubt there's any benefit for the community. I can't think of one. Like you said, I think it's just if you're able to write Swift native code as an app developer, that's all you're looking for and it doesn't really matter that much.

### Mo
  
Awesome. We are slightly over time, so I think we can wrap up the Q&A, the panel and the Q&A there. But can we have a massive round of applause for Saad, Thibaut, and Ricardo. Thank you guys so much for being a part of this.