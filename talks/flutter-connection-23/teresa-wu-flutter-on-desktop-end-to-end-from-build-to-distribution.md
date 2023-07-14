---
slug: "/talks/flutter-connection-23/teresa-wu-flutter-on-desktop-end-to-end-from-build-to-distribution"
date: 2023-06-02
title: "Flutter on Desktop: End to End From Build to Distribution"
author: "Teresa Wu"
video: U5_FbCIqwwY
thumbnail: thumbnails/teresa.png
slides:
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

[MUSIC PLAYING]

Welcome to my talk, and welcome to the event.

And thanks for having me.

So sorry, I'm going to stay a bit closer to here, because it was unexpected.

I should never touch it.

I can talk about it without having a black screen.

But you probably won't like it.

Okay.

Great.

I promise I'm not going to touch that anymore.

My name is Teresa.

I work for JPMorgan as a software engineer.

And I also code a lot with Flutter outside of my existing project.

And I'm also a Google GDE for Flutter and Dart.

I'm based in London.

And it's really nice to come here in Paris.

So I will talk about Flutter on desktop today.

And I have to admit for myself, I actually haven't released a very shining, polished

Flutter desktop application yet.

So I've been trying Flutter for desktop for a while.

And what I will present today is a whole flow of how you can set up the environment of Flutter on desktop, talk about why we need desktop application and why Flutter is better for this environment, and then go on to talk about some UI elements and talk about release as well.

So hopefully you have a very nice 30 minutes journey with me.

Let's begin.

A little bit background, not the entire Flutter journey, because I'm sure you are aware of it.

But for desktop, it was started all from the year of 2019.

That first desktop was actually mentioned.

And through the year, we've seen the alpha release of Mac OS and Linux.

And then coming the next year, we have support for Windows as well.

So as of today, we're seeing the release, the stable release of Windows, Mac OS, and Linux.

And before we go into talk about the tech of setup the desktop environment, look at some of the data, right?

I mean, as of today, if you think about building application on multi-platform, there's more than just those two frameworks.

But those are probably just the one that is mentioned quite often.

The reason is for Kotlin Multiplatform, it was a great framework.

But it doesn't solve the issue you need to solve on a UI level just yet.

So if you are building a cross-platform application on Android and iOS, I mean, you can use either Flutter or ReaLative, right?

I'm not saying which one is good.

Depends on what the project requirements are.

But if you're thinking of just more than mobile application, mobile platform.

Then Flutter has support natively for web, right?

And now it goes into Windows, Mac OS, and Linux, compared to ReaLative.

At the moment, the support for those platforms is either by community or by partner.

Well, unfortunately, it doesn't support Linux just yet.

So right, we actually use Flutter

And now it goes to web with WebAssembly.

But why do we need desktop application?

So, it depends on how often you use desktop application natively. Or you probably forgot about all these beautiful applications we have on desktop. But it's actually similar to what we use for mobile.

For desktop, you can actually access the application data offline, and it's safer to store data.

And in that case, you have a better performance.

In that case, you have better performance.

And again, it's native.

So comparing to web, web has the ability to self-update itself without going through the App Store.

And it's accessible anywhere.

And again, you don't need to install it.

And it's very lighter on resources.

But if we think about desktop, there were so many popular apps we produced on daily basis.

If, for example, as software engineer,

We have IDE.

I mean, there's also online sharing tools now with web tools, but for production application, my first choice is always local, right?

On desktop.

So things I will use on daily basis, right?

Emails, Slack, Zoom, some editors, Spotify, right?

Who doesn't listen to music when you code?

So now we're going to jump in to talk about setups.

And this is a bit different from setting up Flutter for web and for mobile development.

For desktop, if you are using Flutter, you might want to support more than one platform.

That's the beauty of using Flutter.

In that case, you need to think about the three platforms, right, or maybe two.

So we go through Mac, Windows, and Linux.

So before we go into setup, setup,

If you have, for example, using Flutter already, you probably have Flutter SDK installed.

Run a very quick Flutter doctor to see what is missing.

Now we set up Mac OS for Flutter.

And if you are not familiar with Mac OS, and if it is first time using it-- so for example, if you are a Windows user-- so going to Mac OS, of course, you have to have the computer ready.

And there are some minimum requirements.

And the stable version of the OS system is always online.

Check what is the latest version.

And I would always suggest if it's a production project, go with a stable version.

But for your side project, go with any version you like.

Have SDK installed, right.

And then have at least minimum 2.8 gigabyte desk space.

But if you actually just have, for example, 3 gig,

You probably need to have a better solution.

OK, set up the project on Mac OS is actually very, very straightforward.

Probably because myself is a Mac user, so I found this process a bit easier.

So have SDK ready, right?

Install CocoaPods if you are first time using Mac OS to build Flutter.

And once you're done installing the dependencies,

Then very quickly in five minutes, you create the first Hello World project.

And you just call this command to run macOS.

And you should have your first macOS desktop running on your computer.

So very quick and a forward process in my opinion.

And if it's the first time you use Mac or maybe Mac for desktop, you might see this

This folder coming up in your project, what it means, right?

Underneath the macOS folder, there's some subfolders, right?

The flatter one is for some files you generated, but you probably don't want to keep them.

And some platform-specific code, some source code, and dependencies, right?

You don't have to actually manually manage them, but you will see them in your folder.

That's for everything you need for macOS.

So, moving on from Mac, right?

We've done Mac already, which is ticked.

Great.

Okay.

Linux.

I'm not sure how many of you are familiar with Linux or use Linux daily for your development environment.

If you don't mind, raise your hand.

Right.

Oh, nice.

We have actually a few experts here.

So for those who are not -- who don't use Linux daily, again, similar to Mac, right?

Check your system.

So it meets the minimum requirement.

Have the stable version of the release of SDK.

And you might need some other tools which you're probably not that familiar with compared to Mac, which is okay.

But again, for myself, I'm a Mac user.

And setting up Flutter on Linux take me longer.

But it's still quite straightforward.

So again, download SDK, run Flutter doctor.

And if it's the first time you use it, use lots of red cross.

Again, it's fine.

That means we need to install those tools one by one.

So I will talk a bit more about what those tools are.

But let's assume we have followed the advice, right?

We install the tools one by one.

And we need to install Android Studio IDE or the IDE of your choice.

But say here we use Android Studio IDE or IntelliJ or VS Code, right?

And after you've done all the step, we create our application, run the app from the command line or somewhere, you should then see the Flutter desktop uploaded in your Linux system.

Again, it should be quite straightforward process.

So this is a list of some of the tools

I was mentioning in the previous slides when I run Flutter Doctor.

Again, similar to Mac OS, you will have a folder now created in your Flutter project, which is Linux.

And again, it contains some of the tools and the files, right?

And because Linux uses C++, then you have the tooling infrastructure for the C family.

And you have the cross-platform tool for building, testing, and the packaging.

And there's some UI elements and the binding tools as well.

And there's some tools for comparison and decompression, right?

You don't have to understand everything in detail to make your desktop application,

But it's just nice to have the knowledge of what they are for.

And hopefully, you don't have to manage them yourself.

So now, we ticked Linux and Mac OS, right?

But if we are building a desktop application on cross-platforms, Windows is probably one of the frameworks that we never want to miss.

And do we have any Windows user here?

No?

Surprising.

I didn't expect this.

Okay.

Okay.

So we all like similar new choices.

Right.

So for Windows, I have to admit it took me longer, slightly longer to set up because

The system is actually quite different from Linux and MacOS, which are Unix-based.

So again, similar issue, right?

Once you have the Windows machine, check the minimum requirements, have the SDK ready.

I always go with the stable version, right?

And I'm sure this one is just like the minimum requirements.

If you have, like, your machine, it should be fine.

And you should have met all the needed setups.

So for Windows, the requirements is similarish.

Now SDK set up the environment.

But you need more than one IDE here.

You need Android IDE.

Again, any IDE of your choice for Flutter.

And you need to also install the virtual studio.

Not VS Code.

Virtual studio.

You need to enable the settings here for desktop development.

With C++ for this IDE.

So once you've done this process, right?

Then you should be able to create your project, run Windows, and you should see your Windows desktop uploaded.

And the reason I spend a bit more time is actually to set up some of the IDs and some of the environment, system environment, and also to get a Windows machine.

But again, it's actually -- the setting up doesn't take that much time.

I mean, if you have like awakened and don't know what to do, I have a Saturday, you should have two or three hours, you should see your app running. those three platforms, for sure.

But you do need the three machines.

Right.

Of course, right?

If we are thinking of using Flutter for desktop, that means we probably most likely have our Flutter project already, either on mobile or on web, or on both.

So I don't want to actually create a new project on those environments.

How do I transfer my existing project to Flutter on desktop?

This was taken care of, and of course, by design, by default.

You can actually convert your existing project, just adding a support to desktop very, very easily, running this command.

And straight away, you will have those three packages ready for you in your project, supporting those three systems.

So you don't have to always start from scratch.

And in terms of testing, again, because I haven't built a very polished production-ready desktop application, there might be some different requirements on the end-to-end test, the UI test.

But in terms of the testing we need as for basic unit tests and some of the widget tests that wherever you can find from the Flutter library, those are, again, the same as you would use them for your mobile application.

So running them for desktop is similar as you would do in any other environment.

This is one with the beauty of using tools like Flutter for cross-platform.

So you do minimum work so that you have support for all the platforms that you need.

So now we have our machine.

We set up our environment.

We need to start coding, right?

And again, the advantage of using Flutter is that you don't have to redo your code again to have your application running in the new environment, in the new platform.

But there might be some twists or some changes you have to think about to make your application look native as possible for desktop. Some of the things are a bit different on desktop environment. For example, the keyboard, the mouse, right? So the keyboard, so for web application and for mobile, we can use gestures, we can swipe, we can actually tap or click. For desktop, we have the extra additional interactions with user

And this, again, is taken care of as well in Flutter, naturally.

So the mouse input works the same as gesture detector, which we would normally use for existing mobile application.

For basic keyboard, right, so you have options either to handle the action key by key by using the actual key.

For example, key K or key--

So you can create a group of them for shortcuts, right?

You can group your keys together and provide the functions for them as shortcuts.

So those are, again, taken care of, so you can create your own set and your collections of keys.

And another thing which will -- something that we are working on is the key-to-key.

Another thing which will -- something that we need to think about on desktop is data storage.

It's 90% similar-ish than how we store data locally on mobile device.

With something slightly different, right?

In terms of location, and for Android, we have shared preferences, right?

But for Linux and the MacOS and the Windows, where we store things a bit different.

But the API is the same.

Location-wise, they're different underneath the hood.

But again, this is something that you don't have to interact separately as using a framework like Flutter, because this one is provided by the Flutter framework with the same API.

What does it mean is if you want to store-- if you want to access data locally on the computer device,

We can use either the shared preferences to store some keys and the values.

And if you want to store something more secure in a way that--

I'm not saying you need to store your password, but some sensible user data, you can use secure storage just to create your options and then store them as what we do for other platforms.

Right?

Right.

About secure storage, there's a bit-- yeah, some extra requirements for those platforms, right?

So if you run into issues, it doesn't mean you have bugs in your code.

It might be just different requirements for a different system.

And for example, for Mac OS, you need

So, if you run into issues, right, of your code that you couldn't use those functions, check if they are supported at the moment.

Or it could be supported already.

But keep checking the new release from the team.

Again, if we are thinking of not just storing some key values, but storing file, it's also supported on desktop environment.

You can store a large file with a file system.

And the list shows you what is available on each platform.

And of course, on Android and iOS, you have quite good support.

But when it goes to desktop at the moment, there are some storage that isn't available at the moment, like external storage, some caching, and some of the application libraries.

But if you want to just store a file, you can always go with a temporary file system or downloads, for example.

Those are available.

So again, if you run into issues with your code, it might not be your code, or maybe you don't have a bug.

It just -- those API isn't available just yet.

Third thing for this is the screen at the UI level.

And the responsible design is, again, the same for desktop as we use for mobile and for web.

So we use the same library.

You should have responsible design for your UI on desktop.

And a few months ago, in Flutter forward, we heard the mention of multiple windows.

This isn't just some feature we build for desktop.

But once it becomes available, it will go to desktop as well.

What it means is when you have your application running, you can actually have multiple windows.

They can work in a way that it's separated more async.

But they also can sync with each other as well.

This is a very powerful function for desktop applications.

I'm waiting for the news about it.

At the moment, it's still a work in progress.

So we don't have -- we haven't tried it yet.

But yeah, it's waiting for announcement from this feature.

So after myself trying out building application on desktop, right?

And I'm thinking that could be supported as a developer, right?

So the major difference of using desktop with Flutter is the machine.

Because if I use Flutter for mobile or for web, I just need one computer, right?

MacOS.

Then I can build for Android, for iOS.

And for any browsers I want to support.

So that's great.

But when it comes to desktop, if I'm a startup company or I'm a solo developer, I'm not -- I don't have a polished application at the moment.

It's actually quite difficult to actually have three machines for myself to use.

I can either go set up my virtual machine and, again, the development experience on virtual machine isn't as great as if you have a machine locally.

So maybe in the future, right, hopefully we should have either some support for emulator for at least for testing for desktop in our development.

Or maybe if I go to Google Cloud, right, having some pre-made virtual machine I can just load which comes with desktop installed.

So I don't have to load it myself every time I build it and have to terminate the machine as well.

So I hope this can be supported for developers using Flutter from the Google Cloud family, hopefully.

And more documentation and having support for the design system as well, because each of the desktop environment has its own unique design system.

And it's quite mature now for iOS and Android.

It comes naturally of Material Design and Kubernetes.

But this was something we don't see much yet for desktop.

And it could be a blocker for production-ready applications.

And there are quite a lot of very nice, shining desktop applications right now actually released in Flutter.

And this one, I don't work for them.

I don't get commission from them.

I'm just mentioning because I think this one is actually a good example of a Flutter desktop application. This was recently released on Mac OS and Windows. Not on Linux just yet, if I'm correct. I could be wrong. If you want to give it -- if you want to try it out, I mean, because everyone here are Mac users and some of them are Linux users, no Windows users. So if you have a Mac machine, you can give it a quick try. The desktop application works almost the same as the one for the web app, which is great.

Right.

So, we talked about setting up the environment.

I'm not sure how I'm doing with the time, but I assume I do still have a few minutes.

One, two.

Okay.

Okay.

Let's go.

So you can either distribute the application manually, means that you have to set up your developer account, create your bundle ID, make the app release right on Mac system.

And same for Linux, right?

Linux, you have ways to manage applications through the Linux store.

You need to pack it, sign it, and upload it and manage yourself.

So for Windows, it's a bit like Android in a way that you can either distribute Windows desktop application via the store and the store manage all the lifecycle for you. or you can distribute it on your own website.

And you manage the lifecycle yourself.

So you have different options for Windows application.

But if you don't want to do this manually, which takes a lot of time, you can also use a SaaS solution.

And those companies that you see in the slides, they have, at the moment, support for Flutter desktop.

Again, I don't work for them.

I don't get commission for them.

This is like some of the things I found which are super, super helpful for your application if it's production ready.

So you don't have to manage the release manually.

And to give a very quick example, the reason I'm using Bitrise is I used Bitrise before in my other project.

I'm very familiar with its UI.

But every other tools I mentioned here should have a similar workflow of how you can set

So, you can use this to set up your CID for Flutter on desktop.

So, the reason you can use this is that it's accessible by everyone from your team. And you have lots of ready-made functions. You can just grab and you can just drag and use them so you don't have to build them yourself. So, it's super handy

So, my last slides.

Do I use Flutter or not for desktop?

According to my friend, Majid, he will tell you it depends.

But it's true, it depends.

Think about your situation, right?

Do I have existing mobile app already in Flutter?

And does this -- do I want to rewrite it or do I want to just quickly launch the existing application to production, right?

Or is this the first time building my application on desktop?

And I won't distribute this application anywhere else.

It's just desktop only application.

So think about those conditions.

Think about resources you have in your team.

Think about, like, the time you want to release, right?

All those things matter, right?

Not just the framework itself.

And that's the end of my talk.

Thank you.

[ Applause ]

[APPLAUSE]

Thank you very much, Teresa.

I have a-- don't forget to send your questions.

I have a first question myself.

How do you handle distribution for a staging environment?

I know for mobile development, there are some distribution platform like App Center or Firebase App

Distribution.

Is there something similar for desktop applications?

As I was saying, I haven't worked on a production-ready desktop for commercial use yet.

But this is depending on the functions and the support from each store.

This is not something you actually build in Flutter.

That's different from API level of testing.

But I'm sure you have support for those different environments.

It will be quite surprising if you just launch your product to production straight away.

You definitely have the staging environment, develop environment, and either a pre-release environment for sure.

Thank you.

I had a question about the libraries you can find on Pub/Dev.

Do you think there are enough to guarantee like a kind of a smooth list or smooth as possible workflow?

Or just, I mean, just lots of missing pieces?

If you're comparing Flutter on desktop to the support for Flutter for mobile, in terms of the function by the framework, it has a lot of mature UI element components already.

But it does actually have less support from the marketplace.

Like, it definitely has less packages and libraries you can use as of today.

But hey, then you can be the first one building it.

Here's a question from Toast.

Are you aware if flavors are supported by Mac OS?

Because last time they tried, they encountered issues.

So when I first tried out desktop application, flavor was one of the things that I found is not there yet.

But I think I checked recently that you have the packages supporting Flavor now for desktop.

I don't remember who published it.

But when I first tried it, when they launched, it's not.

But as of today, I think there is packages already.

Good news.

Awesome.

Do you know if the Mac OS Flutter uses the Catalyst API?

So there is some kind of compatibility with the iOS libraries integrated into the bundle?

I'm not sure about it.

I can't give you a certain answer for that.

All right.

I think that's all.

Yeah, that's it for me.

Thank you very much.

Thank you.

Thank you for having me.

Thank you, Teresa.

Thank you.
