---
slug: "/talks/flutter-connection-23/craig-labenz-lifecycle-of-a-renderobject"
date: 2023-06-02
title: "Lifecycle of a RenderObject"
author: "Craig Labenz"
video: HtIapq5Vo3w
thumbnail: thumbnails/craiglabenz.png
slides: downloads/life-cycle-of-a-renderobject.pdf
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

As I said, my name is Craig LeBenz, and thank you for attending the lifecycle of a render object.

We're going to continue the talk that I started in the last fall at Flutter Vikings.

And apologies in advance--

I almost dropped it.

This talk, like a gas, grew to fill the size of its container.

So we've got a lot to get through.

Do the click.

Oh.

All right, keyboard it is.

OK.

So that last talk, Lifecycle of a Widget, was about more than just widgets, of course, because those are immutable configuration objects.

They never change.

They have no life cycle.

And just like that was about more than widgets, of course, this will be about more than render objects.

Apologies, I'm going to reuse a few screens--

I have some screenshots of my old slide deck.

Now, we do have a lot to get through, but I do want to briefly kind of recap some of the last things so we can have a shared starting point.

So Flutter either builds or rebuilds your widget tree, syncs it with the element tree, and then all of the render objects-- or sorry, all of your render object widgets have their createRenderObject or updateRenderObject methods run.

And that collectively gives us the render tree.

And once Flutter has its hands on that, it's ready to throw on an old pair of blue jeans and start painting.

Now, I'm not going to spend a ton of time talking about writing a custom render object.

If that interests you, check out the first episode of the Flutter build show.

OK, so let's get to know this darn thing.

I'm going to build up a graphic of its lifecycle as we go, starting with this artistic gem.

And on the left will always be the outside force that has kind of prodded our render object into motion.

And then on the right, we'll build up its lifecycle.

So the render object comes into this world when its mother widget calls create render object.

And then we're up and running.

So the first thing to know about the render object is that it is an abstract class.

And it's pretty unopinionated.

It inherits a handful of basic tree-related mechanics from its parent there abstract node.

And then other than that, it gets to work setting up a few of its own concepts.

So the first of those is layout.

And you can think of layout as the act of a render object sizing itself and then allowing its children to size themselves, within reason, of course.

And this is the beginning of where the adage of constraints going down, size coming back up, and parent setting the position comes from.

So the layout phase happens when this thing called the pipeline owner enters its flush phase.

And the pipeline owner is a very high level class.

It sits kind of at the very beginning Flutter code.

Talked about it a bit in the last talk as well.

But it manages all three of the trees.

And oh, yeah.

So layout is not the only thing that happens in the flesh phase, but it is how this gets started.

So there's a handful of methods that come together for layout.

And they are layout, which is implemented by the framework.

And it's called by that pipeline owner.

And then it recurses all the way down to us, whichever render object we're imagining we are.

And it doesn't really do any-- it doesn't do a lot of work.

It's mostly just bookkeeping.

But it does then delegate to this performLayout method.

And we actually implement performLayout ourselves.

And of course, when I say we implement, I mean, if you ever elect to write a render object, which you needn't ever do.

And then there's one last method, markNeedsLayout.

And this tells Flutter, hey, this render object's getting a little stale.

Let's maybe lay it out again.

Now, the reason that the layout method returns void instead of any actual sizing information is that this allows different subclasses of RenderObject to have radically different layout protocols.

So the most common of these is called a RenderBox.

And that essentially is a form of RenderObject that just says, you probably want Cartesian coordinates, which is simple xy coordinates.

Now, for RenderBoxes, the job of performLayout is to figure out how much space this RenderBox needs and then save that information to the size variable there.

So here's an example of this all coming together in the padding widget render object called render padding.

And we can see the layout.

It just saves some constraints.

There's a ton of bookkeeping.

And then it calls perform layout.

And perform layout then asks the child to layout, and then combines all this information together to figure out its own size.

And we can kind of see the adage happening here.

We can see the constraints are going down to the child.

The size is coming back up from the child.

And we don't see the positioning of the child here, because that happens in the paint method.

OK, which is the perfect segue for painting.

So painting is like the most render object-y thing a render object can ever do.

And for this phase, we stay in this kind of like flush, you know, kind of meta phase.

No one else really calls it that.

This is just my lazy terminology.

But it is still invoked from the pipeline owner calling its various flush methods.

And there's two main methods that come together to comprise painting.

And the first of those is called paint.

And this we implement.

And again, we never really call paint ourselves.

It recurses its way down from the pipeline owner.

We do, in a render object, though, ask any of our children to paint if we're not a leaf render object.

And then the last one is markNeedsPaint.

This is similar to markNeedsLayout from before.

This tells Flutter, hey, this render object, something's changed, and it's got to repaint itself.

OK, now paint takes a couple of these interesting parameters here, offset and painting context.

So offset is the distance between our origin and our parents' origin.

And you might think that, if this is a render box, we just got done setting the size attribute in that layout phase right before this.

So you might think, well, maybe it's true that render boxes can't paint outside of that space that they indicated.

But that is actually not a restriction, which is a good thing.

Because if it was, then it would make the algorithm to paint something like drop shadow or globe effect or anything else with good reason to escape our specified area. would make that a lot more complicated.

So render boxes do not have to color within the lines, which is a little surprising.

And then the next thing is this painting context variable.

What is that?

Well, if you've written or read render object code before, then maybe you've seen lines like this, which I'm now realizing should have been a bigger fun.

Context.canvas.drawrect.

And this kind of line suggests that maybe before we can get all that well-versed with the painting context, we actually need to become acquainted with whatever that canvas thing is.

So that is an instance of the canvas class.

And the first line of its doc string says an interface for recording graphical operations.

So while this canvas object is somewhat modeled after a real life canvas that you might stand in front of and actually paint, it's pretty different.

Because if you really, in real life, stand in front of a canvas and paint, then actual fibers on the canvas get covered in paint, and their color changes.

And the analog-- I don't know, I'm blanking on the word.

But the equivalent-- there's a good one-- in Flutter would be when something starts to produce a buffer of RGBA color values for pixels.

And this canvas object does not do that.

So it's only recording, painting instructions, and how those are going to play out and interact with each other remains to be seen at this point.

Okay.

So going back to this painting context thing, this manages canvases and it can either create spin-off canvases or it can do this thing, add a new layer, which is going to become really important in the second half of this talk.

Okay.

Next up is semantics.

We had a great talk early in the day on accessibility and semantics and accessibility are like best buddies.

So the system is very important because it integrates with the host operating system or the web browsers, screen reader and other accessibility tools.

And this is a huge job of render objects that is kind of easy to forget about.

Layout and painting is super obvious, but semantics is another big thing that render objects handle.

So as for the life cycle, this ends up wrapping up the flush phase.

This is the last thing that the pipeline owner kicks off when it is flushing all of the queued up render objects to build the next frame.

And there's two top-level methods that come together for semantics, and they are describe semantics configuration, really rolls off the tongue, and mark needs semantics update.

And mark -- or describe semantics configuration looks like this.

It takes this semantics configuration object, and it's the job of this method to staple onto that.

It's a mutable object.

Add to it any relevant information that the semantics system will need.

Now, Flutter aspires to set us up for success here by offering a lot of render objects that just work.

But it is very important for us to test our apps with assistive technologies turned on to make sure there are no awkward surprises.

And anyone who is using those and depends on those technologies can actually achieve whatever they set out to do when they launch our app.

So that's super important.

But Flutter tries to make it as easy for us as it can.

OK, so technically, all of that is enough to flush-- well, to get started flushing one frame.

But not all of the code that runs for the first frame has to necessarily run for every subsequent frame.

So I want to talk a little bit about the differences there.

So we touched on a handful of mark needs methods earlier.

Mark needs layout, mark needs paint, and mark needs semantics update.

And other than mark apparently needing hug, it goes with these other three main methods that we were looking at-- layout, paint, and describe semantics configuration.

So the method on the left queues up the method on the right.

But let's actually see how this works.

Let's pretend we're writing a render object.

And all it does is show a string.

So we're calling it render string.

And the way this works is you take that value that's passed in, and you store it on a private attribute.

And then you get to work writing a magic setter.

And of course, you'll have a getter to proxy to it as well.

But this magic setter works like this.

The first thing you do is you have a guard statement that short circuits early if the value isn't actually new.

Then you save the value.

And then it's the job of whoever's writing this code to start calling those various mark needs methods.

So our render string has a new string to show.

Obviously, it will need to repaint.

If it doesn't repaint, then it will continue to show the old letters of the old string.

So that won't do.

But the new string might take up a different amount of space.

So this render object will also need to relay itself out.

But there's a gotcha here, which is that mark--

Well, the whole layout process always implies painting.

And this makes sense because if the size of something that we're rendering changes, then of course, the pixel buffer that it should ultimately produce will have to change as well.

And so we can cross off where we called markNeedsPaint, completely redundant.

We don't need to do that.

Now, this render object does have a new string value.

That's very likely important for semantics.

So we would call markNeedsSemanticsUpdate in this method as well.

And this is starting to look like a complete-- we obviously have not implemented the other important methods.

But this is kind of like how that update process works with a render object.

So these markNeeds methods, what do they do?

So here's some pseudocode.

A lot of bookkeeping has been stripped out.

But this is essentially what markNeeds layout does.

First, it recurses up the tree, talking to all of its parents, and-- well, until it hits a layer boundary.

And we heard about layers a moment earlier.

But it goes up the tree until it finds a layer boundary, and it makes all of its parents also join the party and mark themselves as needing to relay out.

Then it adds itself to a list that the pipeline owner is maintaining, and that will be flushed.

That is what gets flushed for the next frame when the pipeline owner kicks that off.

OK, and then going back a second here,

I just want to hit again on this.

This is one of the biggest things that layers do.

The whole layer part of this talk is still coming up, but we're seeing the first evidence here of how layers can start to segment our render objects into these different little pocket universes that all operate together.

OK, and what triggers that magic setter that we were looking at a couple slides ago?

This one.

What triggers that?

Well, in front of every render object is a render object widget.

So in front of our very simple render string, render object might be this string widget.

And it's in this update render object method down here, where the framework passes in the pre-existing render object to the brand new widget.

And then what the widget does is just very directly plop its attributes right on the render object.

And then this, of course, is the magic setter that we were just writing here.

So this is the mechanism that binds widgets and render objects together and allows the whole thing to work when we call setState.

So all of that brings us to here in the lifecycle of a render object, where updateRenderObject calls the markNeedy methods.

And then that can potentially put our render object back in the queue for the next flush phase.

It's getting exciting now.

OK, next up is hit testing.

And it was always going to have to be render objects that handled hit testing, because the whole point, or the scenario of hit testing is the user touches their phone or clicks somewhere, and the operating system gets coordinates.

And then it says to the Flutter engine, hey, the user's doing something at this spot.

And the engine's like, great, framework, what's at that spot?

And so render objects, as the only things that know their size or their layout or anything like that, they're obviously the part of Flutter that can answer the question, what is at a specific location?

And so the hit test method looks like this.

Again, even though this is long, I've stripped out a crazy amount of bookkeeping.

But the hit test method accepts this box hit test result object, to which it will append result entries, and an offset.

And also note that this all lives on the render box, because the whole concept of hit testing requires some kind of coordinates.

But render object itself doesn't have coordinates.

So it's render box that implements something for hit testing.

And if you ever yourself want to subclass render object, then you will also be on the hook to implement hit testing.

In practice, almost nobody does this.

But the first thing this method does is immediately short circuit if the size attribute that we set during layout does not contain the position.

So this is an interesting distinction because render boxes and objects in general can color outside the lines, but they cannot accept a hit test outside the lines.

And then it just asks all of its children.

It even asks itself.

The default assumption is that the average render box does not care whether or not there's a hit or a click or anything within its bounds.

Think about that render padding render object we were looking at earlier.

It definitely doesn't want to participate in hit testing, and so it just returns false from that hit test self method.

But then, anyway, that method recurses around the tree and builds up all of the render objects that think they may have been hit.

And so that brings us to here in the lifecycle of RenderObject, where any user gesture can get us into hit testing.

A positive hit test result can potentially lead to a callback method being invoked in our widget tree.

That can lead to widget.render or updateRenderObject, which can call a MarkNeedy method, which can lead to the render object being updated in the next flush phase.

It's all coming together.

Now, sadly, all good things come to an end.

And so eventually, this render object too shall pass.

And so the dispose method exists.

And it's called-- we don't have to call it, but it's very critical.

Just like in widgets, if you add a text editing controller or an animation controller or anything, you've got to tear those down.

Same thing with a render object.

If you create a layer or a text painter or any kind of fun render object shenanigans, you've got to clean up after yourself.

All right.

And that concludes the lifecycle of a render object.

But it is not close to concluding this talk.

So another thing to be aware of about render objects is this concept called parent data.

And it's an object that lives on a render object itself, but it's set and typically only read by the parent.

So it's almost like a place for the parent to keep notes about their children render objects.

And here's a quick example of the render flex render object.

This is what sits behind row and column.

And we can see here that I'm spoiling my punchline.

I thought it was going to highlight a couple lines.

Anyway, it's ordering the children and noting on each one what the next sibling is.

In general, parent render objects keep track of things like sizing, layout, positioning, whatnot to make their lives easier later on.

Anyway, I like to think of this like a really bad parent, like Homer Simpson, who makes Bart and Lisa wear t-shirts that say Bart and Lisa so he can keep track of which one's which.

And that's kind of what parent data is.

OK, now some widgets and render objects make really explicit use of this parent data thing.

The stack and position widgets are in that camp.

So if you've ever wondered, how does a position widget know to complain if you don't use it directly inside of a stack.

Widgets aren't supposed to know about each other, they're not supposed to be aware or have requirements about who their neighbors are, but the positioned widget somehow does, and that's because its render object interrogates the parent data that is set on it and makes sure that it came from a stack, and if it didn't, it complains.

Now we've really gotten to a pretty high-level picture of a render object, but there's an an awkward gap in the story as it stands right now, which is that we still have not even come close to calculating color values for any pixels, so surely we are not done.

So to recap, first we had the widget tree, which offers a declarative UI for how we describe how we want our UIs to look.

Then there's the element tree that delivers the imperative code to juggle changes in the widget tree from one frame to the next.

And then behind both of those is the render object tree that sizes everything and records these painting instructions.

But eventually, somebody has obviously got to evaluate those painting instructions, or our users' phones will never light up, and no one will install our Flutter apps.

So toward that end, I'm pleased to introduce you to the layer tree.

You would have been excused for thinking that the render tree rendered things, but it turns out, no.

All right, so once the render tree is done recursively calling paint, then this painting context thing is left holding on to any and all canvases that our render objects collectively created and wrote painting instructions to.

So each render object could have written to the default canvas found at context.canvas or it could have pushed a layer, which we were talking about earlier.

And it's this mechanism where different render objects add a layer to the layer tree that makes that grow from one node where it starts at the beginning of running through the render tree to however big the layer tree ends up actually being.

And so this is kind of like a way to visualize what this layer tree looks like.

There's however many render objects created layers, that's how many layers there will be, and then each layer kind of is holding on to this little subtree of the render objects that contributed to its canvas, if that makes sense.

So this is one thing that layers do, they kind of compartmentalize render objects, and we're going to see the importance of this more in just a second.

Okay.

But there's another thing layers can do, and I like to think of them, or this feature, is almost like being parentheses in a math equation.

We all know that typically math problems are solved by following the order of operations.

But layers can change that, just like parentheses in math can change the output of something by elevating the prominence of a certain relationship or disambiguating the order that things should be in.

Layers can do the same thing in Flutter.

So let's consider some UI written a little bit more like grade school math.

So we have some background plus some offset plus some opacity applied to a circle and a square.

And that might render something like this.

And what's going on here, that opacity is basically a layer that is saying, apply this opacity to all my children, but not until they're first composited.

And so we've composited the square over the circle and lost that bottom right part of the circle.

Even though the opacity is kind of reducing, we should be able to see something behind the square.

We can't because the opacity layer has composited them first.

So if you want this kind of functionality, the layer-- this mechanic is the only way that Flutter is able to deliver this.

So contrast that with maybe a more direct type of layout where the circle and the square do not have to be composited first.

And it's probably what you were expecting to see.

Now the circle below is shining through the square just a little bit.

Oh, also, one thing I do want to say, this is not stuff that we as everyday Flutter developers have to think about.

The widgets that we write, they produce render objects that get all of this stuff correct.

But this is something that Flutter had to think about.

And if you ever find yourself writing a render object, you might as well.

But needing layers is very, very rare.

It's basically only a situation where you know as a render object that you don't trust your children not to screw up the canvas.

But you also know that you need them to all conform to the same transform or clip or something like that.

And in those situations, layers kind of save the day.

But in general, you really don't need them very often.

And especially if you're writing a leaf render object, then you really don't need one because you don't have any kids.

OK, that is the two primary jobs of layers.

They divide our render objects into these little kind of pocket universes that all repaint together.

And then they can be parentheses from math.

All right.

So here is some highly abstracted code that, again, sits all the way at the top of Flutter, kind of like the place where the engine and the framework come together.

And this drives the whole process.

So let's step through it.

It's on the Widgets Flutter Binding class, which you may have seen before when you call insureInitialized.

So in this drawFrame method, we can see the pipeline owner is calling .flush.

Really, that's like five different methods that I'm just imagining are one method called flush.

And then below that, the entire layer tree now exists because the entire render tree has had all of its layout and paint methods called.

So the layer tree now exists.

And that is passed to this thing from Dart UI called the scene builder.

And the scene builder builds a scene, so pretty well named.

And that scene object is essentially a list of display commands and selected shaders that need to run on the GPU.

And then that scene object is passed by this FlutterView class, also from Dart UI, to the graphics engine and-- or sorry, the graphics driver and the GPU.

And they are going to actually start calculating some color values for pixels.

Oh, by the way, this last line, this all happens in the engine.

And I forget where this line happens, but it certainly is not in the Flutter framework.

I mean, it's called in the framework, but then it leaves the framework very quickly.

Oh, yeah, and this, the drawFrame method that we're looking at, if any of you have seen Lifecycle of Widget, this is a persistent callback from that class or from that talk.

So the drawFrame method here is registered to run every single frame for Flutter.

Every time the engine asks the framework, like, hey, man, you want to give me a frame?

This method is registered to be in that callback.

And this line is where Skia and/or-- well, never and.

Skia or Impeller-- no, maybe and.

Technically, no.

Anyway, Skia and Impeller hide in this line.

OK, so now let's teleport ourselves into the graphics driver itself.

We're sitting right next to the CPU.

And we've been handed a couple of shaders from Flutter.

We've got shader A, B, and C. So we execute those shaders, and we get a handful of pixel buffers that they result in.

So shader A is rendering a couple of gradients where the opacity is going down.

Shader B is rendering this diagonal green line.

And shader C is apparently our background shader.

So it's just rendering all white pixels.

And these then get carved up into triangles. and moved on to the next step in this process, which is still in the graphics driver.

There's a little bit of back and forth with the engine on this stuff.

But then this gets composited down into one single pixel buffer to rule them all.

And in the darkness, bind them.

So the red pixel in the top left has full opacity.

So it covers up the green and white pixels below it.

And what we're going to get in the end here is just this red pixel in the very top left of our screen.

And it keeps compositing all the way.

And it keeps going until we get to this orange pixel that has some reduced opacity, so a little green shows through.

And we get this nice little mud water color.

And then it keeps compositing, and it keeps going.

We get the first two blue pixels just fine.

And then we have pretty low opacity on that third blue pixel, so more green shows through.

Anyway, you get the point.

This is how it composites pixels, by collapsing all of these different shaders into one final pixel buffer.

A tiny bit to note, this does imply a certain blend mode.

And you can have other blend modes, but this is the default blend mode that everyone expects you would get.

And so this pixel buffer can be sent back to the operating system, and it will be displayed on the screen.

We've finally done it.

Woo!

OK, to wrap up all of this, there's just a few edge cases that I want to get to, things that I had wondered for a long time and that I think talking about really helped clarify all of this for me.

So first, what happens when nothing is happening?

Let's say you launch the Flutter Counter app on an emulator, and then you realize it's Saturday morning,

I'm going to go for a walk, and you just get up and leave your desk.

Like, is Flutter sitting there just cranking out frames constantly the whole time?

It's not really clear, but it turns out the answer is no.

So any time the operating system's v-sync signal ticks and it asks the engine, like, hey, you got a frame?

If nothing has changed anywhere in the app, then the exact same old pixel buffer is reused, and it's a clean no-op for Flutter.

So that's good.

Number two, what is going on with repaint boundaries?

Well, the repaint boundary is a pretty interesting widget, and it takes us back to the layer tree.

So we talked about how layers work to kind of quarantine the repaint signal that leaves a given render object as it propagates around its neighbors.

So let's pretend-- got to make sure my hand's on the right button here-- let's pretend that-- or sorry, a repaint boundary widget, all it does is insert a layer into the layer tree.

So let's pretend that this layer exists because of a repaint boundary widget.

And it's worth noting, we saw in a render object's paint method, they can add a layer any time they want.

But Flutter's goal is to not really ever ask the average developer to dip below the widget layer.

But sometimes a repaint boundary is really great.

So-- or sorry, a new layer is really great.

So the repaint boundary widget exists so that we can add a layer to the layer tree without having to go through all the trouble of dipping into the render object layer ourselves.

So we used a repaint boundary somewhere in our code, and we now have a new layer in the layer tree.

And so that means that if this render object needs to repaint, it will only propagate to this other one as well, and it's not going to contaminate the whole rest of the tree and cause other things to repaint as well.

The first line of the doc string for the repaint boundary-- no, it's not the first line.

It's somewhere in there.

It says something like, useful for when a parent and a children repaint separately.

So it's possible for the parent and the descendants to repaint at the same time, but when that happens, all the work that the framework did to maintain and track that repaint boundary is for naught because it's just going to have to do all of the work anyway.

So the framework considers the ancestors and descendants of a repaint boundary repainting at the same time to be, like, not great.

Now, that was also really spoiling the plot of a question I was going to ask everyone.

Good job.

There's a scenario where the framework is so certain that a repaint boundary is going to be helpful that it adds one around every one of something.

Any guesses?

Oh, you all know?

Everyone knows that it's scrolling items.

Good, nice.

So scrolling items are just the perfect time for a repaint boundary because the framework has very high confidence that it's about to draw the exact same commands at a slightly different offset.

So it knows that there's going to be repaint signals flying around.

Like if you've got a list view and you're just scrolling, there's repaint signals coming from above.

The list view is capturing the scroll event.

It's moving the offset of things.

But the framework thinks, ah, I probably don't have to repaint those cards that are actually-- the list tiles that are scrolling by, so it wraps each one in a repaint.

Huge, huge performance win.

But there are even gotchas here, and I'm not going to spoil this one.

There are some scenarios that can make -- that can actually disrupt the repaint boundary's ability to be helpful even around scrolling items.

Anyone have a guess?

No one has a guess.

That's okay.

It's if the scrolling item is animating, because if that's happening, then again, you're right back to where you were in the first place where you've got, again, the parents or the ancestors and the descendants of the repaint boundary all needing to repaint at the same time.

And there, look, it says it.

Okay.

Now no one would write code like this, but this is a perfect example of a perfectly wasteful repaint boundary.

We've got a gesture detector that sets some state, then we have two colored boxes separated by a repaint boundary.

The only problem is both colored boxes depend on this same myColor variable.

So they're definitely repainting at the same time.

So this repaint boundary would be extremely ineffective.

Now, this is a really, really contrived scenario.

But how should you, as a developer, think about repaint boundaries?

Well, it's tricky is the short answer.

But the longer, better answer is if you go into the DevTools and you navigate to a specific repaint boundary,

You will find this often humorously worded diagnosis property that just tells you how good the framework thinks the repaint boundary should be.

And then there's this metrics line above it, which is the percentage of repaints where they didn't both happen at the same time, the ancestors and the descendants.

Other than that, a great rule of thumb is you don't need a repaint boundary.

OK, lastly, what does all this mean for performance profiling?

Well, for most frames in most situations, your frame budget is probably going to look like this.

Assume 16 milliseconds, because that gets you

60 frames per second.

So the UI thread tends to finish very quickly.

Dart is very fast at creating and disposing of lots of classes, widgets, textiles, our own state management classes, like very, very fast at that.

And then it passes the baton to the raster thread.

And this runs on the engine.

This does all the compositing.

This is that scene builder stuff and the execution of the shaders.

And this tends to take a lot longer.

Then if there's any time left, the Dart VM loves to squeeze in a quick garbage collection.

So what this means, if you think about the amount of effort that we all kind of tend to spend on hyper-optimizing a build method, like every single const variable, correct, and all these different little tweaks that we might try to think about, they're impacting these two milliseconds here.

And then think about what happens in a build method.

Let's say you've got 50 const widgets and then one little dude that changes.

Well, what's going to happen after set state is called in that widget?

Well, every single render-- or that's going to lead to some render object saying mark needs paint.

That'll propagate to the entire layer around that render object and any other layer in the layer tree get rebuilt.

Then you have a fresh layer tree that's fed to the scene builder.

The scene builder does a ton of work still, even for the const widgets, to re-evaluate everything, distill that into the display commands and the shaders that need to run.

Then that scene is still fed back into the graphics driver. and all the shaders rerun, and all the shaders produce a pixel buffer, and all those pixel buffers are collapsed down into one final pixel buffer, and all of that work still happens again, even if you're surrounded by const widgets.

So we just don't have to beat ourselves up so much about all that stuff.

OK.

For more info on this, this is a really great talk.

Seven years old, pretty much all still perfectly accurate.

Impeller has changed a little bit of this.

If you watch this talk, which you really should if you found any of this interesting-- and of course, most of you probably didn't-- but the only thing that Impeller changed about this talk is Impeller tries to be so fast that it never does any raster caching.

And this talk still mentions some of the wins that Flutter was gaining at that time from doing raster caching that was efficient in Skia.

Special thanks to these three folks who aren't here and may never see this.

But the two on the left are on the Engine team, and Michael Gotebauer is the TL framework team.

None of this talk could have happened without them.

Their genius is only exceeded by their helpfulness.

OK, I went over time.

There it is, folks.

It took me 37 minutes and 58 seconds to get through, but Flutter does this in only a few milliseconds.

Thanks, everybody.

Thank you so much, Greg.
