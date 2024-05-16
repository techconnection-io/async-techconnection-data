---
slug: /talks/flutter-connection/2024/loic-sharma-into-the-flutter-verse
date: '2024-04-24'
title: Into the Flutter-Verse
author:
  - Loïc Sharma
video: 1l22fkWPnos
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/1l22fkWPnos.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: '2024'
allow_ads: false
---
### Loic
I'm Loic, I'm from the Flutter team at Google, and today I'll be talking about Flutter's journey to supporting desktop applications with multiple windows. So you might be wondering, why do we need this? So let's start by looking at some example scenarios.

So first a very common one is if you have a desktop application and you need to manage some settings, oftentimes the application will do this by opening a new window. So in this example, I'm using Microsoft Paint, and then I want to resize my image, and the way Microsoft Paint does this is by opening a new window. Another example that's very common in desktop applications are applications with multiple tabs.

So here I'm using Windows Terminal, and I can drag one of the tabs out, and that creates a brand-new window, and I lose none of my state when I do this. You also see this pattern quite often in chat applications, where you can drag a conversation out into a new window, and then you can talk to two different people at once. Another example that you might not think is done with multiple windows, but it is, is tool tips or context menus.

So in this example, I'm in Microsoft Paint, and I press a little button below my selection feature, and then that reveals a context menu with lots of different options I can do, and then notice how the context menu here extends outside of my main window, so the way that's implemented is by actually creating a second window just for the context menu. So all of these scenarios are very common in desktop applications, and because with Flutter we want to give you the full power of the platform, it's important that we support this as well. So it turns out that you can actually already do multiple windows today.

We have documentation on how to do this and samples, so are we done? Not quite. So the solution we have today is a little bit flawed.

What you need to do is you need to create a new Flutter instance for every single window. And that requires you to write native code. So if you support Windows, macOS, and Linux, that means that you need to write native code three times for all of those platforms.

And we would all rather write Dart code instead. And the second problem is the fact that you're launching separate Flutter instances, so that means that you have separate Dart isolates, and that means that each Dart isolate has its own state. It's not shared across your application, so instead what you need to do is you need to send messages between your different windows, kind of like it's a distributed system.

And state management is already hard enough in Flutter as it is, so nobody needs a headache. So we hear this feedback from our community loud and clear. The issue we have for improving support for multiple windows on Flutter is our seventh highest-thumbed-up issue on GitHub.

It's got more thumbs up than other issues that are popular, like reducing Flutter verbosity. So clearly this is a pain point for our community. So we're on a multiyear journey to properly support multiple windows in Flutter, so let's look at the work that we've done in the last year or so.

So first, the very lowest layer in Flutter, in the Dart side of Flutter at least, is the Dart UI API. So this is what a Dart, a raw Dart application looks like that's using the Dart UI API directly, and this is what it looked like before the multi-window journey. So notice how I'm using this window global to register a callback that's invoked on each frame.

And inside of that callback, I again use the window global to draw something. So this is what we call a single window assumption. It makes an assumption that my application has just a single window.

And how would this work if I have multiple windows? Well, it just doesn't work. So we've had to clean up a lot of these single window assumptions from Flutter to make it support multiple windows.

So now let's look at what this example looks like now that we've started cleaning up some of these single window assumptions. So first, we've introduced a platform dispatcher global, which replaces the previous window global. And using the platform dispatcher, I register another frame callback, and then inside of the callback, I now use a views property on the platform dispatcher.

So a view is just some content that Flutter can render into. So you can think of a view as content within a window. And in this new sample, I just iterate through all my views, and then I render something to each view.

So now this is ready to handle 0 or 500 windows. OK. So then the Flutter framework is built on top of this very low-level Dart UI API.

So let's look at some of the changes that we've done there. So we've introduced some new extremely low-level widgets that you can use. Well, actually, they're low-level, so you probably won't use them directly yourself.

But you might see them in Flutter DevTools if you're debugging your application. So let's talk through each of these. First, at the very heart of Flutter is what we call a render tree.

And this render tree is what's responsible for doing things like laying out your application or painting your application. So if I have just a simple application, like some text on a colored background, that might look like this render tree that I have here. But the render tree tends to be quite low-level and not very convenient to work with.

So instead, what your Flutter application creates is a widget tree. And then the Flutter framework uses this widget tree to create or update the render tree. So on the left-hand side here is my widget tree in the yellow squares.

And then on the right-hand side is the render tree that the Flutter framework creates in the blue circles. Notice at the very top is this new view widget. So the view widget is responsible for doing two things.

So first, it bootstraps the render tree, and then second, it tells the render tree which view it should render itself onto. Okay. Now, let's look at what a widget tree looks like if I have multiple windows.

So now we're using this new view collection widget, and the view collection widget can have multiple view children. So notice how here I'm rendering into two windows, which are denoted by the purple squares. And each window has a view widget at the top of it.

Also notice how I have one single widget tree for all of my windows. However, each window has its own render tree. This is one of the big architectural changes we had to do to Flutter.

Previously, your application had one widget tree and one render tree. However, now, you still have one widget tree. However, you can have zero or more render trees.

So you might be wondering how does state work in this new multi-window world. So it works exactly the same way as it did before, because you still have just a single widget tree. So in this example, I just stuck an inherited widget at the top of my widget tree, and now both of my windows have access to it.

So they can read state from it or share state across the different windows by writing to the inherited widget. And then, of course, whatever state management packages you might be using will continue to work just because you have a single widget tree. And then before we look at the last widget, let's look a little bit closer at how context menus work.

So notice how when I click on this button, the context menu is positioned based off where the button is. And then also, you would expect that if I closed Microsoft Paint, that the context menu would also close as well. So there's a bit of a parent-child relationship between the Paint window and then the context menu that it can open.

So you can represent this using this new View Anchor widget. So on the top left, I have my main application window. And then at the bottom right is the window for my context menu.

And then the parent-child relationship is established using my View Anchor widget. Great. So those are all the new low-level widgets that we've introduced.

Next, let's look at how you can launch an application in Flutter. So hopefully you know this code. This is what you call in your main method of just calling runApp.

And you pass it the root widget for your widget tree. So you might be wondering, where does this render to? Like if I have multiple windows, where would this render?

And this is yet another single window assumption. What's actually happening behind the scenes is that the Flutter engine provides a special magical view that the framework can render into. And the engine actually does some weird tricks.

So for example, if your app is currently in a headless mode and you have no windows, it will actually mock out render calls and act as if you're rendering something when in reality, it's not doing anything at all. So weird magic is never good. We want to clean this up as part of the multi-window effort.

So we've introduced this new runWidget function that replaces runApp. And unlike runApp, runWidget gives you full control over where you're rendering to. So in this example, I'm manually providing which view I want my app widget to be rendered to.

Now, of course, this is lower level. It's more verbose. So it's a little bit less convenient.

So we would still want you to be able to use runApp. So in the future, we're going to be cleaning up runApp to, instead of using a special magical view behind the scenes, it will create a window and then use that window's view to render your widget to. So you should continue using runApp if that works well for your scenario.

OK, so I've covered the things that we've added in the last year or so. Let's talk about the things that we're going to be working on next. So first and foremost, we want you to be able to create and manage your windows using Dart APIs that feel very fluttery.

Unfortunately, that's a little bit harder than you would think because of some problems. So one, different platforms behave differently. Imagine that I try to create a window that's bigger than my monitor.

Or imagine that I try to create a window that's just completely outside of my monitor. How different platforms handle these kind of errors might differ. And we need to create one unified API that is consistent across all of these different platforms.

You may hear us refer to this as the lowest common denominator problem. Another problem is the fact that the widget tree is declarative. So you state exactly how you want your application to look like, and then the Flutter framework magically figures out how to do that.

Unfortunately, for windowing APIs, that doesn't quite work. You might ask the platform for a window of a certain size, then the platform might give you a completely different window instead. Finally, this windowing API needs to be baked into the framework.

We want the material and Cupertino design systems to be able to create tooltips and create context menus, and because these design systems are already baked into the framework, that means our windowing APIs also need to be baked into the framework. The reason this is a problem for us is because normally for these risky kinds of APIs, we would prefer to make it a package. If we ever need to do a breaky change because our design was horrible, we can just bump up the major version, and then the community can migrate over to it when they're ready to.

And if you're not ready to migrate, you can just use that older version of the package. However, with the framework, it takes us a lot of we just can't make breaking changes as quickly. We try to never do breaking changes if possible.

So we need to take the time to make sure that we design this API well enough that we can ensure we won't need to do breaking changes in the future. Okay. So we're experimenting a lot with what windowing APIs may look like, and here's one example that we're playing around with.

So keep in mind that this is all very hypothetical. It may completely change by the time we land it. So this might not be the end result.

But here, I start by creating a window controller, and I provide some size. By creating the window controller actually kicks off an asynchronous operation in the background to create my window, and then in my build method, I provide the controller to a window widget. So what will happen is when the asynchronous operation to create the window completes, the window widget rebuilds, and then it will render my app widget to the window.

So notice how this looks like it's declarative. I have a window widget, but it's actually not. It's actually an imperative API because of my window controller.

And then say that I want to resize my window. So I do that by calling a request update method on my controller. This kicks off another asynchronous operation in the background to resize my window to what I asked.

When the platform resizes the window, which may be a completely different size from what I asked for, this will rebuild my window widget and then rebuild my app widget as well. So that's it for the windowing APIs. Next let's talk about performance.

So on the Flutter team, we care deeply about performance. We're fortunate for multi-window that desktop devices tend to be more powerful. So performance is usually less of a concern for us.

However, we are very concerned about the performance of multi-window on mobile devices. And expanding multi-window support to mobile is maybe blocked based on performance. So we need to make sure that we make investments such that the performance is good enough that we can expand to mobile as well in the future.

So on each frame, this is a diagram of what rendering a frame looks like in Flutter. So on the x-axis is time. And then I have two swim lanes for each of my thread, for each of the Flutter threads.

So the UI thread is the thread that your Dart code runs on. And it's also where the Flutter framework runs. So that's where things like layout, painting, compositing happens.

And then the raster thread is where the Flutter engine runs. And that's where it takes the low-level drawing commands produced by the Flutter framework and then converts them into pixels. That process is called rasterization.

And that's where Skia or Impeller runs, if you're familiar with that. So in this example here, at time 1, I'm rendering my first view on the UI thread. At time 2, the Flutter framework renders my second view.

At this point, the UI thread submits the frame to the raster thread for rasterization. At time 3, I rasterize my first view. At time 4, I rasterize my second view.

And at that point, I have pixels that can be presented onto the screen. It's a bit high-level. It's actually a little bit more complicated than that, but that's good enough for the performance discussions we'll be having.

So a benefit of this design is that we can actually be rendering, sorry, we can actually be working on two frames at what's in parallel. So on the left here in the purple is my first frame. And then on the right in green is my second frame.

And notice how at time 4, the framework is rendering a view while at the same time, the raster thread is rasterizing a view. So this is nice, but we want to see if we can do even more parallelism by parallelizing within a single frame. Okay, so let's look at a slightly simpler example.

So here I'm working on a single frame, and notice how the view 1's rasterization doesn't happen until all of my views have been rendered. So there's a bit of a gap of a millisecond of when I could have started rasterization. So we'd like to re-architecture the Flutter engine so that we're able to begin rasterization before all views have been rendered.

So effectively, as soon as view 1 has been rendered, we are able to begin rasterization. So then notice how view 2, its rasterization is blocked until view 1's rasterization is complete. So today the Flutter engine rasterizes views sequentially, and we'd like to investigate if we'd be able to do multiple views rasterization in parallel.

And then finally, we can do even better, and this is the optimization that I'm most excited for. So today, Flutter, we render all views and then rasterize all views on all frames. But that's actually a little bit wasteful, because what if view 1 hasn't changed at all?

Maybe the customer was hovering over a button on view 2, but then view 1 is effectively completely static. So we'd like to investigate if we can move to a world where Flutter becomes lazy and only processes the views that have changed on the frame. Okay, so that's it for the performance section.

Let's talk about all the other things we need to do to land multi-window. So first and foremost, we have multi-view rendering working on Windows, macOS, and web today, but we'd also like to expand that to Linux as well. So we're working closely with the Canonical team to get that working.

Next, the UI toolkit is a lot more than just rendering. We have tons of other features like mouse and keyboard input, accessibility, and so on. We need to update all of these features to work with multiple windows.

Also, Flutter has a very large plugin ecosystem, and many of the plugins we have make single-window assumptions as well. So we're going to have to go through the entire plugin ecosystem and update them. And then finally, our customers love the rich tooling that we provide, so it's important that we update the tooling to be designed to work well and be helpful in a multi-window world.

Okay, so we're on a multi-year journey to land multi-window support, and you might be wondering, why are we doing this? Is this the right investment for the Flutter team to be making? So here I'm going to be pitching a hypothetical dream of a scenario we may be able to unlock with the multi-window work.

So Flutter today is very successful with brand-new applications or applications that were able to do a complete rewrite. If you look at all the applications at Google that use Flutter, many of these were applications that were brand-new or rewrote the UI entirely to use Flutter. Where Flutter is less successful is with applications, large existing applications that want to migrate incrementally to Flutter.

So for example, imagine that I'm the GitHub application, and I want to migrate to Flutter. And I'm a huge application, so it would be too much work to rewrite my UI, but I want to do it incrementally. So let's say that I want to do this by migrating just my home screen and my notifications tab to Flutter, but then everything else would remain native.

So the yellow boxes would be Flutter content, and then the purple boxes would be native content. Now this is actually harder than you would imagine. Tabs let me switch between them without losing any context.

So for example, I'm able to, on the home tab, navigate into the issues, then find the issues that are assigned to me, and then I can start writing a comment to one of the issues that's assigned to me. And then I can switch over to the notifications tab, look at some pull requests, start doing some code review there, and then I can switch between the home and notifications tab back and forth and write a little bit more comment on that issue assigned to me, and then continue doing my pull request review. None of this data is lost.

Now how would you do this with just a single view? That's actually really hard. You would need to somehow, say I'm starting on the home tab and then switching over to the notification tab, I would need to capture my whole widget tree and all of the routes that I've navigated through that whole navigation stack, all the state, capture it somehow, store it on the side, then go to the notification screen, and then when I'm switching from the notifications tab back to the home tab, I would need to restore all the state and the whole navigation stack I had before. And that's just way too much.

And a much better solution for this would be to just have separate views. So I should have one view for my home tab and then one view for my notifications tab. And then when I switch between my tabs, all that should be is just showing a view and hiding the previous one.

No need to do a ton of state magic. So the hope is that with multi-view, which is one of the features that we're unlocking with multi-window, that we'll make it easier to do incremental migrations of large existing applications to Flutter. So the Flutter team has this phrase that we like to say of embracing the yak shave.

And in this case where we have years of work ahead of us, it's a bit more of a mammoth shave. But we think that by doing this deep, fundamental investment in Flutter's architecture, that it will unlock a lot of value to our customers. And that's it.

### Guillaume
Thank you very much, Loic. We have some questions.

### Simone
Some questions. Just a few. Just a few questions.

It's the end of the day. I think we can stick here for the next two hours responding to questions if you don't mind. But I think the pun piper will mind.

### Guillaume
I'm really impressed by the number of questions on such a technical talk at that hour. You guys are amazing. So let's start with an easy one.

Does it support hot reload?

### Loic
Yes, of course. Yeah, it needs to be an excellent development experience or bust.

### Guillaume
So see, it was an easy one. Okay, maybe we'll keep this one for the last one.

### Simone
Okay, sure. While you're looking for one, I think I had one personal question. So you said that in a way Flutter assumed that the render tree was just one.

So did it break so much stuff there? I mean, how painful was it to refactor that code that was kind of hard-coded in a way?

### Loic
Well, the tech lead for the Flutter framework spent a year fixing that problem. So it was pretty hard, I'd say. Yeah, so before the render tree we would bootstrap the widget tree, and we've completely inversed this actually.

So now the new view widget creates a render tree. There's actually a lot more going on. So we actually have, I didn't mention this in the talk, there's actually a tree of render trees.

So we call this a render forest. This is like another thing that we had to introduce as part of this work. So we are boiling the ocean as part of this effort.

### Guillaume
Lost in the forest. Brace yourselves. Are there any widgets that would implicitly support multi-windows out of the Flutter framework?

### Loic
By that do you mean, what would you mean?

### Guillaume
I mean, from the existing widgets, are there any widgets that people would know of that would automatically, implicitly be usable on multi-windows?

### Loic
So we're hoping that all widgets should still work in a multi-window world. Really, I think we also want to add new abstractions, I think, to make having multiple windows better. Right now we're more working on a low-level fundamental layer.

But ideally all the widgets that you see today should still work across multiple windows.

### Guillaume
Okay, so all of them, basically. Hopefully. Are there impacts on web with those new render tree architecture?

### Loic
So as part of the multi-window effort, we're introducing multi-view. And that's going to be really useful for web as well. We've had a demo where Gemini was generating Flutter applications as part of responses.

So you could ask, I don't know, hey, can you convert kilometers to miles? And they would create a little Flutter application for you so you could do that. And then each response had its own application.

So the way that works is that it's actually one Flutter application, then each response was its own view. So that's one example where multiple views would be useful for web. Another one is say you're migrating your website incrementally to Flutter.

You might want to start by just migrating the sidebar and then migrating the Flutter. And those could be separate Flutter views as well. So we actually, the web team has been extremely quick at implementing multiple views.

They started well after the desktop team. And then they caught up with us, and now they're past us. So we think multiple views will be productionized first on web.

### Guillaume
Awesome. That really is going into the Flutterverse. So this one is a bit more technical, but interesting.

I think from the platform dispatcher, when you draw on all, I'm reading it literally. When you draw on all views, is it on a single thread? And how would it impact the performance if you have 20, 50 views?

### Loic
Yeah, that's a great question. Yeah, so Dart is single threaded, and the UI thread will remain single threaded. So yes, it is iterating.

If you have 50 views, you would have to do it in, like one thread would be running through all 50 views. So my hope, I don't know if we'll be able to pull this off, is that you won't likely have 50 views that change every single frame. So the amortized cost, ideally, should be as good as a single window world, if not better.

Because on some frames, you might not have any views that changed at all. Whereas today, we're always rendering your one view every single frame, even if that might be completely wasteless or wasted work.

### Simone
I guess on top of it, you know which windows actually show on the screen and which isn't.

### Loic
In theory, we could do tricks like that. We haven't started looking into that, but that's something we could look into as well.

### Simone
OK. Awesome. Same goes, I guess, for partial rendering, like render a portion of the screen which is not.

### Loic
That would be hard. I don't know if we'll be doing that, but maybe in the future. OK, right.

### Guillaume
Is there any ETA for that to be released, that you can talk about?

### Simone
Can we switch recording off?

### Loic
So we don't give any ETAs at all on the Flutter team. Things will be done when they're done. It will probably be multiple years, sadly.

So not anytime soon.

### Simone
Yes, I think you're thinking about that question.

### Guillaume
Yeah. OK. Yeah, I think this is actually the first question that popped up on the Slido.

Do you have any Google's roadmap for Flutter to share, other than multi-windows, I guess?

### Loic
Nothing offhand that I know has been changed. We have shared a roadmap earlier in the year. I think that was on our Flutter wiki, and that was also on the Discord.

So as far as I know, that's still the latest roadmap. I'm sure that at Google I-O, they will probably be doing great marketing. They always do wonderful marketing at Google I-O.

It's always shocking as a developer to find out all the things we've been working on.

### Simone
Might I add the latest public roadmap? What about it? Sorry, may I add the latest public roadmap?

I mean, I guess you have a roadmap internally, which kind of, I don't know. It's not shareable.

### Guillaume
So we were looking for some crispy announcements.

### Simone
Oh, no crispy announcements from me, sorry.

### Guillaume
We'll wait for Google I-O in May, I guess.

### Simone
No, we're waiting for the bar, you know. We're waiting for a couple of pints. In vino veritas, as the Latin said.

### Guillaume
Thank you very much, Loic.

### Simone
Yeah, thank you.

### Guillaume
Thank you for sharing all those with us.