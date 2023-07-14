---
slug: "/talks/flutter-connection-23/guillaume-bernos-advanced-topics-with-webviews"
date: 2023-06-02
title: "Advanced Topics With WebViews"
author: "Guillaume Bernos"
video: QMmo6oqmBSs
thumbnail: thumbnails/guillaume.png
slides:
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

Do you hear me? Great. So, hello everyone. I'm really happy to be here.

I hope all of you still have some energy because there are some talks left for today.

Is the sound OK?

I feel like there is some weird noise.

OK.

So yeah, so as Greg said, I'm Guillaume Bernos.

I work at Inverted on the Flutter Fire project.

So if sometimes you have some issues with Firebase on Flutter, maybe it will be me.

That's why I'm also on GitHub.

But today I'm not here to talk about that.

Today I'm here to talk about web views.

So a quick question, who already integrated WebViews in their photo apps?

Oh, OK, a lot of you.

So we'll see if you bump into some of these issues, or if you never.

So maybe you will learn some stuff along the way.

So the first thing that you may ask is why should we use WebViews?

Because there is a common saying in photo that everything is a widget, and WebView is not exactly a widget.

So why should we use it?

Let's start with a little story.

So a couple of months ago, I wanted to have an idea of a side project, like every developer.

And I wanted to create an email client to share email between people and stuff like that.

So I'm like, OK, great.

I love Flutter.

I picked my favorite state manager.

I put RiverPool.

I put Gorut.

I put everything in.

It was working great.

And then I was like, OK, I get everything from the Gmail API, but now I have to display my email.

How am I going to do that?

So at first I was, OK, maybe I'm going to pause the h-tag and stuff like that.

But probably not the good answer.

And I finished-- I ended up using WebViews everywhere because it was the easiest way of doing it.

But I was getting away of Flutter.

So you will see in this talk how to properly integrate the web use so they feel the most fluttery possible.

So the first thing you can do when you have to display HTML is to just transform the HTML into widgets.

That's the easiest thing you can do.

So you can use, for instance, there is a lot of them on Pub/Dev, so I've chosen some package to showcase because I've used them, but every day there is a new widget for doing things that I will present, so maybe you will find something that is better.

So here I've used the Flutter widgets from HTML package, and you can use it to transform

HTML into widgets, so it has a lot of advantages, one of them being you are still using widgets, so everything is integrated with Flutter, so you get optimisation like having performance improvement from impeller, for instance, or having everything properly wrapping and having full control on the theme, it will integrate automatically with the theme, so that's really nice.

But emails aren't just text, often you get like marketing emails or spam or stuff like that that will have a lot of CSS and that will be hard to just represent with basic widgets like text and images.

So if you can control the HTML and can restrict the tag that I use, so maybe you are using a CMS and someone is typing something that is transformed into HTML and then sent to your frontend, maybe it can work for you, because it's by far the most optimal way of doing it, but it will only support basic layout.

If you don't have any choice and any control on how the HTML will be generated and how or merge CSS will be in your HTML, this probably will not be the good solution for you.

So there is two famous libraries for handling web views that I've presented here.

So the first one is the WebViewFlutter, which is the official package by the Flutter team.

So this is really nice.

There is a great support.

There is a non-understand support for web, which means that you have to add another package to get web support, but it's working, and it also supports preloading the page.

So if you have some basic needs for just displaying a web view in your app, or having some basic browser support, it's probably enough.

But there is also another package, Flutter-init-app-webview, which is an unofficial package which supports support web and Mac OS since version 6.0, also supports the page but also supports a lot of other features like WebRTC, service worker, local server, cookie manager, so if you want something a bit more advanced, you will probably need to use this one.

It moves pretty fast and people are really reactive because it's a huge community on

GitHub around this package, so it's really nice to be able to switch to something more advanced if you have more advanced needs.

So for my client email, I went with Flutter in app web view, and I will show you most of my code snippet with this package.

It can be done, some of it, with WebViewFlutter, but it will probably be harder than just using

Flutter in app web view.

So I will show you a couple of examples, and through those examples, you will understand how to properly interact with the WebView and how to integrate it better in your Flutter widgets.

So the first example I want to show you, and the only reason why I have this beautiful app, that's why I had to bring my own laptop.

So as you can see, there is like two small things, and you can imagine that the rainbow containers are WebView.

And since the WebView is a native view, you have to give it a height, otherwise it will just take all the height available, or it will just not work because you need to constrain it because you cannot send its own height to Flutter.

So imagine that you have a web page.

If you want to scroll on the left, it will not be really well integrated. you will see that you have one scroll into another, where on the right, you have properly scroll, so you display the web view.

And then you have some flutter text under.

So that's the problem we are going to solve in this first example.

So the thing, without setting the height of your platform view, you cannot display it properly.

So you will need to get the height from the web view.

So I think the first thing to do when you are using a WebView that you don't control is to embed it in your own WebPage that you will be able to constrain properly.

Which means that you can create a basic -- here it's properly formatted, but you just can put like it in a string, a Dart string, and you will be able to constrain everything.

So as you can see, we have the doc type HTML at the end, the HTML tags, some metastype, and then we have the first part, which is like custom, which is the style.

So here we can put like a min-height, a min-width, as you can see, those are like flutter variables that if you don't give it a min-height, it will get replaced by zero.

Otherwise it will work.

You can also decide to hide the scroll bar, so these are a couple of things that I've added because I needed it, so you can remove the scroll bar, so you only display the scroll bar from Flutter, which can help with the overall feeling of your app.

And then you have some style CSS and some JavaScript that you can add.

So you have your template, and everything will be -- you will always have the same template, and the content -- so in my example, the content from the email will be in the content part at the end.

So once you have set up this page, it will be your base layout that will help you, like, inject in the HTML you have received from the server everything.

So the next step is getting the proper page 8.

So when you are using Flutter in the App WebView, you get a controller that allows you to interact with the web page that has been loaded with the on.stop callback.

So the first thing to do-- I assume that everyone knew a bit about HTML.

I hope it's OK.

But otherwise, you can ask your neighbor.

I'm sure some of you have done HTML.

So the first thing to do is to evaluate some JavaScript.

So here you have the await controller.evaluateJavaScript, which is exactly the same thing as you will have if you are in Chrome in the console and you type something. it's enter, the same thing.

So with document.body.offset8, you get the proper height of all your page, and you can get it, check if your stateful widget is mounted, and that set is eight, and it will probably integrate it into your Flutter app, because then your widget has the proper height, so then you don't have this issue any more. to note is that we wouldn't have been able to do that if we wouldn't have defined this doc type because maybe some email that you will receive will not integrate the HTML properly and you will have only parts of the tag. So that's why you need to have the page properly set up.

Yes.

I have said it.

Next thing you can do is dynamically set the width of your web view.

I think we all went on the website that wasn't properly supported on the mobile phone and then had to scroll left and right just to read things.

So that's not really great and it's not great when you are integrating external HTML into your app. So here we cannot, like, change the width according to the size of the user's smartphone, since it's already taking the full width of your app, so you have to work directly on the scale of your page in order to impact properly all it is displayed, and then you will be able to fit it. So it's basically the same thing that we've done with the eight, this time with the width, so we request from the web page the document.body.offset_width.

And if it's mounted, then we get the size of our page with the media query, and then if the scale is inferior to one, we unzoom properly by using document.body.style.scale.

So we just get some information and then we can execute some JavaScript to change the scale of our web page and properly integrate it.

So this is pretty nice, but often when you go on the web page, there are some things loading asynchronously.

For instance, you have a huge photo and it will take a couple of times to display.

So what I often do is like putting into a timer.

So every couple of seconds, my web page will try to adjust properly to its height and its width, so it's always the proper height for the user.

So there.

That's two problems solved.

Another problem I had when creating this email client was you had to quote a user or text when you are responding to an email, but you don't want this quoted email to be displayed, but you still want to be able to expand it.

And since my eight script was running each second, if someone clicked on the button, they have to wait one second to have the eight properly adjusted.

It will not be good enough.

So I had to run a script from the web view to tell Flutter, hey, I have changed my eight.

Recalculate properly the eight directly.

So as you can see, I have a small script that I have injected in my setup page that I had at the beginning.

And in this script, the first thing I do is I start by IDing all the Gmail quotes elements that have the class name Gmail quote.

Once everything is hidden, I add an event listener for click on each of these collapse buttons.

And when this happens, I'll change the visibility of this element.

So that's pretty easy.

But then the interesting thing in that is the windows.flutter in app web view.columnar click button, which helps to say, Flutter, OK, something happened in the JavaScript.

Now you have to do something.

So this is the JavaScript part that is integrated into the HTML.

And in the Flutter part, you can always use the controller to add the JavaScript on there that will be able to adjust the size of your web view.

So this can be really powerful to get things to work in JavaScript without having to use external dependencies.

So for instance, if you try to parse a JavaScript string

In Flutter, you have to import the in-entl package, which can be a lot of things to handle.

And there is sometimes web dependency issues between packages.

Here, you can just--

I don't know-- parse it in JavaScript, because you have the in-app web view and get it back in Flutter directly.

So it can be used in different ways, but you can write code directly in the web view and get everything back in Flutter, which is pretty neat.

Another subject that we have is web views with Flutter web.

So I'll try to explain, because it's not always clear.

So I'm talking about not running Flutter on the web, but running web views inside the Flutter web app.

So recently, with Flutter 3.7, we added the support of integrating Flutter almost everywhere.

You can put it in a div and add it like CSS effect on it.

It works well.

It's the same thing the way around, like with WebViewFlutter and Flutter in app web views, it's always the same thing.

The web view is displayed into an iframe.

So you don't get any issue because it's pretty separated from Flutter.

The only thing you will get an issue with is if you're trying to add a widget on top of your web view.

It will work properly on mobile, but on the web you will have to use another package just to get the tab properly handled.

So you have to use a pointer interceptor, which is like an official package, but it's not integrated into Flutter directly, which why not?

But yeah, you can definitely use that.

There are a lot of examples.

And apart from that, WebView with Flutter web works pretty well, which is nice.

Next subject, which is really important, is when I started my email client, I was really happy. okay, everything is loading, that's cool.

And then I tried to see the difference of speed with the official Gmail client and mine, and when I was clicking, it was only like two or three seconds of waiting before it was displayed.

So the first thing I've done, I've tried it in release mode, which helped me a lot with the speed, but it wasn't still enough.

So the other thing you can do is like preload the web view constructing the controller early so you can have a lot of different ways of handling it.

You can do it during the animation of the routing, so you're clicking, it's already constructing the controller and start loading even before the loading of the page is done.

Or you can also do it optimistically, which means you know that some emails aren't loaded are not unread, so you will load them ahead of time, so it's more memory intensive, but it works well to have a pretty good experience for the user.

You can also use automatic keep live mix in to keep a WebView ready if you're going to try it multiple times, so if you see the thread list in the Gmail app, when you click, the web view is appearing and disappearing really quickly.

With automatic keep alive, you can keep it so it will have a nice experience.

So yeah, you can always optimise loading time of your web view and it improves a bit between

Skia and Impeller on iOS, which is always nice to see. thing I run into, which I will mention, I have not digged deep enough that, but when you think you may know that, but when you're running your app into Android, you have a different default transition, which is the Android transition between two pages, than when you are running it on iOS, when you have the key personal page transition builder.

Well, platform views are disappearing weirdly on Android, so switching to the Kubernetes page transition model also helps with smooth transitions.

So that's weird on an Android device, but it works well.

So it might help you if you have some issues with transitioning when your web view is disappearing.

Next thing to have a proper integrated experience with your app is the font.

By default, your web view, if you don't have any style or anything, will use the default browser font, which will be probably something that looks like a Time News

Roman or something like that.

So not really well integrated.

In the script page, in the script part of the page

I've shown you before, you can just add any style sheet from Google fonts and apply it to the whole body and it will match the font you are using for your app.

You can also use base 64 strings, so if you're -- you can read your font directly in your

Flutter app and transform it into a base 64 string or just do it ahead of time if you know which font you are going to use.

You can load it pretty easily, so your web view will match your app, even if the user decides to change the font of the app, if you have this option in your settings.

So yeah, there is always a solution to have it match.

And that's why not using the HTML directly, but being able to change it by injecting proper CSS is always useful.

And finally, the last step to create a proper email client was to be able to edit an HTML file.

And this was the hardest part.

And I feel this is the part for which Flutter isn't fully, fully ready.

Because even though there is a lot and a lot of libraries,

HTML editor and SQL HTML editor, Flutter minimal HTML editor, there are a lot of them.

All of them were missing some key features.

Like, for instance, you want to be able to edit part of the quoted email.

So if you are quoting a newsletter with advanced CSS, most of them will fail because they are done just to create new HTML, but not properly edit existing HTML.

So a lot of libraries, not all of them were matching my needs.

And what I've ended up doing is using enough HTML editor which was working for my needs, but I still forked it and modified it heavily to fit my needs.

So I think it's something to keep in mind if you want to interact with HTML directly in your Flutter app.

You will probably need to get your hands a bit dirty to support a lot of things, like for instance, you want to support dark mode, it will probably not be handled properly by most of the editor,

You will have to churn something on your own.

If you want to support web, it will also not be easy at first.

So yeah, something to keep in mind.

So yeah, with that done, I had my email client pretty well done.

And it was my time to forget about this side project and move to the next one, because it's all we do.

So yeah, that's about it.

I hope you enjoyed this talk and if you have any questions, I will be happy to answer them.

[Applause]

> > Okay.

Thank you, Guillaume.

So a few questions.

You mentioned the disappearing WebView problem when transitioning on Android.

Do you notice any other differences in the implementation between iOS and Android using WebView?

I feel it was the most disturbing things between Android and iOS.

Otherwise, both Flutter WebView and Flutter in-app WebViews are pretty well supported.

So yeah, that was the most annoying thing that I had to fix on my own.

Otherwise, other things were pretty well supported.

JavaScript support is pretty on par for both of them.

So that was nice.

And the fix is quite counterintuitive.

So thanks for the tip.

Using Cupertino on Android.

And can you actually-- so you showed that you actually wrote some good lines of JavaScript.

How you can debug them?

Well, to debug this, since it's an HTML5 at the end, you can always copy it into your own browser and debug it directly in Chrome.

But to debug it during Flutter development,

I'm not entirely sure it's possible.

So console log.

Yeah, console log everywhere.

By the way, that console log is actually appearing in the--

Yeah, yeah, console log ordering.

I mean, like break prompts and prop-- but yeah, console.log.

Yeah, sure.

That's only half a joke.

Part of the actual solution.

Console.log.total.

Exactly.

So you talk about injecting fonts.

It's basically the same to inject any kind of style, and you can override the entire style sheet of what the injected web view.

Yeah, exactly.

If the web view is properly coded, you should be able to inject it, otherwise you will have to use the important everywhere, which is not nice, but you can always force it on the web view if you want it. For instance, to properly support dark mode,

I force it to change the font color, whatever it is, I force it in white in dark mode, for instance. So you can always do it something like that.

And, I forgot the question.

I had a question in mind about-- about that I forgot the question.

Maybe one last one about transitioning, too.

When you preload the web view, so is there anything happening with the transition?

Is it preloaded?

Yeah.

Does-- is anything in particular to implement to handle transition when you preload the web views?

No, not anything particular.

You just give the controller to web view, and if the page is already ready in the controller, it will be loaded directly.

So you will only get a really small delay that is almost not noticeable in release mode.

It's really noticeable in debug mode, so you don't have to be afraid.

You already compile your app, and it's pretty quick.

Or it handles the animation by itself.

Yeah, exactly.

Oh, OK, I got it finally.

Did you have to pass much data between the native and the JS part?

And if you did, how did you handle that?

Like, do you serialize and deserialize JSON objects, or not?

I don't do that.

But I think, yeah, that's Triggerify, and you can get on path from Flutter should work properly.

All right.

OK.

Thank you very much, Guillaume.

Thank you.
