---
slug: >-
  /talks/swift-connection/swift-connection-2023/shai-mishali-a-crash-course-of-the-composable-architecture
date: "2023-09-21"
title: A Crash Course of The Composable Architecture
author:
  - Shai Mishali
video: h0Agq-98RZ8
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/h0Agq-98RZ8.jpg
slides: null
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---

Hi everyone, it's so good being in France for the very first time, thank you for the kind hospitality, today I'll talk to you about the composable architecture, before then a quick intro, my name is Shai, I work for a company called , Monday.com, , I do a lot of open source work which you might know are Swift combined related projects and also a huge fan of conferences like this one and hackathons, and that's it.
My agenda is mainly to do my best to not confuse you despite this being a relatively fast-paced talk due to the time constraints.
So let's just get started.
The composable architecture, what is it?
It's a library for building applications in a consistent and understandable way with composition testing and ergonomics in mind, it was built by Brandon and Stephen from Point Free, which you might know from their video series where they built this framework as a video show, basically. What did it really try to solve, though? As you might know from SwiftUI, our
UI is always a function of our state. This is really, really useful and great, but it can get quite difficult as your app grows and matures over time. We usually start off with some simple state, it becomes some shared state, then it becomes some shared mutable state and the most painful is shared global mutable state.
And those last ones are where things get very, very painful.
It really starts getting painful when that shared state is uncontrolled.
That means that mutation might occur to this state and we don't really know from what source.
For example, I might have this state with an array of items and can the user add item true or false, and there might be some services mutating it, but in reality, it's more like a lot of services mutating it, and some view might consume this state later on, and it will have three items and can add item will be true.
But at this point, we might ask ourselves how did we even get here?
Why is this state like this?
In reality, we don't really know, because these can happen in any kind of order.
So this can cause a lot of race conditions and unexpected states, but really it harms maintainability and our ability to reason about our code base.
DCA tries to solve this by having only one way to mutate state.
You have this store object that holds your state, and there is a set of predefined actions, and only sending these actions to the store can mutate your state.
It does this by using something called a reducer, and this reducer is just a simple function,
It takes your current state, this new action, and tells you what is the new state that you want to evolve based on these two things.
So now if I send this set of actions, for example, add item, delete item, and add item again, when I get to this state, I can exactly reproduce how did I get to this exact state, and it's no longer a mystery.
So this is quite a powerful concept that unlocks a lot of great debugging tools and explainability of how our codebase works.
Modularity can also be a pretty difficult milestone to achieve, something that a lot of companies want, because it's quite hard, especially with SwiftUI previews to work on a very, very large codebase, so TCA already has a built-in story to solve this problem.
We can take our big store action state and scope them down to smaller and smaller scopes, so we can work in isolation, and that means we can build each of these pieces in its own in place, work in isolation, very, very small, very fast compile times, and when it's all done we can put them together and work on the primary app or a bigger scope when we need to.
So let's see it in action.
And I'm going to do a quick, not a quick live demo, most of this talk is actually a live demo, so fingers crossed.
Okay.
Let's see if you can see what I'm doing.
Is it all right, this size?
I hope so.
Cool.
So, today, I'm going to work on this Pomodoro timer app.
If you don't know, a Pomodoro timer is something you can type a goal, press play, you get 25 minutes to do some specific task, and then you're done.
So I already have my view, and as I mentioned, to mutate state and run some logic, I need some reducer, so I'm going to create a new file called Pomodoro, and I'm going to import composable architecture.
And I'm only going to create a struct called Pomodoro, and it's going to confirm to a reducer.
And once I do this, it's going to complain that it needs a few things.
The first one is an action, which I mentioned.
And the second thing is a state.
So a state can be either an enum or a struct.
Action must be an enum.
Here I'm going to use a struct for my state because it fits this use case better.
And the last thing it will want is a reduce function, which, again, takes your previous state and your new action and lets you mutate the state.
We can actually make this a bit nicer by using a new reducer builder and provide this body, kind of like Swift UI, and here I will just provide some reducer of state and action.
What happened?
Pomodoro state and Pomodoro action.
But I can actually shorten this further by just saying I want some reducer of Pomodoro.
And that will kind of work under the hood.
And I can have my reduce here.
And it will take my state and action.
And here I need to return some side effect, meaning something that will happen once I finish doing my work.
I'm just going to return none and get back to this later and explain it.
So now we have this very basic thing going on.
Let's plug it to our view quickly.
So in Pomodoro view, I'm just going to have a store.
And again, I can say it will be a store of Pomodoro state and action, but I can also say I literally just want a state.
I can kind of shorten this.
Instead of doing this, I can just say I want a store of Pomodoro.
And that's a bit nicer.
And I'm going to go back to Pomodoro and kind of model my domain before I finish everything in the view.
So first thing, I kind of want to think about my view.
What do I want to achieve here?
So we'll start with a few basic things, which is tapping this button, and I will need a tapped start tapped and a stop tapped action and maybe some state to keep track of is timer active, it's going to start with false.
And now I can just switch over my actions, and the compiler will enforce me and help me to figure out what I want to do and will force me to handle all of these and new ones that I add in the future.
So when I press start, I'm going to change my timer active to true and change it back to false here, and again, I'm going to return none in those because I don't have any side effects to run.
Okay, cool.
Let's now finish plugging our view here.
I'm going to provide a store, this store needs an initial empty state, my Pomodoro state, and a reducer, which is my Pomodoro.
I'm going to copy this to my app as well.
Great.
Let's run the app quickly and see what we get so far.
So I press the button -- sorry.
I forgot to do one important thing in the view itself.
I actually want to use this new store that I have here.
And I can't use it by itself because it's not an observable object, it's just an object to hold all of my state and actions.
So the way to make sure it's an observable object that causes my view to render is wrap it in something called a view store.
And I provide it with my store, and I say, what piece of the state do I need to make my view re-render?
In this case, I need all of the state.
But you might have a smaller piece in your view.
And then I'm going to just get a view store in hand.
And I can finally use it.
For example, here in my button, I can say that if ViewStore is currently active,
I'm going to send a stop action.
And otherwise, I will send a start action.
And also, I can kind of update this icon to have ViewStore is timer active.
I'll have a stop button instead of a start button.
Let's run this now quickly and see what we have.
So I press the button, and it toggles from stop to start.
But how can I know that this is actually doing what I want it to do?
So there's a nice helper that we can use on a reducer here.
We can just tack on print changes, kind of like SwiftUI's print changes.
And this is going to tell me everything that's happening in the reducer.
So now when I press, you will see that I'm getting a stop and start action, and exactly how it causes our state to evolve.
So this is really nice.
Now every action that happens in the system,
I know exactly how it's mutating my state.
Quite useful.
So now let's get to this text field here.
So a text field needs a binding.
And the binding is really just state that we can read and state that we can write.
So in a reducer, we need a way-- we need some state, for example, timer title.
And we need a way to mutate it.
And as we said, the only way to do that is an action.
So I'm going to have a timer title change.
It takes a string.
And again, the reducer here is going to force me to handle this action.
And I'm going to set my timer title to this new title and return none here as well.
And now in my pomo view, where I just have a constant binding, I can ask the view store to give me a binding, and I can have this get and send variation that takes a state, and I can just get my title, and when it changes, I will send my timer title changed with a new value.
Now when I run it, if I type some text, not only does it show up, but also every time
I tap, I get notified exactly how the binding caused my state to change, which really lets us track everything that's happening in our view in this case.
So now I'm going to quickly add in my state some computed prop saying is star disabled, just going to return if my timer title is empty.
And in my view, I am going to change this to have an opacity based on that.
You start disabled, it will be lower opacity.
And it will also be disabled in this case.
And also the text field, I want to keep that disabled while the timer is running.
Because I don't want the user to type anything while it's running, basically.
Cool.
Okay.
Nice.
So, everything is kind of working like we expect it to.
It's disabled.
Once I tap it, I can't change the text.
If I don't have anything here, this gets disabled.
Very cool.
Now, the nice thing about everything we did right now is that it's really, really testable.
So we can go to this prepared Pomodoro test suite, sorry, and I'm going to add a test toggling timer test here, which is going to be async and throws, and I'm going to use a special store called a test store, which is like a regular store, it takes some initial state and I can kind of change this to have what I want.
I will just have a timer title of my amazing work.
And a reducer, which is going to be my pomodoro.
And then I can just try and send an action and see what we're getting here.
So I'm going to do start tap and run my action, my test, sorry.
And now this fails expectedly, because I said that I pressed the button, but I'm not telling it what caused what happened to the state based on that.
So this is actually a really nice error.
It means that every time I do something, I need to assert how my state changed.
So this should cause my timer active to flip to true.
And if I do the same for -- if I do a wait store send stop tapped, I should get timer active false.
And now when I run it, it's all passing.
So now you get really, really exhaustive testing on everything that's happening in my app.
Cool.
Now I'm going to start working on this timer here.
And this is an interesting one.
So a timer isn't really like simple state.
It's a long run in action that runs in the background and you kind of have to manage it.
And this kind of sounds like this asynchronous side effect we talked about.
So back here, I'm going to add a clock, which I'm going to need to wait.
And I'm going to use a continuous clock for this.
And instead, when I press stop, it's returning none.
Now I can actually have a side effect, meaning something asynchronous that happens once I tap the button.
So I'm going to use the built-in run effect, which gets a closure where I can run any async awaitable work.
And now I can finally say here inside, for a wait in clock timer, seconds one.
And then this is going to run every second.
Not sure what I need to do here, right?
So what I want to do here is increment a state.
It's going to be called seconds elapsed.
And I'm also going to quickly add it to my view.
Cool.
And here I want to mutate it, but I can't mutate it directly because, again, everything needs an action.
So I'm going to add that as well, a timer tick action.
And I will say that whenever a timer tick happens,
I will set my seconds elapsed to plus 1 and return none here.
And also when the timer is stopped,
I will reset the seconds elapsed to 0.
And then all I have to do is say that every second is running, I'm going to send a timer tick.
Cool.
Now, let's see what happens when we have all of these pieces running together.
So I'm going to put something, press play, then we have one, two, three, and I stop.
Oh, this keeps running.
So this is a bug, but also not very unexpected.
The reason is that this asynchronous effect just keeps running, I didn't do anything to stop it, right?
So luckily this is another thing just built into TCA for free that you don't have to worry about.
You just tack on this cancelable modifier and pass some ID.
I'm going to create an ID here as a private enum, call it cancel ID, and I will have a case for my timer, and I can just pass it here and say this effect is identified by this ID, and when I press stop, instead of returning none, I will return a cancel effect with that same ID.
And now when I run it, and I stop, it actually stops and the effect is entirely cancelled.
Back to our test, I kind of want to run tests for this case as well.
So back in my test suite, I'm going to remove this stop for a second to see what's happening as I'm running my test.
So now it's failing, but for a different reason.
So it says that if your effect uses some clock or scheduler, make sure you wait enough time.
So what does that really mean?
Even if I could somehow reach my Pomodoro's clock, should I just wait on it for 10, 20,
15 seconds or whatever?
We definitely don't want that.
And the problem here is that we have this clock that we don't control, and we need to inject it from the outside.
So luckily TCA ships with its own dependency library, which is really useful.
So here instead of this static clock, I can just use this property wrapper called dependency and say I want a continuous clock, and I don't even need to specify the type because it's inferred and then everything here is going to work exactly as it did before.
But now this allows me to use this third argument called with dependencies and override my dependencies.
And I'm going to say that continuous clock equals this new clock, which is a test clock.
And now I can control time.
And the way to do this is just say that I want to await my clock and, for example, advance it by one second, by three seconds, for example.
Let's see what's happening here.
Okay.
Cool.
So now something different is happening.
Oh, wait.
Just a second. actually want to send a stop here as well.
Whoa.
That's unexpected.
Just a second.
OK, cool.
So now this is saying that, as expected, I got three actions because I waited three seconds.
I got three timer ticks, but I'm not telling the system that it happens.
And our tests have to be exhaustive with this configuration.
I'm going to say that I expect my store to receive a timer tick, and I also expect it to set my second elapsed to one, and then two, and then three.
And also I expect it to drop back to zero when stop is tapped.
Now let's run it one more time.
And everything is passing.
So, again, we get really wide coverage on even this very weird asynchronous effect, which is quite hard to test in other scenarios.
I don't have to wait.
This could be 2,000 seconds and it wouldn't matter at all.
Let's see a little bug that we can also fix together.
I'm going to set my starting state to start at almost 25 minutes.
And I'm going to just type something and run, and one, two, three, four, five, and it doesn't stop.
And that's a bug, obviously, because we expect our Pomodoro timer to only be 25 minutes.
This can easily be fixed by going to Pomodoro, and every time there's a timer ticked, I'm going to check if my current seconds are equal to some constant I have.
Which is 1500 seconds, which is 25 minutes.
And if that happens, what do I want?
I kind of want to imitate as if the user pressed that stop button.
So I'm just going to send an effect of send, stop, tapped.
Let's try it again one more time.
Thank you Xcode iPhone simulator.
Appreciate that.
Okay.
We have some simulator issues going on here.
Okay.
I'm just going to press play.
Attempt two.
Okay.
One, two, three, four, five.
And it stopped.
It dropped back to zero exactly like we expected it to.
But of course we don't trust ourselves to do a good work here, so I'm going to quickly write a test to confirm this as well.
And I'm going to add a new test timer and naturally.
It's going to be async as well.
And I'm going to do a lot of the same work here, which is basically starting with a store with my mocked clock, send something and advance the clock.
But I'm going to advance it by five seconds, and I'll start with the same value here of the initial seconds elapsed.
And let's run it and see what we get.
The iPhone simulator gods are against me, I see.
Let's give it a moment.
No, it's not.
Let's try this quickly.
Run it.
Run the tests.
Oh, come on.
Just a second.
That's awesome.
Let's give it a chance, one more chance.
God damn it.
I'm going to just try and remove this app and see if it helps in any way.
Chris Lattner, I'm coming for you.
I know, I'm coming for him anyways, for this historical mistake with the simulator. later. Wait, something's happening. Okay. Cool. Okay. So, this, yeah, thank you.
[Applause] So this is failing because I'm waiting five seconds but this is also very reassuring because I'm seeing five ticks and a stop tapped so
So I'm just going to assert that all of these things happened like I did before, I'm going to expect to receive a timer tick, and that's going to change my state to second elapsed
1496, and we're going to do that five times to get through all of these states.
And then we expect to automatically receive a stop tapped, which is going to kind of cause the same effect that this does.
Drop everything down.
And one more thing that I missed here, I'm going to add quickly that also the timer should be reset in that case.
So let's do that quickly as well.
Stop state timer title.
It's also nice that this is really fast to fix when it happens in reality.
Let's run our tests again.
Praying to the lords.
Okay.
Great.
So this is now passing.
We are testing our specific naturally ending case by mocking our initial state and everything.
So this is really, really nice.
The next piece that we're going to work on is actually adding the item to the list.
So I'm going to go back to my app and remove this initial fake state.
And let's see what we actually want.
So if we want to store all of these items,
I'm just going to have an array of them.
Going to be a timer item array.
And once you press Stop, I'm going to add a new item to my list right before I reset it.
So I'm going to check it's over 0 seconds,
So you don't just start and stop.
And then to my state timers, I'm going to append a new timer item.
It's going to just get a UUID, the current title, the current seconds, and the current date.
And let's see what happens to our state in this case.
We can start, one, two, three, and we stop.
And now we see that we see only the diff of the changes here, which is also really, really nice.
We see that a new timer was added with our three seconds and our title.
Very, very cool.
But now let's run our tests and see what's happening there.
And this expectedly fails because we now have this new state that we need to take care of.
So let's try to fix this in saying that we expect stop to have an array with a new timer item, it's going to have some
UUID, it's going to have my amazing work, which is my title here.
And it's going to have three seconds elapsed and the current date.
And now when I run it, it will still fail, but for a different reason.
The reason, as you might -- the sharp ones might have noticed, is that UUID and date will generate a new UUID and date every time, so there's no way this is ever going to pass.
And this is a very similar situation to our clock, we have this external dependency that we don't control.
So luckily we can have exactly the same thing as we did here for UUID generation and date generation, so I'm just going to have a UUID generation here, and a date generator here, and I'm going to replace my usage of this initialiser with a generator initialiser,
And now this production code is going to work exactly the same, but in my test I will mock my dependencies to say that whenever this UUID generator is called, it is going to return always my test UUID, and it can do the same for my date.
And now I can be sure without a doubt that I will always get the same UUID and I will always get the same date.
And I'm going to copy the same thing downwards, just so everything -- to get everything nice and passing.
And now let's grab this array here as well.
Only here it should be 1500 seconds.
Let's run our test again.
And everything is passing.
So now we are controlling time and UID generation and day generation.
We can control all of these aspects over a test, which is really, really useful.
The last thing that we should do is in our view in this list, instead of just having a timer list item view, I'm going to just have a for each of my items, timers, and with every timer, I'm going to have a new timer item here.
Timer list item view, passing a timer, and then some action.
This action is going to be a new action on my reducer.
So what I want to do when I tap that button is open a new sheet, actually.
This sheet is already prepared.
Let's see if I can get the preview running, again, if Xcode gods allow.
And I'll talk about this a bit to let it render.
So this is just a sheet that's going to show the title, the amount of seconds waited, some emoji, and a button to delete the timer item, and it already has, as you can see -- oh, yeah, it rendered.
Cool.
It also has this delete button, and it already has a timer sheet reducer attached to it.
So it only has a single action for tap remove.
So this is really nice, it means that this screen is entirely isolated.
I built it separately, it doesn't know that the parent exists, but the parent does have to know the child.
So let's see how we can start working with that.
Let's start with the basics.
In Pomodoro I'm going to have a new action for my timer item tapped.
And I'm going to say that my ID, that it takes an ID of timer item. point of view, I will send this. Wait. View store. Send. Timer item tapped with my timer
ID. And now if I want, I can just print this here to see that I'm getting the right thing.
And I can do this in two ways. The second one is better. So the first one is just going to my timers array and find the first one with the ID. But actually there's another tool that's shipping with a framework where we can swap out this array with an identified array of my timer items.
This gives us a bunch of super powers related to identifiable items, for example, one of them is I can just print my state timers in a key path of that in a subscript of that specific ID.
And now when I run it, just a second.
Oh, sorry, this should need an await here.
We'll add something, and when I tap it, it will print it as expected, just get it by the subscript.
Cool.
Now, how do I actually glue these two reducers, these two features together?
So I need a way to take my big state, my big action, my big store, and scope them down to this smaller child like we kind of talked in the slides.
And the way to do this is first we need to store both the state and the actions of the child in the parent.
So here it means, for example, that we will need a state that keeps the presented items.
It's going to be called presented timer.
And it will already take the state of the child sheet.
This is like the state of the child feature, basically.
And we're also going to do the same for action.
This is going to call it a timer action, a timer sheet. will take timer sheet action.
This will give us for free child-parent communication, and we'll also be able to know when the child does something and communicate it this way.
One thing we need to add here for presentation-- or two things, really.
First is this @PresentationState property wrapper, which helps us know when the state flips from nil to non-nil.
And when it does that, we'll present our sheet.
And the second thing is a presentation action around our actions here.
And this adds a second layer where we not only have our actions, but we also have a dismiss action.
So we can be notified when the user swipes away or the model closes by some other fact.
Cool, so now we have all this in place.
I'm just going to add a case to handle the child actions, which is going to be sheet and none.
And now I need to do this slicing.
So let's start with a reducer.
So the first part, we can use an operator called iflet.
And what it does is say, give me an optional state.
And when it flips to non-optional,
I'm going to run this smaller reducer to let it do its work.
So here I'm going to say that when I'm getting presented timer for specific action--
I'm going to explain this slash in a second--
I'm going to run this smaller reducer called a timer sheet.
And now you might know this slash, which is a key path.
This slash is called a case path, which is another thing point three basically invented.
It's like a key path bot for cases of an enum.
It is really useful here.
So here I say, when this state flips to null null, and for these parent actions, give me this new reducer.
And now I just need to do the same with my view.
And I'm going to use the sheet modifier, but not the regular one you know, but one that takes a state.
I'm going to take my big store and scope it down, saying that when I have a presented timer, kind of like before, and for my action, which is going to be a Pomodoro action timer sheet, when this happens,
I will provide this content.
So I'm getting a store here.
And this store is luckily already in the shape we expect.
So we're already getting this small store that fits what our child expects.
And now all I have to do is just put this in the navigation stack and put my new timer sheet view with my new smaller store.
And now if I didn't mess anything up-- let's run this.
Add one item.
Let's do another one quickly.
I'm going to press this one.
Sorry, press one of them.
Oh, one thing I forgot.
When you tap, I just print it now.
So let's actually update our presented timer to make sure that it's causing it to flip and do the update.
So here, on timer item tapped, I'm just going to grab this timer like I did before and put it in state presented timer.
But I need this to be a timer sheet state, so I'm going to wrap it.
Timer sheet, state, init.
And now we should have everything I need.
Let's run this again.
I'm going to do this again quickly.
Cool, tap, presents the sheet, shows everything with seconds, and I have this button, and you'll notice something interesting, the parent is getting this action, so now where the state lives is the parent, and I can easily have my parent handle that small children's action.
This is exactly what we're going to do.
So let's go back to our parent here and say when we get a timer sheet presented action for tapped remove, and we know which timer is presented because we have the presented timer at hand, so I'm just going to get its ID, state, presented timer, timer item, ID.
And if I have that, I'm going to go to my timers and say that I want to remove in that specific ID, and I'm also going to reset my presented timer back to nil.
And return none for the effect.
Hopefully for the last time today, I'm going to press this, press delete, and it's gone, and also we can see that it's removed here from my state.
And that's really amazing.
We now have two features, it could be 50 features, and each of these smaller features that are are under the parent feature are entirely isolated.
I can move timer sheet to its own module, work on it separately, move it to a different team, and then just plug everything together with a bit of upfront work and get everything running.
And that's it for the demo.
[APPLAUSE]
Thank you.
A few wrapping up notes.
So with TCA, we're encouraged to model and isolate these different domains and then put them together when we need to, and it's really about providing us with some sort of control, so we need a way to control our state of mutations, our dependencies, time, and of course, our side effects and our tests, so we can control each of these things very simply with that API.
If you want to learn more, there is no way that I could fit more into this slide, I think, so there are so many more topics, actually point three just hit 1.0 with this, with TCA a while back and they started a new video series that goes really deep into a lot of the topics I talked today, so I really urge you to check that out.
Everything I showed you today is open source, of course, TCA itself, but also dependencies, clocks, identified collections, these are all individual frameworks, so if you just want to get identified array and you don't want TCA, you can just take that, if you just want dependency injection without TCA, you can also take that.
And finally it also has a pretty thriving community, check out this relatively new Slack
If you need any help, we'll be happy to assist.
And I don't think we will have any time for questions, but thank you so much for your time, and keep enjoying the conference.
Thank you.
[APPLAUSE]
And if you have any feedback, then I appreciate it if you-- oh, I was turned off, sorry.
Yeah, I was just about to say, if you have any feedback,
I appreciate it if you scan the barcode and send it my way.
Thank you so much.
Thank you, Tariq.
Thank you.
[APPLAUSE]
