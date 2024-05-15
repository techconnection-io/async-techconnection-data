---
slug: >-
  /talks/flutter-connection/flutter-connection-2024/mateusz-wojtczak-demystifying-app-architecture-the-leancode-guide
date: '2024-04-24'
title: 'Demystifying App Architecture: The LeanCode Guide'
author: Mateusz Wojtczak
video: T4B9NQRirKE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/T4B9NQRirKE.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: flutter-connection-2024
allow_ads: false
---
[Mateusz]
Welcome to Demystifying App Architecture, the Lean Code Guide. We'll try to have a walkthrough about app architecture, how we approach it, why we approach it that way and when it's probably a good way for you and maybe when you should think about what you build and maybe do some fixes to that. So, I'm Mateusz and I'm head of mobile at Lean Code, also a Flutter and Dart GDE.

[Marcin]
And I'm Marcin, I'm a senior Flutter developer at Lean Code.

[Mateusz]
Yeah, and you can find us on X slash Twitter at these handles. So, let's start. At Lean Code, over the last two years, we've developed over 40 Flutter apps.

And from that experience, we thought, okay, we can think about what apps we actually build. So, we prepared a couple of logos of our clients and we thought, okay, let's categorize them. So, you can categorize them in different dimensions.

One of them is what's the type of the project and size of the project. So, as you can see, we tend to do rather bigger apps and we tend to do either enterprise apps, which are pretty big, like large scale apps or scale apps that, you know, from the start that have to scale in terms of features, in terms of people and stuff like that. On the other hand, we also can see if we build apps like B2C that are for the end users or are for internal use for some enterprise.

And majority of them are also B2C, so we cannot compromise on UI, we cannot compromise on quality, we have to be pixel perfect, we have to deliver very quality performance also. So, how can we approach all of that? Now that we know our niche, we know our clients, how to fit it in our architecture, right?

[Marcin]
So, that's where the notion of architectural drivers comes in. And architectural drivers is something that is very well known in backend communities, but I believe it's a little less known in mobile and Flutter community. So, I think it will be worth to give a brief introduction to what they are.

So, they are basically factors that influence the design decisions and shape the architecture. And in general, they can be split into four categories. Technical constraints, business constraints, functional requirements, and quality attributes.

So, this is more of a detailed split than the classical functional versus non-functional requirements. And looking at those drivers, you can actually decide how you should shape your architecture. So, the main takeaway from all of this is that it's all about trade-offs.

So, when you build an app, you will be faced with some trade-offs. One of the classic ones is security versus user experience. So, on one hand, you want your app to be secure.

So, you would like to add features like two-factor authentication. You would like to keep the user session short, so they have to re-log in again to provide better security. In the classic example in account recovery flow would be to not showing if account exists for a specific email.

But on the other hand, when it comes to user experience, the requirements are a bit different. So, you would like to have a simple login. You would like to have a long user session so they are not locked out of the app when they open it after a week or something.

And you would actually like to show someone if their account exists or not, because it's just easier for them to proceed.

[Mateusz]
Yeah, and we all know one popular fast food chain app that traded UX for security. So, it's important to know what trade-offs are for you. So, what trade-offs are for us?

So, our assumptions are that as a software studio, we need to optimize for quality of course, but also quick start. So, we want to offer some common features ready from day one like being able to log in with Apple or Google or from the beginning have navigation and deep links and push notification support, stuff like that. Also, we want to be able to scale the project team if our client wants to scale in terms of features and wants to grow.

Also, we want to be able to reuse already working code, right? Because if we have a lot of apps being built in our company, then we already resolved a lot of issues. We already solved a lot of problems and they are working on production.

So, we want to be able to reuse that and fix bugs in one place and maintain that in one place in some libraries or stuff like that. And then we go to another important assumption, which is maintainability and accessibility. So, maintainability means that we want to be able for this app to work in production and for a couple of years and that we can maintain the code base that you don't have to think for an hour how to find some file related to that view and stuff like that.

But also, we want to be easily able to add new features, to add new pages, to extend the functionality, right? And what's the most important assumption is that we cannot have any compromise on quality. We have to deliver the best quality that we can.

We are also in Flutter community. We have to be, you know, we have to show that in Flutter you can build anything, that it's pixel perfect, that it has the best performance and so on and so on. So, to put it simple, we want to offer quality but also battle-tested solutions, right?

Okay, so how it translates into code in our approach. So, first we want to be pragmatic and not dogmatic. What it means is that pretty much we want to make safe decisions that are good in our assumptions and also that don't have a lot of boilerplate, don't have a lot of, you know, noise around the code.

We want to minimize the noise. For example, many times you can see a lot of diagrams and stuff like this where you can see a lot of layers, a lot of abstractions, a lot of code that's noise around the actual functionality. And we should just ask the question, can you quickly explain the purpose of this layer?

Because if you cannot do that in a couple of seconds, I would guess then probably we can just remove it and you probably ain't gonna need it, like the popular saying in a software development world. Because on the other hand, you end up with a lot of code like this when you simply map from one layer to another layer and this code is, like, functionally does nothing from the business perspective. It doesn't deliver any business value.

It's just because you want to have two classes instead of one or stuff like that. And many times it's also about, in this case of layers, you often see code which just executes the same functions from other layers, which is also probably unnecessary, probably redundant code. And if we have too much redundant code and it's hard to maintain it, it's hard to extend it.

That's why I'm talking about it. So as you can see in here, I took an example from Kirill Bubochkin article that's really nice about architecture in Flutter. And here you can see some use case, a lot of abstract stuff, a lot of types around.

And actually when you look at it, what you actually want to do, want to execute, is just this line. You just want to execute one function and give an integer as a parameter. So just do that.

Probably in 99% of cases you just want to do that. And the same goes about project structure. Like, with project structure, layers can be really cumbersome because if you have a catalog with all the blocks, for example, or all the repositories, and you have, and your project scales, and you can see a hundred files that have qubit suffix.

And you are new to the project, for example, you onboard new colleagues to the project, or you just didn't see this code for a long time. You pretty much don't know where to start. You can see a hundred blocks and you don't know which one is actually suitable for your use case and for your task that you have to do.

So, again, as we already talked in many, many of our presentations, we really love doing it in an orthogonal way and just split the project structure by feature because this is more like a business-oriented perspective and now we can see exactly what are the files that we want to work on. If you have a new developer or maybe you didn't see this code for a long time because you worked on some other part of the app, and now if I want to work on charity goals, I can see this sub-feature of active contest page which is charity goals. I go there, I know all the code that's related to charity goals is probably here.

And the most important thing is always think about what you build because, for example, this is the code of set state in Flutter. And as you can see, that's a lot of code. A lot of code and first, like, a lot of code is just an assertion because there's a lot of developers around the world that use Flutter and Flutter team wants them to know why they use it in the wrong way or how to fix it, what are the common mistakes with set state.

And also, you need a lot of Dart documentation for that because you write a framework. But at the end of the day, from the functional perspective, you only have two lines of functional code. And why I'm bringing up this example is that if you write a framework, you have a whole different approach than you if you write an app.

And this is very important about pragmatism. And if you want to be pragmatic, just think, do you really need it? Because, for example, if you build a framework, you definitely need assertions, you definitely need a lot of Dart doc.

But maybe, for example, if you made it in your project, you just needed these two lines of code, right? Okay. So let's go to our architecture.

[Marcin]
Yeah. So now that you know what drives us when it comes to architecture, we want to take you for a tour of how we actually build our apps. So we're going to go through some key points that every app needs to implement, needs to think about.

And let's start with the classic one. So state management. So when it comes to state management, the short answer is that we use block.

As block is both a name of a library and a base class, to be more specific, 98% of the time we use qubits, which is like a simplified syntax. And what we like about block is that the principle behind block, the principle behind qubit is very simple. It's just a class with an emit method, and it just emits some states that can be read later.

So because of that, it's also very predictable, because you can just inspect the series of states that qubit emits. It's easy to test. It's scalable, because it doesn't impose the level on which it exists.

So you can use block for global stuff. You can use it only for our screen. And when it comes to other solutions like RiverPod, we use RiverPod in some projects.

The very nice thing about RiverPod is that it's simple to start with. It provides a lot of good examples. So for example, it tells you how can you handle async stuff, things like infinite scrolling, something which block doesn't have.

You have to write it on your own. But RiverPod is also more like a framework. So if you commit to using RiverPod in a project, you practically end up using it everywhere.

And that's something that we don't want to be limited by, because as I've said, block can be used only in some places and not in others. Another popular solution, MobX, which we actually very like. We also used it in some projects.

The thing about MobX is that it is a bit magical. So a lot of stuff happens under the hood. With block, you very clearly see what's happening.

It's also easier to debug. MobX also involves some code gen. It's not necessary, but if you don't want to use code gen, you have to produce some boilerplate.

The thing also is that it's less popular. So when onboarding new developers, most of them are familiar with block. With MobX, it's harder.

It's something that we also need to think about when it comes to a software studio with many developers. Another popular solution, GetX. GetX is more like a complete framework.

So it's not really about state management. And the state management part is actually very similar to MobX. So that's why we don't want to be limited by a bunch of stuff that comes with GetX.

The thing about blocks is that they actually can easily get boilerplate. So this is some piece of code. On the left side, there's a qubit which fetches some project details from some API.

On the right side, we have a couple of states. So typically, you need loading states to show some loader. You need success state to show the actual data.

And you need some error state. And it's a perfectly fine piece of code. But when you have dozens of features in your app, what typically happens, you end up copy and pasting it and just changing names.

So we realized we started doing that. And we actually created a package called Lean Code Qubit Utils. So you can see it's prefixed with Lean Code, so it's heavily optimized for our use cases.

Also, with integration with our backends. But it's mainly focused to handle scenarios like this one. This is the previous code replaced with a query Qubit Util which handles all the loading error success states under the hood.

We also have some utils for things like paginated lists and so on. So we use block on a higher level. For UI code, you still need stateful widgets for some local state.

And we actually had a discussion recently at the company whether we should use hooks or stateful widgets. Because many of our developers are very fond of hooks. There are some drawbacks to hooks.

But in our discussion, we ended up with the conclusion that we really like hooks because it's just less code. It's easier to write. And also, you can easily reuse this stuff between widgets and even between projects easily.

So actually, the thing that came up as the biggest disadvantage of hooks, they can be misused. They can be used in a wrong way. But if you educate people how to use them, they're really a nice tool.

And we also, again, have our own Lean Code hooks utils. So one of the most heavily used is use block. As you can see, all of our pieces are kind of...

We kind of combine the block, which is our default solution with hooks, and other into a use block. So in our screens, you would see use block instead of block provider.

[Mateusz]
Yeah, and let's go to another important part, which is API communication. It's actually a bit connected to state management. But the most important thing is that you don't want to write API contracts yourself.

And you might want, I think you certainly want to have any API contract. So either you use some external backend or maybe you have your internal backend team and you can sit side by side with them. You must have a contract with the backend.

And you don't want to write it yourself. You have to somehow generate it to have that automatically generated for you so that you know that you always are on the same page. So for example, this is also a query qubit that Marcin talked about.

But the most important thing here is that you want to use your backend like this. CQRS is just our name for our backend, but you can have API variable in here. I mean, if you want to get info about other player from the backend, you just want to have something like this so that you don't think about how it's serialized, was it transport layer, is it HTTP or gRPC.

You don't want to think about it here. You just want to have it pretty nice encapsulated and also have a contract so that you just get other player and you just pass the parameter of player ID. And this also connects with the things that we said about pragmatism that we can remove some layers because this code that would be in this layer is already in our API client.

If you do that, if you have your contracts with API, if you have encapsulated your API communication transport layer in your client, then you probably can, for example, dispose of one or two layers. So you can simplify your code and simplify the usage of this. So this is, in my opinion, this is really important when delivering business value.

[Marcin]
Okay, so now let's move on to forms. And forms in Flutter are simple when you have a simple form like for logging, you have two text fields or something. But we had some projects where forms were really complex.

The best example would be banking apps where there were forms with dozens of fields which would show and hide in different scenarios. So this with raw forms in Flutter is very hard to implement. So we realized that in our two banking apps that we wrote, we actually developed custom solutions, custom frameworks for forms.

And then we sat and tried to combine them into something reusable. So another library in Flutter, it's also, it's pretty fresh. So it's being used in production already in some of our projects.

We haven't been talking about it much. You might hear about it in the future. What we tried to achieve with this library is, first of all, getting rid of manually handling all the text editing controllers and focus nodes.

We wanted it to be easily used with any custom UI, because many libraries are very nicely connected to the material widgets, but we typically don't use a lot of material widgets. We had requirements like scroll to first error, which is actually pretty hard to implement with available solutions. Also we wanted to have good support for conditional fields and fields that depend on each other.

So showing some fields if some other field is checked and stuff like that. And they seek validation that is also quite tricky to do. So we won't have time to get deep into this, but this is like a sneak peek of how it looks like.

It's based on qubits, although it is kind of an implementation detail, in fact, so it might be hidden in the future. So we represent the form as a qubit, and we represent every field as a qubit. So here is just a simple representation of a form with two fields, and we have some utils to integrate it with the UI.

And now let's move on to UI, actually. So UI is a bit tricky, because on one hand you kind of develop the same thing over and over again. In every app you have some button, you have some text field.

But on the other hand, every app looks different. Designers and we also, we don't want all of our apps to look the same. But still, we wanted to somehow gather our expertise in UI development into something that can be shared across developers.

So we realized that we need some robust, highly reusable and adaptable set of UI components. We don't want to be limited by what's in material, because, for example, we had projects where in many projects text field for material, which is a very complex component, is completely enough. But we had some requirements that actually we needed to implement it ourselves based on render objects and very low-level stuff.

We don't want to analyze common UX patterns like infinite scrolling over and over again. You need it in every project. So we want just developers starting a new project to easily reuse what already be done at our company.

We also have to provide some good accessibility by default. So what we have is actually we developed kind of our own design system, which is like a base design system. As you can see, we use widget book for that.

Yeah. Great. Great library.

And, for example, this is our text field, which is very complex. It has a lot of features. We took from many projects.

We analyzed what can be used, what can be put in the text fields by the designer. And how this works is actually this is like a base Dart package that we just copy and paste to a new project. And it lives its own life from then on.

So it's not like we're getting updates from upstream, because that would be hard to integrate. Because, in the end, you take the base, like for a button, and then you change it to fulfill the project requirements. But we actually found that it's easier to just take this code and modify it than to write it from scratch.

With buttons, maybe it's quite simple. But with text fields, as you probably know, it's very hard to take the material and adapt it to your needs.

[Mateusz]
Yes. So as you can see, pragmatism also means that sometimes you just want to copy and paste stuff, which is probably better to think of an abstraction of a text field that will work only in one project. So, yeah, let's go to another important part, which is dependency injection, often mistaken for state management, unfortunately.

So in Flutter, you have basically two options. It depends on what you want to do with your object. If you want your object to live as long as some widget in your widget tree, then you probably want to use Provider, which is the best implementation of inherited widget.

I don't know if it's still the best, but it's battle-tested as possible. One of the, I think, most popular libraries in the Flutter ecosystem. And it just works, you know.

It just works. It just binds your lifecycle to the widget lifecycle, which in UI apps, like most of stuff that we do is connected to UI because we do mobile apps, and they have a lot of UI. So most of our objects are actually using Provider for the DI.

And there are some cases when you just want to have a bug of dependencies, and you don't want them to be connected to Flutter even. Maybe you just have some Dart code. You just want to use some service locator.

And then you have another perfect solution, which is already in the ecosystem, and it's battle-tested, which is GetIt. And we also use that if we have situations like that. But I think the majority of use cases is still Provider.

But remember that there are some drawbacks of Provider. For example, in one of our large-scale apps, one of our banking apps, we had the issue that if you nest too many Providers, then actually Flutter got an error because Flutter uses recursion to traverse the tree of elements. And if you have too much, if you have too many nested widgets, too many nested elements related to the Providers, then it can blow up.

So we had to fix it with some layout builder workarounds. But still, this is the solution for most of our use cases. And if not, then we use GetIt.

Also, worth noting is that our colleague from LeanCode is experimenting with creating a solution that actually combines those two use cases, because why not? So we are not using it, not at all, in production. It's just an experiment, but maybe you may want to, if you like experiments, and you might want to check it out and leave us a comment in the issue or something like that.

Okay, let's go to another important thing, especially if you want to deliver quality code in a quick manner. It's linting. It's part of a, I would say, quick left, which stuff, I'm sorry, shift left stuff, because you might want to have as many errors detected while you are developing or in a PR, and you don't want to have them be detected on the QA stage.

So as you know, you can use lints from Flutter. We also have a linter package, which is LeanCode lint, which the basic thing is that we just have our own analysis options YAML file, but it's not only that. We also use some custom lints, and they are, I think, the most interesting stuff.

For example, we check if your qubit name has qubit in the end, like the suffix, or for example, avoiding conditional hooks, which is very important, because one thing that you can misuse about hooks is that you can put them in an if condition, for example, and it's important that you shouldn't do that. You can do that. And we have a custom lint about it.

Also, for example, if your hook widget does not use hooks, then we can detect that. So also about design system, as Marcin said, we want to use only components from design system, because the worst thing is when you have a design system, but some other people use material stuff, and you have all of the components, and you know that everyone should use them. So use design system item is a great custom lint for that, so you can definitely check it out.

[Marcin]
Okay, now let's move on to our last point, which is testing. So we try to follow some testing policy. The most important thing is that we try to test all business logic, so typically most of our business logic resides in qubits and some other classes.

We test complex UI logic with widget tests. We're also experimenting heavily recently with golden tests, so all of our design system components are tested on a unit test level for every low-level component. We write integration tests for whole screens, so if you use golden tests in the project, we want to have every page have at least one golden test, so we can easily track changes across the UI of the whole app.

If you want to learn more about golden tests, I had a talk in London last year about them, when I get very deep into how they work, so you can find it online. Also, think about pragmatism. As Mateusz said, we don't enforce any coverage thresholds, we don't want to blindly follow the 100 per cent coverage.

Some code doesn't really benefit from having a lot of tests, but it's most important to test core business functionalities. When it comes to end-to-end testing, we're a bit biased because we have our own library, which is a lot more popular than the others, so you might have heard about Patrol, you might have even seen Mateusz's talk from some other conference. So, quickly, we're trying to overcome limitations of integration tests.

It comes with really cool features like native automation, custom finders, so, if you haven't heard about it, feel free to check it out. If you have some feedback, catch us after the talk. Now, how do we put this all together?

We have all these pieces, how we actually use them in a new project. So, we have an app template which is like a repository that we start any new project with. It provides us with easy set-up for new projects.

It comes with example features. Some integrate with example back-ends, so we also have a back-end team. They also have some example app.

Some features are integrated. Those are features like authentication, so authentication logging with Facebook, Google, Apple, et cetera, things like first update feature flags that you typically want in most of your apps, at least at some point, so it's good to have them from day one. It provides a huge cost optimisation for our clients, and, at first, we tried to make the template an interactive script, but that didn't really work well, so we thought it would be cool if we start a new project, you can choose which features you want, which features you don't want, but that was just hard to maintain.

[Mateusz]
Also, usually, you might want the same features.

[Marcin]
So, last thought that we want to leave you with is that you're not forced to follow a single architecture in a project, so, especially in a big app, you can have most of your app follow a feature-based architecture, a typical stuff with qubits, but you might have some parts of the app, some subdomains that doesn't really fit this, so you might have a feature that is very reactive, you might have some feature that is heavily offline, so you don't need to follow every feature in your app, it doesn't have to follow the same pattern.

Those can be in different folders, or even different Dart packages, but you're not forced to follow everything in a single pattern. So, some key takeaways to finish our talk. Be pragmatic, not dogmatic, there are no silver bullets, but we build something which makes sense for us as a software studio.

Find your architectural drivers, the most important thing is that they can change during the lifetime of the project. Don't hesitate to challenge the status quo. Initial architecture might not be valid anymore at some point, and you might have multiple architectures in your app.

[Mateusz]
Yes, and last but not least, we've been working on something new and wanted to tell you about it, which is Flutter CTO survey, it's one of a kind report presenting opinions from CTOs, tech leads, mobile tech leads, Flutter tech leads, front-end tech leads that used Flutter or evaluated Flutter and want to share their experience so that we can know from the first hand from the decision makers, important people that used Flutter, how they feel about it, what are their experiences.

So we plan to release it in July, and if you want to take part in our survey, you can just scan this QR code or go to this link and sign up for that. Thanks!