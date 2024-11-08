---
slug: >-
  /talks/frenchkit/swift-connection-2023/herve-berenger-playing-with-the-limits-can-your-app-run-arbitrary-binary-code
date: "2023-09-21"
title: "Playing With the Limits: Can Your App Run Arbitrary Binary Code?"
author:
  - Hervé Bérenger
video: fvuUIwnAwJA
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/fvuUIwnAwJA.jpg
slides: null
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---

Hello, everyone.
I feel a bit stressed.
We are together for more than one hour, if I don't fall.
So yeah, what are we going to do now?
Well, the talk is entitled "Playing with the Limits and Running Arbitrary Code."
And in fact, between the moment when I submitted the talk and today, I did some experiments.
And not everything went as I expected.
So in fact, I have slightly redefined the talk.
So precisely, we have two objectives today.
What I would like to do is first, side loading.
And second, well, by trying to do so, learn some stuff with trial on many errors, and try to apply it in a fun way.
What do I mean by side loading?
Well, in general, if you have an application and you want to have users to download it,
You have to submit it to the App Store review, kind of gate.
And hopefully, if they are in a good mood, they will accept this, and your app can be downloaded on a user's iPhone.
And what I define as side loading is the fact of somehow-- we don't know how yet-- is that I have some code on my side,
And I managed to shove it inside the application without crossing the gate.
So it's side loading because we are jumping over the fence.
Of course, you may think, oh, is this legal?
There are good reasons to do this.
There are bad reasons also.
Today, we'll talk only about good reasons.
It's not a talk about side loading.
Let's talk about legal stuff that we can do.
And so we saw the what, and now the why.
Why would we sideload stuff in an application?
There are several reasons.
The first one is related to some licenses, some software licenses.
And in fact, it was at the origin of this talk,
Because a few months ago, a colleague came to me and asked whether I could-- he wanted to use LAME, which is MP3 encoder in an application.
And he asked me, would it be possible to load a zip on the load LAME in your application?
Why?
Why would you do this?
Well, because LAME is under LGPL, which is the lesser general public license.
So it's not the GPL, meaning that if you use LAME, you do not become GPL.
It's less restrictive.
It's a bit more restrictive than other popular licenses, like MIT or PSD.
And one of the interesting aspects of GPL, of LGPL, is this one.
You see, it's the text of the LGPL license.
They say that any user using LAME, in this case, should have the freedom and the possibility to run your program with a modified version of the library.
Meaning that someone could see, OK, I use LAMP, but I have my own LAMP.
I prefer to use mine because I know what's inside precisely.
So I want to use my LAMP on your application.
So of course, if someone wants to do this, he cannot ask the App Store to take his LAMP.
So if you want to do so, we have to side load in the application.
Another reason is related to bug fixing.
But imagine sometimes you have your application in production, and one day you realize that there is this beautiful bug inside it.
And it affects a lot of users.
And you would dream-- and you know what the fix is, but it will take several days to have it validated by Apple.
So sometimes you dream of some magic replace the bug by this nice green animal.
Butterfly, sorry.
So this is called-- yesterday, one speaker talked about hot reload while you are developing.
So this is also a kind of hot reload, but it is a production hot reload.
And in this case, we hot reload only like a bug fix,
But we could think of a more wide plugin architecture where you could sideload many modules with the same principle.
And in fact, why I want to do this?
Because it already exists.
On iOS, in general, we hardly do this.
But in the React Native--
I don't know if among you there are some people doing React
Native.
On React Native, there is a tool called CodePush by Microsoft, which also now exists on Flutter, which allows, due to the dynamic properties of JavaScript, which allows to reload stuff in production.
And say, OK, is it fine?
Is Apple Review well at ease with it?
Well, it happens that if you go on the code push issues, on the code push repo, on GitHub, you'll see many, many issues such as this one.
People sometimes get rejected by the Apple review.
I like this one, because the step to reproduce is review the app.
[LAUGHTER]
And up to the point that they have a whole section in the readme where they try to explain that, yes, it complies with the Apple guidelines, so long as you do not significantly modify your application.
And this point is very important, as we can see from the Apple guidelines.
What does Apple say, precisely?
So we have the guidelines and the developer agreements.
So in the guidelines, they make it very clear that you cannot download, install, or execute
Any code which changes the features of the application.
So if we apply this strictly, side loading is forbidden.
And in the developer program license, it's a bit more precise.
So they say, OK, you cannot download binary code.
But up to some condition, interpreted code, the code which is not compiled, may be downloaded if you do not change the primary purpose of the application.
So this kind of opens a window that could be considered as perfectly fine for Apple point of view.
But as long as you do not try to transform your application from the inside or to fool the App Store review, in fact, it can be accepted.
And there is another point in the guidelines.
I mentioned that for educational purposes, you may be able to really download executable code.
This was interesting, because if they say this, maybe it means that it's somehow possible to do it.
So this confirmed-- when I saw this, I said, OK, it's possible.
We'll try to do it.
OK, so let's try to side load.
Ah yes, one more about it.
So concerning the Apple review, it's always the case of, in legal terms, there is a letter of the law when you follow strictly what is written in the rules.
And there is a spirit of the law.
And I think that from some aspects, side-loading does not follow the letter of the law, but it respects the spirit of the law.
Or I don't want to break the spirit of the law.
In fact, I don't want to be evil.
I don't want to fool the App Store.
Just like, for example, I want to fix my bug in production.
So what is our agenda today?
This is our agenda.
There are many acronyms that we will try to understand.
So if you are very familiar with every acronym in this slide,
Maybe you will not learn anything during this talk.
I hope not.
But first, I need to start by some basics.
I'm sorry.
I will say very simple things at the beginning, but I don't want to lose anyone.
And we have all different backgrounds.
A few weeks ago, I was speaking with an Android developer.
And we tried to make a CocoaPod work with Kotlin Multiplatform.
And I said, OK, it's a link issue.
And the Android developers say, what's linking?
I realized that it's OK not to know what linking is, because when you work in the Java world, this concept is less important sometimes.
So very basic things.
Compiling, we know what it is.
It's a fact of take some high-level language and turn it into some binary form.
We call this object files.
And linking, when you have several units of source code, at some point, to have your whole program, you have to glue this stuff together.
And one important aspect of this is that you have to establish links between different parts of an object file.
For example, here, the top part calls a function named sum.
But when I compile main, I don't know what sum is.
It's only when I link that I can find sum.
On the other side, I have compiled sum.
So the job of the linker is to make the pointers point to the right functions.
So compiling is the task of the compiler.
So in our world, the Swift compiler is called Swift C.
And the C compiler, Objective-C compiler, is called C long.
And you may have heard of GCC, which is the famous Unix compiler.
I thought it existed on my Mac, because sometimes I used it.
But in fact, it's-- maybe you can't see this.
There is an alias.
When you use GCC, in fact, you just call C long.
So GCC does not exist anymore by default on our platform.
OK.
On the linker, maybe the name of the linker is less well known.
On our Apple platform, on Unix platform, the linker is named LD, or LLD.
And why does this acronym?
It's because it's derived from the-- it's a very old term,
I from the-- dates back from the '70s, like me.
By this time, the linkers were known as loaders, so in short form, LD.
Good.
Now, you may have noticed in the previous slide that--
OK.
But at the end of the process, I still have your reference to print.
And print is not defined in the compilation units.
So when this compile on link code will run, we have to find where a function named print to call it.
So how can we know where is print?
If you run xcode and attach your debugger to it, you can ask xcode.
It will tell you that print seems to be a function.
You see which slaves in a library named libswiftcore.dailib.
And so at some moment, there's some process which must match your pointers on the system libraries.
And this process is what we call dynamically linking.
So we can link statically at compile time or dynamically at runtime.
Mind the extension.
There are two kinds of object files.
Object files that are aimed at being linked statically, and object files that are aimed at being linked dynamically.
We call them static and dynamic libraries.
And dynamic libraries have a suffix which is naturally
"dilib."
It's important because often when we see all these error messages, it's a word which pops up.
So Dailyb, suffix of dynamic libraries.
Good.
Fair enough.
A short word also about frameworks, also very basic.
But on iOS, we do not manipulate raw Dailyb files.
Every object file is wrapped in a framework.
That's an iOS term, which is-- well, you probably know it.
Just, in fact, a framework is a folder which contains an object file without extension.
Why?
Because the object file can be static or dynamic, so you cannot suffix it.
If you want to be generic, you cannot add a dilute suffix.
And also some resources and a signature, basically.
So on the screenshot, I think it's an Amazon framework, where you can see in the folder when you open it, signature, some resources, some JSON, pictures, and your binary.
Great.
Well, and just with this, we can start to play a little and to solve some issues.
There is one common issue.
I think the Stack Overflow question has more than 1,000 points.
It's when you add a framework to your project,
You never know whether you have to embed it, or embed it and sign it, or do not embed it.
What does it mean?
And I want to answer this question once for all.
So this will be our first demo.
Here we go.
Oh, yeah.
It's not this one.
Start well.
So I made a very short project named Library Demo App, where I have a static library.
Beautiful.
It is with function returning 42.
So it's linked statically.
And if you want to know where does it come from, there is a type-- I'm sorry, but the Xcode, even in presentation mode, the settings are not very well zoomed.
So you have somewhere-- that's the macro type, and it was not at the right place.
Macro.
Here, OK, in your settings, the macro type defines the type of linkage that you expect from your library.
So this one is a static one.
Great.
And of course, the second one is a dynamic one.
Well, same thing.
And I have this project, which tries to link both of them.
These are my frameworks.
I have a third one, but it's not important.
So I have my dynamic framework on my study framework.
So should I embed or not?
Well, what does embedding mean?
Embedding really means wrapping.
If I build my application-- great.
Why is it here?
Here you're pointing to the derived data.
Now I'm going to do something that you have to do sometimes, because you want to know what you generate.
Here is my application, library demo app.
On an app, it's a bundle.
A bundle is a directory.
So you can open it.
And here you see what's inside your application.
And OK, where-- oh, yeah, I have one.
And embedding simply means that your framework will be copied to the destination bundle.
It just means this.
Embed, you wrap it with the application.
And in this case, you see dynamic and static are not embedded.
And the localize is embedded.
So logically, so I'm inside the application.
Inside the application-- I hope you can see something.
Can it be closer?
There is a framework directory.
And inside, all the framework that you have embedded.
Fair enough.
Now, you probably guess what I should do with static-- my static on dynamic framework.
The fact is that Xcode does not make any setup by default.
So let's try to run this application.
OK.
Yes, it's my iPhone. iPhone de papa de Cleo.
It's my daughter.
And it crashes.
Damn.
Why?
What happened?
I will just switch back to the application.
That's the error message.
And one thing I want to do during this talk is that I want you to be able to, when you see such kind of error message, not to scream, but to say, OK, I will understand everything what happens.
So this is our error message.
You have several words, important words.
Here, the first one is dialed.
I did not mention it, but dialed.
You remember when I said that somehow, at runtime, the program has to find its dependencies.
Well, this is the job of a program named DyLD.
And here, it's DyLD with a screaming.
And he said that he could not load some library, a library named DynamicLib.
And this library was referenced by what?
By your application.
You see there is a full path with your application bundle of the binary of your app.
So your app tried to load a framework, logic, because you linked with it.
But it didn't work.
Why?
Well, I'll tell you what it tried.
It tried to load it from several locations.
As you can see, it tried to load it from the directory that we saw inside the bundle.
So inside the bundle, that's line one, there is our frameworks directory.
And we try to look at it here.
But it was not here.
How can we say that it was not here?
And now we are back to the '70s.
We say, Erno.
What is Erno?
If you have done some system programming,
Erno, it comes from the C of the system programming is a Unix world. just a global constant, which if you call some system API, you have an issue.
You don't return-- it does not throw or return you an NSError, but just it puts an error code in this global constant, which is Erno.
It's error number.
And when you have more than 40 years, you know that Erno equals 2.
You can fetch the Erno error codes.
It means not found.
So here, we have the reason why we can understand the error message.
DLD tried to find the framework, but simply it did not find it in any of the directory.
Cryptexes is the name of some pre-compiled encrypted disk images which are inside the OS, a place where some system libraries can be found.
So it was not there.
Also, you also try to look for your framework inside the system directory, in case it was a system library.
And it didn't find it either.
So it couldn't do anything, and it tells it to you.
And of course, if-- well, it's not very useful.
But yes, it's useful.
Should I embed or embed unsigned, or embed without signing?
In general, select sign, because everything which runs on iOS has to be signed in any way.
So in which occasion should you need not sign?
I think that-- well, in my case, I never had the opportunity.
Or maybe I would be glad if you have more experience with some edge cases when these settings value have to be used.
I'd be glad to discuss with you about it.
But in my case, I never had to use embed on the node sign, or always sign in.
I guess that sometimes you don't want to sign if you have some script on the other side who do the signing, and you do not want mess with your signing script.
So now, logically, if I embed--
OK, it's-- we are--
OK, fine.
We're printing the sum of our work.
Good.
Great.
First exercise done.
If I-- yes, I could show you-- how can you know that--
I will give you some tools that can sometimes be useful.
When you want to know whether a framework is dynamic or not, it's very easy.
So you go to your derived data here.
Yes.
When you have bookmarked your derived data in your finder, it's that you're doing fancy stuff in general.
So I will just have a look at here.
That's my dynamic library.
OK.
So if you want-- so I'm inside the framework.
And if you want to know which type of framework you have with you, well, just there's a simple command.
It's file.
Simple as ever.
And file tells you that this is a dynamically linked shared library.
If it was static, it would say that it's a static archive.
And also, yes, how do we-- you remember the Xcode complaint about the name of the library?
But how can you know it?
How did you know that you had to find this one?
Because at link time, we put the nickname of the library inside the main binary.
And sometimes you need to know how your library is known by the system.
And I think it's o2 minus d.
Here we are.
And you see the full name of your library, airpathdynamicclip.framework.
Airpath means-- airpath, it's a runtime path.
It encodes in the library or in binaries some search directories.
So when you link the application,
Xcode put airpathdynamicclip.framework/dynamicclip in the main application and in the framework.
And at runtime, they can find each other. so that at runtime they can find each other.
God, the time is passing so fast.
Well, fine.
Let's go on.
So this was our error message.
So we saw what embedded mean, the app.null is a folder, file to know what type of framework is.
And DILD is a loader.
So in more detail, what is DILD?
So DILD, it's a dynamic loader.
It loads and wires all the what we call Macro files.
It's the name of the object files on Mac OS.
And the important thing to have in mind is that it will run before your main starts, before your application starts.
Because it's going to main your binary runnable.
A Macro file is anything which is on a build on iOS.
And if you wonder where does Mac comes from, which has a very long story.
The term is about 38 years old.
So if you are less than 38 years old, you have to treat macro files with respect, because it's a venerable thing.
What does a macro file look like?
A macro file is divided into several sections.
There are always three sections in the macro file-- the text section, data sections, and linked section.
In the text section, you will find what we call the header.
We have many metadata about the file and the architecture for which the file is destinated.
Some load commands, which describe the dependencies of the macro files.
And your code, most important.
It's funny that the binary code is a text segment.
And there is a data segment with some global constants and an indirection table.
We'll speak about it later.
And what's important to know is that those different sections have different permissions when loaded into memory.
So the text part is executable but not writeable.
And the data part is writeable but not executable.
And why?
Because when I have my compiled code,
I don't want it to be modified when it's executed.
Good.
We'll speak about this later.
Now, this is a Macro file.
And there is something complicated that they did do, because we could think, OK, we just have to find the dependency, put the file in memory, and it's fine.
The thing is, when in your compiled file, you have pointers.
And the pointers, they have a value in the file.
But the value is necessarily wrong, because it's not loaded into memory yet.
So when-- and the problem is that the pointers in the text part are wrong.
They are not necessarily wrong, because there exists one address, which we call the preferred address of the macro file, where the pointers would be exact.
But in general, it is not satisfied.
So the pointers have to be changed,
But the text part, the text segment cannot be modified.
It's a paradox.
The solution is called position independent code, meaning that all the addresses in the text part are relative to the data part.
And at runtime, what they really do, mainly, is writing in the data part to adjust the pointers.
So here it is.
When I load the macro file in RAM, some pointers are wrong.
And even in the data part, here you have some proxy.
It's a reverse pointer to the function named sum.
But it's not at the correct value because they are xy offset.
So what DLD does, it does two things.
First, what you call rebasing.
We add to each address the difference between the address at which the macro file has been loaded and the preferred macro file address.
And the other thing we do is called binding.
And binding is for external symbols where you have to find the address at which you have to jump when you call a print.
So here it is.
Oh, and also the reason why the macro file address is-- pointers are always wrong in a macro file.
It's because of a thing named ASLR.
So it's ASLR.
It's not ASMR, which means address space layout randomization.
And it's an important security feature by which a macro file is always loaded at some random address in memory so that an attacker cannot predict where he will find stuff in memory.
But this operation is called rebase as both things.
So to sum up, the DLD algorithm is the following.
First thing that happens when you start a program is that DLD loads itself in memory.
Then it will introspect your app to find the dependencies thanks to the loader commands.
So in this case, we have, for example, those two dependencies.
This is a recursive process.
Now you have all the dependencies.
Next, you map them to memory in a random manner.
Next, you have to look up the symbols, the external symbols, under two-- oh, there's some step missing.
OK, fine.
Well, not too bad.
So you look up the symbols, apply the different fixings, call the initializers, and you are ready.
But this is a lot of stuff.
Let's see.
And why am I-- no, it was academic part.
No.
What is it useful to?
First thing it's useful for-- you have some time to understand this stuff when you want to fix the startup time of your application.
Because what takes some time as a startup, very often, is precisely all of these operations, which can take very long time. because typically an application has a lot of dependencies.
In general, we have hundreds of dependencies if you include the system libraries.
And you can add this macro environment variable at your Xcode schema.
It will print all the libraries you depend on.
And you can also come to fix up with this fancy Xcode command, xcrun.
And I run those on edging, which is one of our MWM applications.
And it happens that our mixing application has about 1,000 libraries and dependencies, and more than 350,000 mix-ups-- fix-ups, not mix-ups, sorry.
And also it happens that on very low-end phones, like your iPhone 6, it was measured that 2,000 rebases could take up to 1 millisecond.
So if you have 1 million rebases, it takes 500 milliseconds.
And it's a pity, because Apple recommends your app to start in less than 400 milliseconds.
So this is important.
And the problem is that every one year or two, there is a talk at Apple on how to improve your start time.
And the main advice they have is a bit disappointing.
They say, do less during startup.
OK.
I could have guessed it.
So they recommend to have fewer libraries.
OK.
Of course, not using the UN use frameworks.
And also, the other choice, the other way you can improve your startup time is by not using dynamic libraries, so by using static linking.
And well, it's very recommended for many reasons, including mainly for startup type to link statically your dependencies.
And in fact, this is what SPM does.
Because in the background, SPM does not compile on the framework you would depend on.
But when you depend on by code on some dependency,
SPM compiles it as object files.
And at the end, it's linked statically in your application,
I mean, if you are using a standard Xcode project.
But the problem is that static libs make your executable bigger.
And if you are developing an extension, while an extension often has some constraints on the size.
You cannot always use static linking.
So to improve startup type, use static linking.
We also recommend to use fewer classes.
This is because when you open the memory layout of a Swift application, you can see that for each class here, even if it's not an objective class, by the way,
You have a metaclass, a superclass pointer, metaclass pointer, vtable pointers.
And all those pointers require some fixing at startup.
So the more classes you have in your application, the more time it will take to start.
But of course, don't start replacing all your classes by structs, because you would have other issues.
And this guy would appear and say to you, oh, it's a pity.
We don't hear him.
It was Donald Knuth saying that premature optimization is the root of all evil.
So yes, don't replace all your class-based tricks to improve startup time.
Good.
My advice also, if you want to improve your startup time, is to wait, because every year, they bundle some improvements in DLD.
In DLD3 in 2017, they had the launch closures in the dark green here, by which they save-- once they-- the very first startup takes some time, but everything can be saved on disk, and then they reload it from disk the next time.
This is called the launch closures.
And yes, during the last two operating systems,
I've improved different parts of the algorithm.
Good.
No, more fancy stuff.
A nice application of what I said is called hooking.
What's hooking is the process of once all the links have been done in memory, sometimes you could think of, hey, what if I could rebind the links by myself?
So in this case, you see I have Firebase points at Swift core.
And at some point, when calling print, sometimes I may want to have Firebase call myself instead of calling directly a print.
And to do this for real, there is a great tool named Fishhook.
And in fact, I had to use it one day.
A few days ago I was developing-- so yes, the project is named John Lee, because John Luka.
OK.
Got it.
And I had to use Fishhook, because I was using a third party.
In this case, my third party is-- what is it named?
Yes, Fishhook is here.
Sorry.
So it was some third party.
And the problem is that inside the code of the third party, they had left a lot of prints and a lot of NS logs.
And this was important passages, but I couldn't get them because they were sent directly to iOS.
So my idea was that, OK, when this code will code NS log,
I will make it so that it calls me inside so that I can take the message, put it in my own logging system, and then send it to iOS.
Fancy.
And in fact, it's pretty simple to use.
The syntax is a bit not very funny.
So here-- good.
And here, yes, I'm launching the session.
And you see when launching the session, well, some logs are emitted by the third party.
So to prevent this, I just have to rebind the symbols.
This way, beautiful.
So what I'm saying, don't rebind symbol.
It's from fishhook.
So I'm saying that every time you see an nslog, well, instead of calling nslog, it's a bit like swizzling, but more deep.
You will call my own NSLog here.
But if you do so, well, we'll have some trouble, because you will also hook the NSLog, which is your own memory.
So don't do this.
You have to be a bit more subtle.
But being a bit more subtle consists in using terrible function names such as this one.
And here-- you see?
OK.
Here, it's a macro.
It's part of the macro library.
We have a function which gives us all the libraries which have been loaded into memory.
You just iterate on them, and you look for your third-party framework.
And you rebind the symbols only inside the third-party framework.
Good.
And the rest is similar.
Yes, when you play with this kind of stuff, objectives see rules, because in Swift, you have to have a whole mutable pointer everywhere.
It's hardly readable.
Good, and normally it should work.
Yes, and now when I'm calling NSLog here,
I should jump right here.
And you see, it's very fascinating.
Because here we are in the-- you can see, we are inside the third party.
It calls NSLog, but you are inside my code.
Got you.
If you want to do the same with Swift, you can.
But the problem is that in Swift, print is not called print.
So in Swift, I was saying that print is not called print because of what?
Because it's like in C++, you have a method overloading, meaning several methods having the same name, but different parameters.
So in C, on objective C, there can be only one method named nslog, but there can be many methods named print in Swift.
So the solution is to take the method name, take the arguments, hash this together, and we obtain what we call a mangled name.
And this is this name that we have to use if you want to mangle print.
And how do you find the mangled name?
Well, you have to go inside.
If you-- either you know it, either you have to go inside and look at it.
And to look at it, there is this nice tool called Opera Disassembler.
Oh, yes, yes, yes, yes, yes.
Can I zoom?
No.
Do you see something?
So we are inside the-- inside Oper.
And normally at some point, if I'm looking in the-- like in assembly strings, there's something named vaguely print which should be called.
OK.
And I think it's here.
Oh, it's already this one.
Oh, no.
Yes, here we are.
Here we are in a function named-- like load record, it was the name of the function is a third party.
So I know that it's in this piece of code that print is called.
So I find print here.
And you see-- well, here you will see the mangle name of the print function.
But remember, we are in the code.
So we are in the text segment.
This was the beginning of the talk.
So this is not the mangled name of print.
This is the mangled name of a stub which points in the data section where we will find the real name of the print function.
So just look at it.
Here it is.
So here we are in the stub.
Normally, this name here-- no, not this one.
Yes, it's this one.
You see it unmangled.
It's the name of the print function.
And if you want to be sure, you can type Swift demangle-- maybe I have forgotten the first symbol.
Yes, no, it's fine.
So Swift can demangle the mangle name, and you see that this fancy name is, in fact, the name of print with different arguments.
So if you want to-- this is a way you can hook Swift functions, and you just have to put the mangle name here.
So let's move on with more deep stuff.
Now we are ready.
We can side load a function, because we know how libraries are loaded.
So it happens that DLD has an API.
This is a C API.
It's a function named dlopen.
And also, if you want to play with this, it is wrapped inside Objective-C or Swift, because you remember a framework is a directory.
A bundle is a directory.
So if you initialize a bundle with the URL of a framework, and you say to the bundle, load, well, the bundle will load any code which is in the framework.
Let's see if we can do it.
[INAUDIBLE]
Thank you.
Side loading.
So it's a different use case.
I have-- so in this framework, I have a library named Encryptor, which does encryption, powerful encryption.
And I want to load it dynamically, because since it's a cryptic algorithm,
I may want to change the algorithm on my side if I improve my encryption algorithm, and just deliver it to the users without, well, we would be passing through the gate.
So how can we do it?
So this was the third party we want to dynamic load.
Here we are.
OK, well, I just run it.
OK, fine.
So just a basic iOS application.
First thing I want to make sure, just to convince you that I am not fooling you, is that I am asking whether this class is existing.
And it says, you already see it, but it says nil here, so OK.
The class does not exist.
And well, I want to load it.
Where is it loaded?
Sorry, I forgot one thing.
I want to say load it, so I want to take my third party here.
It's the iPhone 1.
So I will zip it from the application.
I will open a document picker.
And I will take a zip file, which is a library.
I will just unzip it.
Sorry.
So this is a media picker.
I take the zip file.
I unzip it.
And I call delopen simply on the path of the unzip file.
And after this, I try to run some code.
It's complicated to run code from a library that you have loaded because you don't have the header of what.
So one way to do it is to-- but if you know the exact interface of the code that you are using-- sorry, encryptor.
Here you see what we know, all we know is that our third party has declared an interface with a function named encrypt.
So what we do is that I will ask--
I will try to call a method with Objective-C, like performSelector.
I will-- because I don't know that there's a class.
I cannot call the class because I don't have it in my code.
But it's loaded in memory.
So I can use performSelector if, of course, if the class is in Objective-C. And it is my recommendation, if you want to do this kind of stuff, still use Objective-C because it mixes very well with the low-level C API.
So I will call a perform selector on loan module yield to create a cipher instance.
And then I will try to cast this inside as a protocol pointer, an objective C pointer, so that it works correctly.
Or I will try to call encrypt on it.
So you see, I'm looking for my class, my loader.
I'm trying to perform a selector load module.
It will return an instance of the class.
And then I unsave bitcast.
We don't like to do it.
This is a pointer that has been returned.
You remember it was a Cypher instance into an interface.
And then the interface-- OK, this
I have declared it on my side, but it's logical, because I know what kind of code I'm using.
But it's only a protocol.
There is no object duplication.
So I cast it into the interface, and I call encrypt.
OK.
So this is the third party.
I have my-- in my data, I have my encryptor library.
Here it is.
Encryptor, it's here.
Fine.
Build.
Products.
OK. iPhone OS.
OK, I zip it.
Compress.
And I share it for AirPlay.
Fine.
So good.
Encrypt the framework.
And at this time, you see you are doing like nasty stuff, airdropping something.
And you load it.
OK.
Oh, and it did not work.
Fine.
Good.
Yes, it did not work, because it was the first part of the talk, because I did not sign the framework.
[LAUGHTER]
Good.
But it's a good thing.
Signed.
It was expected.
Yes, you can see the error message here.
It says, no, we are not afraid of error messages.
It says that, well, the framework is not signed.
So yes, we all said that it was because of code signing that we could not load the application.
So the next section was about code signing, precisely.
And with code signing, what I wanted you to know is that a certificate tells who you are and that you can compute hashes.
But we won't have time.
OK.
All this-- anyway.
And the signature is bundled inside the macro files.
Yes, I will skip this part because it was a lot of console stuff.
And yes, and if you sign, well, it works.
Just believe me, it was very well.
It works, and I was so proud that at this moment,
I answered the call for paper for the conference
Because I was the king, I said, I can do this.
And by the end of August, I tried on a real application.
I generated a test flight, which I did not hit here.
And it crashed.
And it was the core of my presentation.
So I was feeling bad.
Why did it crash?
Well, it crashed.
You are missing a very interesting thing.
It crashed because of mmap, you see?
And I wanted to show you mmap system call, which is a call which loads images into memory.
And it happens that on the test file, this that I couldn't show you, works on a test device, but not in production.
Because, well, if you read the code of the DLD,
So you can understand that, in fact, there is an absolute limitation on iOS is that DLD can only load a framework which is either a system library or inside the model of your application.
And it is a fundamental security feature of iOS.
So what I wanted to do is just impossible.
So the next step is that since DLD did not work,
I wanted to write my own DLD.
And this I can show you.
Yeah, it's very fun.
So how can you write your own DLD?
I like the way it is.
OK, DLD does not want to load my library.
I will make my own DLD.
Where is it?
Yes, I did it. a very simple framework named Parabola, with only one function called square plus.
It's a function, and it does this.
I wanted to do a poke that I could load this framework and call it.
So because you know, DLD takes some bytes that are in a file and put them in memory, and just tells the stack pointer, go there and run it.
So why I wanted to try to do this by myself.
So to do so, again, you open your favorite tool,
Opera Disassembler.
Okay.
Okay, Opera.
File, open.
Okay, Parabola.
Build, products, debug, Parabola.
Parabola.
Good.
So the name was square plus.
Yes, this function is very simple.
It's just this piece of code.
It does multiplication, but it's not very important.
And you can take the hexadecimal code here.
This is this piece of stuff.
So I take the bytes.
And then I put them all inside my application.
So I took the code here.
And when I will press on the unlock or run,
I take this code.
I allocate some memory.
I copy the raw stuff in memory.
Good.
Now, the first time it crashes because the memory is not ready to be executed.
Then I take a function pointer, and I say to this function pointer, point to this memory and run.
So I have a function pointer that points to my raw byte here, and I tell him compute square plus something of x with x again mil, 1,000.
And here we go.
POY2.
OK.
It worked.
[APPLAUSE]
That is something to work.
OK.
So I was very happy with it, so I unplugged my phone and I showed it to my young daughter.
And it immediately crashed when I unplugged Xcode.
Why this? Because in fact, what I did here was that I was breaching this important security principle, which is called W XOR X, meaning that a zone of memory cannot be writeable or executable at the same time.
So mine, I write some memory and then I try to execute it, so the system did not allow to do it.
But why did it work with Xcode attached?
It's because Xcode modifies your code when you set a breakpoint.
Maybe you ever wondered how a breakpoint works.
When you set a breakpoint, Xcode adds one line in your code which raises a signal exception and when Xcode can intercept it.
So Xcode has the possibility to run on the execute code, but not yourself.
What have you missed?
We have reversed engineered some applications which say that they seem to do it, but they don't.
At some point I was tempted to use some JavaScript.
No technological discrimination.
JavaScript is great because of the James Webb Space Telescope.
There was an astronomy moment, but this telescope is operated with JavaScript.
Incredible.
It's here, Lagrange Point.
So they can update it in five seconds.
So I want to update my application in five seconds.
But say, OK, JavaScript, is it easy, fast?
Yes, no.
No, because of just-in-time, which is not enabled on iOS.
I thought it was fast because I first ran the test on Mac OS.
On Mac OS, JavaScript core is fast because you have just-in-time compilation, but not on iOS.
And in fact, on iOS, I did a benchmark with a function called prime counting function, which counts the number of prime number below some value.
And it was 50 times slower than native code.
OK.
So then I tried to run intermediate representation of LLVM because of Quin V. Esquimaux.
This was a kind of joke.
So there was a part on LLVM explaining what is the intermediary representation, which is what the compiler produces that LLVM optimizes and then you generate some binary.
And well, I find-- so this is the intermediary representation.
And I found this interpreter in Chinese with two stars. and I spent a few days with it, and it did not work, so I quit.
[LAUGHTER]
And then one day-- OK, maybe three minutes.
And then one day, I fell from my toilets, and I threw this.
And this was WebAssembly, in fact.
And WebAssembly-- well, you know what WebAssembly is.
It was great.
We use it at MWM.
We have ported our audio module on a website.
Very interesting resources.
But I made some experiments with JavaScript.
For your experiments, try with C. Start with C on the M script
M. And there is also an interpreter of WebAssembly.
And this is why I started--
I tried it because I said, hey, I could put a WebAssembly interpreter in my application, compile some Swift to WebAssembly, put this on a server, and download it in my application.
And this way, I would sideload not binary code, yes, but WebAssembly code.
And if it is fast enough, it's about as good as binary.
And well, I quickly discovered that it was feasible because we have a very fast interpreter, which is called WASM3.
I did some benchmark with the same benchmark.
If you want to play with this line in green, here it took me several hours to find the right one before being able to compile and load.
And once you do it, it looks the same as JavaScript.
Instead of evaluating a script, you load an interpreter.
You can add some callback functions and just call a function.
And it happens that in release mode, interpreted WebAssembly on iOS on device is only five times slower than a native code.
So this becomes pretty interesting.
Also, there is a Swift project, but very oriented for the web, which can produce WebAssembly binary from Swift.
OK, I had a lot of trouble with Wazy.
And the problem also is that if you put a WebAssembly interpreter in your application, you have a kind of virtual machine which uses 32 bytes addressing in the app, while you are using 64-byte bit addressing.
So when you want to communicate, it's a bit complicated.
You have to ask the VM to allocate the memory to have 32-bit pointers.
The YZ binding is too long to say.
And what's incredible is that with Swift WebAssembly, you can use in your interpreter a large part of the foundation library, and even use codable and decodable.
So this was-- it simplified my life to serialize data from the virtual machine to the main one, to the main application.
OK, so the performance are terrible, so you can use some kind of proxy to switch between memory addressing and raw data.
And maybe if we can take one minute.
[LAUGHTER]
[SPEAKING FRENCH]
World premiere.
I will try to put an application in live, in production, during a conference.
This application is fine.
Does it still work?
Yes.
This is an application which you take some music, and it generates a nice web form.
And then you can export a video and share it on a social medium.
So this animation here has been computed in WebAssembly.
And what I would like to do-- and it's the application in production, right?
The one for which I had some letter.
And I have a workspace with my main application on the WebAssembly part, which is in Swift.
It's incredible, because you are really writing some kind of Swift.
And what I would like to do maybe change the color of the application.
OK, so I will put some rainbow color.
And I could also maybe add some other applications.
So I have used-- because you don't have UI kit in Web
Assembly, so I'm building some entities which represent the main parameters of animations.
OK.
And here I'm doing calculations because it's
Better than a JSON.
It's not just I change the color in a JSON.
You can change your code, actually.
And I create layers with different applications, with different animations.
Good.
Set the Swift-- sorry.
OK.
Swift connection.
Remote animations.
Here I have a script which builds the Swift code and puts it in the application directory.
./build/webassembly.
Optimized for production.
Good.
Here I have-- where is it?
In my resources, I have the WebAssembly file.
Join finder.
It has been generated right now.
I will compress it.
Good.
OK, jump.
Take it.
No, please.
It's in the-- yeah, yeah, yeah.
Come on, come on, come on.
They are eating me in the--
I will not leave this stage until it works.
OK.
So now-- oh, it's in production.
It's imported.
I wanted to have you count down to five.
Three to one, OK.
And now I will just launch this application.
So it has detected that there was a new binary.
The fact is it's a bit heavy.
It takes a few seconds to download.
And if I play here-- yeah.
[APPLAUSE]
So sorry for being so late, really.
But this is a world premiere.
We have put some code into production, some Swift code in production in a real application.
And that's when it takes to update the space telescope.
So well, thank you very much.
I had also many--
I hope we can discuss together about all this stuff.
Thank you.
[APPLAUSE]
