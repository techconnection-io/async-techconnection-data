---
slug: "/talks/react-native-connection-23/cedric-van-putten-debugging-should-be-easier"
date: 2023-06-01
title: "Debugging Should Be Easier"
author: "Cedric van Putten"
video: eWY7rHo_94U
thumbnail: thumbnails/cedric.png
slides:
tags: []
year: 2023
conference: react-native-connection
edition: 2023
allow_ads: false
---

My name is Cedric van Putten.

I'm a software engineer at Expo, and I want to talk a bit about something that you never should do, like that thing there.

So why do I want to talk about debugging?

During the React Native survey of 2022, you all complained that the biggest pain point in React Native was upgrading.

Luckily, we solved that kind of with Expo, conflict plugins, and pre-build.

But the second one was debugging.

Now, maybe we're not really sure, or I wasn't really sure why that was.

So I started dogfooding, and I created this small, simple, little app.

It's a simple to-do app where I try to reverse the order of the to-dos from latest to oldest, and then scroll all the way down.

Now, that didn't go so well.

At first, it worked fine.

But at some point, it crashed.

And after some really dark hours and a lot of tears later, I fully agree that debugging should indeed be easier.

So let's go together through the current state of debugging in React Native.

Now, the first one should be very similar or very familiar with anybody who has used React Native for some time.

The debug.js remotely is a mode to enable on your device that basically moves the whole JavaScript runtime execution to your computer.

Now, this is great because you can actually use your browser to debug certain things.

What is not so great is the implementation of it, where if all the communication between the native layer and the JavaScript layer now has a delay, because it has to go over the network, it could make your app very unusable.

And some of the issues you couldn't even find, like network race conditions, for example.

So that's not really an option for us here.

Let's check what else is available.

Tools like Xcode and Android Studio, like the actual native tooling, can give you very good insights in things like the native layers, like what is being rendered where.

It can help you track performance issues.

And a visualization like this is actually very close to impossible to do with just JavaScript tooling.

Something that isn't super great of the native tooling is the JavaScript side.

So in here, we can see that we have a blob of stack traces caused by an exception somewhere in our code.

But we are not machines, right?

So it's very hard to actually read this.

What is left for us?

Well, Flipper gives us some impressive tooling.

It doesn't really help us in the use case that I run into, where somewhere in the code an exception is being thrown.

And as you could see, we get the exact same stack trace blob, but colored red this time, which is also not really helpful.

So all of these tooling right now have their pros and cons.

Debug.js remotely is not really possible anymore with Hermes and synchronous communication with JSI.

So that's not an option.

Native tooling works great, but not for our use case.

We don't want to visualize the native layers, we want to track the error that's coming from JavaScript.

And then there is Flipper.

Now, to keep it civil, I don't want to spend too much time on Flipper.

But if you want to read all about it,

I would encourage you to engage in React Native Discussions and Proposal 641.

In there, there are some pros and cons of Flipper explained and a possible new direction.

So I would definitely encourage you to just read that.

So let's take a step back from debugging React Native, because it clearly is missing something.

And let's take a step back to the React world.

Like, how are they debugging?

They also have to debug certain JavaScript side issues.

So how do they do it?

And for that, we just have to take a look at web.

Now, on web, you have browsers instead of apps, right?

So you can pretty much right-click anywhere on a page, at any page, and select the inspect.

This will open up the network inspector, which consists of many things.

You can execute code through the console.

You can check the source of any website.

You can even check the network inspector to see what kind of requests they are making.

So that's pretty impressive.

And I'm kind of jealous on it, actually.

It is also not just supported by one browser.

It's literally all of them.

It's not even browsers.

Node.js also works with this, although in limited form.

And it's not just the inspector itself.

There are very specific tooling that you can use using the same system to connect to your app or to your website.

So how can we leverage this inspector protocol,

I like to call it, into React Native.

Now for that, we actually have to take a closer look at how Node.js is doing it, since they are not a browser, but still using the debugging workflow of the inspector.

And for that, they actually implement it right inside the engine.

And luckily for us, Hermes is doing the same thing.

So with plain React Native, we can actually use it right now.

So all you need to do is go to whatever browser you're using, go to the inspect page, add a new target discovery.

In this case, it's just Metro.

Then from there, we can connect our app to it, and we get multiple remote targets.

Each of them is inspectable, and once you click it, we have the debugger.

Now unfortunately, this is not fully complete or not a full replacement for Flipper.

There are things missing here, namely the network inspector.

So at Expo, we thought, how can we make this better?

Or can we make this a true different way?

And for this, I can show you some pre-recorded videos.

But I think it's more fun to just play with it.

So over here, I have my very simple app.

I will just start it in offline mode real quick.

There we go.

And as you can see, I have a lot of to-dos.

So all the latest to-dos is actually listed on the bottom.

So let's just scroll to the bottom every time when I open this screen.

Now, when I reload this, there is an issue.

And this issue is actually caused by something related to the flat list.

Now, I'm not going to spoil it yet.

For this, we're just going to try and capture the error.

So how do I open the debugger with Expo?

We just press J. And there we go.

Right now, we have pretty much access to our whole code base, the actual source as well, where we can just figure out what's going on.

And since I'm using Expo Router, I have to enable a couple of things, because behind this lockbox error, we actually have the Expo Router catch all exception page.

So let's pause on code exceptions as well, and then just retry.

Now, in this case, it's actually worked, which is interesting because that's part of the bug.

Now, this actually only was an issue for new users.

And it was related to the data that was being sent, which is like no items at all.

So let's go back and forth and try to reload this as well.

Does it load?

Live coding is always risky.

Oh, boy.

Well, actually, this is something that we're also going to improve.

But right now, it looks like it's stuck, right?

It's not doing a lot.

It's just showing a spinner.

And that's because we actually hit our error.

So with this, the debugger paused on the exception that was thrown.

In our case, we have no idea yet where it comes from.

But what we do have is the right tools to find it.

So on the right, we have an interactive call stack, which is way better than just a blob of text.

And we can just go from top to bottom.

So the first one is browser.

The second one is virtualized list.

Well, that's not our code.

Something related to flat list, which is interesting since we use it.

But it's not exactly the issue.

So our issue is within this part, which is our code.

Now over here, we can see that an exception is being shown on the scrollToEnd function.

And that's interesting.

But we have no idea why yet.

So let's undo this.

Let's try and capture the moment that it will actually cause the exception.

So let's continue.

There we have it.

It failed.

Let's retry it again.

So right now, it did not fail yet.

It just paused the execution just before running the function.

And if I go here, I can actually interact with the code as I type.

So in here, we have our list ref that refers to the flat list that I control.

We can even check some information in here.

We can see that it registered properly.

So if I do current, yeah, we have the same thing.

And now I'm actually trying to run the scroll to end.

And there we go.

We have our exception.

So something is not right with this function and the state that the code is in.

Luckily, on the right, we have the scope, where we can just browser to or browse through whatever variables we have over here.

So since the only thing that mostly changes are the todos loaded from the API, we can actually expand the todos and figure out what's going on.

So in here, we can see a lot of variables coming from React Query.

And one thing that is interesting here is that there is no data.

And for new users, that makes sense, since there are no to-dos.

Right now, I kind of faked it, but that was the issue, where you cannot scroll to end on a flat list without any items, which causes this exception.

It's actually a bug in React Native, I would say, but it's good to know that this is happening in our app.

So let me fix that real quick, where

We have data from the API.

And we only scroll to end whenever the todos has some data.

And there we go.

Let me restart everything.

My bad.

There we go.

So right now, our app is back to life. we can scroll to end.

Like if I refresh it, it will actually reload the page or reload the screen.

And it will scroll to end, exactly what I wanted.

Now, why is this interesting?

It's because we can actually dive really deep into the code.

But we can do a lot more things.

So let's open a debugger again.

And since the data is coming from an API, it's very handy to know where the data exactly is coming from.

For that, I need to prep a bit more.

Give me one sec.

So whenever I pull to refresh, it will just fetch the data again.

But our API is fully visible in here.

So you can see I'm running locally.

But I'm just fetching some JSON, which is exactly this data.

So without too much trouble, I can just inspect whatever API calls I'm making and figure out what is going on.

And you have pretty much access to all of the requests, including definitely the fetch request, but also some of the native sites.

For example, when I load my own avatar, which can be loaded since I'm offline right now, but over here you can see that I'm actually making a connection to my avatar from GitHub.

Unfortunately, we don't have internet, but I can fix that later.

The image, whenever loaded, will actually be visible in the preview as well.

So you can load your asset, or you can keep track of the assets that is loaded, even the size of the assets that is loaded, and can give you really good insights in if your app is optimized or if your images need some optimization.

And lastly, it's really fun to use it like this, but we have to switch back and forth all the time, right?

So that's suboptimal, and it could be better.

So luckily for that, I actually-- let's hope this works.

With one command, using the VS Code Expo extension,

I can actually connect directly to my app.

And there we go.

We're in.

Now, this is not super interesting right now.

But one thing we can do is we can actually pause before rendering of the app home screen.

Now, let me try to rerun the render function of that.

And whenever I try to reload the data, it gets the same data back and won't trigger a rerender because we're using React Query.

So let me change the data in the server real quick as well.

And there we go.

We're at exactly the same area just before rendering the function.

And we can do pretty much what we can do in the Chrome debugger, but all related to our code.

So we can actually have really exact locations of our code related from the stack trace or the call stack.

And we can just browser through it again.

We can even execute from here as well, which is very interesting, where if I go to the debug console and run the test function that I had in there-- well, live coding example, but-- wait, maybe here.

Yeah, there we go.

So in here, I can just execute code whatever I want in the whole call stack.

I can even set states on your components if you want to try something out.

And all of that with just a simple command.

Now, just getting out of it will continue the app as it was.

So you can just literally code and debug at the same time.

Now, this is available.

It's currently experimental.

Let me show you right here.

If you want to try this out, you can actually do that.

For this, you will need the Xcode DevClient right now.

And make sure you're using expo48.0.16 or higher.

I think we're at 18 right now.

Then you have to configure your app.json build properties with the unstable network inspector, and then build your app.

Once you do that, you have to start the bundler with the expo use custom inspector proxy environment variable.

This will enable us to enable some CLI stuff that that will allow you to inspect the network requests.

Now, all of this tied together, we kind of get some things for free as well.

For example, if you want to use CSS in your logging, you can actually do that, since we're using an existing tool that supports it.

You can use .group, .time for performance benchmarks or logs.

It's all there.

So with this, we at Expo believe that debugging indeed should be easier right now.

Thank you.

Follow me on Twitter or on Blue Sky, or find me around the place if you want to talk about debugging.

[APPLAUSE]

## Q&A

All right, we have a question from Benjamin. I guess that question comes up a lot, but does it work with a non-Expo app?

Yes, kinda.

So the network inspector does not work without the expo dev client.

That's built into that area.

But the general debugging workflow is actually implemented in Hermes.

So that should work with React Native.

The tooling to start it up will be improved in the community CLI, I believe, where you have a one-click Hermes debugging option.

But that's coming, that's not there yet.

And I believe Alex Hunt mentioned that it's supposed to be around 0.73.

So, kind of, but it will be better in the future.

Awesome.

And speaking about the future, what's next? Are there some more tooling, cool stuff that could come in this, basically?

Yeah, like there are so many things that we do not leverage yet in the debugger that supports it, actually. like we have element inspector.

It does not work yet, but we do have the Chrome or the React dev tooling right now in Expo.

You can use that if you press Shift M, and it will open up.

It will be great if we can combine that into one tool, so you just have one tool to debug them all.

Yeah.

- That would be fantastic.

Maybe like a question, like, okay, so Flipper,

Flipper, it was supposed to be like the one tool to debug them all.

And one thing that was nice is, you know, people could go into it and write plugins and everything.

Like, how do you think you could get people integrated in this kind of new ecosystem to write, like, I don't know.

I remember there was a Flipper plugin, for example, to display images of your app, like, if someone wants to do that.

So we are actually talking about that with Meta, with Microsoft, and some other partners as well, where we want to enable users or other companies to write certain plugins or extensions for it.

But right now, we're very early.

So everything is still experimental.

So right now, you don't have a function to do that.

But it's definitely on our list to talk about.

And again, since we're using the Chrome debugger,

That already supports plugins, right?

So it will be actually interesting to see if we can have native-only extensions inside the Chrome debugger as well.

Awesome.

Yeah, looking forward to it.

Yeah.

Nice.

Thank you, Cedric.

[APPLAUSE]
