---
slug: >-
  /talks/frenchkit/september-2023/ibrahima-ciss-swift-macros-the-key-to-efficient-and-elegant-code
date: '2023-09-21'
title: 'Swift Macros: The Key to Efficient and Elegant Code'
author: Ibrahima Ciss
video: 4sHbfdBE6eI
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/4sHbfdBE6eI.jpg
slides: null
tags: []
year: 2023
conference: frenchkit
edition: september-2023
allow_ads: false
---
Hey, guys.
Bonjour à tous.
So today I will be talking about Swift macros, the key to efficient and elegant code.
So for those who don't know me, my name is Ibrahima.
I am an iOS engineer from Senegal.
I work at Zappo, a private bank.
I am Bionic6 on Twitter, or the exiting.
And I do some YouTube video on iOS mastery dev.
So before starting this talk, I want to thank the conference organizer for having me in this beautiful city and for organizing, obviously, this pretty cool conference.
So maybe a round of applause for them.
[APPLAUSE]
All right.
So now, without any further ado, let's get started.
So-- oh, OK.
So we're going to talk about the new Swift macros.
So first, what are Swift macros?
[INAUDIBLE]
Second, we're going to talk about the different types of Swift macros we have.
After that, we're going to build our own macro with some live coding, the second live coding.
I hope that Xcode will behave just right with us.
And we're going to close this with some shortcomings when it comes to macros.
Now, what are macros?
So a Swift macro is just a compiler plugin that extends Swift language.
And basically, what you need to know about that is that it's going to help you generate some code, right?
Like you write a macro to generate a new code.
And why to do that is, obviously, to reduce the amount of boilerplate code.
But when it comes to reducing the boilerplate code, we already have functions, right?
Regular functions, right?
We all use regular functions to keep our code dry, right?
To don't repeat ourselves.
But the particularity with Swift macros are that they are compile time.
We have some help from Xcode, since they are compiled time -- since they are compiled time -- since we have compiled time checks, and, yes, XCode can help us generate some compiler errors while using them.
So, we do have two types of macros.
The first one is a freestanding macro.
And the second one is an attached macro.
And we even have some subtypes.
But for the first one, the freestanding macros.
So those kind of macros appear on their own.
So they don't need to be attached to a type, right?
Like a struct, a class, or a enum.
And they always start with the hash sign, I think, right?
And generally, they also return a value.
So still for the freestanding macros, we have a freestanding macro, which accepts an expression,
And a freestanding macro which accepts a declaration.
OK, now let's talk about the attached macros.
And as the name implies, those kind of macros are attached to an existing type, right?
Either a struct, an enum, or a class.
And so they always start with the @ sign.
And for those kind of macros, we do have five subtypes.
We have an attached peer, an attached accessor that can generate some getter and setters, an attached member attribute, an attached member, and an attached conformance that you can use with your protocol to conform to them.
And something worth mentioning is that you can have many attached macros for types.
So you can use an attached accessor and an attached conformance for one type.
All right.
So now I think it is time to build our own macro, right?
Let's do it.
[NON-ENGLISH SPEECH]
So OK.
OK, can you see?
OK.
I'm going to close this and that.
Here we go.
So in order to create a new macro, we can come here, new file, and create a package.
And for the package, now we have these Swift macros.
OK?
Let's click on Next.
And we are going to call it a secure URL.
Let's say that we have an iOS app, and for that app, we only deal with secure URL.
So URL starting with HTTPS, right?
So I'm going to call it secure URL and create that macro.
Let me maybe zoom.
OK, expanded.
So here, we already have a template.
When you create a macro, it comes with this template.
So let me expand this.
So we have those-- OK.
So we have inside this source folder, we have actually three other folders-- the secure URLs, the client, and the actual URL macros.
And let's see the manifest file, this package.swift file.
You can see here that you have this new compiler plugin support, which is new.
And what it allows us to do is to import, to have this macro, this macro target.
So it comes with-- oh, no.
So it comes with this new import thing, right?
And we do have also this Swift syntax, which is imported directly.
So technically, you can write a Swift macro without this Swift syntax, but it will be super difficult.
So the recommended way is to use Swift syntax, which is kind of rude sometimes.
OK.
So after that, we have this macro.
And we have this secure URL macros here.
So this is where your macro code will be hosted in this secure
URL macro file.
And we have this secure URL.
Why it is not in the same folder or-- yeah, why it is not in the same target is that you don't want your app binary to import this secure URL target.
So here is this secure URL file is just for the declaration of the macro.
And the secure URL macro is for the implementation.
So when you import the macro in your project, we don't need to know how it is working, right?
So you just import this declaration.
So if you stay on this file, so what do we have?
We do have just this first macro, which comes with the template.
And this one is a freestanding expression.
And it is called stringify.
We do have this secure URL client with the main.
And this one is not required.
You can totally delete it.
It is an executable.
You can delete it.
You don't need it, actually, in your project.
So you have here the declaration.
And this secure URL macro, inside this folder, you will have the implementation.
And here, you have the plugin that will use your macro.
Now, let's create our own macro.
What I will do is I'm going to have another macro that is called secure URL. it is complaining because I will return a URL.
So I need to import from a foundation.
And by the way, I will delete this stringify as well.
All right.
So here, we use an external macro.
And the module for that external macro is the secure URL macro, which is defined here.
And the type is secure URL macro.
So we need to come here in the secure URL macro target or file and define here the actual implementation of our macro.
And let's do that.
I'm going first to delete this, since I won't need it anymore, this stringify macro.
So let me see.
I think it is this one.
And yes, so it is this one.
For now, I'm going to change this plugin to export that secondary URL macro and fix those errors, which are really scary for now.
And you can see here that it is complaining because I need a URL error, another type.
Let me define it here.
All right.
OK, no more errors.
And originally, what we have here-- so the thing is with macro is that you can't run them and execute that macro directly.
So you can.
You can.
But one way to do that is to run your unit test.
Because if you do a Command-B, yes, it doesn't see this stringify macro, because we delete it.
That's OK.
And I can delete that as well.
The stringify is not defined here in the test.
I don't need that stringify.
Let's call it secure URL, which is of type secure URL macro dot self.
So what I was-- let's see if it is building.
So it is building.
It is building fine.
And even when you run this project, you will not see any output, right?
So one way to deal with this macro is inside this test file, you write your test for the macro.
So let me actually delete those tests as well.
And a few tests for this macro we are building.
So let's test first the happy path.
And maybe format this a little bit.
All right.
So let me run this test.
OK.
Okay. It succeeded, but what I want to do is to know exactly how my macro is working.
So in order to know how it is working or to debug that, you can add a break point here, okay? Inside the definition of your macro. So if I hit command U again, it is going to stop on my program.
And now you can use the command line and inspect the macro.
Like here, I want to maybe inspect the argument.
So you can peel the-- nope, I need to step-- maybe step down.
OK.
OK.
So you can use now Xcode to debug your argument.
So here, the argument is a string literal--
I don't know if you see here.
Maybe let me zoom it a little bit.
OK.
So you can see that it is a string literal expression syntax with an opening code and some other object inside, like the segment.
And for the segment, we have the content, the actual content of the segment, which is a new URL.
Like here, it is a HTTPS./google.com.
And you can still explore the other argument types or the segment, like what are the segments. or I need to step, or maybe let me place it here.
OK.
Now you can explore the segments as well.
So forth and so on.
So this is, as far as I know, the only way to debug your macro for now.
OK.
So our test is passing, right?
We do have here some error to generate when, for instance, the argument given doesn't start with an HTTPS, since we want to have only secure URL, right?
So if it doesn't start with HTTPS,
We return here an error, which is not HTTPS, with a description.
And the cool thing about the macros is that since it is compile time, you can get some guidance, or some guidance about the error, something you are doing wrong. like here, I do have this URL error.
And if, for instance, at compile time, you use this macro and the user does use your macro, but doesn't start with the HTTPS,
Xcode will generate a code.
And this will be this string you just put here.
And you can actually test that.
We can go on the test and write another test for the unhappy path.
So let's add a new test for the unhappy path.
Here it is.
All right.
So here, we use this assert macro expansion, and we give it this secure URL by using Google, the URL without HTTPS.
And it shouldn't expand, right?
Here, in the expanded, it does expand by giving us a valid URL with the URL string.
But here, it won't give us this URL.
Basically, it will generate us an error.
And this is how we test this kind of error.
So I think let's build and run really quick and see if our project is building.
It is building fine, I think.
And here, we export our macro.
So we build our first macro.
But now, how to use this macro?
I have here a project, testing macro, which is just a SwiftUI project.
So it is a basic app, just the skeleton you have in SwiftUI when you create a new SwiftUI project.
And I'm going to add the macro we just developed.
But one important thing is, in order to add it, you need to close-- typical Xcode thing-- you need to close this macro project you are working on.
So it won't work if you still open it.
Yeah, VVX code.
So I'm going to import it here.
Let me add dependency.
And now we have a local-- you can add a local dependency.
Let's add the one we just created.
And what's his name again?
Secure URL.
Let's select it.
OK.
We don't actually need the secure URL client.
It is empty.
So I'm not going to add it in my main target.
And let's add this package.
So it is added, and it comes with Swift syntax.
And one drawback of importing this macro is that it will obviously come with all its dependency.
And one of the dependencies is Swift syntax.
And Swift syntax is super heavy, right?
So you will-- on debug mode, it takes something like less than a minute.
But on release mode, it can take something like three or four minutes or plus.
So you need to be aware of that when you import your macros.
So let's build and run.
Maybe let me just import the secure URL here.
OK.
It's called see this new target, which is cool.
Let's build and run.
And you see we need to wait, actually, for this macro to build, because it is using Swift syntax, which is heavy.
So let's wait for some seconds.
Hopefully, it will compile successfully.
OK, the build is successful.
So now let's use our macro.
So I can say let URL equal-- since our macro is a freestanding one, so we need the hash.
And the name of the macro, it's a code definitely that's it.
And now we can here have our macro, OK?
And our URL generated by the macro.
And let's say, , swift-connection.io, .
And you see that I can't build anymore because it fails.
Why that?
Because this , SwiftConnection.io,  is not secure.
So we need to append the HTTP.
HTTP.
But before that, let's see the error.
So this is typically the error we defined on the macro.
So this doesn't seem to be a valid secure URL.
Please provide a valid one.
And it often starts with an HTTPS.
So you can give a really descriptive message to your errors.
So it needs to start with HTTPS.
Let's go ahead.
HTTPS colon slash slash.
And voila.
The error is gone.
OK?
[APPLAUSE]
Thank you.
So this is our first macro and how we use macros.
Let me go back to the slides now.
If I found them.
Where are they?
OK, cool.
OK, so what are the shortcomings when it comes to building a macro?
I think that you saw some of them.
The Swift syntax is super, super, super difficult to master.
I said it three times, right?
Because it is.
It is like yet another programming language.
And in order to use Swift macro, you don't have to use it,
But it will be super difficult if you don't.
So it is recommended to use it.
But yeah, it is kind of awkward to work with this Swift syntax.
And as I said, it adds some dependency because it is kind of a heavy package.
So it will add some build time to your project.
Yeah, up to you to see if it is worth for your project.
And as we saw, it is not that trivial to debug.
So if you want to develop your own macro without having a set of unit tests, which I don't recommend, it is almost impossible to debug your macro.
So what we've done is to add some breakpoint to the actual implementation of the macro and run the unit test that will pose the execution of the test.
And after that, you can debug and play around with the Swift syntax tree.
So without having a test, this can be real difficult.
And yeah, last but not least, testing, even testing the macros can be really painful.
What I mean by that is that you can-- let's say that you update just a bit of your test.
We can actually do that.
Let me bring Xcode again with the macro security URL.
OK, what I mean by that is that here, you can-- where's the test pass?
Here.
OK, so let's run this test again.
I think it will still pass.
We didn't update the code.
OK, it does.
And let's say that I do that.
Let's say that I do that.
I just format the code.
This is a valid Swift code, right?
Some people like to have the code formatted, especially when we have more than three parameters.
You tend to put each parameter on a new line.
This is a valid Swift code.
But when I run again this test, it's going to fail, right?
Because it is waiting for you to enter the exact same formatting as well.
So imagine having like 1,000 or 100, 100 or 1,000 of line of code.
This will be super difficult to debug if you accidentally introduce a white space or something like that in your code.
So this can be really tricky to debug in those kind of situation.
So testing can be difficult for that.
And yeah, so this is all I have for you guys today.
So to recap, we saw-- yeah, we define what are macros and why to use them.
We saw the different types of macros.
And we did create and use one in a project.
And we saw some macro shortcoming, right?
So this is-- I give you a few seconds to scan this QR if you want.
So you will have the ultimate-- this is the ultimate resource to learn Swift to Macros.
So I give you a few seconds if you want.
OK.
Good?
>> Yeah, I was joking. But it is actually this one from -- it is actually this one from
-- from -- from Christoph, which is a real resource. I promise. And, yeah, you will
So, this is a GitHub repo that collects all the resources when it comes to macro, the video from WWDC and other cool projects that are using the macros.
So I highly recommend to check this one.
I forgot, but point three is starting a new video series about macro, which is worth to watch as well.
And yeah, if you want to keep this conversation going, here are my contacts.
I'm bionicsis almost everywhere.
I'm just active on Twitter and LinkedIn.
And yeah, thank you for listening.
[APPLAUSE]
Better than it was before.
So many questions.
I'm hungry, though.
Yeah, so if you're hungry, just wait like 15 more minutes.
All right.
Or you just kidnap Vincent, and so we'll skip the Vincent talk.
But the first question was, how we can--
I mean, is it possible to declare fix it actions?
Yeah, it is.
It is, but kind of difficult. This macro thing is not that trivial, right?
But yeah, it is definitely possible.
You will have that option in the diagnostic something, right?
We use.
So yeah, it is possible.
All right, just to be sure, the difficult part is the API to handle the fix.
- The fix, exactly.
(laughs)
- It's also difficult to know ahead what kind of error you're going to have.
- Exactly, exactly, exactly.
- Okay, so I'm guessing this is pretty difficult, like we've said it a few times already.
So do you think-- who do you think should spend time learning macros?
Because I'm guessing not everyone needs to dive into this.
I mean, everybody.
Like, if you are kind of curious, you want to explore new things, especially in Swift,
You can definitely try at least to build your own macro, starting with freestanding.
But I do highly suggest to have a look first on the Swift syntax first, because it is essentially what you will use to build your macro.
So it is an essential part of it.
Speaking of Swift syntax, is it possible to distribute a macro as a built binary, a pre-built binary, to avoid recompiling each time a Swift syntax?
I don't think so.
I don't think so.
So yeah, it comes-- so I mean, it is possible, but you have then to ditch completely Swift syntax.
And like I said, it is super difficult to write your own macro without Swift syntax.
So you can technically, but it will be super difficult.
And to your experience, is there already something you really want to put into your production code as soon as it's available?
Or do you think it's more like syntactic sugar for now?
Or are there really some things that's going to be really unlocked from this feature?
Yeah.
I've seen some interesting use cases. especially with the link I shared, we do have a spyable macro.
And that spyable macro is-- you use it when you have a protocol.
And yeah, when you write tests, the typical thing to do is to implement that protocol with stubs calling, make sure that this method is being called, et cetera.
So for instance, we have a macro that does all the heavy lifting for us.
So sorry, it is doing that right now.
But now we have, for instance, a spyable macro, which you can import to do that work for you.
So those kind of use cases will be kind of interesting.
And it will save you a lot of time when you adopt it in a project.
Nice.
And in your experience, are you able to import any kind of library or even the whole foundation?
Like, can you use even URL request in a macro?
Yeah, I think.
Like, we imported a foundation, and URL request is a part of foundation.
So I think that you'll be able to import many Apple framework.
I think that's all.
So thank you very much.
We do have one question for our presenters once again.
How did you do the screenshot Zoom thingy?
I get this question every time.
So I used an app that is called SniPose, S-N-I-P-O-S, accent. I'm tired, guys. It is called a Snippo, you can check it on the app store and you can zoom a specific area on your screen.
>> Thank you. >> Thank you very much.
[APPLAUSE]