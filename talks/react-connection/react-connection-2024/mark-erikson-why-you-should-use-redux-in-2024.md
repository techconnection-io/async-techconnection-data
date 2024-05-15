---
slug: >-
  /talks/react-connection/react-connection-2024/mark-erikson-why-you-should-use-redux-in-2024
date: '2024-04-22'
title: Why You Should Use Redux in 2024
author: Mark Erikson
video: CSPU67v7yTQ
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/CSPU67v7yTQ.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: react-connection-2024
allow_ads: false
---
[Mark]
My name is Mark Erikson, and today I'm very happy to talk to you about why you should at least consider using Redux today. A couple of quick things about myself. Cool.

Clicker actually works. I am a senior front-end engineer at Replay.io, where we are building a time-traveling debugger for JavaScript. It is an amazing tool.

It's incredibly powerful technically. It will also save you a lot of time, both debugging bugs and fixing flaky tests. If you haven't heard about it, please try it out.

Come ask me questions. I'm very happy to talk about it. I am an answerer of questions.

I will happily answer questions pretty much anywhere there's a text box on the Internet. I collect all kinds of useful and interesting-looking links. I am a writer of extremely long blog posts, and I am a Redux maintainer.

Fun fact, Dan Abramoff only worked on Redux for one year, and then he handed it off to me in 2016, so I've been doing this thing for about eight years now. But most people know me as that guy with the Simpsons avatar. So why are we even having this talk anyway?

Historically, we maintainers have really not spent any real time trying to market or encourage people to use Redux. Instead, we've actually spent most of our time telling people when they shouldn't use Redux at all. And a lot of that is because Redux has been really overused.

Especially in the 2016-2017 era, people were putting in Redux in a lot of places it never should have been at all. So our goal as maintainers is not to, like, get Redux more market share. We just want Redux to be a very good tool so that if you choose to use it, it works very well for you.

But we still see questions all the time of, when should I use Redux, or how does Redux actually compare to this other tool? So I actually kind of got, like, convinced to do this talk. So I've spent most of my time answering these other questions.

This is actually the first time I've tried to give a talk that actually kind of, like, says, like, here's why it's worth actually trying Redux. So this is a little bit different for me. So the goals for today.

We're going to start with a bit of a history lesson and go back and look at why Redux was actually created and what was its purpose? What problems was it meant to solve? We'll talk some about how both Redux and the React ecosystem have evolved over time.

We'll look at some of the tradeoffs involved if you actually do use Redux. And then, yes, we will actually talk about some good reasons why you might want to use Redux today. Now, I've already got less than 20 minutes, and I already talk in too much detail anyway.

I'm not going to compare Redux to any other tools. I'm not going to dive into specific technical details. This is more of, like, an abstract marketing talk, I guess.

But I'm very happy to answer those sorts of questions later. So I am a really big believer in understanding history. Why were tools created?

What was going on in ecosystem? What were the influences on these tools at the time? So jumping in the way back, Machine, for those of you who weren't around at the time, React came out in 2013.

And a year later, Facebook came back, and they said, we've been using React internally for a while, and we've run into issues with client-side state management. The infamous problem of the notification counts aren't staying in sync between different parts of the page. And back then, it was very common to use libraries like Backbone to manage your data on the client, and these were based on event emitters.

And sometimes you'd change a piece of data in one place, and 20 different events would ricochet across the app, and it was very hard to keep track of what will actually change when I update this piece of state. So Facebook came out with what they called the Flux Architecture, and the idea was if we centralize the state management and we make this consistent one-way data flow, it's going to be more understandable to track when, where, why, and how things are getting changed. Now Facebook didn't release an entire library behind Flux, it was a little more of an idea with a couple of helper utilities.

And ultimately, most of Redux's design decisions and naming patterns come directly from this Flux Architecture concept. This unfortunately led to a period that I refer to as the Flux Wars. Between 2014 and 2015, 50, 60, dozens of different Flux libraries all came out, most of which had names based on Back to the Future jokes.

And during that time, Dan Abramov was getting involved with the React community, and he began to write about why Flux made sense as an architecture. So big picture, Flux was designed to solve client-side state management, maybe including fetching data from the server, and overall make it easier to understand how state gets updated in your application. So in May of 2015, Dan began to work on his own Flux library.

He wrote a post called The Evolution of Flux Frameworks, and he began to work on the library that would become Redux. And I copy-pasted some of the initial goals that were in the readme at the time. And it had things like everything about Redux should be hot reloadable.

You should be able to make a change, have the code update, and not have to reload the entire page from scratch. You ought to be able to update to individual pieces of state that your component needs. It ought to enable dev tools for understanding what's going on inside the code.

And it should be extendable. Now a couple years later, I wrote a couple blog posts that looked back at the original creation, and I tried to kind of expand on these themes. What were Dan and Andrew thinking as they worked on this?

So Redux was really just another Flux architecture library, but the overall goal is it should help you maintain your state update logic. And in doing so, these actions should have a semantic history. You should be able to read descriptions of the user did this, the user did that, and kind of understand what was going on in the app.

It was based on functional programming principles like immutability. It's designed to make more of your code testable, and we want you to be very explicit about how data gets updated in the program. Along with that, it had a few opinions.

You should organize the update logic and the data by specific areas of the code. The core should be pretty small, but it should be extensible. So Redux itself was basically created in a two-month period in the summer of 2015.

And Dan and Andrew iterated very quickly through design ideas and settled on what we now know today as Redux. Dan had his famous talk at React Europe 2015, where he first demoed it. The 1.0 version came out the next month, and over the course of the next year, as React was getting very popular, Redux basically killed off all the other Flux libraries. And pretty soon, people began to assume that if you're using React, you have to be using Redux as well. Now, I took over Redux in 2016, and Redux itself has changed significantly over the last several years. There was about a three-year period where we rewrote the internals of the React Redux library multiple times.

We tried to improve performance. We switched over to using modern React context to try to work better with future React changes. And then this hooks concept got announced.

So we reworked the internals of our API to use hooks internally, and then we published our own hooks API as well. And so ever since 2019, we've had this hooks API as the default way to use Redux with React. But over the years, there's been a lot of complaints about Redux.

Things like, I have to touch five different files just to make one change, or there's too much boilerplate involved. And we want our users to have a good experience. So in 2019, we released a package called Redux Toolkit, which is a wrapper around the original Redux core that includes APIs that make it a lot easier to use Redux.

A year later, I rewrote our tutorials to teach Redux Toolkit as the default way to use it. And in fact, in 2022, I marked the original Redux create store method as deprecated in the documentation tag. It still works.

Nothing breaks. But we wanted users to see, like, the little strikethrough that says, don't use this. Use Redux Toolkit instead.

And I still have people yelling at me because of that decision. So last year, we put out Redux Toolkit version 2, which modernizes the packaging and has better ESM support and improves some of the APIs. So while the core ideas of Redux haven't changed, the way we use Redux today has changed significantly.

So why did people even choose to use Redux in the first place? Like, what were the reasons people were using it back in 2015 and 16? Some of the reasons are very historical.

The old React context API was actually very broken. You couldn't pass new values down through it consistently. And so a lot of people used Redux to get around that.

The React community was really big on this idea of flux libraries, and Redux was the best flux implementation. At the time, you could hot reload components, but they wouldn't maintain state the way that the current React fast refresh loader does. And then, of course, it's all about the thought leaders.

Like, you know, it's either your senior developer has already chosen to use Redux, so you don't have much of a choice, or, you know, people on Twitter are saying you should be using Redux. But along with that, there was a lot about the architecture. React is kind of based on functional programming principles, and so Redux uses functional programming as well.

Those went together. React has, you know, your state is based on your component tree. Components pass data to the children, but sometimes your state isn't always shaped that way.

And in general, Redux is about moving state and logic out of the component tree. Sometimes that's good, sometimes it's bad, but this is a useful pattern to have. It was also about predictability.

So there's a very consistent data flow pattern. All the state logic gets centralized to trigger it, the UI dispatches an action. It also made it very easy to test pieces of your code, like the reducers.

And finally, yes, time travel debugging and the Redux dev tools are a really big deal. So which of these still makes sense today? It turns out that most of those historical reasons are gone.

Modern context works great. Nobody remembers that flux was even a thing. Modern hot loading works great.

But the architectural and predictability principles are still the same. These are still things you would care about in an application. Now the React ecosystem has changed a lot.

Back in 2015, everybody was focused on client-side state management. And instead, we've seen a shift to thinking about fetching and caching data from the server. And we've seen a lot of very good tools created to work with this.

Apollo Client for GraphQL, React Query for various other data fetching. There's also been a lot of shift in how people think about Redux. Every tool follows what is like the S-shaped adoption curve.

It comes out. People get really excited about it. And then they find out there's actually all these pain points.

And eventually, you kind of settle into, okay, we know the things this tool's good at. We know where it has problems. And there were a lot of problems with the early Redux usage patterns.

So, you know, the boilerplate, frankly, came straight from some of the documentation and some of the design choices. And in general, the ecosystem has a lot more tools and choices. We've shifted from talking about single-page applications to server-side rendering and multiple pages.

We've got a lot of choices around how we do the data fetching. There's other libraries like Jotai and Zustand and, you know, all these other tools that give us more options for managing state. And there's a lot of tools that focus on data fetching.

So the React ecosystem today is very different than it was in 2015. As I mentioned, Redux has changed as well. We went from the original tiny Redux core library to Redux Toolkit, which provides built-in solutions for most of the standard things that Redux devs need to do.

And as part of that, it includes our RTK query data fetching library. It's very similar to React query conceptually, but it's built on top of a Redux store and works great with the rest of the Redux ecosystem. React Redux has changed.

While the old Connect API still exists, today we teach the Hooks API as the default. It's much simpler, a lot easier to understand, and works better with TypeScript. And Redux early on was very unopinionated.

It's like, eh, organize your files however you want, name your action types however you want, we don't care, pick and choose, it's up to you. And this was great to get the ecosystem off the ground, but we've seen people try to solve the same problems over and over. So we've tried to start providing actual opinions and guidance, organize APIs in a way that gives you a consistent structure, and try to make Redux projects more consistent and similar.

So one of the things I've learned as I've gone in my career is that the further you go, the more you use the word trade-offs. Everything has trade-offs, nothing's perfect. And Dan said early on that Redux is designed to answer the question, how is your state going to update when something happens?

It's not going to be the shortest amount of code, it's not going to be the absolute fastest performance, but we want to make things predictable and understandable. So what are some of the trade-offs of using Redux? Redux adds a layer of indirection.

You have to dispatch an action instead of just updating a state field directly. This is more lines of code. You have to look at a couple extra files, but it does scale better as the application gets larger.

So you add a little more verbosity, but you get consistent behavior no matter how big the application is. If you move all the logic into a single store, you know where all the state is. You can look at it all in one place.

You can see the history in the dev tools. It's easier to log what happened to it over time. This can be abused.

The early Redux docs talked about like having a single centralized state. The somewhat intentional implication there was you should literally put everything in your app in Redux. That was kind of overstated.

So like today we emphasize like the global state portion of it. Putting form state in Redux is really not a good idea. Please don't do that.

And it can be harder to access the state in files that aren't related to React. The idea of updating your state via reducers. Reducers are pure functions.

They're predictable. They're easy to test. But sometimes trying to write that logic as reducers and slices can be a little more awkward than other approaches.

Prior to Redux toolkit, it was very easy to make mistakes doing immutable updates. Accidental mutations were by far the number one common bug in Redux apps. Fortunately, with Redux toolkit, those problems have gone away.

Finally, Redux wants you to manage your state as plain JS objects. Now, this goes very well with React. That's how React wants you to do things as well.

This makes things like the dev tools possible. There are times when it might be a little easier to do things with maps and sets. And you're really not supposed to use those with Redux or React.

So the actual sales pitch time. Why would you consider using Redux today? Now, in some ways, I'm actually a little too reasonable.

It is very hard for me to stand up here and say, you should use Redux. Like, I can't make myself do that because I know the tradeoffs and because I know that there are many other good tools out there. But if you want a list of reasons why you should consider Redux as a possible option today, this would be my list of reasons.

One is that it gives you a good, consistent architectural pattern. There is value in moving logic out of the UI layer, in centralizing the behavior and having the UI focus on just saying, here's a thing that happened, all the state updates go there. It does make it easier to understand what's happened, both because of the history aspect of dispatching actions and seeing what changed in the Redux dev tools.

It is very widely used, much like React itself. This is admittedly the nobody ever got fired for choosing IBM argument, you should use this thing just because it's popular. It's not a great argument, but it is a legitimate thing to consider.

Many people know Redux. It's widely understood. It's not like, you know, some guy's side project that has three stars on GitHub.

It is very well documented. We, and by we, I actually mostly mean me, have spent a lot of time working on the tutorials and the documentation and explaining concepts. There is a lot of good information about how to use Redux.

It currently has better update performance than React context. There's been discussion of React adding a context selectors concept to improve performance, and it sounds like they finally have some ideas for how they're going to do that. That still doesn't exist yet.

But at the moment, it's easier to make just a few components update when needed. Redux toolkit has a lot of tools built into it. We've seen the things people do when they build Redux apps.

We know what kinds of problems they need to solve. And Redux toolkits provide things that you can pick and choose that will help solve most of those common problems. One of those includes data fetching.

It turns out that when we talk about side effects in applications, it's basically just I want to fetch data from the server. And so we've got the RTK query piece of Redux toolkit, which makes it really straightforward to fetch data from an API. It works really well with TypeScript.

We love TypeScript. We think everybody who uses Redux should use TypeScript. Before Redux toolkit, trying to use Redux in TypeScript was really, really hard.

And so we've put a lot of work into Redux toolkit's TypeScript types so that you can use it in a very simple way. And finally, even though most people using Redux are using it with React, Redux has always been UI agnostic. It works anywhere.

You can run JavaScript on the server, on the client, in, I don't know, some embedded device somewhere. And so there are times that that is still a valuable thing. So this is not supposed to be a you must use Redux set of arguments.

Frankly, I could give a list of reasons why you shouldn't use it. I could give a list of reasons why Jotai or Zuestend are very good tools in some cases. But the bottom line is Redux still works great.

It is still a very valuable tool. And there are a lot of good reasons to consider using it beyond just, well, yeah, my company has 15 projects that have it, and I guess we should still keep using it. It is still a tool with a lot of value, and there are good reasons to consider using Redux today.

So thank you very much. I've got a list of links here. And I will have the slides up on my blog sometime later today.

Thank you.

[Christophe]
Thank you, Mark. Let's just convene over. Please take the center seat.

How was that? Who here uses Redux? That's too few of you.

So full disclaimer, I'm a big Redux fan. I've always been. And actually, in terms of TypeScript, moving to RTK in, yeah, please take a seat.

Moving to RTK in my training material. because we shifted over to TypeScript, and yes, indeed, manually typing vanilla Redux was a pain. It was like a lot of boilerplate.

[Mark]
It was really bad. People would write action types in a JS file, and then they would write TS types for the action types, and then they would write TS types for the objects.

[Christophe]
It was so bad. It was so bad. It was kind of a mess.

So bad. I know. I wanted inference.

So yeah. Okay. So do you want to start with questions?

Probably have, like, good questions from the audience.

[Romain]
Three questions. So if you have to write Redux from scratch today, what kind of change would you do?

[Mark]
It's funny, because so much of what we did with Redux Toolkit was based on both seeing how people used Redux and seeing the other, like, the community extension libraries that they had built to try to solve standard problems. Between 2015 and 2018, I used to keep a running list of every Redux-related library.

[Christophe]
The ecosystem links? Yeah.

[Mark]
And, like, there were so many... It's a book. There were so many libraries that people had, like, 50 libraries that all solved the same problem.

And so, like, certainly if I could go back with the knowledge we have now, like, we'd basically just recreate Redux Toolkit, but we couldn't have created Redux Toolkit without knowing what people were doing with Redux, and, frankly, also, we couldn't have done it without the invention of Ymir.

[Christophe]
Yeah. Yeah. Shout out to Michel.

Ymir is awesome. Yeah. Ymir is great, really.

I really liked when Ymir came in, because, especially when you have, like, a deep, deeply nested update, it's very easy to get it wrong.

[Mark]
Dot, dot, dot, state, dot, dot, dot, state, dot, dot, dot, dot, dot, dot, dot, dot.

[Christophe]
And arrays. And arrays. And before we had the with helpers or something, you would have to do some crazy concat stuff with arrays.

Yeah. Yeah. For sure.

Okay. This one thing, do you have any idea what the usage ratios are between, like, just RTK and RTK query? You know, what would you describe as, like, the sweet spot in terms of project or team for actually using RTK query?

[Mark]
So I don't have hard numbers for how many, like, I can look at NPM downloads and see, like, here's the total number of Redux downloads versus the number of Redux toolkit downloads. And Redux toolkit depends on Redux. So the overlap is kind of like this.

Because RTK query is part of the Redux toolkit package, like, I can't explicitly break out those numbers. I can do searches on GitHub and see how many imports and usages of create API exist. I can say that anecdotally between looking at what issues get filed in our repo and the kinds of questions we get asked in our Discord channel, a lot of people using Redux are using RTK query, which is good.

That's what we want to encourage. We currently have something like 150 open issues that either are asking for new features or tweaks or wanting us to improve the code generator tools for RTK query. So based on those anecdotal statistics, it seems to be a pretty good percentage.

[Christophe]
Cool.

[Romain]
So I have two questions about the evolution of Redux and Redux toolkit. How do you stay creative about what needs to be done? And also, how do you gather inputs from the Redux community?

[Mark]
So we have always kept an eye on, you know, like, what are people doing with Redux? What kind of questions are they asking? What kinds of problems are they trying to solve?

And if you go back and you look at the history of Redux toolkit releases, we got the initial version out the door with create reducer, configure store, create slice. Those solved the basic principle of, you know, setting up a Redux app. And then it's, well, people do data fetching in thunks.

That's hard. Let's make create async thunk. And then, okay, data fetching is still hard.

Let's make RTK query. We don't like sagas and observables are really hard and complicated. Can we come up with a simpler option?

You made the listener middleware. So it's just sort of been like a what is sort of like the next obvious remaining problem that people have that we would like to solve? We absolutely have taken in lots of input over the years.

I've written some articles that recapped, like, when we created a Redux toolkit or the listener middleware or the hooks API, like, what happened? Like, you know, maybe I had an initial idea. Someone else wrote the proof of concept.

There were debates over the exact shape and behavior of the API. The React Redux hooks API in particular had multiple comment threads that were like 300 comments long. That was like trying to herd cats.

Yeah.

[Christophe]
But it's mostly because of, like, the most discussed issues or voted or stuff. Yeah. Yeah, for sure.

Okay. And let's wrap up with this one, and then there's the break, people. What would you say is, like, the single most maybe underrated facet of Redux?

[Mark]
The concept of modeling events as or modeling actions as events and not setters. This is a really subtle concept, because nothing about the code directly changes. You're still writing dispatch with an action and handling it in a reducer, but the mindset of the UI just says here's a thing that occurred with some associated data, and then any part of the app that does care about it can do something with it, versus the mindset of I'm going to dispatch set first name.

Set last name.

[Christophe]
Which is actually bad practice. Right.

[Mark]
And it's like the it's a combination of changing how you name the actions, kind of like a past tense, this happened name, to do added instead of add to do. But then it also results in dispatching fewer actions in a row, thinking of it as a broadcast that anyone can listen to. It's a very subtle thing.

It can be hard to kind of, like, show or explain, but we've tried to encourage people to think that way, because we think it leads to a better app architecture overall.

[Christophe]
It's a lot more maintainable.

[Mark]
Yeah.

[Christophe]
For sure. Yeah. Well, thank you very much, Mark.

Thank you. Everyone, Mark Erikson.