---
slug: >-
  /talks/swift-connection/swift-connection-2023/daniel-steinberg-floating-down-an-asyncstream
date: "2023-09-21"
title: Floating Down an AsyncStream
author:
  - Daniel Steinberg
video: zYUt8O-u9Sg
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/zYUt8O-u9Sg.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/5b9f2bd5088849bbbeebebbf53df8f89/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---

So I'm going to be talking about async streams, which sits in a nice place.
For those moving from Combine, an async stream was a nice way to publish values without using the Combine framework.
And if you're not ready to go to iOS 17, you can't take advantage of observable yet.
And so async stream fits there too.
There's going to be a lot of code, none of it live.
The code isn't important, but the ideas are.
So as you look at the code, get the ideas, and you can always come back to the code later.
So here's the app we're building.
Every couple seconds, a second or two, a new entry appears on the screen.
It's just a number framed in a circle. applause for this. [ Applause ]
So the way this works is the main view is just a grid of entries. Those are the little circles with numbers that you saw. And vending those, providing those is the entry controller and it uses a framework we're all familiar with. It's at publish. So that's an observable object there. And that's how the at publish sends that back to the main view. We're not going to pay attention to that part of it. We're going to pay attention to where we get these numbers from, and that's from the model. And the model is going to vend us these ints that will then be turned into entries. And the question is, how do we get that information back from the model to the entry controller? And there's lots of techniques. There's combined, as I mentioned. Async stream we'll get to at the end. But let's start with notification center.
Did I hear someone cry?
So here I am in my model.
And so when it's time to start counting, I'm just going to use a while loop and count up to ten.
And I'll sleep for one to two seconds and then I'll increment my count and then I'll post a notification.
And what I'm posting, some notification name, is something in the user info dictionary and
And that's where I'll post my count for the number key.
And we'll start things off when model's initialized.
You good?
All right.
Let's connect this to the controller.
And the first thing I have is my entry controller, which I'll connect to the main view.
As I mentioned, it's an observable object.
I've got this published property that is an array of entries, and I had to import combine.
Oh, Daniel, you could have imported foundation.
Yeah, but then you're hiding that you're using combine.
I want you to be aware of it.
We'll put it on the main actor because we're going to be viewing the results of these.
And now let's connect to our model.
And now let's listen for notifications.
And so here's how I listen for notifications.
I have this method register for notifications.
And you've done this forever.
You have a notification center and you ask the default center, add observer, self name, object, model.
And the thing that's missing, of course, is the callback to a method.
And so this version of notification says when I get the right kind of notification, call me back and call this method on me.
And that's a very objective C kind of way of doing it.
You send a message to somebody.
That's the square bracket thing.
So that's why that's an opt, ob C method.
And so I get back my notification and I see with an if let did the notification have user info?
If it did, I keep going.
I look inside the user info and say, well, do you have an entry for number key?
And if you do, is it an int?
And if it is, that's my number.
And then I just create my entry from that number.
Little detail.
I have to display the entry.
Not so important.
I have my display method.
I push to the main thread and I append.
And it works as you saw before.
Oh, so awesome.
Okay.
This is old fashioned. method that we called back. And this signature is old-fashioned. How old you say? Well it comes from this which goes back to 2001. Some of you in this room aren't that old. iPhone isn't that old. iPhone didn't come out until later. And so even though this says it was available on iOS 2.0, that was years after this method shipped. And so in 2009 Apple introduced block-based programming.
And we got this version using cues and blocks.
And so if we go back to the old way, with this gunk there that we're calling back, what turned it on its head with the block-based one is we took that stuff and we put it in the closure.
And the only difference was we had to say whose self was.
And then this worked. And that was awesome.
One of the things I think is really cool about Apple is they have this technology that they introduced in 2001 and as things change, they go and revisit it.
So for example, when Combine was introduced in 2019, they introduced a publisher for notifications so we could subscribe to publishers instead to get our notifications.
And in 2021, when Apple gave us Async/Await, they gave us this version, which gives us an asynchronous sequence of notifications.
An asynchronous sequence is a sequence, instead of thinking of them all being there at once, it's a sequence over time.
I don't know when the next element of the sequence is gonna come.
So let's use this version and rethink entry controller.
I don't have to change the way I post notifications.
There's nothing async about that.
It's the way I receive them.
For technical, excuse me, reasons,
I'll move the main actor inside.
And now I'll let notifications equal this guy, the new method, which is notifications named.
That's my async sequence of notifications.
You think, oh, I've got an async sequence.
How do I consume a sequence?
Well, in my list for numbers, I use a for loop.
This doesn't compile.
Don't worry, it's just a slide.
It'll compile in a minute.
And the reason it doesn't compile is notifications isn't a sequence, it's an async sequence.
So if we go back and think about sequences for a moment, and a specific sequence, sequence is a protocol, an array is a concrete instance of it.
So say I have an array of ints here and I for through them for element to my sequence and maybe I'll print them out. It turns out, although we don't think about it very often, that this is actually syntactic sugar.
And it's syntactic sugar for asking our sequence for its iterator and then using its iterator to get the next element.
Iterator.next returns an optional, and as long as we get something that's not nil, that's the next element, as soon as we hit nil, we've come to the end of our array of our sequence.
And so we while let through that.
While let is awesome.
If you've if let and guarded let and thought there was no more to life.
While let says, if it's not nil, unwrap it, assign it to element and do the body.
And as soon as you encounter nil, you're done with the while loop.
And so that's what I mean by that top thing is just syntactic sugar for that bottom thing.
So you say, well, that's a sequence.
What changes in an async sequence?
So there's my notifications.
That's an async sequence.
And so instead of an iterator, I have an async iterator.
Ooh.
And when I call iterator next, it's an async iterator, so that's an asynchronous method.
I have to await the next element.
It might take a while.
And so now if you look back at your for loop, you see what that space is for.
I have to for await the element in my sequence.
So let's go back to our actual example.
In our actual example, I was listening for numbers, and now I know I need that to be a for a wait because notifications is an async sequence.
And we're so happy except it still doesn't compile.
And it doesn't compile because I'm using a wait in a context that doesn't know about asynchronous.
So either I have to wrap it in a task, or what I'm gonna do is I'm gonna just label listen for numbers as being async.
And now I take the same code I had before in my closure, and I paste it in there, and when I come to life,
I initialize an inside of a task,
I call listen for numbers, which because it's async,
I have to wait, and it works.
It's just awesome.
So I have this code that I've seen a couple times, and I really don't like this code.
And I have this methodology called HDD, which many of you know is hate-driven development.
(audience laughing)
And hate-driven development is I take code that I hate and I get rid of it.
And so I have my notifications, which is an async sequence of notifications, and I have this code that I hate.
Let's see what we can do about it.
And the first thing I do is I look at this if let here, and remember that takes user info, which may or may not exist.
If it does, it if lets it and you go, oh, Daniel, that's just compact map.
It is. And now I have an async sequence of those user info dictionaries.
And I don't need that anymore.
And now I have an if let where I look at the user info dictionary and if that number key exists,
I read that value and if I can, I look at it as an int and that's just another compact map.
And now I have an async sequence of ints.
And the final thing I look at is this let entry equal -- I'm transforming number, which is an int, into an entry.
That's just map.
And now I don't have code that I hate anymore.
I have this nice path which gives me an async sequence of entries, and all that's left is to display the entry.
And so I take my async sequence of entries and back in my code when I listen for entries, because I'm not going to call it listen for notifications anymore, or numbers, I for weight my entry in my entry sequence and then I just display the entry.
And that's code I can live with.
And when I call listen for entries, it works.
You think, oh, that's good.
We've now seen async sequences.
What's with this notification center?
Can't we get rid of it?
Yes, we can.
So, we're going to start with combined and then we're going to get rid of that.
And so, I go to my model again and I get rid of this notification center stuff and I just make count published.
What changes in controller?
And it's kind of cool, not much.
So, what changes in controller is I connect to my model.
Maybe I ask my model for its count, but that's an int.
That's not what I want.
If I ask it for dollar count, that's a publisher of ints.
And Apple said, oh, we're moving from combine.
People want to use async sequences.
Let's add a modifier values which transforms a publisher of ints to an async sequence of ints.
And still I'm going to map that int into an entry.
And as a technical thing for people that have dealt with combined before, you know that you need to drop the first element because it's eager.
It'll present that first element there.
So again, let's think about sequence as a protocol.
Array is a concrete thing that conforms to it.
And I can't just have an array.
I've got to have an array of something.
An array of ints, an array of entries.
In the same way, async sequence is a protocol.
And we're almost done with the talk and we're finally getting to the subject.
Async stream is like the array of that world.
It is the concrete async sequence.
And so let's go back to our model.
And I've got my count.
And it's no longer published.
And I'm going to create an async stream of entries.
I can't just create an async stream.
I've got to create an async stream of something.
And I do that with this make stream of, and so I make a stream of entries, and what I get back is a tuple.
And the first element of the tuple is my async stream so that I can subscribe to it and I can do that same for wait in in it.
The problem is how do I put things into the async stream?
How do I throw little entries in so they float downstream to whoever's waiting for them?
And I do that with what's called a continuation.
And that's the second thing I get back.
So way down here and start counting.
After I've incremented my count,
I'm gonna say continuation, throw this into the stream, throw my entry made from that count.
And that's all there is to producing async streams.
So let's go back to the controller and see what changes there.
I've got my model.
And down here I'm going to display my entry that I got from the models.entry sequence.
It's just that easy.
Ready for a quiz?
Okay. Async people.
What happens when I initialize?
Here prints immediately.
Because what happens with task is, even though listen for entries runs forever, I'm taking a task and I'm shoving it to the side and say you work over there, I'm going right to the next line. But if I move that print here into the task, now it's blocked. Here never prints to the console.
And that makes us rethink what we've done. It's because this thing never finishes. This while let entry, I'm always waiting for the next one. You say, but why are you waiting? I'm only ever gonna give you 10. It's because I didn't clean up after myself. And so if you can, if a stream doesn't run forever, please remember to say it's finished and then the person consuming it says okay after
I reach 10 I'm gonna continue from there and print here. Got more questions. What
What if I introduce a filled model?
So I have a model and I have a filled model and I'm going to listen for filled entries the same way I listened for entries.
This time I listened from the filled model.
So I've got these two things that I'm listening for and in my task I wait, listen for entries,
I wait, listen for filled entries, but this guy is blocked. the second guy won't execute until the first guy finishes.
So when I start this, I'm only seeing the plain entries.
Now the filled entries are being produced,
I'm just not consuming them.
And that's why when I get up to 10, you'll see most or all of the filled entries appear at once.
Once I'm no longer blocking it, it's an asynchronous, it's able to get all of the next ones almost at once.
So one way to get probably the behavior we want is to have two separate tasks and listen for entries in one of them and listen for filled entries in the other one.
That's not blocked.
And so now it looks something like this.
They won't always come in order
'cause they're pausing randomly one to two seconds.
So maybe I'll get two of one or two of the other, but they're all coming and neither one is blocking the other.
Now, I want to leave you with disappointing news because that's what I do.
There's one thing you have to be wary of with the async stream or in fact any async sequence. If I use the same model for both, so I've got two for loops listening for the same one.
What you've got to think of is, undo the syntactic sugar.
This one is saying, give me the next one.
This one's saying, give me the next one.
Only one of them's gonna get the next one.
And then the other one's gonna get the one after that.
And so if I have two things listening to the same async sequence, each one only gets a portion of that sequence.
And so you'll see some of these are filled and some of these are plain.
And so that is my quick entry and introduction to Async Stream.
Thank you.
(audience applauding)
