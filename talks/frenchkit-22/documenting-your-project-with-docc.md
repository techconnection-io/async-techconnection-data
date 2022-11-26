---
slug: "/talks/frenchkit-2022/simon-b-stovring-documenting-your-project-with-docc"
date: "2022-09-30"
title: "Documenting Your Project With DocC"
author: "Simon B. Støvring"
video: paR2INQMc3s
thumbnail: thumbnails/simon.jpg
slides: downloads/documenting-your-project-with-docc.pdf
tags: ["DocC"]
year: 2022
conference: frenchkit
edition: "2022"
allow_ads: true
---

0:00:33.9 Simon B. Støvring: Bonjour or bonsoir, I never know which one to use. Yeah. Well, my name is Simon and I've been doing iPhone development or iOS development since the iPhone 3GS, so that's around 13 years or so. And today I'm here to talk to you about documenting your project with DocC, DocC being the keyword here. That's what we'll dive into over the next 10 minutes or so. And I should note that this is a lightning talk, we only have 10 minutes. So some of it will be a little fast-paced, there will be some, "blink and you missed it", moments. So yeah, sit tight.

0:01:08.0 SBS: Let's rewind time a bit. This is me about 2 years ago, and I had started developing my open-source framework called [Runestone](https://github.com/simonbs/Runestone). Runestone is an open source Swift package for building performance text editors for iOS. Yeah, notice the two cups of coffee, must have been a rough day. And Runestone is written in Swift and I finished the development around May. And I should note, I will use Runestone, my own source package, as an example throughout this presentation, but everything we are talking about today also applies to your internal frameworks and even entire apps. You can document anything with DocC.

0:01:51.7 SBS: Now, when I finished the development of Runestone in May, I asked myself a question, "How can I document my project?" I had an open-source project, and if I want anyone to adopt this it's important that I provide them with the material they need in order to adopt it. And for an open-source project like Runestone, that's great documentation. So yeah, I asked myself the question, "How can I document my project?" And the documentation that I've spent the most time with is Apple's documentation. And Apple is documenting Swift frameworks, amongst others, and I have a Swift framework, so it's only natural to look to them for guidance. And as you all know, Apple has great documentation. Look at this PDF of `SCNAnimation`, I mean, it lists all the initializers, it lists all the instance, properties and that's about it.

0:02:44.9 SBS: This is not documented, this is just a list of symbols. Yeah, but actually, this is fine because Apple's documentation isn't that bad. I know we like to laugh at their documentation now and then, and some of you might have seen this, "No overview available" project that was trending a few years ago. Apple's documentation is actually quite great. Look at this example of WidgetKit. On the left hand side, you have a table of contents showing all the symbols in this documentation, showing all the articles and so on. In the bottom, you can search. Apple even has a summary of the framework in the top, it shows API availability. There's a longer description, there's a note here that catches the user's attention, and I guess says something important about this framework. And there's even a graphic. Now, if we scroll down a bit, we have the same list of symbols as we had on the `SCNAnimation`, or we have a similar list, at least, but this time it's actually documented. There are these small summaries below each type. And if we select one of those, we even get a code snippet that we can copy from the documentation and into our project and get started using this.

0:03:58.1 SBS: Apple's documentation is great... When it exists, that is. So that's when I remembered DocC. We can actually make documentation that looks and feels similar to Apple's. And that's when I remembered that this photo has some strong Nickelback vibes.

But as I was saying, Let's take a dive into DocC. DocC is a documentation compiler built and maintained by Apple, and it was introduced in 2021 as a replacement for the old HeaderDoc tool that we used for documenting our Objective-C code. Some of the dinosaurs might remember this. Yeah, and DocC builds documentation that looks and feels similar to Apple's. And that's super-important here because when we are documenting our project, this is a great benefit because many of the people we are working with are used to using Apple's documentation. You just can't get around that.

0:04:57.4 SBS: DocC basically works in this way. It takes some Swift files, some Markdown files, and some resources as input, compiles the thing and outputs a DocC archive. Now a DocC archive is really just a website and that's gonna become handy in just a couple of minutes. That means the DocC archive contains a bunch of HTML files, some style sheets, and the resources that you are provided as input. Your Swift files documents the symbols that is your properties, your functions, protocols, other types you might have. And it does that in comments within the source code. The Markdown files, they provide structure to your documentation. That means these Markdown files specify how the documentation is presented to our users. The Markdown file is also used for articles and tutorials. So in summary, Swift, Markdown and resources go in, documentation comes out.

0:06:01.7 SBS: Let's take a look at an example of documenting a function using DocC. We have this function called `search`, it takes a single parameter as input, query, and it returns a list of search results. Now, if we run this function through DocC, generate the documentation for it, we get this. This is not much better than the documentation we saw previously of `SCNAnimation`. It lists the function name and we see the declaration, not that helpful. So let's improve that a bit. We'll start by adding a comment above our function, a summary that DocC will show in specific places. We'll also document the parameter and the return value using this specific syntax. So our parameter is the query that we wish to find matches for, and the return value... Well, that's the results matching that query.

0:06:56.9 SBS: We'll also add a code snippet to our documentation. And remember, we're still inside our Swift source file. And we can use this Markdown and we can add this code snippet using Markdown. So here we are creating a search query and we are passing it to our search function. This helps our users quickly get started using this function. We'll also add a longer description that like describes how or what our code snippet does. Notice this double backtick syntax around search query and search for, that's part of Apple's sprinkles they have added on Markdown. So DocC uses basic Markdown, but with some of Apple's sprinkles on top and this is part of it. So it's like Apple has this dialect of Markdown, so to say. And this double backtick syntax means that when the DocC compiler compiles our code and generates documentation for it, these symbols will turn into links to other places in our documentation.

0:08:01.1 SBS: Lastly, we'll add a note. Remember, we saw a note earlier in the documentation for WidgetKit. We use this syntax with an arrow and write, `> Note:` and then our actual note. And in this case, we're documenting the runtime complexity of our function. And please don't validate this, I don't think this complexity is right. And now if we compile this instead, we actually have great documentation by just having a few lines of comments in our code base. So notice here that we have the longer description of our function under the discussion section, with the links to search query and search for. We have our code snippet that users can copy paste into their own project. And we have a note describing the runtime complexity.

0:08:42.9 SBS: So let's fast forward a bit to a scenario where we have this great documentation for all the symbols in our app. That is all the classes, all the protocols, the properties, and so on. Then we get a landing page that looks like this. This is an output of DocC. Now one thing that comes to or like catches your eye here, is these topics of articles, classes, and if we scroll down a bit, we see protocols. These are headers, these topics group your symbols on the landing page. And if you look at the documentation for something like `FileManager`, you'll see that Apple groups symbols under huge groups ike, "adding and removing files", or "listing contents of a directory", which are much more helpful than this. So let's improve on this a bit.

0:09:36.8 SBS: We'll add a Markdown file with the topics that are relevant for our framework. In this case, we have essential types to get our users started using our framework. We have something for tweaking the appearance of our text view, and we have symbols and types for adjusting the syntax highlighting. Where we have our topics, we can list our symbols under each topic. In this case, one of the essentials is the text view and the text view delegate, and so we'll add those again with this double backtick syntax. And under appearance, you'll find something like theme and fun traits, and so on. Now, if we take our documentation again and we compile it and provide this Markdown file as input, we'll get something that looks like this instead. Now we have headers saying, "Essentials, Appearance, and Syntax highlighting." These are like use cases for our framework. Our users can browse our landing page, scroll down to find the use case they're interested in, and quickly get started.

0:10:40.3 SBS: So let's fast forward a bit again. We can improve this landing page by adding a longer description of our framework with a detailed overview of all of its capabilities. We can add some imagery that catches the eye. And in this case, we're also adding at the bottom of the page that redirects users to the app store where they can actually try a sample app of our framework, for an example app that uses our framework.

0:11:01.9 SBS: We can also add this structure to our specific symbols, to our types. So in this case we have the text view, and notice we have topics underneath saying, "Initializing the text view" and, "Responding to text view changes", and so on. That structure that's applied to the documentation. We can also write articles. These are just plain Markdown files. Some of you might already be writing articles in Markdown. And of course we can add code snippets and so on. And an example of an article could be an article that helps our users get started using our framework, but we can actually do better than that. We can add an interactive tutorial using Apple's dialect of Markdown that guides our users step by step through setting up our framework and creating the first text view and so on.

0:11:56.4 SBS: Now, unfortunately, we don't have time to dive deep into this in this lightning talk, so if you want to learn more about this join the classroom tomorrow at 9:30. So now we have our great documentation and the next natural question to ask ourselves is, "How can people read our documentation?" One thing is having documentation, but if it's not available to our users, then it doesn't really matter, right? Well, fortunately that's quite easy. Anyone that depends on our framework, our Swift package in their project, can go up and select, Product, Build Documentation, and that'll present them with this window, that's Xcode's developer documentation window. You might have seen this already when browsing documentation for HealthKit, WidgetKit, WeatherKit, UIKit and so on. And now the documentation for our framework lives as a first class citizen within the documentation for the other frameworks. Remember I mentioned that DocC really just outputs a website. Well, that's super handy because that means we can just host it as a website.

0:12:55.1 SBS: So I have a setup where Netlify monitors some changes in a Git repository that contains my Swift package. And whenever it see changes, it builds the website, aesthetic side, and then it hosts it on docs.runestone.app. So now my documentation is available online. So to summarize, Swift, Markdown and resources are provided as input and DocC generates a DocC archive. And that archive can be browsed in Xcode and online. And if you're building an open-source package, [Swift Package Index](https://swiftpackageindex.com/) will even be able to host this documentation for you. So I'm not here to say that you should document your projects. I'm here to say that it has never been easier to make great documentation that looks and feels similar to Apple's. So maybe you should document your projects.

0:13:51.1 SBS: Now, we only had 10 minutes and we've only covered the tip of the iceberg. So if you'd like to learn more about this, I think you should join the classroom tomorrow where we'll be working with this example project for creating and customizing these characters. Yeah. So to summarize, if you want to get your paws dirty, join the classroom tomorrow at 9:30. That's it.

[applause]

0:14:22.4 Greg: Thank you Simon.

0:14:22.8 SBS: Sure.

0:14:22.9 Simone: So do you have a classroom about this?

0:14:28.7 SBS: Yes, I do. [chuckle]

0:14:30.3 Greg: Is it tomorrow at 9:30?

0:14:33.5 SBS: Yeah, it is. [chuckle]

0:14:35.2 Greg: I think the message is clear.

0:14:36.6 SBS: Yeah, the message is clear. Yeah.

0:14:40.9 Simone: I have a question for you. What's the limit for classrooms? How many people?

0:14:47.3 SBS: I've heard it's 30.

0:14:48.7 Simone: Yeah, that's a good answer. Thank you. I might have questions, when we talk about documentation. What should you include, and what you must include, in your opinion, in documentation?

0:15:03.1 SBS: Well, you should have documentation for your entire public interface, I think. And I think the key things to great documentation, in my opinion, are these summaries and code snippets. I think code snippets is a great way to document your project because it really helps people get started quickly and it can show the relation between maybe a function and a type, as we just saw in the example here, where we created the search query and passed it to search for. Yeah, and then of course, I think it should also contain some article or interactive tutorial that helps users get started, provide a starting point.

0:15:41.9 Greg: Question, but not for you, for the audience. Can we have a bit of light for the audience, please? Who tried DocC yet? Really a few people...

0:15:51.3 SBS: Alright, a few.

0:15:51.3 Greg: More trollish question, Who writes documentation? Not that much. Not that much. Okay. Thank you.

0:16:04.5 Simone: A question from the audience. Can you ensure your code samples are always compiling as you update your frameworks?

0:16:13.5 SBS: I don't think DocC provides any functionality to verify this, but I suppose one way is to ensure that everything that you have in your documentation, any code snippet you have, you also... You might have a unit test for it and you might not be testing anything that this compiles. There are ways to get around, I think.

0:16:32.9 Simonne: And so that's basically all. Anybody who might have additional questions you know where to go tomorrow morning.

0:16:47.1 SBS: Yeah. Sure. Oh, and I should mention I have stickers as well.

0:16:50.4 Greg: Oh yes!

[applause]
