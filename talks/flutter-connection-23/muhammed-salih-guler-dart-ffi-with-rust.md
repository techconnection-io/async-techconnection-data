---
slug: /talks/flutter-connection-23/muhammed-salih-guler-dart-ffi-with-rust
date: 2023-06-02T00:00:00.000Z
title: Dart FFI With Rust
author: Muhammed Salih Guler
video: oQb_yTJJKI4
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/oQb_yTJJKI4.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/flutter-connection-23/muhammed-salih-guler-dart-ffi-with-rust/slides.pdf
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

I will time myself so I can be on time.

So today, I'm going to talk to you about how Dart FFI works with a bit of Rust.

The point of this talk is to teach you the possibilities of FFI, what it is, and what can you do with Rust as well.

About myself, I'm Sali.

I am based in Berlin.

I have been working at AWS for a year now.

Before that, I had been an Android and Flutter developer for several years.

So none of this information is important to you because I'm not going to do any of these right now.

I'm going to show you how the different things work.

So my slide is super animated, so that's why it takes some time.

So today's agenda will go into three different categories.

I will talk to you about what is .ffi and why ffi is important.

And we will talk about Rust really briefly.

I will show you the syntax of it.

And lastly, I will show you how you can send information, receive information.

And we will talk about what can you do in the complex scenarios.

So first, .ffi.

Before we say .ffi, how many of you know what ffi means?

OK, awesome.

And then this is the perfect talk for you, because Hanna did have Flutter works with

FFI, but this is the perfect one for you.

FFI stands for Foreign Function Interface.

It gives you a chance to communicate with languages like C, C++, Rust that works in the low level, and gives you a chance to communicate with them in both directions by using higher level languages like Dart, Java, or many other that is going on out there, like JavaScript as well.

The important point of FFI can go into six different categories.

The first category is accessing native libraries.

You can use the FFI to use some tools that have been created for you like sound test engines and so on that has been created with C or C++ or Rust, like these low-level languages.

And this gives you a chance to have a working version of these directly coming for you in the applications that you have.

The second point is when you have a code that is required in a platform-specific way, you might need to write it with the platform channels, and you might require a lot of work around it.

But thanks to these low-level languages, they might have APIs that are making these calls available to do it on those languages.

So you don't need to write any platform channel.

You can just write the code.

It will work multi-platform, and you will take that information back.

Another point is in performance, a lot of SDKs and languages that we have comes with the extra toll of the tools and so on that, even though we get rid of many of the unnecessary parts, they're still, when they're bundled, they're heavy.

But when you use these low-level languages and create these libraries, the performance will be improved, and the size of the app and the libraries will be going down as well.

You can also write cross-platform applications by using these languages too.

You can directly connect to each API.

And once you are in your platform, you will just call the code once, like you do in Flutter.

And it will bring the possible and the correct one for you.

And lastly, you will open yourself to the experimental features that is going on in the world or with the platforms that you write the code in until they are ready in your platform.

So this way, you would be able to actually just get the native performance even without waiting.

I know you would say that, yeah, we were doing this with platform channels.

Is it wrong?

It's not.

But at the same time, FFI gives you a chance to do it a bit more performant.

It's a bit more complicated, for sure, but it brings also the positive sides with it as well.

So Dart FFI, you want to know how to use it?

It's not yet.

We will now talk about quickly Rust before we move forward.

Dart FFI is the tool, by the way, like Dart FFI is the tool that is going to give you all of these chances by using Dart, like all of these low-level bindings that you have by using Dart language to the low-level languages.

We will show you in a second.

First, Rust.

Like, Rust has started off in 2006.

It was a personal project.

Then it got bigger.

Mozilla became a sponsor of it.

They used it to create their own engine as well.

It became so big in the meantime.

The advantages of the Rust can be in four different categories.

The biggest part is memory safety.

In Rust, whatever you do is immutable out of the box.

If you want to have something mutable, you need to do it yourself, and you need to be in control.

Memory safety comes with many different aspects of Rust that I'm not going to tell you now.

But one thing that you need to know is that Rust brings out--

Rust comes as a control for you, and you need to control everything that you create and bind everything to a point until you create your application.

You will not be even able to run your application if there is an open ending.

Rust is a syntax that you will see that it is really familiar to the languages that you know.

It has a main function.

It has cool features like pattern matching and so on as well.

And syntax is quite familiar if you're coming from C, C++ world, or languages like Kotlin or like Objective-C also-- not Objective-C. C# also actually had an impact on the language as well.

Lastly, in the Stack Overflow survey, you might see that Rust is the most loved language.

Everybody loves it.

The reason is that the community is too vibrant.

They're constantly bringing something new.

And everybody wants to see something new in an easy way.

And luckily, they are bringing this in by creating libraries called crates.

Rust has its own packaging system like we have in Pub.

It's called Cargo.

And when you use Cargo, you can also use it as a CLI tool as well as your packaging system as well.

So let's see how you can create a simple application in Rust.

First, you will use Cargo new and the name of your application.

Once you create the application, it will look like this.

It will have a main file.

It will have a cargo.toml file.

This toml file might sound familiar to you.

It's like the pubspec.yaml file that we have.

It is keeping the configuration information for us.

In the cargo file, you will keep the libraries and so on, or give the library information as well.

Like Dart, the entry point of Rust is also main.

The main function can also have parameters that are passed by CLI or the entry point of your application.

But everything happens from the main function.

The main function here has a simple print line called hello world.

In this hello world example, you might see there is an exclamation mark.

This exclamation mark is called Markrows.

And Dart actually takes advantage of it to create strings that are concatenated, and basically anything that you-- this was a super simple example, because we have many folks who has not done any Rust.

But it is basically giving you a higher chance or a higher power of using functions here.

So how you create functions is you will use the let keyword like you would do in Drift.

And you can either define the type of the data,

Or it will infer the type as well.

It is totally up to you to decide.

And you can also have, like I said, the pattern matching on strings.

Or you can have range for the integers.

Or you can have Boolean checks and return any value that you have given type.

And in here, for example, you can see in the name example, it picks one of the names and prints whatever it is.

It checks out the age.

It checks out if it's new or crazy or whatever it is.

So right now, let's keep this function in mind.

When you create a function, you write fn as a keyword, and you write the name of the function.

When you write the name of the function, you will put underscores in between the words.

Let me be on time.

Yeah, perfect.

And in the main function, if you go ahead and run this application, it will just say, hey, my name is Salih.

I'm 30 years old.

That is the output that I have when I run the Rust application.

The goal that we have right now is to actually run this by creating a Dart application as well.

So first, let's say Dart create fc.

That is like Flutter connection Dart.

And once you create it, it will have a template of creating a CLI application.

If you do not like this one, our friend, Hanan, created a nice CLI tool with very good, very good venture.

So I really like that one as well.

Anyhoo, so when you create it, it will look like this.

We have the bin and lib folders, and we will work on the lib folder.

So you will open up the lib folder, and first thing that we are going to do is to actually create a function.

This function is called introduce.

One thing that we are doing here is that first we are getting the path of our dynamic library.

The dynamic library is the library that you have generated out of your Rust application.

And if it's Mac OS, it's Dialib extension.

If it is Windows, it is the SRA extension, and so on, so forth.

For opening up or running the dynamic libraries, what you need to do is to call the FFI libraries dynamic library.open function.

It will go ahead and bring that dynamic library information to us.

And next thing that we are going to do is we will create two type definitions.

First type definition is the definition of the function that I call on the other side of the library.

The second part is its translation to my Dart code.

In here, what I do is I say, OK, go ahead and look up for a print introduction function that I have in Rust and bring that to me as a function.

And this function will be in the void type.

And afterwards, if I run the introduction, it is going to hopefully print out my name.

But before we do that, we need to change a couple of things in the Rust side as well.

So one thing that we need to change is we need to make our print introduction function public.

So we use the pub keyword here.

Also, we need to make it available for C library, and we're going to use the keyword "external" and saying that this is a C library operability function that is introduced to the outside.

And lastly, we have something called noMangle, which is a way for us to prevent this function to get lost in between, you know, like name shadowing and so on.

So, after we do this, then we mention that this function is going to create

And we will just build it. And once we build it, when we run the data application, it is going to print out what we had before.

Quickly, let's see how we can send and receive information.

The data types are similar as any other languages in Rust as well.

And here we have the integers that we are going to be using.

We will expect an integer value.

And we will expect a value of the

And we will just return the addition of it.

So, we build the library again.

You go back to our library and say, okay, the function that we called has changed. Now we are returning integer, not the void anymore.

So, what we are going to do is we will look up for a function, send out the numbers that we have, and expect the print -- expect the printout to have five. And when we run this function again, you can see that we have five.

And if you run this function again, you can see that now we have received the result that is calculated in Rust and showing up here.

But you might be asking, how about complex scenarios?

Like, what happens when I have complex objects?

The first thing that you can do is to actually use JSON to serialize and deserialize objects in both ways.

Because the communication will be faster if you are stick to the primitive types.

For the other ways that you can do is you can use a platform agnostic language like Protoss or like the Smitty from--

OK, this is the first time that I'm going to say AWS.

And it is going to give you a chance to generate models and so on in both platforms and keep it consistent as well.

And once you do this, you will have like platform agnostic contracts between the platforms, and you would be able to actually go ahead and run complex objects as well.

Lastly, I want to give a shout out to this library.

It's Flutter Rust Bridge.

Everything that I did earlier on, I did it by hand.

But in complex scenarios, this Flutter Rust Bridge is actually the binding library that I would recommend you to use, because it will do a lot of code generation for you by using FFI gen, behind the scenes, and so on.

And it will give you a chance to also serialize and desterilize your objects as well.

It's really great.

It is memory safe.

It gives you the whole power of Rust in the Dart side as well.

I really like using it.

So in complex scenarios, I think this is a great addition to your project.

For resources, you can check out the docs that I shared over there.

And these are the social media links that I have in case you have a question and want to reach out to me.

I think I am on time.

So thank you very much.

And yeah, have a nice day.

[APPLAUSE]

> > Thank you, Sally, for the great talk.

I have a first question.

Don't forget to send yours.

So you showcased here a Rust application integrated in Dart application.

What about portability?

How would it work on iOS device or mobile device, desktop device, because we just talked about it?

> > Yeah.

> > How would it work?

- Excellent question.

Earlier on in my career, I worked on an app that has taken advantage of Rust in a way that it was working on all platforms, not only like Mac OS, Windows, it was also working on mobile as well.

The reason that we picked Rust is that it has, like I said earlier on, a way to even write native code inside it to make a communication with the platforms that we want to attack, not attack, but to attach.

And that's why I need the beer.

And--

[CHUCKLES]

Like--

Backstage.

Yeah.

So that is why, like, Rust portability comes with its flexibility as well.

So when you are able to write code for the platform that you're hosting on, all you need to do is to let Rust take care of the platform that you belong in, because it understands where you're running it and which platform that it's operating at that moment.

And then the portability part is not a problem.

You just still communicate with it in the Dart code part.

Because that's why I used the Dart code example here.

And it's not ready yet.

I promised Hanon to make it open source on Monday.

So I will have an example of how you can, for example, create a file picker that is only working on Dart CLI, which is pure Dart at the end of the day, to select a file in Windows, Mac OS or something, and upload it to the S3 buckets, and to prove the portability part of it.

So yeah, TLDR, it's portable.

- Awesome, and we'll see more on Monday.

- Yeah, exactly.

- So I have another question about developer experience.

How, you gave an example of the add function, or what if the interface of some REST function I'm calling, changes, would I get on the Dart side a lint error?

Would it just break at compile time?

At what point in my developer experience would I get the warning?

So the process is actually quite straightforward, like you would do with any other libraries.

At the end of the day, when you change something, when you break something in the application, if you load that library, if you break something in the library and load it in your project, then it break in the compile time. You will not wait until the runtime. Because the contracts that you have, the signatures of the functions, if they change, if anything related to it changes, it's not dynamically typed. It's actually like works in a type way that you would know if even a type of the data that is requested has changed as well. So one thing to keep in mind is that once you

If you create it for the first time and if you are responsible for creating both signatures of the functions, what you would do is if you wrote something wrong in the beginning, then it will break in the runtime.

It will say that, hey, you're trying to call an integer, but it's not an integer, it's returning a void.

And then it would break at that point.

It works like unit test at one point, I would say.

So you showed us this example of Dart talking with Rust.

Will there be other languages that would be interesting apart from Rust to connect to Dart?

Yeah, like C and C++. I think that was the first thing that attracted a lot of people.

Like any other low-level languages that people would like to have, if they support FFI, then it should be fine.

Because at the end of the day, the FFI logic comes from the fact that being interoperable with the C as well.

So Rust gives you a chance to publish a function in a way that it might be interpreted by the receiving end as a C language parameter, even though it's not.

So that's why, like, we need to, if the language supports, yeah, why not.

Maybe one last question from Mathieu.

Dark to Rust rely on FFI. Do you think it's possible to build a code generator to create a direct interface between Dart and Rust?

100%. The thing is like, it's a lot of work, but at the end of the day you can say that it's not a magical thing, it's science and it can be portable.

Also what you can do is you can make the...

Like, the Dart FFIs point is to make it available for the C and C++ kind of languages.

But if you want to make it special for Rust, you can make the Rust do the heavy work for you and just a simple connection from the Dart side.

So in my opinion, the answer is yes.

But we need to discuss the engineering details, obviously.

Yeah, great.

We'll probably encounter some problems, but...

Yeah, I mean, I want to encourage people, we all know that writing software is not easy and just like runs somehow.

It takes time.

Thank you very much, Sadiq.

Thank you very much for having me.
