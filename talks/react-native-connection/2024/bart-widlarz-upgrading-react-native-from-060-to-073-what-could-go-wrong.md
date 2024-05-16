---
slug: >-
  /talks/react-native-connection/2024/bart-widlarz-upgrading-react-native-from-060-to-073-what-could-go-wrong
date: '2024-04-23'
title: 'Upgrading React Native from 0.60 to 0.73: What could go wrong?'
author:
  - Bart Widlarz
video: oUo-lCselbE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/oUo-lCselbE.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: '2024'
allow_ads: false
---
### Bart
And, yeah, that's true, I do parkour for, like, 15 years, actually more than I know React Native. And today I'm going to be talking about upgrading React Native from version 0.6 to 0.73. But let's call it 60 and 73, because we all know that React Native is still not in v1. So what could go wrong?

And it seems that actually quite a lot of you answered that upgrades are really, like, the pain point in React Native. This is the results of a survey State of React Native from 2023, and upgrades are fourth on the list. If you look a year before, it's actually in the first place.

So I have a question for you. So if we can turn the light on for a while, can we, yep. Who of you have issues with upgrades in React Native?

Yeah, right. And those whose hands are down, the question to you, you didn't have any, right? Yeah, okay.

So my story, I mean, from my experience, like, upgrades are hard, thanks. And if you look into React Native versions, you can see that the version 60 is the last one which has some, like, let's say, reasonable documentation. And everything below is in this kind of danger zone place where when you try to go there, it's something like that.

Actually, it was like that for, like, last week. Until last week. Then they fixed it.

But, you know, it says something, right? And we have asked the community about what are their strategies for upgrading React Native. And I gave this context that I'm now going to give to you.

That we have this, we had this app that was unused and unmaintained for five years. So the assignment was to upgrade it and make it live again. And what the community gave us was kind of what we actually knew from our experience.

Let's go through it. So in this kind of updates, you can, like, rewrite the whole thing and step by step add new functionalities that should be there. You can try with going step by step as well.

We have this kind of middle steps in between. But in general, the, like, vibe was good luck, mate. It's not going to be smooth.

So what could go wrong? Quite a lot, right? But before I start telling you our story, I'm going to quickly introduce myself.

I'm Bart. And, yeah, as I was introduced, it's Wydlasz. It's hard to pronounce.

I know. I'm the CEO of the Wydlasz group. We are a React Native agency.

We do work such as this. So we upgrade, add features to the app. We do some performance optimizations and stuff like that.

But you may know us from the community work that we do. We've been basically maintaining and we created React Native Notificated, React Native Emoji Keyboard. We contributed a lot to React Native Maps.

And the last but not least to React Native Video, which actually going to be going live with the new version, stable version v6 quite soon. And if you want to get access to inter-player, which was mentioned today on the previous talks, you need to upgrade to v6 definitely. And in next versions, we also want to have the new architecture support fully.

So this is just a matter of time. But let's get back to our story. So here we are, like no code changes for five years.

Apple has pulled the app from the store. And the assignment is to make the app live again. But this is just the tip of the iceberg because like the issues we faced, there are much more of them.

Like the wrong tool versions, navigation version 3, deprecated SDKs, unmaintained forks, library patches, React Native upgrade itself, custom modules, broken CICD, outdated packages. Oh gosh, you see, right? So let's start from the beginning.

We need a plan and we need to upgrade React Native itself. So the possible approaches that we have is like kind of the ideas we brainstormed and from our previous experience. And in this case, we decided to go head first and upgrade to the latest target version.

So the battle has begun, right? We started the same way as most of you would. That is with the good old React Native upgrade table.

We're feeling pretty confident, pretty defined, so we select source and target version. And that is not the only battle preparation we have. We really wanted to use Flame AI as an additional AI assistant.

And Flame AI really does help sometimes and can speed up some changes. And its interactive mode is totally awesome. So we started conducting the upgrade together.

I mean, we and Flame AI, our team and Flame AI. And time passes by, some things go smoothly, some not. And Flame AI, for example, did not properly edit some files.

Like an example, changes required to be done in pod file were not applied to all of the targets in the file. It also skipped some other files, for instance, gem file. We had this hypothesis that it might be because in the app version 16, this gem file was added manually and the example app in the upgrade helper, it wasn't there at all.

But never mind, we just needed to modify it by hand. And that's what we did. By the way, for Flame AI help, I was charged something like $2.

And it saved me more than one hour, probably two hours of mundane and error-prone work. And you can guess, my hour is much more than $2, right? So it was helpful.

And while Flame AI helped a lot, we decided that some changes we'll do manually. Like in case of Xcode project file. We all know that these diffs can be huge, hard to reason about.

So I wanted to verify everything closely by myself. One thing that I missed, though, was updated build script phase, which was changed compared to how it worked in previous React NT version. But besides these issues and a couple of other issues, we have wrong tool versions, particularly with CocoaPods.

We managed to upgrade React Native itself. So it means we're done, right? That's the end of presentation.

But no, no, no. We're not done yet. Sorry for the confusion, yeah.

We have some other stories, right? We still have something to tell you. Now that we upgraded the React Native itself, the time has come to tackle all the dependencies.

And you see this app is actually not a simple to-do list app. This app is, its main functionality is audio and video calls. So you can imagine.

And it was like five years ago. And also, you may ask, probably maybe already asking on Q&A, why not Xcode? Like five years ago, if you wanted to build something which uses so many native elements, Xcode was totally out of reach, actually.

So this code base doesn't have any Xcode code. But let's get back to what we have. We have tons of outdated packages, right?

What are we going to use? We're going to run align-debs to see what needs to be upgraded. And with one of the multiple build time errors, this was caused by old version of NetInfo package.

And we were prompted by this align-debs to basically upgrade from v3 to v4. 11. Quite a distance, right?

Quite a distance. And we did that. Like, let's see what's going to happen.

It says so. I'm going to do it. So we were excited to see what's going to happen.

And the build time error was actually gone. And we're good to go fix other build time issues with other libraries. And once we resolved all the build time errors, we tried to run the app.

And it turned out that NetInfo was throwing an exception runtime. Like, you know what I'm talking about, right? It happens if you don't read all the changelog of all these remaining packages.

It occurred that addEvenListener method no longer existed. So yes, someone should have read this changelog or compiled TypeScript. And actually, in this codebase, there were TypeScripts.

Quite well-maintained codebase, that is, right? But no worries. We did that later.

We compiled. We read the docs in the places where it was needed. But in this kind of interactive approach, you can actually read the errors and fix them step by step.

Instead of reading, like, 100 pages of documentation in changelog that happened in the community for the last five years, I can tell you this changelog is huge. So quick look into the error docs, and we fixed that, right? And that's how we basically handled most of the community dependencies.

We've got React Unity upgraded. We got most of the community dependencies upgraded. But some libraries can't be updated.

Like, why? I mean, some, they basically no longer exist. And I have a question for you, if we can turn the light on for a while.

Do you know React Native Fabric, hands on? Yeah? So now it might be a confusion, right?

Do you mean, like, the new renderer that we were talking about before? But no, I mean React Native Fabric, the, let's say, toolkit for analytics and crash logs that was later moved to Google Firebase ecosystem. So that was over there, and it was very old.

So we basically needed to migrate, right? But no worries. In this case, the issue wasn't in changing all the codebase, because in the codebase, there were this code wrapper.

So on JS side, there were just one place where it was used. So we changed that, and we made some adjustments in the native code, similar to how it worked in Fabric. And yeah, that's how we migrated most of the dependencies to new ones.

And we realized that there are not only these community dependencies and these no longer existing dependencies, and those React Native dependencies that were moved from React Native to community. No, there were also outdated internal SDKs. Like, you can sometimes think that open source tools aren't documented enough.

But listen to this. In case of community libraries, you can always reach out to some other community members, read the docs, issues. But like in our case, there were no documentation for these SDKs, and they were under heavy development because of the web app, which was not part of this mobile Android iOS React Native codebase.

Don't ask me why. It was like that. But the SDK was under heavy development, and we were using the old one.

And the changelog between five years from now until now doesn't exist. Like, imagine, it's like internally, these tools are built in front of the whiteboard, over the coffee. People were just throwing things like, oh, hey, Mo, I'm going to basically update API.

OK, no worries. Just send it over to me. Oh, yeah, OK, it's sent.

And sometimes this is the way it's handled, because the only people who are using it are a few developers, or like thousands of developers, but not like thousands of people as it is in open source. So we reach out to the team that exists. It's another team, not the team that built the SDKs five years ago.

And we basically tried to figure out all these errors and try to understand in this kind of reverse engineering style thing what has changed and why, which is like the most important thing here. Because when we asked them about the changelog for its last five, six years, they said that no, there's no anything, not in this case. But yeah, we handled this in this more like collaborative way than just reading this changelog.

But it affected the flows of video, audio calls a lot. And by the way, while we are at flows and screens and navigation, when I said that we updated most of the dependencies, I meant that we decided to stick to navigation version three for now. So like the API is different, very different than it is now.

And try to make it work with React Native version 73. Is it possible? Yeah, like, well, let's see.

Within all the API changes in React Native made these past few years, there was removeEventListener method that was removed from the dimensions module. And we all know that properly handling event listeners is crucial to not having any memory leaks. So React Native navigation version three was calling this method.

And we were experiencing crashes. Like we're in this hacker mode right now. So don't judge me.

But we really wanted to keep this navigation version free. Why? Because it's so coupled with the whole architecture and with the code base, you can't actually turn it off for a while and give some more time to do it later.

Like it's not the thing that you can basically label to do later. So we temporarily fixed, let's say, fixed this issue by applying a patch to navigation with a patch package library and used new API. A patch for navigation was not the only one we added.

We also needed to change an old unmaintained version of React Native internationalization. But keeping navigation version free was actually not the only thing we needed to do. And it was more challenging than we thought because we also needed to kind of fix the pre-created React Native safe area view library, which was used by one of the module of navigation.

I think for error was basically in a newer version. So now we needed to hack it in a way that it forces navigation to use the newer version. And we did that by adding a resolution, simply re-declaring version and package JSON like that.

As a result, we could stay on version free of navigation and some old internationalization library for a little bit longer. Oh, and I didn't mention before that all this changed now we're running locally. So if we want to build a project around linters, we couldn't trust the pipelines to support us.

Since a Mac mini runner had been, that the pipes were running on, were somewhere in the basement of the office. And it's gone. Nobody can find it.

And we didn't want to really have this in-house setup again. We decided that with the client that, yeah, don't do it. We need to migrate to some cloud solution.

And you have some options like Expo EAS. And for some tools, it's too late. Like App Center, for example.

Thanks for being here. Yeah, but this tool is out now. So you're going to need to migrate to something else as well soon.

And here, I really would like to finish here and say we covered everything and everything is fixed. But we can't do it. And we have even more challenges here.

Like team morale, you can imagine. But also wrong tool versions. I mentioned Cocoapods.

Most of them were over there, but not only. Unmaintained forks. Give me a second.

I'm going to talk about it in a second. We animated version 1. Who remembers this lovely DLS?

So like special language for animations almost. Permissions API has changed. That's also something that affects the flows of mostly video calls, right?

You need to ask for permissions. But also account management risks. You need to really have this partnership relationship with the client when you communicate the issues that are so abstract.

And let's get back to unmaintained forks. For a while, I mentioned video calls. So some of you may know WebRTC.

Some of you maybe even know React Native WebRTC. In this case, we had this fork that was five years old with no documentation and nobody to ask for some help. And this part is actually still in progress.

But we're on good track to also deliver this. And here, I wanted to say that React Native Committee is awesome because all these tools that we have used are great help. I wouldn't imagine working without them.

Really, thank you, the committee. Great. But with all of these tools available, upgrading is still a pain point.

And you really need to use some more tools than that. And most particularly your brain, right? Skills and experience and time and motivation to successfully handle missions like that.

So from all of the upgrades, that was definitely one of the most challenging that we did. And we've been doing currently. But I don't need to tell you how important it is to keep your versions updated.

That was told before on other talks when we were discussing that if you want to have better performance, you need to have the newest React Native and the libraries need to be upgraded as well. Here, during this presentation, you've got a chance to hear out the story of this particular case. And we have learned a lot during this and other cases like this.

So we have gathered these tips. And if you want to learn more, actually, you need to see this. We're going to be publishing this e-book.

They're going to guide you through some React Native upgrades based on our experience from the cases that we had. And we even have some downgrade situations. So I really want you to basically not having the same stress and so much time spent on things that can be documented somewhere.

This is like the tentative plan that we have here. So there will be time-saving tips, things that you don't read in the docs of tools. So enhanced documentation, strategies for different approaches.

And I really want to also add some time estimates on different approaches so that you're ready to discuss with the managers. Also some communication tips when it comes to discussing with business and managers and our real stories. So basically, that's it.

Thank you very much. And you can reach out to me. I'm here.

You are awesome. And I'm happy to answer your questions from the Q&A session. Thank you.