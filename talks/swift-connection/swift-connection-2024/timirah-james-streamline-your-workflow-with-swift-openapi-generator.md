---
slug: >-
  /talks/swift-connection/swift-connection-2024/timirah-james-streamline-your-workflow-with-swift-openapi-generator
date: "2024-09-23"
title: Streamline Your Workflow with Swift OpenAPI Generator
author:
  - Timirah James
video: y__RdURMZys
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/y__RdURMZys.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---

### Timirah

Bonjour, everyone. My name is Timirah James, and I'm a technology evangelist on the Worldwide Developer Relations team at Apple. And I'm also a member of the Swift Contributor Experience Workgroup.

I'm so excited to be here today and talk to you about how we interact with back-end APIs. How many of you are working on an iOS app right now? The entire crowd.

Okay. All right. WatchOS?

Okay. All right. Mac?

VisionOS? Okay. All right.

Awesome. Okay. Now, how many of you call a back-end service in your app?

Most of everyone. Perfect. Perfect.

Okay. Dynamic data is the nature of most apps. If we put our phones on airplane mode right now, a lot of the core functionality of some of our favorite apps would be very limited.

We're talking streaming apps, social media apps, even health-related apps. As developers, networking is something that we all should be thinking about. So today, I'm going to show you how a tool that we released just last year, Swift OpenAPI Generator, can assist in generating all your networking code on both your app and your server side.

So you spend less time focusing on that code and more time focusing on the actual code that your users will interact with. The code that makes your app special. When you're thinking about handling network requests, you've got a lot of things to consider.

You've got to make sure you're making the right request. Like, what's the base URL of the server? What path components make up an API endpoint?

What HTTP methods should you use? And how should you provide your parameters? And these are just some of the questions to consider when you're calling a server API.

A lot of us here are likely familiar with making network calls and parsing data using tools like URL Session. And URL Session is a great way to make network calls, but it's still on you as a developer to create and keep track of all the appropriate requests for your API. So when you find yourself building more complex apps and you need to make hundreds or even thousands of requests to services and build a complex set of API endpoints and parameters, not only do you need to handwrite a ton of code that's repetitive and verbose, you're also responsible for defining and ensuring that the API contract between the client and the server stay in sync.

So this makes this a very manual and error-prone process. And it detracts you from focusing on the core logic of your app. A great solution to this is OpenAPI.

OpenAPI is a standard format used to describe the structure of an API. It allows you to document the behaviors of the API more specifically, like a blueprint. And it describes what requests you can make, what data you need to send, and what you can expect back.

With OpenAPI, you document the service behavior either in YAML or JSON, and these machine-readable formats allow you to benefit from a rich ecosystem of tooling for things like test generation, validation, and interoperability. One thing that OpenAPI is especially known for is tooling to generate interactive documentation, and this allows you to explore and evaluate the API endpoints more directly. But the core motivation of OpenAPI is code generation, and this allows developers to use spec-driven development via what's called an OpenAPI document.

This document serves as a contract detailing all the endpoints, parameters, data models, and behaviors of your API. And what makes this contract so special is that as you modify your API, it's recognized and honored by both the server and the client. Swift OpenAPI generator was built for developers to leverage the familiarity and the features and the performance of Swift and spec-driven development for Swift apps.

It's a package plugin that generates all your networking code and defined behaviors from your OpenAPI document in Swift for both the client and your server side. So what does this mean? This means that by automatically generating the networking code, you no longer have to handwrite or maintain that networking code.

Another benefit is that Swift OpenAPI generator runs at build time. So this means that the generated Swift code is always in sync with the OpenAPI document, and it doesn't need to be committed to your source repository. And since your code is always in sync, it grows and evolves as your API does.

What's powerful about API evolution support is that if you're collaborating with other developers, say, on a development team, or you're an engineering manager and you're onboarding other developers, and let's say someone modifies your API, they add a new endpoint or change the name of it, the compiler will make all parties aware of all the modifications. And it's a great way to keep everyone aware and in tune with what's going on with your API. OK.

I'd like to try something out. I built an app. OK?

It's actually a life-changing app. Thus the pause. This centered around a topic that's very near and dear to my heart.

My hair. Yes, my hair has been pink for 10 consecutive years. Yes.

OK. That deserves a round of applause. But I'm actually thinking about changing it.

Yeah. I said thinking. Thinking about changing it.

So I built this simple randomization app that allows me to simply hit a button to iterate through a couple of emojis with different hair colors to help me decide which one I'll choose next. OK. It looks like purple.

OK. Purple is not too bad. Purple is not a bad look.

But if I wanted to take this life-changing event a little further and let other people vote on which color they'd like the best, this would actually require making a network request, right? So let's extend this app with a server back end and use Swift open API generator to generate the client and server networking code. All right.

So to start off, I'm going to use Swift open API generator to create an API for submitting and fetching my voting results. I'm going to integrate that code within a server to handle the request and conduct it to an iOS client where I'll display the results in my UI. So here's what I need to do to start.

First, I need to create and define an open API document. Then I need to use that document to generate the Swift APIs that I need on both the client and the server side. And once that code is generated, then I'll connect my back end service to my iOS app.

To get started, we need to know that the Swift open API generator plugin expects two input files in your target source directory. The open API document and a plugin configuration file. The plugin configuration is written using a concise YAML schema which specifies the code that the plugin would generate.

In this case, we'll generate types, which are the reusable types derived from the open API document. And then we'll also generate the server stubs to implement our API handlers. Now, let's take a look at the open API document.

In this document, I've named my API voting service. I've listed a base URL for the server and defined a path and request for my API. I defined my results path and a get method named vote results.

The results schema reads that each result returned by the results endpoint is an array of objects. And each object represents the voting results for a specific Memoji. And each Memoji contains two properties.

Memoji ID, which is a string representing the identifier of a Memoji, and count, which is an integer representing the number of votes that is received for that Memoji. Both Memoji ID and count are both required fields, which means they must be present in each object. Okay.

So now our open API document is defined. Next, I'm going to start building my back end service. So there are three elements I'll need.

All right? First, I need to add the correct packages to generate our code. Next, I'll need what's called a transport, which is the integration layer for Swift open API generator that allows the generated code to work with a web framework.

And I'll need a handler. So let's start with our packages. In my package manifest for my server, I've added some dependencies that I'd like to highlight.

I have the generator package plug-in, which generates the code at build time. I have the runtime package, which allows me to make use of the generated code. And for this demo, I'll be using Hummingbird to build my server.

And I've also included the Hummingbird transport for the open API generator. Let's go back so you can catch that. You can use server transports for Vapor and AWS Lambda as well and learn more about the available server transports via the Swift open API generator documentation as seen there.

Perfect. Okay. On to building my server.

In my main function, I created a new Hummingbird application, which I then used to create an open API transport. Then, I created my handler type, which I've named MemojiHandler, and that conforms to the generated Swift protocol. This type will ensure that all of my API operations match my open API document.

In the next line, I use the generated register handler's function to configure and set up the Hummingbird server, and this routes all the documented API endpoints to the functions provided by my handler type. So, that's it. Now that I have all the pieces to get my server up and running, let's take a look at the project in Xcode.

Okay? Here, I have my MemojiHandler, and it's conforming to the generated Swift protocol, API protocol. And this sets up the routing and the server for each of my API operations.

But I just noticed that I have a function for getting our vote results, but I need a function that will actually allow the votes to be submitted. Okay? So, let's add that into my open API document.

So, here's my vote results operation. Let's add another here called submit votes. Okay.

So, that should do it. Let's build. Great.

We have an error. This is expected, because I've added my submit vote operation, and now my handler is incomplete. The compiler is reminding me to conform to the protocol, and I need to provide a function for each of my documented API operations.

And now I'm missing one. So, let's go ahead and add the missing server stub using fixing. All right.

I'm just gonna add some logic here to actually store the vote submissions. Okay. So, let's try building now.

Let's keep an eye on our console to make sure the data is ready to go. Okay. Cool.

So, our server is now up and running, and it's listening on localhost. Yeah. Okay.

All right. So, now we're ready to connect it to our iOS client and actually get some data flowing. Okay.

Let's get that going. So, here's my iOS client. First thing I like to point out on the left in my project navigator is that I've added both the open API document and the configuration file, just as I did in my server project.

Except if I go into my configuration file, you can see here that I've updated it to specify that I need the code to be generated for the client. I also went ahead and added all the necessary packages to operate with Swift open API generator. Okay.

So, I've added my Swift open API generator package plugin, the Swift open API runtime, and then since this is an iOS app, I've gone ahead and added the URL session transport package. It was also necessary for me to configure the target to use the open API generator plugin. So, I did this in target settings, build phases, and in the run build tool plugin section, I've added the open API generator here.

Okay. So, getting started in my Memoji hair pull app file I have here, my first order of business was to configure our client. So, let's draw our attention to these few lines of code right here.

And this client type is defined by open API, and it requires us to define which server we should use as well as the transport, which in this case is URL session transport. Okay? So, now that we've configured our client, we need to write functions.

Let's get our functions up and going to submit and fetch our voting results for our corresponding Memojis. So, let's go into my custom Memoji view. All right?

So, each listed Memoji will have its own matching button for the user to go ahead and submit their votes. So, I need to add a function that will allow us to do that and perform our submit vote operation. So, let's add that function in an extension of Memoji view at the very bottom.

Okay. All right. Okay.

So, now I've added a submit vote function that allows the client to make a network request for a specific Memoji. So, now we need to call this function when the user taps to vote. All right.

So, now we have our logic for how the votes will be submitted. Now we need to write a function to fetch our vote results. Okay?

And so, we can update our UI to map our corresponding votes to the Memoji. Okay? So, I'll do that here in my results view file.

Here, I just have a full list view of each Memoji. And we just need to add a function to go ahead and fetch those results. So, let's go ahead and add this at the bottom here.

And voila. With this one function, we've made an API call that has type safe accessors for the response status and body, which is okay. And the JSON content, which is deserialized automatically into a generated Swift value type.

Okay? Next, we just need to call this function in the right place. And just for the sake of this demo, we're gonna call it upon refresh.

All right. So, let's try it out. We've got our server running.

So, now, we just built our app. While it's building an assimilator, we're gonna go and try to submit some votes. All right?

So, I hope you all will help me out. I've heard already heard a couple of opinions here. Okay.

All right. We're ready to vote. Okay.

So, I'm biased. So, green? Oh, my goodness.

You don't love me. Okay. All right.

Purple? Purple. I'm hearing purple.

Blonde? Pink? They said stay pink.

Okay. Okay. I'm hearing blonde.

Blonde. Okay. Pink?

Okay. Purple. Okay.

Three more seconds. Any more votes? Speak now or forever.

Hold your peace. Okay. Green.

Okay. All right. And we're gonna pull to refresh in three, two, one.

Okay. All right. Okay.

So, this was a lot of fun. So, apparently, I'm going blonde. So, now, let's reflect on what we've done here besides having too much fun.

Okay. So, we conquered a few things today. So, we started by creating and defining an API using a single OpenAPI document which specified the interactions between our iOS client and server.

And with this document in place, we used the Swift OpenAPI generator to automatically generate all of our necessary networking code for both the client and the server. After generating that code, we integrated it on the server side to handle our API requests. And finally, we used that networking code in order to make requests within the client to update the app's UI.

And now, apparently, I have to go blonde. Swift OpenAPI generator is a handy tool that allows you to take advantage of the power of spec driven development using a language that you're already familiar with. This tool helps make network calls less error prone by generating all of that networking code for you so you don't have to handwrite it yourself as your API grows in mass.

And as you enhance the complexity of your apps and your APIs evolve, Swift OpenAPI generator has the power to uphold API consistency between your server and your client, fostering a more cohesive collaboration amongst developers working on the same applications. If you'd like to learn more, check out these really cool WWDC sessions, meet Swift OpenAPI generator, and explore the Swift on server ecosystem. And you can explore that on the developer app or on our brand new Apple developer YouTube channel.

Don't forget to like and subscribe. I also want to highlight that Swift OpenAPI generator is just one of many other open source projects that you can explore on Swift.org. And it's filled with lots of sample code and starter projects for you to jump right in and start building.

And lastly, come join us and join the conversation on our forums to chat, connect, contribute, and learn more about all things Swift. I hope to see you there. We'll see.

And have a happy conference. Thank you.
