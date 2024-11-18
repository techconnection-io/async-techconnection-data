---
slug: >-
  /talks/swift-connection/swift-connection-2024/rick-van-voorden-swift-cowbox-easy-copy-on-write-semantics-for-swift-structs
date: "2024-09-23"
title: "Swift-CowBox: Easy Copy-on-Write Semantics for Swift Structs"
author:
  - Rick Van Voorden
video: m9JZmP9E12M
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/m9JZmP9E12M.jpg
slides: https://storage.googleapis.com/async-techconnection-downloads-events/swift-connection/swift-connection-24/cowbox.pdf.zip
tags:
  - Performance
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: true
---

### Rick

Bonjour, je m'appelle Rick, je suis très heureux d'être ici aujourd'hui, merci, merci. I say hello, my name is Rick, I am very happy to be here today. I am a software engineer from Los Angeles, California, yeah, and about six months ago I built a project called SwiftCalbox.

I want to show it to you today. SwiftCalbox is free, SwiftCalbox is open source, and I'm going to show it to you today. I would like to begin with some background and philosophy.

What is a copy on write data structure? Why do we want a copy on write data structure? What problem does this solve for us?

And how do we build a copy on write data structure using Swift code? I want to show you how does SwiftCalbox solve this problem with a live coding demo. I will discuss a case study, which is a sample project from Apple.

We will migrate to SwiftCalbox and then measure the performance improvements. Finally, I will share with you some tips and tricks, which is some advice for you before you use SwiftCalbox in your own projects. Great.

So let's get started with some background. This is a quick review of reference semantics and value semantics. An engineer named James Dempsey has a very good essay on this topic.

I will have a link on the final slide. This is an example from James. Suppose we create a Swift class called person with a var location string property.

We create a P1 instance with location Los Angeles. We create a copy P2, set the location of P2 to be Paris, and now we print the location of P1. Well, person is a class, so the location of P1 is Paris.

These are reference semantics. How about person is a struct? We create a P1 instance with location Los Angeles, create a copy P2, set the location of P2 to be Paris, and now when we print the location of P1, we print Los Angeles.

These are value semantics. And we like value semantics. I like value semantics.

Apple recommends you choose value semantics by default when building the data models of your application. Value semantics give you code that is easy to reason about locally. But you may be paying a performance penalty for value semantics.

Let me show you what that looks like. An engineer named Jared Khan has a very good essay on copy and write semantics for Swift. I will have a link on the final slide.

This is an example from Jared. Suppose we create a Swift struct. We call it, there it is, container.

And we have 10 stored instance properties and every instance property is a 64-bit integer. What is the memory footprint of this container? The memory footprint of the container is 10 times 64 bits, which is 640 bits, or 80 bytes.

That's one instance. But what happens when we make a instance? The copy is going to be 80 bytes.

This is a value type. This is a value type. So this is a value type.

So when we copy the 80 bytes, we copy the value over. Let me go back one more. Okay.

So for n copies of the same data, when we model container as a struct, the total memory footprint is 80 bytes times n instances. But what happens when we model container as a class? So the memory footprint of the first instance is 80 bytes of data and a pointer.

On a 64-bit architecture, this pointer is 8 bytes. So the memory footprint of the first instance is 88 bytes. What happens when we make a copy?

Well, the memory footprint of the copy is 8 bytes. We share the data between both instances. So for n copies of the same data, when container is a class, our memory footprint is 8 bytes times n instances plus the 80 bytes of data we pay one time.

So when we compare these two side by side, we see that when we model container as a struct and we make many copies of this struct, we use one order of magnitude more memory after many copies. That's 10x memory. So that's a bummer, man.

So what do we do about that? Well, what if we had a type that was reference semantics dot dot dot and value semantics? So this is a copy on write data structure.

Copy on write is not a new idea. You can find examples from Unix in the 80s, 10x in the 70s and BBN Lisp running on mainframes in the 60s. For Swift, what we're going to do is a strategy where our interface of our new copy on write type will follow value semantics, which means we can continue to reason locally about our code, but we're going to build a type whose implementation follows reference semantics, which means that when we make a copy of this data structure, what we copy is a pointer to some shared storage to improve performance when this type is very complex. Some examples you might be familiar with are Swift array, Swift dictionary. These are copy on write data structures.

They look like structs. You use them like structs, but when you make a copy, you copy a pointer. When engineers from America say cow, we say acronym.

Copy on write. I believe you say lavash. So how do we build one of these fancy data structures?

We're going to go a little bit fast here, but on my final slide, I will have a link to a talk from Johannes Weiss from 2019 that goes into a lot of detail on what I'm about to show you. So the first step is we create a Swift struct called person. This is a let ID string and a var location string property.

We create a private class. We'll call it underscore storage. We put the variables in underscore storage.

We build a member-wise initializer and a copy function, which returns a new storage instance with the same values copied over. This is also sometimes called a box. You may hear engineers say box.

It's a form of indirection. Our struct person then can save a reference to an instance of this storage, and our member-wise initializer then forwards those parameters through to underscore storage. Our ID string becomes a computed property.

We return the ID from storage. Our location string becomes a computed property. The getter is not so difficult.

We just return the location from storage. The setter has some very important work to do, which is when we make a copy of this data structure, what we copy is a pointer to some shared mutable state. If we mutate a copy and we see that same mutation in the original, that would be bad because we would be breaking value semantics.

So to preserve the value semantics, we guarantee that when we make a mutation, we make a mutation on a unique instance that is not being shared. When engineers call this a copy on write data structure, this is the copy on write. You can also think of it as copy on mutate.

And that's the code. This is cool. You know, this is good code.

Engineers have been shipping code like this for years on Swift. This is awesome, but, you know, I look at this code and I think I don't want to write that code. I mean, it's a lot of code.

We're only looking at two properties, but what about four properties or eight properties or 20 properties? That's going to be a lot more code. And maybe I do just kind of, you know, write the code all once in a, like, hackathon, but then what about three months later or six months later when some new engineer has to come add a property and now they have to touch, like, 30 lines of code just to add a property.

That's a bummer. And this code looks kind of scary. You know, there's that known unique reference and if I make a mistake or I ship a bug, I am corrupting model data across my application.

Well, that sounds really bad. And this code looks kind of like repetitive boilerplate code. So, you know, in my experience, engineers, we don't want to build repetitive boilerplate code.

We want to do something else with our time. So what actually ends up happening is you ship something that looks like this. You see a to-do comment.

Copy on write. Fix me. Copy on write.

Maybe your company calls this wish list or backlog. It makes me sad. So let me now show you a better way.

And I'm going to transition to Xcode. And I'm going to do some one-handed typing now. Two-handed?

Oh, merci. Merci. Julia.

So what I'm looking at right now is a Xcode Swift package executable. Right now this is just hello world. Localization is good.

So I'll make this a bonjour Paris. Build and run. There's bonjour Paris.

Cool. Before I show you what Swift cow box does, let me build an application on a regular Swift struct. This is from our previous example.

Struct person. Let ID string and var location string. I'll create a P1 instance with location Los Angeles.

Create a copy P2. Set the location of P2 to Paris. And then I'll print P1 and print P2 to console.

Great. Build and run. And here we see that P1 location is Los Angeles and P2 location is Paris.

Cool. These are value semantics. Person is a struct.

Now let's see how Swift cow box can migrate this type to copy on write semantics for us. Step zero, which I have already performed, is the Swift package description will add the GitHub.com repo where you can find Swift cow box and you can see that we now have these dependencies available from Xcode. Here's is import the cow box repo.

The first step is struct person is going to add the at cow box macro to the main declaration. If any of you are new to Swift macros, there are some very good WWDC videos from one year ago when they were released. Var location string is going to add the at cow box mutating macro to indicate that this property will get and set.

Let ID string should get but does not set. So we're going to add the cow box non mutating. We have to transform let into a var because we cannot attach a macro to a let property.

And from Xcode, if I now control click on cow box, I have the option to expand the macro, and Xcode will show me all of the code that is built at compile time by Swift cow box. Here you see the storage class, you see the member wise initializers, you see the getters and the setters, and you see that the setter is performing the very important known unique referenced function call. So this is like 30 something lines of boilerplate and it's written by cow box, which I think is pretty cool.

So let me now build and run and let's watch what happens. So I build and run and the console is printing like something weird, underscore storage, what happened? Well, the default string interpolation behavior of a Swift struct will print the stored instance properties.

But the default string interpolation behavior of a Swift class will not print the stored instance properties. We can fix this. We can make struct conform to custom string convertible.

If I now control click on cow box and expand the macro, I can see that cow box has built a var description string for us using the values from copy on write, self ID and self location. If I build and run now, I see that we P1 location Los Angeles and P2 location Paris. We have migrated to copy on write semantics and we have preserved value semantics.

I just showed you custom string convertible. A person knows about some more protocols you might be interested in, like equatable, hashable, encodable, decodable and also codable. If you expand cow box now, you see that all of the code to conform to those protocols is written by cow box.

The equals operator, the hash function, coding keys, decoder, encoder, this is now like 60, 70 something lines of boilerplate all written by cow box. You don't have to write it. You don't have to maintain it.

I don't have to review it. It's copy on write semantics made easy. Merci.

So I showed you some of the theory. Why is a copy on write data structure potentially good for performance? I showed you a live demo in Xcode, how does Swift cow box make it easy to migrate to copy on write semantics in your own projects.

What you may not know is what is the real world impact? Why do we really care? It's a cool demo, but so what?

So I want to conduct an experiment. This is a sample project from Apple. It is built in Swift UI.

It is called food truck. Do you know the food truck? You have the food truck in Paris, the mobile kitchen.

This is American food truck, sells donuts and pastries in California. This is a Swift UI app. We're looking at a table component on the right.

This app launched two years ago. When Apple launched this app, you navigate to the table component and we display 24 donut orders in a table. That was two years ago.

Now the app is very popular. There's a lot of business and the owner of the food truck navigates to the table component and displays 24,000 orders. Three orders of magnitude, more donuts, a lot more business.

The chef, the owner writes to us and says performance is slow. The app is freezing. There is a beach ball.

So that's sad. Let's see if Swift Calbox can improve performance for us. We're going to go a little bit fast, but if you go look at the sample app repo from the Calbox GitHub, you will see a very long readme documentation with all the details about this experiment and a lot more details that I do not have time for today.

But the basic experiment is going to be we launch this app in instruments. If any of you are new to instruments, there are some good WWDC lectures to catch you up. It's a tool for measuring performance like memory and CPU.

We're going to launch this app in instruments, navigate to the table component. We will select the top order of the 24,000, change the status of the top order to completed, and then we selected the number two order, change the status of the number two order to completed, and we continue 3, 4, 5, 6, 7, 8, 9, 10. We run that in instruments.

We measure CPU and memory. And then we go back into Xcode, we import the Calbox repo, and we migrate the order struct, which is the data element, the model type in this table. We migrate the order struct to Swift Calbox.

We run the same experiment, we measure the changes, and here are some highlights. Corn animation commits reduced by 31% with Calbox. Hangs and hitches, which is expensive work blocking on main thread, reduced by 18% on Swift Calbox.

Persistent memory bytes reduced by 8%. And total memory bytes, which is active persistent memory plus memory that was retained and released over the app life cycle, reduced by 38%. So, like, this is awesome, right?

Like, these are double-digit performance improvements to CPU and memory. This is legit impact. And what I really like about this is the diff we landed to ship this impact is basically plus one line of code.

Import Calbox. We did add some macros to a type that was already declared, but all of the code to manage copy-on-write data storage, that came from Calbox. We don't have to write it, we don't have to think about it, we don't have to maintain it.

And what I also really like is Calbox is a non-breaking change. So, we did not have to refactor code in our component graph. We did not have to refactor code in adjacent models.

Those call sites remained the same. So, right now you might be thinking, Rick, you are a genius. Thank you.

I'm going to put Calbox on everything. Well, no. Let me tell you about some situations when performance might not improve.

I want to be completely transparent with you. I will start with compile times. So, Swift Calbox is a macro, which means you're going to be building the Swift syntax repo.

If this is your first time building Swift syntax, you will see compile time slow down. There is a runtime penalty. We use object-oriented programming when we create shared storage, which means we have to call alloc, retain, release.

This is a heap object, which is more expensive than a struct, which is just on the stack. When you make many copies of this data structure, you will save CPU, but if you have a struct that is never going to be copied, do not use Calbox. Just use a regular struct.

The memory we use is a pointer to some data. If the data that you're attempting to share is less than or equal to the width of one pointer, you are never going to save memory. If you have a 64-bit pointer that points to a 64-bit integer, well, Calbox is not the right tool for you.

For very simple structs, just use a regular struct. Do not use Calbox. There is also a situation I know about called accidental quadratics.

Some of you may have seen this before. There can be some situations where you have a for loop that is performing many iterations, and every iteration is performing a mutation on a Calbox struct. In some situations, every iteration is copying all of the data storage, and this can slow down your performance.

This is a problem that happens to other copy-on-write data structures, not only Swift Calbox. For some strategies to detect and also defend against this, I will have a link to a talk on my final slide from Corey Benfield from 2019. A very good talk.

It goes into a lot of detail about this topic, so please watch that to learn more. If you're ready to get started, my first advice is start with a baseline measurement. This is just kind of like good advice in general when you're going to do a refactoring.

Measure the state of your app today, and this is your control group. Once you have that measurement, measure CPU and memory. I recommend Ordo 1 benchmarks.

I'm also a contributor. I like Ordo 1. You can also use Apple instruments to measure Swift UI.

I'm not a contributor, but I like Apple. When you're ready to migrate to Swift Calbox, choose one type to migrate. This is your experiment.

A good candidate to migrate would be a type with many bytes of storage, so you save more memory. You would also want to choose a type that is going to be copied many times over your app lifecycle. Something I didn't have too much time to talk about is you may want to choose a type that is checked for equality many times.

There's a lot of details in the readme documentation, but we perform an optimization in Swift Calbox. If we check two Swift Calboxes for value equality, we can perform a check on the reference, which is 01. If two Calbox structs point to the same storage reference, we can return true in constant time, so the actual data that you're storing could be 100 bytes.

It could be 1,000 bytes. If two Calbox structs point to the same storage, they must be equal by value, so we can save a lot of performance with this trick. Measure your changes.

Go back to Ordo 1 benchmarks and instruments. Measure your changes and compare your results. In conclusion, I will say that if you choose to write a copy-on-write data structure, you can write all this code.

You are a 10x engineer. I am going to use Calbox. You can download Swift Calbox at GitHub.com, Swift Calbox. You can find the Calbox repo, which you can import into your own projects. You can also find the Calbox sample repo, which is the fork of the Apple sample project we used to measure Swift UI performance, and both of those repos come with long readme documentations with a lot of details that I did not have time for in this talk, so please check that out. You can follow me at GitHub.com for some more open source stuff I might be working on. Special thanks, my friends. See you on Jeff, not Bill. Thank you for reviewing an early version of this talk.

All mistakes belong only to me. For references, I promised you some references. These are some very good essays, lectures, and presentations that were very educational to me building Calbox and also building this talk, so if you want to really learn more about this topic, please check out these references, and now I say merci.

### Rob

I love a really technical talk, a really deep talk right before coffee, and you can get your brain back together. One of the things that really got me was you'd say copy a lot, or, you know, if you copy it, you know, but, I mean, back in the Objective-C days, we actually typed the word copy, but I haven't typed the word copy in a long time. How do you know when you're copying when it's a struct?

### Rick

So there are some situations when the compiler can help you, but in my experience, in my opinion, is these are happy accidents. Prepare for the worst case, you know, worst complexity, which is ON. So if your struct is ON and you pass it as a parameter to a function or you add it to an array and then you make a copy of that array and then mutate that array, in some situations, yes, the compiler can work some magic and maybe help you out there, but assume worst case.

In the repo, there is a command line package that runs this code to copy, and all it is doing is just putting, you know, n items into an array, making a copy of that array, and then mutating the array, and that's triggering, you know, all n bytes being copied.

### Rob

You said something really surprising there. You said passing it to a function?

### Rick

If you have a struct, so this is a good question. So something that I hear sometimes is maybe engineers who are coming from a new platform may think that Swift structs are copy on write by default. We don't get that out of the box.

When I brought up array and dictionary, the engineers that built those data structures made them copy on write, with a lot of just kind of manual code similar to the code that we saw. It's open source, so you can see it for yourself. But if you pass a struct to a function, in some situations, the compiler can help you out, but in some situations, it can't.

So as an engineer, if I look at a situation and I say sometimes I'm going to have to pay an ON cost, to me, that's an ON algorithm, so.

### Denis

So one question that comes up a lot is, like, people who have been listening to the past presentation, and they're kind of worried, how is this going to affect if you're, like, using strict concurrency? You have to worry about something specific, or is it just, like, any of those things?

### Rick

So Calbox doesn't really know much about concurrency. The check to ensure that a reference is unique is an atomic check that is down in the arc retain release system. So that's already atomic, so we're okay with that, and that's the same check that Swift array and Swift dictionary are built on.

We're just using that same pattern. If you have a struct that is now sendable, so, like, we think to the person example, you know, struct person, ID string, location string, if that type is sendable and you make it Calbox, it will still be sendable, so, yeah.

### Rob

So, I mean, you use that example quite a bit. String and array and I think some of the others are already copy on write. So I like, well, the question was, is there any danger of, or is there a problem or advantage of wrapping a copy on write type in a Calbox?

### Rick

So, yeah, that's a good question. I like the string example because it kind of makes, like, a good demo, but the order struct, if you actually go into the sample repo, which is the fork of the Apple project, the order struct is actually, I think, 140 bytes of storage. It's maybe 15 times the width of one pointer, and it is there are nested types, there are other structs that are in there, there are ints, there are enums, so that is a great candidate.

As far as whether you want to make a copy on write type part of your copy on write data storage, I don't have the one correct answer for everybody in this room. A lot of this is going to depend on how you're using it in your own projects. What I like about Swift Calbox is it is a non-breaking change.

So the code to put Swift Calbox into your app and kind of try it and run the benchmarks, you're going to spend more time writing the benchmarks than you will spend migrating to Swift Calbox. So try it for yourself, you know, see how it works in your apps, come up with an experiment, run your experiment, and then measure and compare your results.

### Rob

Well, thank you so much. I think it's about time for coffee, right?

### Denis

Yeah, I think I can get one. Do you have one more? I'm so sorry.

One more just question. I've seen some weird case where the compiler doesn't help you out a lot. It's like whenever you have a computed property, you might just want to say, okay, I want to access this property and modify it, and then something weird can happen and you get called a get, then a set, and then the copy on write doesn't work very well.

Do you know how we can maybe fix that or not? You have a computed property that you wrote yourself.

### Rick

Yeah. And then you call...

### Denis

Basically the computed... Basically the property is an array, and you're like, okay, whenever I call this property A, give me the array that is stored somewhere else. And whenever you just call A and, I don't know, insert an element, you're just going to get a get call, then a set call, and then at some point you have some kind of weird behavior because you have two pointers on the array.

### Rick

Are you talking about... I think I can answer your question if I think I know what the question is. So there can be some situations, and this kind of leads back to your question, which was there can be some situations where you do see an accidental quadratic because an array is a copy on write data structure.

If you store a copy on write data structure in a copy on write data structure, there can be some times when if you make a change to the sort of inner child struct, that may trigger another copy. If anybody is familiar with underscore read and underscore modify, there are these semi-private APIs that do help in this situation. We don't use them in cow box, we use the public getters and the public setters because I want to ship something that everybody can use and not be limited by some pseudo private API.

We may ship read and we may help for this, but then engineers would kind of be on their own. You can use this, but be careful because it's not completely official. So that might help with those situations.

Okay, great. Thank you. Merci.

Merci. Thank you.
