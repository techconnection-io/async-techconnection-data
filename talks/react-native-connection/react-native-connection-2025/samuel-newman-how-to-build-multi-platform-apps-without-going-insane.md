---
slug: >-
  /talks/react-native-connection/react-native-connection-2025/samuel-newman-how-to-build-multi-platform-apps-without-going-insane
date: '2025-04-02'
title: How to build multi-platform apps without going insane
author:
  - Samuel Newman
video: Z0ffsDvbVII
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/Z0ffsDvbVII.jpg
slides: null
tags: []
year: 2025
conference: react-native-connection
edition: react-native-connection-2025
allow_ads: false
---
### Samuel
  
Bonjour! Hey everyone! Great to be here. Yeah, I'm gonna cover how to build multi-platform apps without going completely insane, because it's hard on the sounds. Yeah, I'm Samuel. I work at BlueSky and I have done for about a year now. I work on the app, which is, as you can guess by me being here, is React Native. BlueSky Social is a microblogging website. It looks something like this, at least for me, because I use it mostly through the iOS simulator. Most people use like an actual phone. Yeah, I thought I'd just quickly go over the history of Blue Sky, just for a bit of background. So it was started by Jack Dorsey in Twitter as like a project to decentralize Twitter, so to build a protocol by which Twitter could be decentralized. Jay Graber, the CEO, founded Blue Sky Social as like an independent organization. So like we were never part of Twitter, we were just hired by Twitter effectively. So 2022 protocol developments. In June, we started building a reference app. So the broader goal was to make Twitter decentralized, but we thought we needed an app to kind of prove it out, proof of concept, MVP the protocol, basically. That all changed in October. I don't know if anyone was following the news, but Twitter changed. So in 2023, we started launching an invite-only beta, and we basically took this reference application and decided just to go for it. 2024, we had the public launch, and as of April, we have 33.8 million users and only going up. Why do we build with React Native? Because, and more specifically, why React Native Web? The dev team initially was one guy, Paul, the CTO, now CTO. And so we had to build for, you know, we had to build good enough apps for three platforms. And, you know, it's just not feasible to build the same app three times in a row on three different code bases, three different languages. Like that's, it's just not possible when you're so resource constrained. React Native is obviously the answer to that. We also needed maximum iteration speed, you know, we had to move fast. Also, our backend is in TypeScript, so obviously it helps to have the SDK kind of same language. It's good. It's good, actually. React Native is very good. We've had a great experience with it. But also, it's not easy to be a multi-platform codebase. It's one codebase, but three times... a cap of maybe three times as complex. You know, there's a large surface area for bugs. Components, you know, they can turn into so many different things that you've really got to like it. It's a huge QA button. There's also the question of, you know, how is it fitting in? You don't want an app that runs everywhere, but kind of feels like a stranger on all the platforms. Like the point is to be native. So... Yeah, it's quite difficult to get to that level of polish that people expect out of their apps. The answer obviously is to build abstractions, but that's not always easy. Abstractions cover up what's going on by their very nature, and if you get that wrong, it can really make your life a lot harder, and possibly even harder than it was originally. You either make the surface too simple and then suddenly you can't configure it. But then also there's the flip side of that. And I'm sure a lot of you have experience where you need to do too much configuration every time. So every time you use a component, you have to spend ages like fine-tuning all these props and stuff and it's a pain or you need to use platform select everywhere like that's not making your life easier that's making your life harder so i thought today i kind of go over some like uh guidelines some like uh tips and tricks for making good abstractions. Step one is identifying your target. So like, what do you want? What are you trying to make? So normally you're trying to, you know, you have a goal of, you know, you need to show some information. So for example, like a dialogue component. You need to show some info to the user in a way that pops up and then they dismiss it or press a button or something like that. Each platform has its own idioms for what that should be. On a phone, it's typically a sheet that you can swipe away. But obviously on a desktop, you don't want to be swiping with a mouse. That's ridiculous. You want a modal. And on tablets, maybe a popover? I don't know. So you have what you want it to look like, what do they need? So a sheet needs a handle and needs a scroll view. A modal might need like a close button. A popover needs like a place where it pops from. And then you need to define the surface to kind of cover all of this. And basically my main takeaway, this is a big argument for the composition pattern. Composition is great. I feel it's a little bit... not everyone loves it. It quite, you know, it's a little bit boilerplatey, but as I'll get into, I think it's the right move here. So this is how one might do a dialog component, right? You have a root, a trigger, the content, the handle, the close button, and the scroll view where you put your stuff. React Native, obviously, sometimes you need a flat list instead of a scroll view. So the composition pattern, you know, lets you kind of swap out bits and pieces and it lends itself very well. This is a little bit out there, but this is a... I tried to make a visualization of like... Oh, God, not too far. Sorry. Okay. I tried to make a visualization of API surfaces. So, like, they're vaguely the same shape. They overlap a lot. But they don't completely overlap. There's like sticky-outy bits. There's, you know, there's a big bit green, on the green one, there's a big bit that sticks out the bottom that doesn't overlap with any of them. And I feel if you just try to cover that surface with just like one big element and just put a thousand props to try and kind of figure out every different variation, it's going to be far more complex than what you started with. And so how I feel the composition pattern works is that you just try and cover each of these sticky-outy bits with more specialized components, and then overall you glue it together and you're able to cover this API service in a much cleaner way. Yeah. There we go. Yeah, so like yeah, each platform has unique requirements. And while they broadly overlap, you know, you got to... Yeah, and not all components need to serve all platforms. That's another important thing. Like don't try and make... They are different, they are unique. So you know, that's okay. Let's get into some examples of how we do dialogues, I guess. So here's a very simple dialogue. It's just a sheet and it has info and you can dismiss it. The handle is a handle. The scroll view, we just put a scroll view in a native sheet and that works very well. Same story on Android, it goes to pretty much the same thing and even though it's under the surface, it's an Android native mobile. The API surface is full intensive. As an author of these dialogues, you don't need to care at all. It all works. Then it comes to web, and obviously web is completely different. We don't have a handle, but we have a close button now. And then a scroll view. Well, web doesn't really have scroll views. You just have a div with overflow. So we don't actually use a scroll view on web. It's not... we instead take that scroll view component and we present just a completely different interaction. So here's an example of a really tall dialog that we have. So if you have lots of labeling services like I do, we instead make the entire dialog grow and you can scroll the entire sheet instead. So, you know, you can adapt for what works best on each platform. What about a flat list? So on native, it's much the same idea. Obviously, you can't stick a thousand GIFs in a scroll view. That's just gonna explode your terrible Android phone. So instead you need to virtualization with a flat list. But in terms of UI, it's the same. It's just a scroll view in a sheet. We've got a handle, we've got a flat list. Pretty simple. On web, however, we can't do the same thing as we did for the scroll view because it needs to be infinite. So instead we contain it, the close button goes outside because it no longer fits inside. And we put the... we put the content within a scrollable area. So yeah, you've got to give these things a fair amount of thought. With web especially, it requires very different UI idioms, and so it takes good abstractions to make this seamless. Let's get into a bit more of a complicated example, like a menu component. So what do we want? We want like contextual options. Like when on a post you have like, sorry, you have like the primary like actions, like the light button, but there's a bunch of other stuff you can do a post. So let's hide that in a menu. On web, that should be a dropdown. And on native, it could also be like a UI menu, like a native UI menu. But I don't know if anyone's used a Zygo on Android. But oh my god, that looks so bad. It looks so bad. So let's use a dialog instead. This is the API we want to use. It might seem really boilerplatey, but instead we, on native, it transforms to like, it's the same dialog component we were using earlier, but with some just opinionated styles in there. Each menu goes to one of these options and it looks pretty native, but it's really just mostly kind of views with styles. On web however, we use a Radix dropdown. So like this is a very different interaction. But the API just from a user perspective, like building these menus, we have tens of these menus and you just don't have to think twice about it. Yeah, if you get this right, it makes authorship so much simpler, it makes the developer experience so much better, so it's well worth the time investment, and it lets you get so much closer to the native feel without needing to write everything you make three times over. I like to use native components a lot and I recommend you do too, but that's not always the answer. I thought I'd demonstrate why our app doesn't support iPad yet. Here's the sheet on iPad. Oh no! iOS tries to be helpful and use a different idiom, but obviously that doesn't work in our case. So, but you know, iPadOS tries to be too helpful, but actually it makes it so much worse. So it's totally fixable. I know how to fix it. You can make it like a popover instead that like falls back to a sheet on an iPhone, but just need to get around to it. Why bother? Because, I mean, at the end of the day, you don't need to do this. You could make monolithic components with lots of props. But I feel like a real strength to this is that it... when you separate yourself from the actual implementation, it unlocks a lot of power. And a great example of this was we used to use like JavaScript based sheets, but they were giving us a lot of trouble. Like they weren't accessible at all on Android. There was like keyboard problems. There was like scrolling problems. They never quite worked right. So one day my colleague Haley sat down and was like, screw it. I'm going to rip these out and I'm going to write my own Sheets implementation. And she did it in two days and it was amazing. But the beautiful part was of that is that we didn't actually touch any product code at all. That was all because our abstraction was pretty solid. We were just swapping out the implementation and it just worked almost completely seamlessly. It was amazing. Now I'd like to show off a new kind of menu that I've been working on. Coming soon. DM reactions. So this is made custom with reanimated. It's fully JavaScript, except for that bit. That bit's the native emoji pop up. But what I think is pretty cool about this is it uses exactly the same API in our product code as a normal menu does. So, oh, and it's cross-platform. Yes, it looks like the iOS one, but it's fully cross-platform because it's reanimated. But yeah, like when it comes to how it looks in the product code, even though it looks radically different across the three platforms, all of our kind of like business logic is completely identical. And it's the fact... On web, it is literally just a menu. I just do the platform extensions and I just exported menu from menu. How it works is also pretty funny. You might be thinking, how on earth did you get that component and pull it out on top of the blurry bit? I struggled with this for a while, I was trying to do some strange portal implementations but that doesn't work because you kind of have to fake portals and then we had text with links in it and that relied on the navigation context nothing was working, everything was breaking, so I was like "screw it, what if I just take a screenshot of the elements?" and paste it and just send the base 64 text up to the top level and just put it in an image and that's what i did and i'd spend like a good day trying to find reasons i shouldn't do this and i couldn't come up with anything um sometimes the simplest solution is the best solution. Yeah, closing thoughts. Yeah, cross-platform doesn't have to slow you down. It just requires a fair amount of care. Write good abstractions and use composition. If you build abstractions right, you can... you can have a feature velocity, you know, equivalent to, you know, just building for single platforms. And if you can reach that state, then you're golden. And finally, have fun. Thank you. That's it. You can find me on BlueSky. This is a starter pack for the App Protocol dev community. I didn't really talk much about App Protocol on this, but it's a thriving little ecosystem that's popping up. Very fun with React Native. So if you're interested in the future of social apps and social protocols, I highly recommend you give App Protocol a look.

### Mo
  
Thank you for the talk. I think being able to use React Native across multiple platforms is important and then you have to think about the right abstractions and I think you're touching on a lot of important points there. Don't know if I agree with the screenshot thing. Still confuses me, but we'll see. I need to think about that one for a little bit. It's super cast. I won't argue that it's not cast. Have you not heard of Zego? All right, me and you are going to have a chat. I'm curious to kind of ask you, what's been the... You've obviously used React Native Web probably in one of the most widely used platforms out there or applications out there. What's been the biggest quirk or annoyance for you with React Native Web as a package specifically?

### Samuel
  
Good question. Yeah, I think that the... You can say you love it. I mean, I do love it. But also it's coming... I came from like a more like a react... JS background. So coming into this strange, uncanny valley world of kind of going into the native APIs and then back again, it was a bit of a steep learning curve.

### Mo
  
Yeah. There's, I think, Caddy might have written an article about this on the Expo blog about like, going from web development to native. And I think there's a lot of gotchas. Like it looks very similar, like 80% is similar. And then the 20% really surprises you when you step into it. Yeah, no, for sure. An interesting one, because obviously like your job is working at Blue Sky, but you also do open source contributions or your app is open source. How is that impacting your day-to-day life? given that you know you're not only tending with internal stakeholders but there's random people in the community who see what you work on and you're also involved with open source efforts how do you balance that what's the challenges of doing that?

### Samuel
  
I'd say it's overwhelmingly positive. I really enjoy like all of our stuff being out there it's a great feeling and we've had some really great community PRs we make sure that you know keeping track of them. I know multiple people in the audience have opened PRs with this guy. I promise you I'll get to them. I just am so busy, but I will get to them. But I say the one downside is that it's impossible to do anything in secret. Like we shipped April Fool's joke. So we made a branch called like Update Sentry or something like that in the hopes that nobody would click on it because it sounds boring.

### Mo
  
I'm presuming someone found out.

### Samuel
  
I think we got away with that one.

### Mo
  
Oh, cool.

### Samuel
  
In the past, we tried to do the direct messages project in secret, and that really didn't last very long. People were like, "What's all of these weirdly named branches?"

### Mo
  
Yeah, fair enough. What was the April Fool's joke out of curiosity?

### Samuel
  
We decreased the character count by one. at 299.

### Mo
  
That would drive me mad. Cool. Just wondering if there was a cascade effect there as well. So like, did you delete any posts that were 300 characters?

### Samuel
  
It was a grace period.

### Mo
  
Cool. Good to know. Someone's asked, desktop app when?

### Samuel
  
When?

### Mo
  
I'm just quoting this at this point.

### Samuel
  
I mean, it could be done. It's a question of, I don't know, do we do the React Native macOS? Do we do a supercast React Native web electron?

### Mo
  
Oh, I would love to see that. Not because it would be good, but it would be so bad. And so entertaining.

### Samuel
  
Yeah. maybe one day in the far future, but three platforms is plenty enough for me right now.

### Mo
  
I guess that touches on something quite interesting, which is like, you say three platforms is a lot, right? What do you feel like is the cost of adding every single extra platform? Like if you tomorrow had to use React Native Mac OS, What's your gut instinct saying? I know you haven't done it in practice.

### Samuel
  
No, it's an increase in QA. You know, already it's quite a burden having to check your work three times, especially like, you know, reviewing PRs and stuff. Like checking everything three times and three times on device. Also, it's just time consuming. And then it relates it to the talk. You're going to build these abstractions at an additional time. So that requires even more thought.

### Mo
  
And how much of your time do you think is spent on building these abstractions versus just building the business logic itself?

### Samuel
  
I think we're over the hill, but from time to time, I need to build a proper select dropdown is what I need to do next. But now that we've got the dialogue sorted and the menu, I think we're in a good place.

### Mo
  
Yeah, I think it raises an interesting question, which is like, you know, what is the ultimate cost, not just QA, but like development cost of every single platform that you add? And when does that trade off tip? And I don't know the answer to that. But I feel like web should hopefully suffice for everyone's blue skying needs for now. Fingers crossed.

### Mo
  
Another question that's come in is how influential is the UI/UX, I guess maybe your design team's input when you're implementing a shared component or API for each of the platform, how heavily do they get involved and start to think about the intricacies of should this be a dialogue or should it be a bottom sheet or so on and so forth?

### Samuel
  
Is there UI/UX? Sorry, that was the first question. We don't have a very strict structure. I feel like we have a pretty limited set of tools in our toolkit at the moment. So I feel that kind of like guides us, points us in very specific directions. You'll notice that if we need to do something, we probably are using a dialogue.

### Mo
  
Yeah, fair enough. Okay, so you're trying to work within the bounds of what's already there and use that.

### Samuel
  
Yeah, that definitely shapes our design. I mean, we only just hired a designer like last week. Good luck. So we don't... our app was more evolved than was designed. It was a kind of natural selection kind of thing.

### Mo
  
You know, it works. It sure does. It's non-design-driven development. It's great. Cool. Awesome. Thank you so much, Samuel, for doing this talk. Really appreciate it. Really cool topic and cool to see what goes into building Blue Sky on a day-to-day. Massive round of applause for Samuel. Thank you.