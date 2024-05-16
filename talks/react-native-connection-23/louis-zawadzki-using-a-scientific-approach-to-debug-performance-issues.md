---
slug: >-
  /talks/react-native-connection-23/louis-zawadzki-using-a-scientific-approach-to-debug-performance-issues
date: 2023-06-01T00:00:00.000Z
title: Using a Scientific Approach to Debug Performance Issues
author:
  - Louis Zawadzki
video: AWnLonnZNBo
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/AWnLonnZNBo.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/react-native-connection-23/louis-zawadzki-using-a-scientific-approach-to-debug-performance-issues/slides.pdf
tags: []
year: 2023
conference: react-native-connection
edition: 2023
allow_ads: false
---

So my name is Louis.

And today, I want to talk to you about how we can solve performance issues with a scientific approach.

So to start with, a little bit about myself.

I used to build React Native applications for a few years at BAM.

And about a year ago, I joined Datadog.

So for those of you who don't know what Datadog is,

Basically, it's a platform that enables you to have observability across all of your system, and that includes your React Native application.

And that's what I work on.

I'm building the React Native library for Datadog.

And so after I joined, I was asked, how can we improve performance tracking for React Native applications?

And so I thought, well, what would I do if I had a performance issue, and how could I improve that process?

So let's say I have this very simple app that you can see here, $0.99 on the App Store.

So it's very simple.

It's a Hacker News clone.

We have two buttons on top where you can order the stories, either by top score or by date.

And as you can see right now, it's not very fluid.

We can see it takes about one second when we click on a button to update the content.

So definitely there's some performance issue here.

So what would I do in that case?

So I would probably go to Google, type React Native performance issue, and I would find some documentation, some blog posts, some articles, some tools that enable you to monitor your performance, some conferences.

But the problem is you have a performance issue to solve right now.

And so you don't have the time to implement everything that's explained in these articles, in these blog posts, and you probably don't have time to watch all these conferences.

But this time, I had the time to watch all of this and to read all of this.

And so I started to put things together once again.

And this is what my screen looked like at one point.

And I started to make connections between things.

And I realized there's something that's very valuable, actually, that I could use to improve my performance debugging.

It's that 99% of performance issues come from 25 causes.

So obviously, those figures are not totally correct.

But to get the idea, it's not like when you have a bug, where the issues can come from hundreds of different reasons.

Most of the times, it comes from a very small list of causes.

So today, I won't go through the list of causes.

I will share them with you at the end of the talk.

Instead, I want to show you how you can use a scientific approach and this list to solve your performance issues much faster.

So what happens when you have this performance issue?

You don't actually know what's the cause of your issue.

But you know, you have some data, and this data, I call it symptoms.

Because it's a bit like when you go to see a doctor.

You don't say, "Hi, doctor, I have a triple fracture on my tibia."

You say, "My leg hurts, I'm in pain."

Actors to you.

And this is kind of the same thing here.

And from that data, these symptoms, your doctor will probably identify a few possible causes.

Maybe it's a fracture, maybe it's something else, and it's the same for us.

We can look from the symptoms that we have, what potential causes can we have.

And then we have documentation on which tool we can use to validate those causes.

So same thing, your doctor will send you to do an x-ray or an MRI of your leg to figure out what's going on.

And once we have identified the right causes, we can look at documented fixes, and we can fix our problems.

OK, that's very theoretical, so let's apply that to our examples that I showed earlier.

So first, we start by observing symptoms.

So what symptoms do we have, really, for React Native?

So we have a few of them.

So I will go with two simple ones.

The first one is the UI frame rate of your application.

So that's the frame rate of the thread that's responsible for rendering your native application.

And the second one is the JavaScript frame rate.

So that's the frame rate of the thread that's handling all your JavaScript code execution.

So if any of this frame rate is dropping, your user will start to notice it, and your app will feel a bit laggy.

And so depending on which one of these frame rates is impacted, you will have different causes.

So how do you show that in your app?

Probably the simplest way is to use the PerfMonitor on your emulator.

So here, I can see that with my application, my UI thread stays around 60 FPS.

But my JavaScript thread has a frame rate that's dropping.

So I know it's coming from the JavaScript thread.

Now, you might be thinking, OK, I know with performance issues,

It's better to look at things in production.

So I encourage you to use observability.

So obviously here, I'm going to use Datadog.

But there are many other services, like Sentry, Firebase.

They all have performance monitoring for React Native.

And here, you can see, for instance, that when I click on the two buttons,

I have something that's called a JavaScript long task.

So a long task is basically a chunk of JavaScript code that's taking a while to execute and that blocks the thread.

So here, we can see that we have four long tasks.

OK, so now that we have this data, we can look at our list of causes.

And I select three potential causes for this problem.

The first one, I call it large selectors.

So it's when you're selecting data from a data store, and the formatting and selecting this data, getting it, is taking a lot of time to execute.

Second one is too many renders.

So I'm rendering too many components that are not actually displayed on the screen.

And finally, useless renders.

So it's a bit different.

This time, I'm rendering components, even though they didn't change, and that could be avoided.

So now I need to select one of these causes.

So I go through my code, and this is the code for my selector.

So you don't need to understand everything that's going on here.

I'm using Redux, and as you probably can see,

I'm getting a list of ideas and doing a map.

This is other ideas.

Then I'm looking at the list of stories.

I'm doing a find, then a filter, then a map, and I have 500 items.

So I'm looking.

Maybe this is not very optimized, right?

Maybe that's a cause of my issue.

So I want to check that, if that's the real cause of my issue.

So how would I do that?

I would run an experiment.

So what's an experiment?

This is where the scientific method can help us a bit.

To describe it very simply, we need at least two things.

First, a protocol.

So what am I going to do?

So here I'm going to click on a button and observe the execution time with console.log.

And then expectations.

So in which case do I figure if it's the root cause for my performance problem?

So here I expect my execution time to be over 400 milliseconds.

This might seem a bit trivial, but I'm sure we've all been there looking at our debugger, trying to figure things out, or to expect to see something to miraculously show up.

So having this in mind will save you a lot of time.

So let's run the experiment.

So this is the same code from my selector.

At the start, I get the timestamp.

I've toggled the actual code.

And then at the end, I get this timestamp and I print the difference.

And this is what I see.

So I see selector time 49, selector time 35.

So these numbers are in milliseconds.

So it's still significant, but it means it's not the only root cause for my performance issue.

Something that's interesting, I only clicked once on a button and I got two logs.

So I'm thinking, OK, maybe large selectors is not the only issue.

Maybe I have some user's renders.

And actually, it's the same experiment to validate too many renders.

We're going to use our beloved Flipper and the React DevTools and to see what happens.

And so same protocol.

Again, I click on the button, and I see what happens in the frame graph.

And this is what I see.

So here, what's important to see?

First of all, I see that my Stories component-- so that's a top-level element of my page-- has a self-render time of 30 milliseconds.

And that's about the time it takes for my selector to run.

So I'm thinking this is probably my selector time.

So I've already identified what this is.

Then I see that my score view is rendering a lot of components.

So if you remember in my application,

I only see maybe 10 items in my list.

Here I have more than 80 components.

So I definitely am rendering too many components.

And then we can see that even though I clicked once on the button, I have two render phases.

So definitely, again, we have some useless renders.

So now that we have identified the causes for our problems, we can apply the fix.

So here, I would look at my list that I've done with-- in which I have written the fixes for each problem.

And so for large selectors, for instance,

I can change the data format so it's faster to query data.

For the too many renders, I can optimize the flat list

So it doesn't render as many components when it mounts.

And for the useless renders, I can use React.memo on my component so they don't render again if the props haven't changed.

Last step, we need to check the improvements.

So we can do that very simply again, just looking at our application.

So this is what we had before.

And if we look at it now, it is a bit better.

So now it's a bit more reactive, but it still feels like something's slightly off.

And again, it's very hard to tell if you test on your phone only.

So once again, what's going to save you?

Observability.

So looking at what we had before, we had four long tasks when clicking on the two buttons.

And now we still have one long task remaining.

So we know that we've improved things, but still not perfect.

So we can still improve things a bit.

All right, I'll stop here for the example.

And let's recap a bit before wrapping it up.

So if you want to try a scientific approach solve your performance issues, five steps. The first one is to add observability so that you're ready when you face a performance issue. When that happens, you can observe the symptoms to select the causes. Then when you've selected the causes, you run experiments to validate which ones are really impactful. And once you've done that, you can fix the found causes with the documentation that you have found. And finally, you check the improvements. Okay, so as I promised you,

All of this is not worth anything if you don't have the list of causes.

So I've created a notion space from my research where you can have the list of causes.

They are classified by symptoms and categories of types of issues.

And you can download them by scanning the QR code.

So I encourage you to try it out.

Give me some feedback if you think it can be improved or if you think another format would be also helpful.

And I thank you very much for your attention and your time.

[APPLAUSE]
