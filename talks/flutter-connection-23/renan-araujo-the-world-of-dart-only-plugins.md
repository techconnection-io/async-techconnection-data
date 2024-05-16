---
slug: /talks/flutter-connection-23/renan-araujo-the-world-of-dart-only-plugins
date: 2023-06-02T00:00:00.000Z
title: The World of Dart-Only Plugins
author:
  - Renan Araujo
video: C1AgQMLXPDE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/C1AgQMLXPDE.jpg
slides: null
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

There we go.

That's all my French.

Sorry for that.

OK, so yeah, let's talk about the world of Dart-only plugins.

I think I had a different idea for a title, but it was going to be too big.

But it's in the slides.

Anyway.

OK, non-important stuff.

My name is Leonardo Ujo.

I am from Brazil.

But recently I moved to Portugal.

So I live in Portugal, in the city of Porto.

I work at Variable Ventures.

It's a consultancy company in the US, specifically focused on Flutter.

I work as an OSS engineer.

So this means I maintain open source packages and tooling that we have, all of them around Flutter and Dart.

And also, I am a OSS contributor in the collective-- it's not a company or anything like that, but it's a collective of folks that love Flutter.

It's called Bluefire.

And among of-- hello, Bluefire.

There's someone else from Bluefire there.

And among the packages that we maintain, there's Flame, the Flame engine, which

And we're going to have a talk at the end of the day today here with Lucas.

OK.

So, OK.

Important stuff now.

We're going to talk about something that has been living in my head and been free for a couple of months now.

And, OK, so as a Flutter developer, when you talk about accessing native features, there's just mostly one way you think about that you can have access to those things.

And those are the method channels, the usual way of building plugins.

But recent developments in Dart allows us to have access to major APIs in a different way.

So I'm going to just try to give a fast sneak peek on it, because it's an extensive topic, the FFI.

So let's go for a quick sneak peek and hopefully an example.

All right, so first and foremost, let's look into how plugins are built, what's the structure of Flutter plugins today.

So to do that, we have also to understand the structure of a Flutter application.

So every Flutter application that we write has this structure that here we are going to represent as a bunch of rectangles.

That's a fun way to represent things.

Actually, this diagram you can find in the actual Flutter documentation.

It's anatomy of an app.

I really recommend the documentation.

It's pretty fun.

OK, so when we talk about writing stuff, everything that we write, state management, all the widgets that we write, the packages that we use, the Dart package that we use, they're all in this first layer that we call the everything we write.

It's the actual app that we write, everything under lib.

After that, below that, we have the Flutter framework.

That's the Dart part of Flutter that sustain whatever you do, so material, all the widgets,

API, all the gesture recognizers.

So everything under /flutter on GitHub, it's on the framework.

And then sustaining the framework, we have-- oops, sorry.

That's the problem of Keynote.

There is the Flutter engine.

OK, so the Flutter engine is mostly C++.

So it's where there's the core APIs for Flutter, things like the graphics core or text composition, for example.

And also, there is an API that we access sometimes.

If you work a lot of the canvas, there's the Dart UI that comes from the engine.

So mostly C++.

And then there's Embedder.

This part is the thing that connects Flutter to the platform.

So this is where we have access to the platform's gesture engine, for example.

So yeah.

So this is the embedder.

It's specific for the platform.

So for example, on iOS and Darwin, actually, it's Objective-C. And Windows, for example, is C++.

And then we have something else that we have access to.

It's actually everything under the platform directories.

So under Android, under iOS, there's the runner application.

So this is the actual thing that we will compile and send to the store.

So we call the runner.

It's also written the platform code.

So yeah, that's pretty much how a Flutter application works.

So the two parts that we have access are these two blocks of code, the top one and the bottom one.

And when we want to write a bridge between these two parts, we have something that we call the method event channels that we can, from the Dart side, to call native things that we can write the counterparts in the runner.

Plugins are a way to modularize this thing.

So plugins are usually part Dart and part native code.

And the Flutter tool takes care of putting

And this is a Dart package.

So, yeah, this is how a plugin works.

Normal plugins work.

Today I want to show how different it is if you go for a

Dart only thing.

So, a Dart only plugin, basically, you write like this.

This is a France flag. I tried to do some kind of homage here.

So, there is the plugin part.

And this is the Dart package.

And then we have the plugin part, which is where you write the functionality that we want to write.

So, it's always related to the feature of our package.

And then we call -- what we call bindings.

So, the native API. So, this is still Dart 2.

And it's mostly -- most cases generated using either the FFI gen tooling. It's a package that they're there.

And then, you can use the package to generate the bindings.

And then, you can use the package to generate the bindings.

And then, you can use the package to generate the bindings.

And then, you can use the package to generate the bindings.

And then, you can use the package to generate the bindings.

And then, you can use the package to generate the bindings.

And then, you can use the package to generate the bindings.

And this leaves in the registry in the operating system.

So yeah.

So basically, this is how it works.

You have the plugin package that we isolate the functionality.

And we call the bindings.

And the native libraries are in the operating system.

So it's totally independent of Flutter.

It's an actual Dart package.

So most packages that are written like this can be used on Dart CLIs, for example.

So it's sort of independent.

And yeah, some more differences-- calls are totally sync.

And since they are generated, the APIs are generated, they are somewhat type safe.

So type safe calls, they're sync.

There is no dependencies on Flutter.

And yeah, in packages, that depends exclusively on this.

You don't need to have any setup when you install the package.

Just install the package and start using.

OK, so let's go for an example.

So let's pray for the gods of live code today.

It's actually not code.

I'm not going to be coding here.

It would be crazy in a lightning talk.

Just want to show something.

So this is an application I wrote.

So this is just a text field, like text field, material, stuff, and some buttons.

So a basic Flutter app.

But the thing here is we can write anything.

I'm going to write this text here.

And I copy.

And this copies with formatting.

So I copy with the HTML format.

And I can go to some document.

In this case, I'm on some document.

And paste here.

And we will paste with the same formatting that I copied here, basically.

And this works in both MyCode and Windows.

So let's look a little bit into the code here.

So I isolated everything under this packages directory.

So I wrote in a way that looks like a plugin that's federated.

If you know what the federated plugin in Flutter is, it will be-- you recognize here some patterns.

So the front-facing package that we have is only this function that we just, by platform, we select the correct implementation.

So we have implementation for Windows.

And another one from Mac OS.

Sorry, Linux folks.

OK, so for Windows, for example, this is what FFI code looks like.

Looks pretty much close to how objectives see.

So if you ever wrote something that puts anything in the clipboard on Windows, this is the basic boilerplate.

We allocate memory, we lock memory, we write stuff. and the location and the memory, then we open the clipboard, write to the clipboard, close the clipboard, free the memory.

That's it.

We control memory allocation all the time.

But this, most importantly, it's all Dart.

But at the same time, it's kind of easy.

These classes are all the actual interfaces of C++ classes that lives in the Windows 32 package.

I guess this is in the -- specifically in the user 32 framework on Windows 32.

So yeah, this is how we write -- how we read from the clipboard.

And then we put everything in a common interface that's implemented by both macOS and Windows.

So let's look into the macOS implementation.

So if you ever wrote anything to the clipboard on Mac OS, we're going to recognize.

And even if you wrote objectives in your lifetime, we're going to recognize some elements now.

Here we have bindings to the actual EMS passport class that lives on the app kit.

Actually, Cucur.

And yeah, we get the general clipboard here.

Passport, sorry.

And yeah, we have methods writing the clipboard on Mac OS

And it's pretty more simple.

You don't need to allocate memory or anything.

But still, you have setString for type.

And you have support for the actual types here.

So we can put all of these formats on the Clipboard on my class.

And we have the actual bindings here.

And if we look back into the NSPassport class,

And it actually -- oof.

This file is so big.

NSPassport.

NSPassport.

Come on.

It's a class.

Here.

Extend NSObject.

This is kind of crazy.

And it's Dart.

And this bindings, we don't have yet.

Something like package window 32 for macOS.

So I had to generate a package.

And I'm going to show you how to do it.

So, I had to generate my own bindings here.

So, I put this in this package.

That is basically uses the FFI gem.

So, I'm going to show a little bit of the configuration here that I use.

This we use a header file in the system to generate the bindings.

And then the package loads the dynamic library from a di lib.

So, this is on Windows is the DLLs.

On Linux is the SO files.

And this is a dilib.

We load in runtime.

And then we have the AppKit ready to use.

Okay.

So, yeah.

That's pretty much the example.

And then, okay.

And the Flutter side of things.

We have the HTML, WCOP, and it puts these tags, italic, and bold.

That's pretty much it for the example.

All right, so we have some drawbacks.

First, there are some severe multi-threading limitations when it's about Mac OS and generating

And you can see that there's a lot of different APIs that are available.

And you can see that there's a lot of different APIs that are available.

And you can see that there's a lot of different APIs that are available.

And you can see that there's a lot of different APIs that are available.

And you can see that there's a lot of different APIs that are available.

And you can see that there's a lot of different APIs that are

And that's pretty limiting for some APIs, for some specific frameworks, for example, game controller, which was my initial intention to show off today.

So yeah, this kind of stuff is limiting.

But there are use cases.

There are passwords, sound, for example, those things work.

And okay.

There's some ways you can load dynamic libraries.

And the dynamic library is open.

You load the library in runtime.

And it's unclear how Apple will treat your app if you submit your app using this.

You can use dynamic library process because some frameworks are packaged directly to the IPA. So, those things are available already in build time.

So, you don't need to call open, but

And it's not clear how Apple will deal with that, too.

Okay.

And there are some other use cases coming on.

There is I think a highlight is the JNI gen.

JNI gen is a way of generating bindings to the JNI, which is the Java native interface.

Basically, it's just like this.

But for Java-based operating systems.

For example, Android.

So there's a nice video about this from Google I/O.

And yeah, there's more stuff.

I put everything in the link here.

And this example is also open source on my GitHub.

So yeah.

That's pretty much it.

We have time for questions.

I guess.

[ Applause ]

[APPLAUSE]

I start with a very important question.

How can you actually write Objective-C code without square brackets?

I mean--

[LAUGHTER]

Yeah, I mean, this bind is the fun part of this.

We don't need to actually write those things.

They were generated by FFIGen.

So these header files, they contain the interfaces and the methods that we can call.

And then the FFIGen creates the Dart versions of these APIs.

Of course, in some cases, for example, we just saw on the Windows implementation, you still have to care about all the memory allocation stuff.

So it's very sensitive, especially when you use the clipboard thing.

If you don't open the clipboard after you write on it, it will be closed for all programs.

So it's pretty sensitive in that part.

I guess that's kind of a drawback, too, this implementation.

But it's still Dart.

So I have another question, Raven.

I saw that there are those prefix NS, NS window, and on the old Objective-C object.

How would naming conflicts would be handled if you have some classes named the same between Objective-C and Dart?

How does it work?

Yeah, this generated code now lives in the one file, specifically in that generation there, which is pretty big.

So the NS stuff are all,

I think the FFHM manages name conflicts by itself.

So you have, I could show there, there's NS object one, NS object two.

So the internal parts, they increment names to avoid name conflicts there.

But because everything is inside one Dart file, it's isolated to that library.

So if you are importing two different files with the same name, you just use the show or hide syntax.

Just like any Dart code.

Yeah.

> > We have a question from Alois.

How much bindings affect bundle size?

And there is any sort of tree shaking for that?

Yeah, you can optimize how you generate the things by passing some options.

So you can either exclude everything and include only the interface that we want and the dependencies of it.

So it kind of is a tree shaking in the generating time.

And also Dart has tree shaking compiling.

So from my trials, it doesn't affect that much.

It's just also use something like, for example, MS Passport inside of its implementation depends on a lot of classes.

So it's not only the classes that you use, but the dependencies of that class.

And that can increase depending on your use case.

But it's -- in the end, it's not that huge.

The biggest problem in this case, it's not the case that this example that we're using, libraries that in the operating system you can ship the dynamic libraries with the application. In this case, AppKit, the dynamic library is always shipped if you're using or not this kind of implementation. So if you are creating your dynamic library that will go to your bundle. Yeah. We have another

Another question from Mathieu.

Can FFI be used to create a plugin for Cocoa pod library, not already included in Flutter?

Yeah, I think that's the case that we just showed here.

Actually, in S Passport, originally in Cocoa.

So we are getting from the app key to header.

Yeah, so yeah, sure.

Yeah, it's pretty useful, I guess, in that case.

And what about memory?

If you did some iOS, you know that Objective-C has a very old-fashioned way to handle memory.

Is that actually handled well by Dart, who actually holds strong references to NSObjects?

- Yeah, it's still, the bindings for Objective-C, this is still something preview, I forgot to mention that, for Windows 32, there's already a package and there are already people using that in production.

But for Objective-C, it is still in development.

So this is kind of a sneaky peek into the future.

And memory allocation and memory management is still the things that we're still trying to figure out in some aspects.

But from my use cases there,

I couldn't find any kind of memory leak after several trials.

So yeah, I don't think it's something

It's ready now for production by any means, but it's pretty close.

All right, I think that's it. Perfect. So thank you very much.

This closes also the first part of talks for this morning.

And so you will be able to enjoy a coffee break until 11.20.

So like 20 minutes for taking a break and so see you later.

Thank you.

Thank you, Renan.
