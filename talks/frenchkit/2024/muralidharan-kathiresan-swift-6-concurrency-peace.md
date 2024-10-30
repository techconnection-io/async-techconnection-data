---
slug: /talks/frenchkit/2024/muralidharan-kathiresan-swift-6-concurrency-peace
date: '2024-09-23'
title: Swift 6 + Concurrency  = Peace
author:
  - Muralidharan Kathiresan
video: pUwiuxdMWsY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/pUwiuxdMWsY.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: '2024'
allow_ads: false
---
### Muralidharan
Swift6 plus concurrency equal to peace. I know what you might be thinking, how can concurrency be done in peace? I should be crazy, right?

I can totally relate to it. I everything is good, calm, or when you leave everything and decide to quit. So let's see shift six concurrency is peaceful, if it is peaceful, in which way?

Before we dive in a little bit about myself, I am Muralidharan Kathiresan, you can call me Murali, hope that will be easier. I work as senior IOS developer at Bally's in London. I'm originally from India.

I created shiftpublish.com, a bi-weekly blog with my friend Shahrukh to share my thoughts about IOS development. When shift six was announced this year, I was worried. You might be worried too, if I'm not wrong.

The reasons are because it's a major release version after five years, lot of panic by thinking our apps will start breaking and then adoption pressure, the learning process especially, getting familiar with the latest additions, new APIs. This is the hardest one, to be honest. Finally, affecting your timelines, delivery timelines, project milestone.

But are these really a thing to worry? Let us find the answers. This is one of the code base where I initially tested the shift six with Xcode 16 beta.

Before doing anything, the project had around 20 warnings. That's the first screenshot in the left. When I enabled the strict concurrency check only at the app target alone, it was 400 warnings.

When I enabled in all the targets, that project had around some local SPM packages as well. It was 1600 warnings. That's nice, right?

No sign of any peace. I was a little curious to check, but you might be thinking, why do I have to update my app, which does not have a race condition at all? Or you might work a long time to fix all your race condition issues and then it might be free.

And then you might be thinking, they said actors already solved data races. What has happened now? If you like me working in the Objective-C from a long time, you might think like Objective-C had its problem, but at least I didn't have to rewrite my app every year.

So shift six compiler is the first version which includes shift six language mode. That means when you install Xcode 16, you get the new LLVM compiler and you get the shift six language support with it. This is the compiler or tools version.

If you want to check your compiler version, you can run shift C-version in your terminal and it will show whatever version you are currently in. And whatever the language supports, it's the language version. You may think everything is normal, right?

It's same like the previous releases. What's kind of new here? This compiler version back supports shift five and even shift four.

If your current project is running on, for example, shift 4.2, when you move to Xcode 16, you can still continue using the same shift 4.2 version. When you create a new project or a package in Xcode 16, the default language version is shift five only because shift six language mode is an opt-in only feature. And when you want to update your project to shift six language mode, this is where all the breaking changes happen.

So the good news is not to panic. At the same time, that's not for long. These are the new additions added into shift six, all the shift evolution proposals.

The major additions in this and the ones we are interested in today are all related to shift concurrency. These are the ones, the highlighted ones. This is exactly me when I saw all those new additions.

Now we are clear the shift six is an opt-in only mode. And if you want to opt-in, there are breaking changes. Shift six not only added new features, which we just saw, it also made some previous features mandatory.

For example, the forward closure or something which is really released in the shift 5.x versions also, they have made it as a mandatory one in shift six. You can check this in the latest Xcode. If you can go to the build settings under compilers upcoming future, you can check them.

Whatever is mentioned as breaking changes by the shift team in the left hand side, you can see the corresponding entry in the Xcode also. Shift six comes with a new language mode that prevents the risk of data race at compile time. This guarantee is accomplished through data isolation.

When you pass the data between concurrently executing code, the compiler will validate is the data safe to reference them concurrently or mutually exclusive. You can simply assume this by the mutable state can only be accessed from one isolation domain at a time. It's a form of synchronization similar to locks.

If you have used the locks before, the major difference is here, this data isolation protection happens at compile time itself. Isolation comes in two flavors. One is static, another one is dynamic.

Static isolation, like actors, global actors or isolated params are all part of static isolation. It provides compile time enforcement, so fewer runtime checks and safer. Next is dynamic isolation, like asym isolated and precondition isolated are all part of the dynamic part.

Here, this is a runtime enforcement. It offers you flexibility, but at the same time, this may introduce data races. Everything is non isolated by default.

You must take some explicit action to change this default state. It's not actually a type I brought in here so that it will be easy to understand. Always prefer the static isolation mode for compile time safety and use dynamic only if it is needed.

So an independent unit of isolation is called an isolation domain where you add your methods, declare variables, everything is an isolation domain. The area or transition point between one isolation to the other, a border you can simply say, it's referred to a isolation boundary. If you are moving values into or outside of an isolation domain, that is called a crossing and isolation boundary.

This is a very important concept. This is where all these problems come in. Let us see some examples to understand these three concepts better.

Isolation domains will always fall into one of these three categories. Isolated to a actor value or isolated to a global actor or non isolated. Here I have added everything into one single example.

Basically, you can picture out them separately too. Each domain, as we've seen, has its own boundary exhibit its own boundary. This is an example of crossing an isolation boundary.

The add with global isolation method, which is actor isolated, right? It is trying to access the main actor isolated property synchronously. Basically, this crossing of an isolation domain can happen anywhere between any two isolated domains.

Other than this, values can cross the boundaries indirectly when captured by closures also. If you are working extensively with closures, that you need to check that time also. Let's see a few important breaking changes and hints to get ready for complete checking.

If you check out this code, like static variables, the global state are accessible from anywhere in the app. This is flexible, but this visibility makes them particularly harmful, especially for concurrent access. Before this data is safety, global variable patterns relied on us, the programmers, we need to be carefully access them.

Now, global or static var is not concurrently safe in a non-isolated context, and the compiler won't allow you to. If possible, convert the global or static to a let constant. Also, you need to check in your types too.

You may get an error there also. If the value is used only within a certain concurrency domain, then try to add a actor instance, maybe a global actor instance, as I added here, for example, at main actor attribute. So it will make the compiler happy.

Generally audit the type. If it's similar to here, if that is concurrently safe, then you can use non-isolated unsafe also. But we need to be careful and audit the type in advance.

SIFT achieves data risk safety primarily using two related concepts. It's actor and region isolation. Those are the fundamentals for all this data risk safety, which determines where a value is stored and where a piece of code executes.

Of course, there are sendability checks also. When you have a non-sendable type like this, it's not sendable. It's a reference type for some reason.

Before SIFT 6, if you create such an object and then pass it along to an actor, the client.store.shared is an actor instance, right? This is crossing an isolation boundary from the main actor's open new method to the shared actor's client store. This is an error because compiler suspects there might be a data risk.

That may be true also because it can be accessed by both parties concurrently. But in SIFT 6, with the new region analysis, it uses a flow sensitive pattern and then understands you are creating this client value, passing it to other actor. Okay, it's not sendable, but we are not going to use this again in this main actor instance.

The only purpose of sendability is to prevent concurrent access. Because of there are no more accesses here, this is actually safe. We just moved it to another actor.

That's the place where it's owned and modified. This is a great addition truly, which makes it easier to work with non-sendable types efficiently. And then when you want to cross border, you don't have to worry much.

Thanks to this functional analysis. Prior to SIFT 6, there was no option in isolated parameters. If you want to capture the non-isolation context, for example, if you want to call this function from a non-isolated instance, you cannot, because you must pass in an actor for sure.

But if you see there is no actor instance for non-isolated, right, which is very strange. I have faced this many times. So SIFT 6 fixed this inability to express the non-isolated in params.

So isolated params can now accept optional arguments. So you can basically pass nil now. The second problem is the language had no convenient way to capture the current isolation.

So you can manually do this now, but it involves a lot of boilerplate that every place, wherever you call this method, you need to have to deal with it. So SIFT 6 introduced the hash isolation, a new special expression form. It can basically capture your current isolation.

It's not like if you use the hash line or hash file, it's the same pattern similar to it. Let's see some enforcing actor isolation checks dynamically. What are we have seen before?

Most are static. Let's see an example for the dynamic one, which means at runtime for non-state concurrency context. Absolutely.

So let's take this protocol defined in some external modular package. Now, when I import this package and conform to this protocol, what happens? The compiler gives me error stating that main actor instance cannot be used to satisfy in non-isolated blah blah.

How to avoid this? We can add a non-isolated keyword and make it a non-isolated before the function. But is it good?

No, right? Because we will lose all this static disk. Static data is safety here.

So what's the correct workaround? SIFT 6 adds the ability to annotate a conformance with at pre-concurrency. Previously, we had it for importing whenever we are importing some package or other component modules.

Now you can use this pre-concurrency attribute for the types also. When you do this, it has the same runtime effort as we've seen in the non-isolated context, but without sacrificing all the data race checks. This is cool, right?

Let's take another example. Again, here there is a non-sendable class and then I train and then there is a try send method. It accepts a non-sendable value.

I want to basically do the same thing I did little before in region isolation. I want to pass it to main actor from a non-isolated ASIC instance. Before SIFT 6, it's an error, but it totally makes sense because the compiler do not know how all the variable is used at the wherever the call site is.

In fact, it is possible. Some might be safe, some might not be. Not only SIFT, lot of code analysis tool faces these kind of problems and then they typically solve with the general pattern like adding some metadata.

So SIFT 6 also did the same thing by introducing the new contextual keyword sending. The sending keyword is related to the sendable protocol, but in a slightly different way. Here we are saying whenever this non-sendable value is sent into this try send method, we transfer the ownership basically and then it can be passed to another domain, especially another concurrency domain safely.

So please keep in mind if a function parameter or a result type, this sending keyword can be used to do the return type also. If that is annotated with the sending keyword, it to be discontinued at the function boundary and it is safe to pass to another concurrency domain. Every declaration in SIFT has some well-defined static isolation.

You can determine what the isolation is, but if you are using closures, that's little difficult because we can't find what is the current isolation. So if you check here, I don't know what is the isolation context here. So if you can add at isolated any to a closure, means we can access all the isolation information now and you can deal whatever is your purpose.

Yeah. But when I first saw this, my initial reaction was what closure have property now? This looks weird.

So what kind of function is this? We have seen little bit of isolation journey. So let's try to find out.

This is a non-isolator, right? So because everything is non-isolated by default. Next, this one.

Any guesses what kind of function is this? Yeah, exactly. Correct.

So this is a function that's isolated to the global actor. Here, the global actor is the main actor. So last one, any guesses what kind of isolation is this function has?

So this function runs in the context of the past actor. Whatever is the actor past, that will have that isolation context. In Xcode 16, Apple made significant adjustment to the view protocol in SIFT UI framework.

We know only the body property was annotated with main actor, right? And it was, there are a lot of confusions also why only the body property was annotated with main actor. Now, the entire view protocol is annotated with main actor, not just the body property.

This changes backward compatible too. So basically you don't have to worry. What this means, all the types that's conforming to the view protocol will now automatically receive the main actor annotation.

Yes, if you run this code in Xcode 15, it will return you false. But in Xcode 16, the same code, this will return you true. Since the entire view is annotated with main actor now.

If you have added main actor to your SIFT UI views before, now you can remove them. So if you want to come out of this isolation context, basically you may have some performance thing or you don't want to run certain things in your view in the main thread, you can use the non-isolation like this. This will print false in both the cases.

So also remember incremental migration is the recommended one. If you are using Xcode 15 and from SIFT 5.8, you need to use the experimental feature compiler flag to test all the changes. So if you are using Xcode 16, but if you are using only the SIFT 5 language version, you need to use the upcoming feature compiler flag and in Xcode 16, if it is SIFT 6, everything will be turned on by default.

So there are many challenges are there with this isolation concepts, to be honest, like we need to be careful when switching the contacts and it is absolutely sometimes it's sequential execution, right? So performance can take an impact. We need to be careful on that part.

And the other thing I felt is high learning cost for you and your team. Everyone has to be aware of the new changes. It's very hard to debug sometime, especially in case of any data race issues.

Normally data race issues are already hard. With this new changes, it will be a little more hard. So if you face like actor re-entrancy or if you are trying to cancel a process, these things you need to be a little more careful now.

And sometimes I felt the migration process from existing of your code base might be unclear at certain places. So these are the challenges of isolation. So how to decide when to do this upgrade?

If you are actively working on adding more concurrency features to your app, or if you are the one struggling like me to find how to reproduce crashes in your app, then you might start thinking about migration sooner than the others. Also, if you maintain a public SIFT package, consider about moving to SIFT 6 sooner so that all your users will get beneficial too, right? So you can follow along the popular packages, SIFT 6 adoption on the SIFTPackageIndex.com.

They have a clear view of how much data is there. So far it's there and how much packages have solved that. Yeah, you can check that.

So if your app is organized into multiple modules, you can migrate one module at a time. It's usually easier to start from the app first, then migrate the modules it depends on. If you ask me how much time it will take for your app to migrate, it totally depends on the size and the type of your project.

I personally recommend determine the isolation part of your project, which is a little bit doesn't have that much coupling or other things and then work on it first. It enables you to open some small pull requests so that everyone will be aware on the changes. For example, either an individual target or test target, something like that.

Enable upcoming language features for SIFT 6 one by one. What are the new breaking changes we have seen in the Xcode? So you can enable them one by one.

Increase the strict concurrency checking from minimal to target first, then finally to complete. After fixing all the warnings in each repo, you can change the language mode to SIFT 6. So I highly recommend you to listen to this podcast from SIFT Package Index with Holibora, the manager of the SIFT team.

I found answers to most of my questions here. SIFT 5.10 was overly restrictive and SIFT 6 removed many false positive dead arrays warnings through the better sendable conformance and other region isolations we have seen. So the areas we need to concentrate and address have become clear now and safety has improved.

So the takeaways are it is hard, definitely. Please take your time. The goal is to utilize the language features not to clear the warnings.

So understand isolation concepts first, then you can step into the migration. That's very important. Otherwise, we will be struggling to find the warnings.

What is this error? These things. Yeah.

Plan the process with your team in advance and share the knowledge with each other. So there is a lot more concepts out there like atomic mutex. If you want to do some manual synchronization, there is a concept called mutex introduced in the latest version.

But due to the time constraints, we haven't looked them. And it's especially for iOS latest version alone. You can check them also.

And instead of just sharing the deck, suddenly today I got a thought. Why can't I write an article about all the contents which we've just seen? So you can scan this QR code.

The details of SIFT 6 concurrency details are in my website. Yeah. So these are the handles if you want to connect with me.

And feel free to reach out any time. Thank you.

### Ellen
One thing that I had a question about, one of the things that you said that when you're migrating things one at a time, it's easier to migrate the app first and then the modules rather than doing the modules before the app. Why have you found that to be easier? Okay.

### Muralidharan
So every project is different. So it's my view. We had a lot of composable packages first.

So each package was supporting different code bases. So we shared those packages immediately. So the app layer was pretty thin.

You know what the app is exactly doing. So that is the first step. So if you can able to solve them.

Otherwise, as we've seen, we can use the pre-concurrency attribute to improve the performance of the app. The non-concurrency migrated once. So it was easy to start from the app.

Yeah. Thank you.

### Julien
First question from the audience. Maybe I can rephrase a bit. What's the worst data race you had to fix or correct?

### Muralidharan
Sorry, can you please repeat?

### Julien
What's the worst data race you faced within your migration? Yeah.

### Muralidharan
We have a long-term issue. The app was stuck in the launch. So our product team was continuously digging us on this.

But we couldn't be able to solve. We were trying to do instruments and other things. But when I started this change, I was able to see a lot of other things.

Where was the problem? We were trying to download all the resources during the launch. And that time, it was having some concurrent issues.

So it was a little helpful. It was not that much, to be honest. But we at least know the place of it, where it was exactly the problem.

So that was the app launch was having issues. It took too much time and it stuck. And that's especially for some customers, not for everyone.

### Ellen
Nice. Can you talk a little bit more about the pre-concurrency app attribute? So it's basically marking things that are written before concurrency was invented.

And it seems like you get really different benefits from marking something as pre-concurrency versus just sort of saying, oh, this is non-isolated or this is... Yeah. So can you talk a little bit about what are the advantages of using that annotation versus sort of what are the other escape patches that people use?

Yeah.

### Muralidharan
So if I'm using a common package, something, the third-party tool, I don't have a control over it, right? So I can't suddenly change what are the packages I own or my team owns. We have the control.

So that's why I think this pre-concurrency attribute comes in. So you can import them. This import, a package with pre-currency was previously there.

I think it was 5.7 or 5.8. I don't know. But this attribute, you don't have to completely import all the packages when you're importing. You can only set the type for whatever is the protocol or whatever is the particular type you are trying to import.

You can have it. So whenever we were using non-isolated, we are completely telling the compiler, I can take control of it, okay? So that means we are taking the risk.

So that's why these two new proposals were doing a lot of addition for the dynamic checks. So with this, a little more helpful, actually. Yeah.

Okay. Thank you. Thank you.

### Julien
And how about combined? Do you think it would check for data arrays at some point?

### Muralidharan
Yeah, I was expecting this question. So whenever there is a release version, right? So there are certain things.

I was reading dispatch queue to the task, then combined sequence to the async sequence. Yeah, there are always this equal to that new similar versions are there. But it's according to the usage, for example, I have used Rxiv for five, six years, very long time.

Yeah, so if your project is combined, okay, it will still be working. There is no point that you should definitely move it to tomorrow, within tomorrow, this thing. But I don't think there is no special data races, since we are using the old APS, something, something, nothing.

So these data issues are specific to the way we implemented a certain system in the code. So irrespective of the whatever API is there, this shift6 new addition help us to find them in the compile time. There are certain languages which had this from the earliest version.

Shift is evolving, right? That's why we are having these things now, not before a few years.

### Ellen
I think, what's your take on just sort of, I've seen a couple of people talk about like, I'm just going to turn on swift6, fix the things that are easy to fix, and then turn it back off until I'm like ready. Like, what's your take on like how whether that's actually valuable to do that, before you have a better understanding of how all of this isolation works?

### Muralidharan
Yeah, very good question, actually. As I told, it's an opt-in mode only. There is no rush for anyone.

I think this is the first time Apple made like that. So every time we need to run, but this time it is a little more flexible. So there is no problem that you need to mind.

So for example, if you see my shiftpublish.com, my blog is completely made up of shift. So I opted myself on the first early time itself. I wanted to check since it was very less code, but I can't do it for my entire office code base, because we shared with a lot of people.

It can't be done usually. So we started to do one by one step at a time. So I will say, we can start it, so it will give us a lot of new benefits.

And then to find the data races, as you asked, these checks will be really helpful, but it's not something you need to do it right now. So as you mentioned, understanding the isolation concept is very important. So I jumped into AsyncAwait when these things came.

I had a few issues without knowing them properly used. I have my own experience. So what I will tell, data isolation concept is very important.

First we need to be clear, then stepping into will be really helpful. It will be easy there. Okay, thank you.

### Julien
And thank you, Marit.

### Muralidharan
Thank you.

### Julien
Thank you.