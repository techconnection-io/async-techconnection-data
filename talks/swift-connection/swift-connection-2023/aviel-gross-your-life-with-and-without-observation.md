---
slug: >-
  /talks/swift-connection/swift-connection-2023/aviel-gross-your-life-with-and-without-observation
date: "2023-09-21"
title: Your Life With (and Without) Observation
author:
  - Aviel Gross
video: NhgTZu0Hi98
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/NhgTZu0Hi98.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/446406f98b8d497ca481e5b681e6a684/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---

Hi everyone, welcome to your life with and without observation.
Hopefully you get the reference, if not, go fill those gaps.
From the Barbie movie, by the way.
So let's start with some history about the observation framework.
So first of all, observation, the first draft appears on the Swift repo on February, and the first pitch on the Swift evolution forums on March.
First review in April, only then Apple announced it in WWDC, but then it was accepted for second review only in August, which is pretty recent.
It's actually part of the standard library, which means it's open source, which is actually great for us, it means we can poke in the code, which we're going to do in a few minutes.
It's implemented for Swift 5.9 as you probably assumed.
And the main goal is to replace observable object and then potentially KVO, at least based on the pitch that they had in their proposal.
So first of all, why do we even need a new framework?
You know, we had observable object in combine, I was so bad with that.
So the biggest issue with observable object is that changes are at the object level, which means views know that some object changed but they have no idea what actually changed in the object.
It depends on combine, which means Darwin only, which means Darwin is Apple, which means it cannot go on Windows, Linux, all that.
It is very easy to cause performance issues in SwiftUI with observable object, if you're using patterns like Redux and similar patterns, and you're not careful, it's very easy to kind of like tank your performance.
It requires default value, so you cannot do optional.
It requires a single instance, so you cannot have an array of observable objects and you cannot have any other collection of observable objects in your view, and it breaks with nested observable object, you cannot have an observable object inside another observable object, that also breaks.
So just to kind of like, as a quick reminder of the syntax, the observation is opt‑in, so you have to say this is published, that is published, I care about both the model and the year of the car, and then later we see that we have some view with some car, and the body is only using car.model, that's the only thing we present on the screen, but
But later when we change the year, that view still refreshes, and that's because observable object doesn't know what changed in the car, it only knows, oh, car changed, I need to create the body, it doesn't even know that it doesn't use the year of the car.
So just to summarise, it's using combine, like I said, it's using property wrappers, the ad's published, it's opt in, so you have to declare for each one, you cannot tell which properties changed, and then any object change refreshes all the dependent views and no optional collection is to blah, blah, blah, all the things I said, but it's iOS 13 plus which is great because we can actually use it.
Observable on the other hand, because it's part of STD lib it means it's usable anywhere
Swift is usable, it's using macros, the new hotness that we heard about yesterday, it's
It's opt out, so everything is observed by default and you have to opt out to not observe something.
It does know what changed, and so only if the view is actually using a property that changed only then that view will be refreshed, and it supports all of those nice things like optional collection, nested, you can just do all of that and it just works, but for
SwiftUI it's iOS 17 plus.
So how does it look?
We have a new syntax, first of all.
We have this macro instead of protocol.
We don't need to do anything, we can just do var model, var year, because everything is observed by default.
And then the state object is simplified to simply state.
That causes new behaviour, otherwise it will just be, you know, some sugar and not very interesting.
So the main behaviour change is that in this case, when we change car.year, the view is not refreshed.
Because observation knows that we only care about car.model, we do not care about the year, so it's just not going to diff the view and it's not going to refresh the view.
So the big question is how does it know?
And it kind of looks like magic, right?
It's like some magical thing.
And you might think, oh, maybe it's some private API stuff, maybe it's some crazy reflection, you know, mirror stuff, maybe it's parsing the body of the view at compile time and creating something on the side.
It's actually none of those things.
And we're going to, like I said before, now we're going to poke around into the code base of observation and see exactly how it works.
How observation works.
So, like I said, we have new syntax that is creating this new behaviour.
So we're going to look under the hood of this new syntax and see how that new syntax helps us create this new behaviour.
So we have this macro at observable.
And the nice thing with Xcode 15 is that we can do right click on the macro and ask Xcode to expand that macro.
And then we get that.
This is a lot of code.
But trust me, not much is actually happening here.
And I'm going to walk you through it.
At least the part you should care about.
It's not actually a lot.
So first of all, we have another macro, suddenly, which is called observation tracked.
And then we have this underscore version of the value.
So all we did is we said we have this var value that is some string, suddenly we have underscore value that was created for us that is also initialized to the same value, to string of one, and it's observation ignored, which is another macro.
And then we have this new observation, whatever that means, we're going to see in a second.
This object, as you can see, it's not static. we create this model, then we have another value of this observation registrar.
And then we have two functions.
One is access, which all it does is it's saying observation registrar.access, that's it, and it provides self, the model, and the key path.
The property we accessed.
And then we have with mutation, which is kind of like the setter version equivalent of access.
This one provides self, key path, and this mutation closure, which we're going to see in a second.
So you can see we have these two new macros, so observation ignored, there's nothing to expand here, it's an empty macro, it's just meant to mark for observation of the compiler to not, you know, not observe this property.
Observation tracked, however, has more stuff that we can expand even further and that goes outside of the slide.
So imagine you still have all of this, but then you also have that.
And so when we expand observation tracked, we suddenly see this very interesting thing.
So suddenly this value that we created, and we thought it's just data, just a string, this now became a computed property, it's not data any more.
And so now we say, oh, okay, so the underscore value, that's now the data, and this is just a computed property that access the underscore value, but before it access that value, it calls access, which now we know all it does is just calling the registrar, and it calls in the setter, it calls with mutation, which also we know it's just calling the registrar,
But the interesting thing that you can see here, it doesn't change the value, it actually creates a closure to change the value, and it gives that to the registrar.
So this is what we wrote, we created some, you know, model with a couple of properties, one, two, three, very small and very simple, and we added this observable macro, and this is what we got from the observable framework.
We got this getter and setter, and both of them are calling the registrar, and both of them are calling these functions on the registrar access and with mutation.
So later when we run the app, we have some view, and that view has some body, and the body of that view is accessing, you know, that value in the model, and that is going to call the getter, that is going to call the registrar, and that is going to call the access.
So, call the body of the view, it's essentially calling access on the registrar for any observable model that we have.
Then later somewhere something happened, we got some new data from the server, whatever, and we called some function that is changing that value, and so that is calling the setter, which is calling with mutation on the registrar.
So let's start with the access.
So access, what it does, there is a lot of pointer related code here to, you know, for memory safety and all that, you can ignore that, we're not going to deal with that for now, it doesn't really matter, but what actually matters here is that we have this underscore thread local.value, and that thread local.value is a static value that is local to the thread, and the type of that value is observation tracking access list.
And to that access list, we call add access, and we give, again, the key path that we got, context, context is essentially just everything that ‑‑ basically the entire state of the registrar, everything the registrar has, it's almost like passing the registrar itself as a reference, basically.
So that thread local.value, it basically stores all the registrations, so whenever some registrar calls add access, it is basically getting into the same value, the same static value,
And that is because thread local.value is a TLS thread local storage, which means it's essentially global value for the thread.
So it's almost like a single tone, but for this one specific thread that we're running on currently, which is probably the main thread in the case of SwiftUI.
And the type is, like I said, observation tracking.\_accesslist.
So when we call add access in access list, so access list itself has this dictionary of entries, which are basically identifiers to an entry.
This entry you can see inside add access, it's basically -- it's just a value that contains that context, that holds on to that context we got from the registrar, which again is just a state of the registrar, and then we add the key path.
And so eventually we're going to have this dictionary that has all the key paths from all the registrars with the context about those registrars.
So we already learned about two main players that we have in this framework, the registrar and the underscore thread local value, the destroy, again, is one pair observable object instance, and it's kind of just like a proxy to register all the get and set calls, and the access list is one per thread, and this is the list, the main place that keeps all the registrations.
Then we have observation tracking, which is the third player that we're going to look at right now.
So observation tracking, that's the main entry point into the framework, and it has mainly
Mainly, that's half true, but let's imagine that it has mainly one public global function, which is called with observation tracking on change, and it takes two things, it takes an apply closure and an on change closure.
The apply closure, this is where we register anything we care about.
Right?
So in this case, we are iterating some cars, and for each car we want to print a name.
The fact that we call that name calls the getter, registers that we care about the name, and then when the name changes, the on change is what's called, and then we print, you know, do whatever.
And so you can kind of like imagine what maybe happens in SwiftUI, this part is not open source, so we cannot view, but it's probably something similar to what you see here, there's probably some kind of render function that calls with observation tracking, accesses the body inside the apply closure, and then eventually when something changes, all we need is we just need to do recursion and render ourselves again, right, and get the body again, do the diffing, whatever we need to do and refresh the view.
So for example, we have some view, we have this car.model, and we use that model inside the body of that view, and then later we change the model to Peugeot F08, however you pronounce it. The interesting thing here is that if we pass the object itself, the car itself to the sub view, now we did not access any property of the car in this view. This means that this body is not observing car, even though we are using the car object, we have it in state, we pass it to sub view, but we will not be refreshed when any of the properties in car change because we do not use any of the properties inside car. So we can pass the view kind of like a proxy to the sub view.
Sub view is probably using the car.model somewhere, so sub view is going to register to refresh whenever that model changes.
So with observation tracking, that entry point I mentioned, it's a very simple function, actually, it doesn't have a lot, it has two things that it does, generate access list and install tracking.
Generate access list, mostly what it does is just call apply, and then it records an access any access and registered observed properties.
But if you think about it for a second, those just happen for us, right?
We just call a getter that calls the registrar that calls the access list and we're pretty much done.
And so this is everything that happens inside generate access list, we literally just call apply and then we just grab thread local that value and we have everything we need, because when we call the apply, it called somebody, it called the registrars, and it registered everything.
There's a lot of thread safety and pointer manipulation code here that I completely deleted.
So if you actually open the repo and you look at it, you'll be like, oh, what's going on, it's a huge function.
It's all boilerplate.
This is the actual logic of what's actually happening there.
And then we return the access list that we got.
What we do with that access list, we call install tracking.
And install tracking is another function that takes that list of things we accessed and things we care about.
And the on change closure, that's what we got from the caller, this is what we need to do when something changes.
So inside the install tracking, we are iterating that list, and we connect each access, each, you know, a key path that was accessed in any of the observed objects to this on change closure.
So again there's a lot of pipeline code here that I'm skipping, but this is kind of like a simplification of what that function does, and basically all it does is it just iterates the entries inside the access list, and for each entry it's called a register tracking, and remember the entry has the context which is the registrar basically. the properties, that's a list of each key path that was accessed for that entry, for that object, and the on change closure.
So just a reminder, we have this access list, it's all in this entries dictionary, and those entries are all the properties connected to the context of the registrar.
Inside the register tracking itself, this is reaching inside the registrar itself through the entry, we're getting these properties and the on change closure, and then we create this observation object.
I actually now don't remember if it's a value or class, so I'm not sure it's an object, but we're creating this observation type that holds on to the on change closure, this is what we need to call eventually, and all the properties that we care about.
And then the registrar itself keeps, retains the memory of those observation values.
And this is where we finally connect between, you know, we have the registered properties, the things we care about, the things that when they change we want to call something, and we have this on change closure on the other hand.
We have the on change closure on this side that we want to call eventually, and then finally the registrar has the connection between them.
And that's basically it, because now the registrar can just take care of it, now the registrar knows what we care about, it knows what to do when something changed, and it can just call the on change closure.
And that's basically it, that's pretty much how observation works.
That's -- there isn't much more to it.
Let's use an example to kind of summarise what we just saw.
So we call with observation tracking, we provide two closures, apply and on change.
We call apply, when we call apply, things get called, you know, some bodies and some views, so we have some user, some car, and they have some properties, and we call the getter and the setter, sorry, only the getter at this point, and those are calling the registrar, those registrars are all giving what they have to the access list, and then we just get the list, and then we pass the on change to those registrars that we have access to them through the access list.
And then at some point, the user had a birthday, so we need to change the age.
We're calling set on the age of the user, that set again calls the registrar, now the registrar has this observations array, sorry, dictionary, and it just looks for the key path of age on the user, and it checks, oh, am I observing age, looks like I'm observing age, calling on change, and cancels the observation.
So now that we know at least in high level how observation works, honestly it's not that much high level, it's basically this is pretty much it.
There are a few things we need to keep in mind when we are using observations.
So if you watch the WWDC tutorials on how to use observation, this is kind of how they present that.
You know, this amazing beautiful world, everything is perfect, there's no problems.
In reality, at least in the next, I don't know, couple years, three years, until we can actually use only observation and forget observable object ever existed, this is what we have for now.
This is kind of like our reality currently.
And even if we don't have, you know, some of us might have observable object and -- sorry, observed object and observable in the same project, and then it's probably going to be very confusing, even if not, at least mentally we will have to, you know, maybe you'll jump in between projects that one migrated and one didn't, one is iOS 17 plus, one is iOS
16 plus.
So either mentally or actually in the code base we will have to do this understanding between how things work with and without.
So the first and maybe the most confusing thing is property wrappers.
If you have a view, bless you, with a state, and if you're using observable, like I said, you can just put at state, right?
But if you're using observable object, you have to use state object, you cannot just put at state, because at state is only for value types before observable.
The annoying thing here is that Xcode is not going to say anything, Xcode will be very happy, no warning given, but the object will not be retained, because only if you have state object for observable object, the object is retained and only then you will see any changes.
So you have to use state object.
So if you're using observable, using state, if you're using observable object, using state object.
The other thing is the observed object property, which usually we had to add that to some child view that is receiving a model from a parent view, now I'm seeing the slide is actually wrong, it should not be equals model, it should be receiving a model type from a parent view.
And so with observable I can just do let, I get the model from somewhere from a parent view and it's observed and everything is fine.
With observable object if you don't remember to use observed object then it will just not be refreshed and then you'll be very confused what's going on.
So again if you're using observable you can just use simple let, if you're using observable object you have to use observed object.
And here I can see that the slides are actually correct in the code.
So this is kind of like a summary, I don't know if you, for those who like to take pictures of useful slides, feel free to take this is a good snap slide basically showing what I just explained.
Again, state object versus state and observed object versus simple.
The other thing is state versus identity.
So this is also true with observed object.
It's not a new thing, but it can be maybe extra confusing with observable.
And the reason it can be extra confusing is because we think that, you know, observable is so great, it's solved all of our problems, we don't need to worry, if I didn't use some property then I don't even care that I have that model in my view, it's not going to refresh.
Sort of.
So with observable object before observation, we had this state object, and let's say that we have this root view that creates a branch view that creates a leaf view.
And we don't want the branch view to care or know about the model, we want to basically inject this model that we have all the way to the leaf view and keep everything in the middle decoupled.
So we used environment object, that was great.
And that way branch doesn't even need to know that model even exists.
Now we might be able to say, oh, I don't need that stuff, I can just pass the model to the branch and then just pass the model to the leaf and branch is not using model, so everything is fine, branch is not going to be refreshed, everything is like I expected.
But here's the catch.
If you change a property inside the model, yes, that is true, because the state changed and branch is not using any of those properties.
But if you change the model itself, then you change the identity of the view.
So if you look at the root here in the body, we're not changing model.something, we're not getting to any getters inside models that's calling the registrar, instead we have an entirely new model that's a new class, that's a new address in memory, and that changes
This is branch's identity.
And so now it's not that the dependencies of branch change, it's that branch itself as a view changed.
And in that case, yes, branch will be refreshed in the case that you see here.
And then both -- in this case.
So you might say, okay, this is interesting, but I don't see how this actually applies to anything in my life that I care about.
So here's a real world example that kind of makes it very easy to see.
So imagine we have a list with some data, and we access some value inside this data, right?
And this is very simple, each row in the list is just a text with a label and some value.
At some point we want to update the data.
And so let's say that we obviously want animation because we want the app to look great and be animated.
And so the code here is just a weird way to basically replace between the first and the second value, right?
We take we grab the value index 0, we give 1 to 0, and then we give the temporary to

1.  So, we basically replaced the values inside the model between 0 and 1.
    So that means that if we had if the values were also these numbers, like 0, 1, 2, 3,
    You would see that the top row, suddenly the number changes, and the second row, the number also changes.
    And that's exactly what you can see.
    The animation is a little bit fast, so, but I'm going to spoil it to you, one and two are going to be replaced, but because we didn't change the identity here, we only changed the dependencies, each row in the list essentially says, oh, I can handle this update myself,
    I don't need the list to handle this animation for me.
    And so they don't know about each other.
    So one just fades into two and two just fades into one.
    So look at that for a second.
    There you go.
    Hope you didn't miss it.
    And so maybe this is what we want, maybe not.
    But this is what happens when the dependencies change but not the identity of the view.
    What if we change the model itself?
    So we actually take the object that we have at data at index zero, we give it to -- sorry,
    We take index 1, give it to index 0, we take index 0, give it to index 1, now we change the objects themselves, now the text view actually changes the identity.
    Because the object changed and not just dependencies inside that object.
    This actually changes the animation, so now the object is saying I changed as a view,
    I don't know how to animate myself, I don't know how to animate my changes, I need my parent, which is the list to take care of that.
    And then the list animates those changes, and now you're going to see an animation that maybe you were expecting, which is the two rows replacing themselves.
    There you go.
    So this is kind of like an interesting example of where you can just visually very clearly see what happens when the dependencies of your view change, but it's the same view, versus when the identity of the view change, and it's just a different view and then SwiftUI has to basically take away the old view and put a new view instead.
    And it's very easy to get confused with observation.
    So that's that.
    The next thing is escaping content closure.
    So there is this design pattern in SwiftUI whenever you are creating container objects, right?
    You are taking this content closure, some generic type, and you are taking it in the initialiser, and usually the best practice is to open that closure inside init and not hold closure, but instead to hold the content itself after you already opened it.
    Let's think about it for a second with observation.
    This initialiser is going to get called in a body of some view, right?
    Some parent view is going to create the subview and create and call the initialiser because they create that view inside the body.
    So we are now inside the body of some other parent view.
    So this means that whatever happens inside content in whatever property is getting called inside this closure, even though only we the subview care about it, the parent view is the one that's going to register it and observe it.
    So if we have this content view, we pass content and it's some text that access model.value.
    Model.value is registered to content view, not to subview.
    Because this is when the closure is called.
    And observation doesn't care, you know, where was it in the code, all it cares is that it was called as part of the same apply closure, as part of the same body.
    And then later we change model.value from whatever it was first to some other string.
    And you can see here content view is only using other value.
    And if you remember the example I showed all the way at the beginning, this looks like that example where I could say, oh, this is great, value changes, but we don't care about value because we're not using it, so we're not going to be refreshed.
    But yes, we are going to be refreshed, because that closure we passed to subview was getting called inside our body.
    And the interesting thing is because we already opened the closure, maybe we don't even show that content.
    So here we pass show some boolean flag, we pass false, we're not even using that content in the subview, that doesn't matter.
    The content view is still going to be refreshed and also the subview is going to be refreshed because of that, even though we're just not presenting this content anywhere.
    So instead if you drop that customise initialiser and you just keep the content as a closure in this case, it's not going to be called and it's not going to be refreshed unnecessarily.
    So first of all, content view never refreshes in this case, because like I said we don't use model.value, we only use model.other value.
    And then even subview will only observe and be refreshed when show it is actually true.
    So as long as show it is false, we don't even use that content, we don't even open that closure and it doesn't even matter what happens to model.value, it can change a thousand times, it doesn't matter, that view will never be refreshed, only when show it is true, now we care about the content, now we are going to observe model.value.
    You might be asking, okay, so should I stop opening closures everywhere in my app?
    I'm not saying that.
    I think it's a case by case situation, so I don't know if there is suddenly a new best practice versus what we have until now, but I think this is just something to keep in mind and it's very interesting way to see the difference between what we had before and the behaviour we have with observation and how the fact that observation doesn't care which view using which property, all it cares is that when you call somebody of some view, anything that got called inside that body for whatever reason is going to be observed for that body.
    Then lastly, there are some things that are not supported with observation.
    Some of them are by design, some of them will maybe be supported later, some of them are just bugs that we're still waiting on the team at Apple to improve, but as of today, so first of all, you cannot do lazy properties, if you have lazy var, you're just going to get an error, cannot be used on a computed property, because if you remember, this value now is not data anymore, it's a computed property, and the computed property cannot have lazy.
    Property wrappers, if you have some custom property wrappers, exactly the same scenario, you will have exactly the same error, cannot be applied to computed property.
    And finally, no value types.
    Observation as a decision as of the second review that passed in August, just simply does not support value types, it's only classes, only reference types.
    So a few takeaways, I think it's really useful to learn how observation works, because it looks at the beginning like, you know, just a simplified version of what we had before and nicer syntax, but actually there is a lot of confusion and a lot of changes in the logic that I think is important to know, and I think once you do know that and you have that in mind, it really helps to build solid apps, or if they're not solid, then at least easier to debug issues when you do have them.
    And then, like I said, it's not just new syntax, there's a lot of behavioural changes and it's important to keep them in mind.
    And then know your state or know the syntax you need to be using for each framework, because
    Xcode unfortunately is not going to help you.
    And finally, it is a very powerful framework, I think it's a great framework and I think it has a lot of potential and benefit, but it's not a silver bullet.
    That's it.
    [Applause] >> I'd start with a question on -- that applies to both things, which is about debugging.
    So how do you debug those stuff, both observables and async streams?
    Apparently, I can't debug a microphone.
    Async streams, it's pretty standard.
    You're following the flow through.
    It's just the async side of it.
    And Apple introduced some nice testing macros so that you can test some async things too,
    So that's been helpful.
    Well, with observation, I think Xcode, first of all, did an amazing job with the fact that you can just expand the macro.
    Something I didn't show is that once you expand the macro, you can actually just copy the entire code base, the entire snippet of that expanded macro, and paste it as is, and then drop the @observable declaration.
    And you get exactly the same behavior.
    You don't lose anything.
    Everything walks exactly the same.
    And then it's your code.
    And then you can just debug it.
    And you can see what's going on.
    And so you can see exactly how it runs.
    And you can add print statements or whatever you need and breakpoints.
    You can also set a breakpoint inside the expanded macro.
    Even better.
    And then you can just print from there.
    Even better.
    So what I'm getting from both subjects is should we expect at some point combined to be dropped completely?
    Or is it still something that we're going to have for a long time before it can be completely replaced from SwiftUI and everything else?

- So people get upset when I say this, but it's the line from Castle Blanket that combines going away, not today, but soon and for the rest of your life.
- And one of the things that hit me when you talked about observation.
  And I was like, OK, there's so many things happening away from what I'm doing myself because there are some microbes, et cetera.
  Should we be really worried about some memory issues?
  Should we think about, oh, there's going to be so much trouble with zombies, et cetera?
  I am not aware of any memory issues with using observable.
  You mean the access list, right?
  I'm not aware of any memory issues.
  I can only assume that Apple ran tests.
  But who knows?
  I do see that they occasionally add more and more.
  In the last three months, I've been tracking that part of the Swift 2 Pro.
  And every time I see a new PR with a new test to check a new edge case, they found-- like for example just a month ago I think they realized that nested, if you call it with observation tracking and inside you call it with observation tracking again, it was broken in some way, so they fixed it and added a test to that.
  So they keep finding those edge cases and they keep fixing them and adding tests to them.
  I'm not aware, I haven't seen anything about anybody's complaint or seen anything.
  One of the things I love about Observable is if you have a class that you make observable and you're observing it in a view way here, you can put controllers in between even structs and computed properties since this is registered to say I want to know when anything changes.
  It like reaches through and says I'm tracking number all the way here.
  This is a computed property that uses number then it gets those updates too.
  There's a lot of just really nice magic because the first thing people said who came from combined was, well, how do I republish something?
  I consume it and then republish it.
  You don't have to.
  Computed properties makes it very easy.
  Exactly.
  And that's actually why nested observable objects don't work, because they are very explicit.
  They call object will change, right?
  And then that doesn't make the outer observable object to also call object will change to notify the view, OSwiftUI.
  In this case, like I said, nobody cares.
  It just doesn't matter.
  A property gets accessed, it gets registered, you're done.
  A question that is more about architecture than about the implementation itself.
  What's your advice on the granularity of using observability or async streams in your SwiftUI views?
  So should we have them, observability, basically in subviews, even nested subviews, or whether or not?
  Well.
  But yeah, I think it's a really good question, because I already showed a couple of those caveats and I think there were some things that it took maybe a year or two, but eventually we realised, okay, this is how we should do this in SwiftUI, this is how we should do that in SwiftUI, for example, the Redux pattern, you know, Apple doesn't say it explicitly, but they sort of say it implicitly, you probably should not do Redux style, which is a huge context with everything, because of how observable, sorry, because of how observed object is working, and then observable came and kind of like threw all of that out the window, but it has other caveats, and I think we might see some changes in patterns or in best practices in terms of performance, in terms of architecture, in terms of how to organise your code and how to organise your views with, for observable, that might be actually very different from
  So, we have a lot of things that we can do.
  We can do a lot of things that we can do to make it more user-friendly, but we have a lot of things that we can do.
  We can do a lot of things that we can do to make it more user-friendly, but we have a lot the more power you're getting.
  And then if you need to reach back and change something, you need the @bindable to do that.
- No questions?
  All right, I see more questions from the audience.
  There's all specific about observables.
  I had personal questions, not personal to you, but to what's going on in this field.
  So basically we've been living until very recently with no async in Swift.
  And then all of a sudden, we go combine async streams observables.
  So as a developer, I would say, what's going on?
  So is Apple getting a [INAUDIBLE] roadmap or something like this?
  I'd say more that we have been using async for a long time, but now we're being more careful about it.
  You can't say that KVO and notifications-- we've been using async since the beginning, but now we're finding out that we made a lot of bad mistakes and bad decisions and we weren't careful.
  Async is forcing us to really be careful with things.
  So I recently went through code base for one of my apps and you notice I'm very careful instead of importing foundation or Swift UI import combined so I could find every use of it and replace it with observable and I'm delighted.
  The code has gotten smaller, easier, and I really was a fan of combined.
  So this is not a combined hater.
  I remember one of your talks on Eric's Swift back in the day.
  So, yeah.
- I guess so.
  All right.
  So, that's all.
  So, thank you very much indeed.
  (audience applauding)
  (audience applauding)
