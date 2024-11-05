---
slug: >-
  /talks/frenchkit/swift-connection-2024/douglas-hill-zoom-transitions-a-comprehensive-guide
date: '2024-09-23'
title: 'Zoom transitions: A comprehensive guide'
author:
  - Douglas Hill
video: qA69uZDd53Q
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/qA69uZDd53Q.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Douglas
All right, hi everyone. It's really great to be here in Paris. So I'm Douglas Hill and this talk is going to be, this is quite a short talk, but we are going to go in as much detail as I can in quite a very specific new addition in the iOS 18 SDK.

So Apple brings, you know, gives us a lot of new APIs every year. But this one is my particular favorite. It's a very nice small addition.

So, yeah, let's get started. So what kind of transitions are we talking about? So this is the sample project I'll use in this talk.

And for now, we'll get to the code later. So for now, look at the preview on the right-hand side. We're familiar with these standard transitions that are available for our apps.

So this navigation push and full screen cover transitions. These have been around since the first iPhone. And we use these as the building blocks to put the screens of our apps together.

And they're fine. Like users know what to expect with this. But there's, for something like this where we're going to see a full screen image view, there's something a bit more fun we could use.

So this is a zoom transition. And so you can see how the thumbnail image zooms up. It's a bit like in the photos app when you tap a photo.

And what's really very delightful about these is you've got these interactive dismissal gestures. So that two-finger pinch. The, like, swipe from the edge and swipe down.

So this is a great transition to visually suggest a sense of space. It feels like a less heavyweight transition to the users. It's more like they're just looking at something in more detail rather than going over to a different screen.

And in fact, this really reminds me of the, when the iPad came out in 2010, I just spent ages playing with the photos app, pinching in and out of photos. Because it's, you know, although it's a digital experience, it just feels kind of physical that it has the, you know, the way it directly responds to your touch. And I think this is one of the things that made me get into iOS development is these kind of really nice transitions and animations.

Okay. So, yeah. How would we go about implementing something like this?

Well, yeah, there's a few things we might need to take care of. You want to have all these different dismissal gestures and getting the animation perfect. So Chris's talk, you know, would help with some of this, but there's still a lot more to do.

So we have seven minutes left for this talk. So there's quite a lot to cover. No, of course not.

In the iOS 18 SDK, we can get this kind of effect with just three lines of code. Now, I can make this project available if you like, but it's really very simple. So here we can see in Swift UI, it's we really just need to tell the system the view that we're zooming to, the view that we're zooming from, and then we have to connect those two together.

So you can see there's this navigation transition modifier that we use for, in this case, it's the destination of a navigation link, and this means that when you, you know, you still have the navigation bar at the top, as you'd expect, and it will include a back button, but it will use this alternative transition. And then this is paired with a match transition source on the view that we're animating from. In this case, it's an image in the list row.

And then this namespace at the top is just a way for Swift UI to link these two together. For a modal presentation, with a full screen cover modifier, it's very similar, just slightly different places where you apply these modifiers for the zoom transition. And then over in UIKit land, in this case, the code setting up the transition is all in one place.

So just before you are pushing or presenting the view controller, you can set this preferred transition property, which we then, you know, in there we say that we want a zoom, and then we provide a closure that the system can use to look up the, you know, the view that the animation starts from. In this case, I've shown the most comprehensive version. It's kind of checking if the data change while the, like, the final view, while that's visible, or if there's something like a cell reuse happening in the collection view or table view.

So if you have gestures in the view that you're showing, which you may have for scrolling or for pinching, basically the system does the right thing, and it gives your gestures will have precedence. So this means, for example, in order to get that swipe down to dismiss, like, first the user would need to scroll all the way to the top. So that's fairly okay.

This API is available on almost all Apple platforms, but it doesn't actually have an effect on some of them. I think it wouldn't really make sense on, like, watchOS, for example. So this is fine.

But it's a bit unfortunate if you are building a Swift UI app for, like, across iOS and macOS, you need to write, like, conditionally compiled code just for macOS. There's also a bit of an interesting situation with Mac Catalyst to be aware of if you're making, like, a Mac app using that route that if you scale to match the iPad, you do get the zoom transition, but then if you optimize for Mac, you lose it, which is a bit, I guess a bit of a shame because, you know, you see this kind of effect in Apple's Photos app on the Mac. So I think it would be appropriate.

So hopefully this is something they address in a future release. Just a couple of things about how to make sure this effect looks really good. So what I showed before was zooming on an image.

You could use this for something like this where you're just showing text, like the new zoom transition API. It's okay, but it's not really excellent. It's not the best fit here.

It's much better if you have something like a document viewer or a video that you're going to, like, show from a thumbnail image. Have a look at this animation that I've slowed down. You see the look at the ferry image on the top right.

You can see and also as it dismisses, see how the image kind of shifts and is visible twice during the animation. So you can see that I've taken a screenshot during the animation here. The reason for this is that the zoom transition always goes to the full screen view.

Whereas in this case, the image that we're zooming into has a different aspect ratio. So there's this mismatch during the animation. There is API to fix this if you are setting up your transition in UI kit.

So this is where we, like, with this fixed. The API is called the alignment rect provider. So you can see side by side the improvement like during the animation.

One thing I noticed is that this, I can't find a way to set this up in Swift UI only if you create the zoom transition in UI kit. So I hope that's something that's addressed in a future release. Or possibly I've missed a way to do this, in which case I would really love to know.

You may have also noticed that there's this, like, black border around the image during the transition. So this is just the background view of the full screen image view. If there were any toolbars or anything, you would also see those here.

And this is different from the effect in Apple's photos app where only the image gets shrunk, whereas the background and toolbars fade out during the transition. I think the photos app looks a bit nicer. But anyway, for now, this is not what Apple has built into the SDK.

However, considering we can get this new effect with just three lines of code, I think this is a really good tradeoff. Yeah, I would encourage you to look for places within your app that would benefit from this. You can see it's not going to be a big project.

It's quite a simple thing to set up. It just adds a bit more delight to your app and makes it easier for users to find their way around. If you are interested in reading more about this, so I have a kind of blog post format of this talk that's over at DouglasHill.co, which is kind of my online home where I'm posting occasionally about iOS development and sometimes about traveling around by train. For the last nine years, I've been working at PSPDFKit, where we make a SDK for viewing and editing documents. It's always super interesting learning things there in making an SDK. And finally, if any of you are around London or if you're visiting, I've been involved for a while in the organization of an iOS developer meetup NSLondon.

It would be great to see you at one of our events if you're around. Yeah, that's all. Thanks very much.

### Rob
I like the short things that give us something you can take away and just use. Thank you. There was a weird thing, though, in your code example that I didn't understand.

What's a namespace?

### Douglas
Yes, that's a good question. The problem this is solving is that in SwiftUI, your view hierarchy is being rebuilt each time it's updated. So I think this is why you see the ‑‑ I would say this is more simple to understand conceptually in UIKit because you actually have a ‑‑ your views have a ‑‑ like, they are reference types.

So you can say when the system needs to know what view should I be animating to, you just provide that view. Whereas in SwiftUI, it's a slightly more abstracted connection between them. So really, all the namespaces, it's like a unique identifier, I think, within your whole ‑‑ I mean, it's wrapped behind this macro.

So you kind of don't need to think about the details. But it is ‑‑ when you set up the transition, you are providing two things, an identifier for your model object. Because this may not be globally unique, you're also providing this namespace that it exists in.

But I kind of think of it more like the namespaces, it's just with these two things together, the system can uniquely know that this view animates up to this one.

### Rob
Okay.

### Douglas
Okay.

### Denis
From the audience following up on namespace, we're wondering, is it safe to inject the namespace inside the environment? Or is there a cleaner way to do it?

### Douglas
I think that should be fine. If you're, like, if you're setting up multiple different places in your app that have Zoom transitions, I think as long as you don't mix up your namespaces between them, I don't see why there would be any problems with this. Okay.

But, yeah, like, yeah, the code sample was very simple there. But if you have more, you know, complexity in your, you know, like your list row, yes, you may then have that be a separate view and I guess you could use the environment to simplify parsing that namespace down to that. Okay.

### Rob
So I always get really nervous when in UI code there's this, well, it's not implemented, but you can call it. What does it do in that case?

### Douglas
Right. So like on watchOS or on Mac Catalyst if you're using the optimized setting, you'll just get the normal, like, push transition from your, like, navigation stack. Or if it's like a modal presentation, you'll just get the standard slide up.

So it does, like, this would also be the case if you're supporting versions before iOS 18. Like, the, well, the functionality in that will still be there. You just will get a different transition effect, which I think does, it makes a big difference to the feel, but it's technically everything will still work in the app.

So I think it's quite, it's a fine for work.

### Denis
Questions that comes up, is it possible to customize a bit the transition? Because, for example, the example given is, like, if you're displaying a sheet, maybe you don't want to you want to disable the zoom out when you slide down. Is it possible at all?

### Douglas
I don't think you could do specifically that. I mean, that is the tradeoff with this. You get the effect for three lines of code, but there's not a whole lot you can customize.

So I think, I mean, I think for the vast majority of apps, it's a very good tradeoff. But, yeah, I think it's fun, like, this is a fun thing to implement, and I did, like, it was a rainy weekend a few weeks ago, and I had a go, like, implementing this from scratch just to, well, as a science project, and I made decent progress, but even, like, most of the day on it, it was not completely finished as a kind of reusable component. So I don't know.

It's probably not the best use of, like, your company's time if you're if you need to implement this effect. Yeah, I think the I guess the programmer in me is, like, yes, this is fun, but more like the project manager is, like, no, let's do it the easy way.

### Denis
Well, thank you for your time and for this great presentation. Thank you. Thank you.