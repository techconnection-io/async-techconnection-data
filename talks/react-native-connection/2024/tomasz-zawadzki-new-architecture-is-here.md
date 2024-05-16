---
slug: /talks/react-native-connection/2024/tomasz-zawadzki-new-architecture-is-here
date: '2024-04-23'
title: New Architecture is here
author:
  - Tomasz Zawadzki
video: jf0WTF4z8O0
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/jf0WTF4z8O0.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: '2024'
allow_ads: false
---
### Tomasz
I'm Tomasz Zawadzki. I'm a software engineer, as mentioned. I focus primarily on research and development efforts, maintain libraries like reanimated and also contribute to React Native Core.

And today, I will be talking about the current state of the new architecture. So, first of all, what is new architecture? It's a redesign of the core internals of React Native.

It is meant to eliminate some existing architectural level limitations of the framework and unlock new capabilities. So, it mostly changes how things work under the hood. And ideally, it should work with little to no changes in React JS code.

And apart from this, it also unlocks new APIs added in recent versions of React for crafting better experiences. So, what exactly was not possible? First, building adaptive UIs often requires measuring some views prior to painting.

Think of tooltips. So, in old React Native, measure was mostly asynchronous. Also, use layout effect was kind of broken.

And React 18 just wasn't possible to implement in React Native. There are also different cases, for instance, text input. It can be modified either from JS or from user events.

So, there can be some desynchronization. And also, the render function is called on the JS thread, but the scrolling happens on the UI thread. So, Fabric will then architecture will not solve the second and the third problem here.

It will just give you the tools. It will give the tools to solve for library authors. So, the React Native we know today is mostly asynchronous.

This is implied by the unique threading model. So, in most of the mobile applications, we have the main thread, which is also called the UI thread. And if there are some specific calculations that we want to run in background, then we just start new background threads.

But in React Native, the React JavaScript code runs on a separate JavaScript thread. And this is for better responsiveness. Because only the UI updates are scheduled to be run on the main thread.

And similarly, events are handled on the main thread, but its callbacks are scheduled to be run on the JS thread, which might introduce delays between the action and the reaction if the JS thread is busy. So, the communication between JS and Native is carried out by a so called bridge. So, when JS wants to update a view or invoke a Native method of a Native module, it creates a payload object, serializes it into JSON, and pushes it into the queue.

And then, sometime later, on a different thread, the Native site pops out the item, deserializes it, and runs the associated Native code. So, the bridge was simply a message queue for instructions like rendering views or calling some Native methods. And also event handlers.

So, the bridge was limiting React Native in its asynchronous design, message batching, and serialization costs. So, that's why it's one of the most hated pieces of React Native architecture, as it introduces some serious performance and memory overhead. So, here's how it looks on the new architecture.

Let me explain the four pillars of the new architecture. JSI, TurboModules, CodeGen, and Fabric. So, JSI allows for faster and synchronous interfacing with Native code.

Instead of calling the Native code via bridge, we can directly call a C++ function synchronously, just like it was a regular function. And from there, we can call Java via JNI or Objective-C code or C++ layer. It also works the other way around.

We can also call regular functions from C++ code. So, this is possible thanks to JSI, which is a C++ API for interacting with JavaScript run times. JSI supports Hermes and JavaScript core, but also Node.js or Google's V8. So, anything you can express in JavaScript code, you can also do that from C++. But note that JSI function calls are fast, but not free. So, please don't overuse them.

Next up, we have TurboModules, which are the spiritual successor to Native modules. So, Native modules, they use bridge, and TurboModules, they use JSI. And Native modules, some APIs in React, like alert or keyboard or linking, they were implemented as Native modules.

And right now, with the help of JSI, they are migrated to TurboModules. And TurboModules also go in pair with CodeGen. So, Native modules, they used to be dynamically typed.

So, the data had to be serialized and parsed. And in a case of type mismatch, the only feedback that the user would get was a run time error. So, that's why TurboModules come with CodeGen, which ensures type safety.

So, CodeGen is a tool, a script that runs during app build and generates a thin layer of code that will be compiled along with the application. So, think of it like generating abstract classes that the developer needs to implement. So, this way, if the interface changes or you forget to apply the new types in some places, you will get an error in compile time.

So, the interface of a Native module is called a specification or spec for short. And specs can be written either in flow or TypeScript. And there are also dedicated types like float, double, or int32 that you should use instead of number.

So, CodeGen is used not only for Native modules, but also for Native components. It serves the same purpose, type safety, and single source of truth for the JS interface. So, it ensures type safety for props, commands, and events.

And finally, the core of the new architecture is Fabric, the new renderer. So, renderer is the part that translates React JS components into host platform views, like UI view on iOS. So, previously, the renderer used to use the bridge to communicate with Native, so it was asynchronous.

And now, it is exposed as a TurboModule and uses JSI. Also, previously, there had to be two separate implementations, one for Android and one for iOS. And now, the common logic is written in C++, which allows for better code reuse across platforms and also makes it easier to implement new platforms.

Fabric also introduces a completely different rendering pipeline, makes some changes to the threading model, and it comes with new event system and new rendering patterns. So, here's the part where I would explain how Fabric works in detail. But we don't have much time.

And also, this is not really interesting in some places. So, I've read the whole article on React Native blog, and these are just the most notable highlights that I want to share with you. So, the first highlight is render scenarios.

So, here's how a regular React render works. The update is triggered on the JS thread. It can be a state change or some timer or some interval.

And it is followed with a React render. Then React Native layouts the components using yoga and commits the new shadow tree and mounts the changes on the UI thread. And Fabric makes it also possible to run this whole pipeline on the UI thread in case of a high-priority event that UI needs to reflect.

Fabric also makes it possible to interrupt this pipeline. So, low-priority events trigger new renders. In case of a high-priority event, we run the whole pipeline on the UI thread and then follow up with a render on the JS thread.

It is also possible to commit C++ state updates, like changing the scroll offset of a scroll view without the render phase, because the C++ state is never exposed to JS. So, the second highlight are view optimizations, and I'm pretty proud of the slides that I will present right now. So, let's consider this example.

Here, we have four nested views, but only two of them affect layout. So, these views are not reflected in the final view hierarchy. Fabric just keeps them to minimize the number of native views.

You can disable this optimization by setting collapsible prop to false. Now, let's consider this example. There's another optimization called view reparenting, which also affects the native view hierarchy.

So, Fabric avoids deep trees, so the chain of views is mounted like this. You can also disable this optimization with one prop. And here's how it behaves on Fabric.

And finally, there's an optimization called view recycling. On the new architecture, on the old architecture, unmounted views were deallocated, and newly mounted views had to be allocated again. I told you.

So, on the new architecture, there is a recycle pool that stores references to native views like UI view to prevent frequent allocations and deallocations. So, when the view is unmounted, its state must be reset to default values. So, React Native calls a native method called prepare for recycle.

And then, when another instance of the component is mounted, React Native checks if there is any recycled instance in the pool and uses it. So, now, a little bit of history, because you might think that this is, like, leading edge technology, but it isn't, because Fabric is in development since 2018. It was announced by Eli in his talk in 2019.

And then, it was announced to the public in 2021. You could actually enable Fabric in your React Native app since 0.68. So, is there anyone who uses Fabric? Yes, Meta uses it internally in their apps.

So, I can share the details, but some apps are using Fabric for several years now. So, I'd like to reference this talk from App.js that Krzysztof and I presented two years ago. And during that talk, we mentioned that we started migrating our libraries to the new architecture, and, in fact, we did.

So, in early 2022, we released the very first versions of our libraries. In fact, the first library to support the new architecture was React Native screens. And then, we quickly followed up with gesture handler and reanimated.

So, it worked really well in our apps, like, in our example apps, but we had no real feedback from a production app. So, our goal was to migrate a true production app to the new architecture. So, after App.js in late 2022, an opportunity came to migrate their app to the new architecture, and Jakub Piasecki and Wojciech Lewicki were leading these efforts, and they had to pave their own way, because, to my best knowledge, no one else did it before. And spoiler alert, they did it. So, I'm glad to announce that last week, the new architecture finally hit the production on iOS, and we even wrote an official blog post. So, congratulations to Jakub and Wojciech.

So, the process was relatively straightforward. They started from enabling a flag. So, when you install your dependencies, you just add one environmental variable, and that's all.

And by the way, you can check if a fabric is enabled in the Metro console logs. But then you see this. So, unimplemented component something.

So, the app will generally work fine, but if there's some native component that hasn't been migrated yet, there will be a red rectangle. So, these are the native components that have not been migrated yet. So, they had to make a list of all native components used in the app, and the list of all the libraries that were not supporting fabric at the time, and they had to migrate all of them one by one.

So, here's a list of libraries that they ported, and it's not complete, because at some point, we just lost track of the count, and the app was doing active development, so there were, like, more features coming to the app, more libraries, so the process just wouldn't end, but hopefully it ended. So, the process was quite similar and repetitive, but some libraries had their, like, quirks, some issues that needed to be taken care of, and most of these issues were related to layout calculations or recycling. So, that's why I showed you the most notable highlights.

So, the third phase was QA and bug fixes. They have, like, really good QA team that found all of these issues, and it's in the works right now. So, probably, you're wondering, should I migrate?

So, yes. Yes, you should. The new architecture suffers from the chicken and egg problem, so, like, people are hesitant to adopting from people are hesitant from adopting it because there are too few applications that already use Fabric, and also that's the reason why the support is so, like, not good.

Sometimes, the support for, like, new architecture in some libraries might be missing, but the new architecture is the future of React Native. It's really, like, inevitable, so, also, the process right now, if you think how the React Native release crew does their job, they have to test both on iOS Android and Fabric, so there's many configurations to check. So, this process can't take that much time.

It can't last for too long. So, I guess that sometime in the future, the new architecture will become the default, and, in fact, it kind of did because the new architecture will be the default since the new architecture will be default in React Native 75. So, as for the, like, community libraries, there is still some support missing, so, Brent from Expo and the Expo team, they have prepared a spreadsheet of top 100, like, most popular libraries in React Native ecosystem.

They have sorted it by popularity, and they are working on they are, like, communicating, contacting the library maintainers, making sure that the libraries work. Also, Alexander Mikulski from the Expo team, he prepared a really cool CLI tool that reads your package JSON, scans all of the native dependencies, and checks one by one if it supports the new architecture or not yet. And, migrating doesn't need to be that difficult, because, since I believe React Native 72 or 73, there's also an incremental way of adopting it.

So, there's an interplayer which allows you to use old components in the new architecture, and you can enable it this way. So, there's a file called ReactNativeConfig.js, and you can just add two props for each platform separately. You just list the names of the native components, and it just works.

So, congratulations to the meta team for making it easier to migrate. So, you might think, what are the benefits of using the new architecture? So, these benefits come at, like, different levels of abstraction.

So, first, there are new capabilities. For instance, you can use on the new architecture, you can use concurrent features from React 18 and React 19. You can also use React suspense.

You can have multi-priority events, and also the synchronous measure that I've mentioned earlier. As for the code-based improvements, it's, like, there's more type safety. There's a shared C++ core which makes it easier to maintain, and also there's less sterilization in the process.

And for the user, there are also some UX improvements. Probably there will be a faster start-up of the application, because the modules, they can be initialized lazily, and also performance. It might be faster.

So, I was wondering what's the benefits in terms of performance, and found this great discussion by Samuel from meta, and there are some benchmarks. It has been measured on React Native 72. Right now, we have 74, so things might have changed.

And these are, like, synthetic benchmarks for 1500 and 5,000 components. So here's how it looks on Android. For view, a little bit faster.

For text, almost the same performance. And for image, quite good. And here's the iOS part.

So, views, like, notably faster. Text also notably faster. And image, well, quite good.

But new architecture wasn't meant to solve performance problems. It was meant to solve, like, remove some architectural-level limitations without affecting the performance too much, because, in most of the cases, as mentioned, we also run the performance of the apps, and, like, most of the cases, the problems are not in the native code, but in the React.js code. This is the main source of all performance issues in the applications.

So, there are also some things that I wanted to highlight here, like, next steps. So, the first thing is breaches mode. This, like, removes completely the bridge object from the code base.

There's also a thing called static deconfigs, which is also codenamed as Venice. And finally, web alignment. So, there's a lot of efforts at Meta from Ruben and others to make some changes to allow React Native more today, like web browser.

So, specifically, new event loop model, DOM traversal, and better conformance for styling. So, yeah, that's all. Thanks for having me.

### Mo
Thank you very much, Tomasz. Let's head over and get some Q&A started. Okay.

So, before we get started, I've been told that whilst I've been in the center of that stage walking around like a madman, that my head was not illuminated, so you guys were all seeing, like, from the bottom down up. So, let's just take this as headless React conf. Sorry, that's an awful joke.

All right. Cool. All right.

So, I do want to do something before we start. Is there anyone who is a native of Krakow here? Great.

Can you give me two random locations in Krakow? Okay. Second destination?

### Tomasz
You can't really verify my answers, do you? I can tell anything. Give me a route.

So, probably, I would go by tram, let's say, 22.

### Mo
Okay.

### Tomasz
I can't verify this, so you can just be BSing, and I will just accept it. And then, basically, any tram that goes south.

### Mo
There we go. The human city mapper. Great.

All right. Let's jump back into the actual Q&A. I'm sorry.

I get distracted very easily. All right. So, I want to start with the use case that you have, because I think there's a lot of theory around the new architecture, but it's great to see it being put into practice.

So, from a benefits perspective, with the Expensify app that your team helped migrate, what were noticeable benefits or goals that you had after the migration was done? So, what do you think it unlocked practically for the Expensify team to migrate over to the new architecture?

### Tomasz
I think that's too early to say, because the new architecture was enabled last week or two weeks ago. So, right now, there are some issues that need to be still resolved, and we are yet to see what are the capabilities. There are some, like, in terms of performance, I believe that the new features from React 18 and React 19 will make it easier to apply some optimizations on the JS layer of code.

So, we'll see how it goes. Maybe it's a topic for another talk.

### Mo
Yeah, maybe so. So, that probably leads to the next question, which was you've not measured performance yet before and after the migration.

### Tomasz
Not yet, but I'm wondering what are the metrics here. It's not, like, it's difficult to find one metric. We can use time to render.

This was the metric that Samuel from Meta was measuring. But I believe that there are, like, multiple metrics, and you've got to choose the right ones.

### Mo
Yeah, cool. One question. So, we'll play a little bit of a betting game here, okay?

If you were a betting man, which I don't know if you are or not, firstly, if you had to place a bet, which React Native version do you think will drop support for the old architecture?

### Tomasz
I can say I signed an NDA. Oh, you know this already. Perhaps.

### Mo
You can't just do that, man. Man. Surely that's a violation of your NDA in itself.

Anyone really wants to know the answer, you can always kidnap him and force it out of him. Let's play this betting game in another way. If you were a betting man and you had to place a bet, you've said that the default being the new architecture is in version 75.

When do you think version 75 will be released?

### Tomasz
I'd say, like, three months from now. Recently, there's, like, the releases of React Native are very frequent. And there's also, like, more commits in each release.

So, the release crew is doing, like, really good job. It's, like, really well organized. So, things are, like, things are going really good.

### Mo
Cool. Awesome. Bruno says it's not a question, but just congratulations and thank you for all the good work that you're doing.

So, just that shout out there. Thanks to the team. The Expensify changes that you folks did, I presume the libraries that you went through, you recommitted that back to the actual open source repo.

So, is that available for everyone, or is that just done on, like, patches of the libraries?

### Tomasz
Great question. So, it depends. Like, most of the libraries, they, like, the team submitted PRs to the original repositories, and the changes were merged and released without problems.

There are some libraries that were, like, unmaintained. So, probably the best idea here is to use, like, patch packages. Also, another alternative was to, like, just fork the library, but it doesn't make sense to, like, split the ecosystem.

So, it's better to have the changes perhaps as patches. Like, this works in Expensify. So, I believe that's the right approach.

### Mo
Cool. People obviously love FlatList so much. And so, have you seen any benefits to FlatList from the architecture?

### Tomasz
So, not yet, because the FlatList still works like it does on the older architecture, but there are some, like, new types of events. There's, like, a synchronous event that will trigger the render pipeline on the UI thread, and this is something that we really want to investigate, as after mentioned, maybe come up with, like, a different library for a list. There's many packages of lists for lists in React Native.

So, this is a definitely tough topic to work on. But I believe that we should investigate that. Like, let's see how it works on Fabric.

### Mo
Yeah. So, a practical question someone was wondering was when you're migrating from the old architecture to the new architecture, the errors that you see whilst you're upgrading, are they mainly showing at build time, or are they happening at runtime? Is it both?

Like, how is that kind of split, and what's the process look like practically?

### Tomasz
So, there should be, like, no errors in build time, assuming that the libraries do their job good, do their job well. For runtime errors, like, it depends. Like, definitely Fabric changes the rendering pipeline, so some things happen earlier, some things happen later than they used to.

So, like, for specific issues, there were some, like, issues related to view recycling, some props from, like, third-party libraries, they weren't reset. So, like, weird things were happening on the screen, basically. But once we found the root cause of the issue, it works well.

### Mo
Cool. And then one final question. Well, I'll reframe the question.

So, is React Strict DOM using some pieces of the new architecture, like Fabric? There are slightly different streams of work, albeit React Strict DOM has part of that RFC, which you mentioned, which was unifying things like the event loop and bringing them closer to the web API. So, let's go in that angle, and I wanted to ask you what you find exciting about some of the changes that are happening with the new event loop that's coming through and also the DOM traversal APIs that are coming through.

What do you think that will unlock for us as a community and as people that use React Native?

### Tomasz
I believe this will lead to more code reuse, just like Kadi said during the previous talk. Like, there's better possibilities for code reuse. There are some APIs that you cannot really use on React Native.

Like, okay, maybe we've had examples. But if React Native is close to the web, then it will be just better for the developers. Like one codebase, multiple platforms.

### Mo
Yeah, exactly. And we can reap the benefits of the very large React ecosystem as well.

### Tomasz
Exactly.

### Mo
Lovely to chat with you, Tomasz. Thank you for bearing with me as I asked you very stupid questions, and appreciate it. And a big round of applause for Tomasz.

### Tomasz
Thank you.