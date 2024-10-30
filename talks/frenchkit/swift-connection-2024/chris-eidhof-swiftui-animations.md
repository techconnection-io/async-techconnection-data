---
slug: /talks/frenchkit/swift-connection-2024/chris-eidhof-swiftui-animations
date: '2024-09-23'
title: SwiftUI Animations
author:
  - Chris Eidhof
video: CPzf_0tRwcE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/CPzf_0tRwcE.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Chris
I hope everybody's excited after lunch. I hope you didn't eat too much and fall asleep. Let's do animations.

Everything will move on screen, so that should be a lot of fun. When you think about animations, there's so much to talk about and so much I would love to talk about. There's the theory behind animations, there's the design of animations, but today we're going to focus just on the SwiftUI part of animations, and not all of it.

We're going to look at four examples. The first example is going to be a basic animation. We're going to tap a heart and it should fill the stroke for us.

The second example is going to be a little bit more advanced. We're going to do a phase animation, which is sort of more than one thing at a time. It's in phases.

The third animation we'll look at is a key frame animation where we fill and stroke the heart but not at the same time. And the fourth animation will be pretty advanced, I think, is a particle animation where we use canvas and timeline view. And these are increasingly complex, and so if you stop listening after the first animation, you should be okay.

But then you can go back at some point. Let me increase the font size for you a little bit. Okay.

This should be a bit better. Move the simulator over. Okay.

Here we go. So we have a heart. We stroke it with tertiary, align with a five, and it's 200 by 200.

Now we want to animate a red stroke on top of that. So the first thing we'll do is wrap this heart in a Z stack and duplicate it. So we're going to have another heart that's red.

And, of course, it covers the first heart completely. Now we want to animate this. And I want the stroke to sort of fill.

And there's a really useful modifier for this, and it's called trim. And if we say trim to 0.5, it'll show the heart, the red heart, like half stroked, right? So the heart is a shape.

We trim that shape to half of its path, and then we stroke that trimmed shape. If we would change it to 0.75, of course, you see more of the heart. And so this is the value we want to animate.

And we're going to add a tap gesture to our Z stack. And whenever we tap, we want to toggle an is on Boolean, which we still need to define. So we'll do that.

Estate property. And now as the next step, we need to animate this line, right? And so it says 0.75, and that should be a ternary. So if it's on, we want the value to be 1. And if it's off, we want the value to be 0. So we can do a ternary operator.

And now if we tap it, nothing much happens. So the thing you always have to remember when you're doing these kinds of tap gestures and you're dealing with shapes is that only the non-transparent pixels are tappable. So we'll add a content shape.

And now our entire heart is tappable. Okay. So now we have a heart that's tappable, but it's not animating.

And this is a teachable moment, actually. We learned about this yesterday. So it's not animating.

And it's actually really interesting to think about because we are, if we tap it, it's either red or gray. And so what is an animation, right? Well, with computers, an animation is really when we see the values change over time in between that red and gray.

And so another way to put that is we need to interpolate those values, right? So we need to, I don't know, like take one second to grow that trim. And that's what an animation is.

If we see over time the value slowly going from A to B, then we have an animation. And so it's really easy to do this in SwiftUI. And maybe 80% of your animations will be this easy.

You can just add .animation default, value is on. And that says whenever it is on, value changes. I want the change to be animated.

And so now it works. And it's a little tricky to understand why. And what's happening is SwiftUI is taking a snapshot of the view tree before the animation.

Then you have the state change. It applies the state change. And during that state change, we have a .animation modifier which will update the views and animate any of those updates. And I have a little future version of instruments that will help us here. So here we have that same view. And we can look at the view tree here.

So this is the view tree that corresponds to the view we just wrote. We have our stroke animation, our frame modifier, our animation, content shape, and then the two hearts, one with the trim applied. And if we go back in time to the start of the last animation and scroll to the top, we can see that this is on is going to change from true to false.

And it starts updating the view tree. And here we can now see that it starts updating this view. It's going to re-render the body of our content view because the state changed.

So something weird happened here. Thank you for letting me know. No problem.

Let's try it over here. Okay. Thank you. Yes. Okay.

So let's see if we can go back here. Go back to... Oh, yeah.

We need to animate this first. Yes. Okay.

So let's take a step back. We see the view tree here on the right. And the is on is false.

And I'm going to rewind to the start of the last animation. So it's true. It's going to change to false.

And then it's going to start animating those changes. So it's going to go and update our stroke animation. It's then going to update the frame modifier.

And so this update goes all the way down the tree. The little thing you see in between the stroke animation and the frame is the current transaction. And the current transaction is empty.

It starts updating the frame. Nothing changes. It starts updating the tap gesture.

Nothing changed. And it hits the animation. And it now knows previously my value was true.

It's going to be false. And so now all of a sudden, as I update further down the view tree, I have to animate those changes. Right?

And so it starts updating the content shape, the VStack. Nothing changed. Then it hits the first heart.

Nothing changed. And then it hits the trim modifier. And remember that we had the ternary there.

And so now it changes from zero to one. And the trim modifier, and this is the attribute graph here on the right, that now has this animation attached to it. Right?

And so if we go there, we can see that it's going to change from one to zero over .3 seconds. And so as we then animate, it will use this timing curve over here. We previously set default here in this example, it's easing out, to animate in between zero and one.

And so that's what's happening roughly under the hood. And yeah, we can go back in time and look at that and we can really see here if we look at the trim modifier, as we go through this animation, you can see the value changing, the timing curve increasing, and the value will become zero. Okay.

Let's see if we can continue. Yeah. So you can make it slower and then, yeah, that works.

The slowing down of animations is really useful when you're debugging, but you should be aware or should be careful with it, because it can change the behavior when you're replacing animations, the speed modifier. Okay. Next example.

Phase animation. So we have a heart, we have our untapped gesture, we have a state property ready, and we want to do a phase animation. First thing is we can fill it with is on, and so this is not animated, right?

It's just switching between the two values. So we can add an animation and now it will be animated. So that's really easy.

And so the fill is not animated. And lots of things in SwiftUI are animatable, but what we want to do is sort of go from the center of the screen to a heart that jumps out and then goes back, right? And so that's not something you can easily do with the default animations, because the default animations, remember, they take a snapshot before and after and animate in between those two snapshots.

So in other words, they animate from A to B. What we want to do is go from A to B back to A. So the view tree afterwards and before is the same.

And this is where phase animators can come in really handy. They're the simplest way to achieve this. So we can wrap our entire view in a phase animator, and we can see a few parameters here.

The first parameter is the phases. So we have false and true. And we have a trigger.

So the trigger is the easy part. Whenever the is on value changes, the animation runs. The phases, we have an array of two values.

You can put any value you want in there as long as it's equatable. And we receive the current phase in our closure. That's the active parameter there.

What the phase animator will do is when the view is at rest, it will render with the first phase. So in our case, false. Then as the trigger changes, it will add an animation to the second phase using the dot animation or rib animation or something similar.

And then when it hits the final phase, which is in our case the second one, when it hits the final phase, it goes back to the beginning. So in this case, it will animate from false to true back to false. And it will call the closure with every one of those values.

So now if we make it a little bit smaller and add our first scale effect here, we can see if we tap it, it scales up and back down. And so previously before phase animations, these animations were quite hard to do in Swift UI, but now it's really easy like this. And we can make it a little bit smaller.

It's a bit nicer. Maybe add a rotation effect as well. It's a bit much.

Maybe half of that. It's still too much. Maybe half of that.

So this is nicer. And then the final thing we can do is add an offset. So this works really in almost the same way as the other animations that we just saw, except that it is sort of doing a completion handler.

It animates from false to true, and when that completes, it animates from true back to false. And if we had more phases, it would do it multiple times. And you can combine this with the default animation, so you can see that if I tap it, it animates the color of the heart, and at the same time, it starts animating to the true phase and then back to the false phase.

Okay. Sometimes we want more complicated animations than just phase animations, and this is where keyframe animations come into play, and keyframe animations are a different beast. They allow you to do an animation for some value and then maybe halfway through the animation or at any point in time you want, you animate a separate track.

And if you've ever used something like Flash or if you've used a video editor or something like that, you know this, where you have a timeline with multiple tracks. And the big difference here with the regular animations is that we're not animating the views anymore. We're not animating properties of the views.

We're animating a value that we choose, and so we can choose whatever we want that we want to animate, and then SwiftUI will call a closure with that value for us. So how does it look? Well, we want to animate the trim and the fill, but not at the same time, right?

We want to offset these animations in time. And so we could just do it in a naive way. So we can animate the opacity and we can animate the trim and we can add a dot animation, but you'll see that this looks funny, right?

It should really do the stroking and then start filling when the stroking is almost done, and so this just doesn't look right. So we'll remove that animation and wrap our ZStack in a keyframe animator. I'll use zero for the initial value.

We have the same trigger pattern, and we'll have no keyframes for now. This initial value, that's the value we want to animate, and we can choose what we want there. So I put a number in, and there are many ways to do this.

My preferred pattern is to see, okay, I want to animate these two properties, so I'm going to create a struct with those two properties, in this case the opacity and the trim progress. So we'll add a struct value, and it has an opacity and a trim, and this is the thing we're animating. We're not the views anymore, we're now animating this value.

We'll have an initial value where the opacity is 0.1, and an initial value where the opacity is 1, and this corresponds to the off and on state. And now we can use that initial value. So we can use it here as our initial value, and it's behind the simulator, but you can see now that we get this value as the parameter.

And we can replace the is on with our value, and the key thing to remember here with the face animator is as it's making the changes to that value type for us, it's going to call this closure 60 times per second, 120 times per second, whatever your display rate is. And so don't do anything too expensive in there. So we use the value now, and we have no key frames, so we need to add those.

We'll create two tracks, one for the opacity and one for the trim. And for the trim, we use a cubic key frame to the value 1 over two seconds. For the opacity, we just say move to 0.1, which is basically saying stay at 0.1 forever. So now if we tap it, we get a strange behavior. It fills up. I tap it again, nothing happens.

I tap it again, now it animates. I tap it again, nothing happens. And to be honest, I'm not 100% sure how this is supposed to work, but I know how to make it work for me.

The first thing we could do is we could say, okay, we're going to move to 0, and then we're going to animate to 1. So now if we tap it, it always animates from 0 to 1, right? It always fills up this stroke.

We want this to be dependent on whether we're on or off, so we'll add an if condition around this and an else case, and in the else case, we do basically the opposite. We move to 1 and then animate back to 0. And so now we have basically what we had before at the very beginning of the talk, just in a way more complicated way.

So that works, and now we can focus on opacity. So with the opacity, we want to start fading in from 0.1 to 1 towards the end of our stroke, and so the stroke takes two seconds, so we can start maybe after one and a half seconds. There's no way to really say, like, pause for one and a half seconds, so what we're going to do is we're going to say if we're on, we're going to move to 0.1, and then we're going to animate to 0.1. We are already at 0.1. We're going to animate to 0.1 over one and a half seconds, and then finally we will animate to 1. Let me scroll up a bit. Yes. Okay.

So that is the if case. This code doesn't compile like this. In a keyframe track, you always have to have an if and an else, and so in the else case, we're going to say move to 1 and go back, and let's see if this is already the correct preview.

Yes. No, not quite. Okay.

Now we can see it fading in towards the end of the stroke, and both animate out at the same pace. I'll play it again. You can see the stroke happening, and then you can see it fading in, and so keyframes are really useful when you want to have these more complicated animations that don't always happen in parallel, but maybe like offset in time.

Okay. So, now, for the most complicated part, which you might not ever need, but it's still really fun, and it teaches us about how animations actually work under the hood, which is rolling your own animations with timeline view and with canvas. Okay.

We have a heart, and I changed it up a little bit. I didn't want to use my shape now. I have just an image, and that's a symbol, and it displays like this, and we want to emit multiple hearts that sort of float up in space, so the first thing we will do is add a modifier for this.

This is our particle modifier, so this is a regular view modifier with your body, and in the background of our content, we put a canvas. Canvas is a view that lets you do immediate mode drawing, which is a way to really efficiently and quickly draw things, and it's very unlike SwiftUI views where SwiftUI takes care of everything and here you get to do the drawing, and we will need to use our modifier, so we will add our dot modifier here, and then we need to do something with the canvas and actually draw something, and the simplest thing we could do, which is a lot of code, is just to fill up the entire canvas with a colour, so let's do that. We create a rect path, and we fill it up, and it uses the foreground colour, and so then we can see exactly how this canvas fills up behind the heart, and it sort of takes on the size of the heart. The heart reports its size, and the background makes sure that the canvas becomes the size of the heart with that padding.

So, because we want to do particles, we need a bigger canvas, and so we can add a frame where that's 300 by 400, and then that looks much nicer. The next step is that we do not want to fill here. We want actually to draw hearts, and you can put SwiftUI views into your canvas using symbols.

We can add a symbol, a particle symbol, and we just use our content view and tag it, and then we can immediately resolve it inside the drawing closure. So now we have our heart, we resolve it using the tag, we can force unwrap it because we know it's there, and we can draw it. So now we draw our heart at position zero, and what you can see here is that the centre of the heart draws at the origin, which is not really what we wanted, but that's the way it works.

So the centre of the heart is now at zero, zero, that's why it's clipped. Let's remove this filling. We don't need that.

And now we just have our heart there, and it's clipped. So instead of saying at point zero, we can, of course, choose a different CG point so we can draw it at 50-50, and now we can see our entire heart, which is much better. What we want to do instead is, of course, start from the centre, right, or particles should start from the centre.

So canvas is a lot like CG context, if you've ever used that, or something like context in canvas in HTML, in JavaScript. We can translate our canvas, and that's what we're going to do. So we're going to add a translate and translate by half the size, right, half the width and half the height, and now our second heart is drawn at 50-50 from the centre.

And if we would change it back to zero, now it's exactly behind the other heart. Okay. So we can draw stuff, and the cool thing is this drawing call, we can put it in a for loop and draw many copies of our heart in a very efficient way, but we need to animate, and for this, there's the timeline view in SwiftUI, so we can wrap our canvas inside a timeline view, we can set it to dot animation, which means that it's going to call our closure 60 times per second, 120 times per second, however fast we want to, however fast our device animates, and it's sort of in sync with the display refresh rate, right? So if you've used CA display link, this is basically what that is in SwiftUI, and so every single time the system renders a frame, it's going to call that closure, right?

And so, again, be very careful what you put in there. You do not want to do anything expensive in here. And so it runs this closure, and we're not doing anything yet, and our timeline view, it has this timeline context in there, and it basically tells you the current refresh rate of that timeline view, and it tells you the current date.

We want to animate, so we want to say, for example, move by ten points to the right, but of course if we have the current date, we also need to know when our animation started. So we're going to add a state property for that, we're going to say the start time is now, and then in our timeline view, we can compute the elapsed time of the current animation by taking the date from that timeline context and computing the time interval since the start time, so that way we know exactly how long our animation has been running, and if we want to move by ten points per second to the right, we can easily do that now, we can just say our X position is elapsed time times ten, and now you can see it moving to the right by ten points per second, and this is a linear animation, there are no timing curves, there's no easing, it just always moves by ten points to the right.

One of the things that's always really useful when you're trying to build these kinds of animations is to also be able to run the animation again, because now it's gone, and so that's luckily also quite easy by just adding a tap gesture and resetting the start time, and so now it moves by ten points to the right, and if I tap it, it starts at the center again, and if I tap it again, and so on. Okay, let's move the Y position and make sure the heart moves up as well, so that's the same code, right? We now move by minus 30, so we're moving upwards, and you can now imagine that you could basically build any kind of animation you would want in any way you want, it just gets more and more complicated as far as the code goes.

We want our heart to sort of go up, and this sounds like a sine wave, don't be too afraid, so we'll just wrap our X position in a sine wave, and now we can see it going up, right? And we can increase the amplitude to 50, and now it goes up and has a bigger amplitude. These three lines, that's exactly what our particle is, right?

Like we want to have multiple copies of these three lines and have different particles. So to do that, we need to create a particle struct, something went wrong there, we're going to create a particle struct, and we're going to just start with a random amplitude from minus 50 to 50, and then we need to create a state property to hold our particles, so we'll start with no particles, and we need a tap gesture where we create five particles, so this creates five random particles. Now we need to go back to those three lines, wrap them in a for loop, and if we now run it, it looks exactly the same as before.

We're not using the amplitude from a particle, so now there's not one, but five hearts moving up there. So let's use our amplitude. We can change that 30 to p the amplitude.

It's not quite the effect I was hoping for. This looks very, yeah, not random, and it doesn't look like the effect we were going for. So how can we solve this?

And we now need to sort of delay every particle, right? So we want to have maybe a random delay, and you can see that we need to invent basically all of these things ourselves now, right? There's no SwiftUI that's helping us.

So let's add a delay to our particle. We'll add a random delay of two seconds or somewhere in between zero and two seconds, and now we have a random delay, and we can use that, so we can compute the current time for each particle as the elapsed time of the entire animation minus the delay. So that's our time variable, and we can replace those two occurrences of elapsed with time, and so now if we run it, also not quite right.

I don't know if you caught it, but the particles start below the center. So if I tap it, start below the center. That's not what we want.

We want to start at the center. The reason is that if our elapsed time is zero and our delay for a particle is minus two, the time variable here will be minus two. This is why it's sort of below the center.

It overshoots in one direction, and so that's a very easy fix. We can just add a guard statement and say, okay, if the time is less than zero, we continue, and so now we have the effect we were going for. Two more quick additions is to add some fading in, so we could do, for example, compute the opacity as the time divided by three, so now it's actually fading in and fading over.

We want to have one minus time by three, and now it's going to fade out over three seconds, and if we want to increase that to four seconds, that would look like this. So it's very, very manual code, and it gets very complicated as you write more of these things, but it's also doable, at least to write it, not to read it afterwards. So now it fades over four seconds.

That's all I have to say. Thank you, and I'll take your questions.

### Denis
So the first question from the audience, and the main question from the audience is, what is the tool you're using to draw the graph? Xcode, right?

### Chris
It's just SwiftUI, yes.

### Denis
Okay, and do you use it when you're creating a complicated animation? You need to just think about it and using it that way, or is it just a teaching tool?

### Chris
Yeah, yeah. So I also teach workshops. I don't want to take away from John and Greg, but when I teach SwiftUI workshops, I use these tools to teach things, yes.

### Rob
Okay, why do you make the rest of us look bad? No, okay. So it seems when you get up to those timeline views, and they're quite powerful, are there any helpers?

So can I do ease in, ease out at all, or do you have to go to Wikipedia and look up all the formulas?

### Chris
Yeah, so you can, there is a type called unit curve in SwiftUI, and that gives you these easing curves, and you can use that to compute. So I was, for example, computing the capacity by saying one minus time divided by three. So that is a linear animation, right?

So as time progresses, the value gets, well, actually goes down, right, to zero. So if you take that as sort of the progress, and the progress would be between zero and one, you could feed that into one of these unit curves, and then you have that for you. And what's actually really cool is, I didn't have time to explain that, but now I do.

The keyframe animations, you can create a, so I use the keyframe animator, but there's also a type called keyframe timeline, and it just gets a value and keyframes. And you can say, keyframe timeline, what's my value at time 0.2, or 0.21? And so you can combine the timeline view of the canvas and the keyframe timeline to rewrite the code I just did in a much simpler way.

### Denis
Ah, okay, okay. One question we have is like, how do you choose between the with animation wrapper and the animation modifier?

### Chris
Yeah, so we saw that the animation modifier, as we started updating the view tree, at some point it started adding that animation, right, and it started passing it down the view tree. And so if you want to have local animations that are sort of built into your view, you can use the dot animation. The with animation does a similar thing, but at the root of the transaction.

So if you say with animation is on equals true, it will start the update of the view tree from the top, and it receives the animation in the transaction straight away. You can even, so what happens is then the next question maybe, what happens when you combine the two, right? Like you have your transaction, and you do with animation, and it has a very fast animation, and then you have a dot animation that's slow.

Now what happens? So the dot animation will overwrite that faster animation, because it just goes down the view tree, it sees my value changes, I'm going to change the current transaction. And you can also turn that off if you want to in the transaction.

And so to summarize, I would use with animation when I want to control from the outside how things are animated, and if I want to put animations into my component, I would use dot animation.

### Rob
Okay. So you said transaction a couple times. Yes.

And if you're old enough to have worked in core animation, it feels kind of core animation-y. Is, if you've worked in like CA Layer or even DrawRect, the old school DrawRect, I mean, how close is a thing like Canvas to what we're used to?

### Chris
I'm not completely sure. I don't know enough about the internals of core animation, how that works. From what I remember, it's quite different, but it serves a similar purpose, it just has the same name.

I do think that both systems were made by the same person, so there's definitely some overlap there.

### Rob
Can we use, it feels a lot like a DrawRect call, though, inside Canvas. Yes. Can you do most of the things you would think you could do in a DrawRect?

### Chris
Yes, yes. It's very, so the Canvas and the DrawRect are very, very similar, I think. And so the Canvas, you get a context, and then with DrawRect, I guess you get a CG context.

And so, yeah. You have, you cannot pass every single view into a Canvas. You saw me put the symbol into the Canvas and resolve it.

And if it's, I think if I remember, if you have like an AppKit view, for example, or a UIKit view that's not, I don't know, there are some limitations, and then it will just render something very ugly. But you'll find out quickly when you do that.

### Denis
And one more question, maybe. When you work on an animation, it looks great, but when you put it in the end of the user, sometimes they just press the button really quickly, and you're just like, oh, I spent so much time, and it's kind of glitching. Is there a way to have something like reversible and just at some point go back without having that kind of glitch that's like, OK, start from the bottom and animate?

### Chris
Yeah. So there is a few techniques. So I think one of the things that, so I started diving really deep into the animation topic, not just for this talk, but in general.

And so one of the cool things that iOS did, I don't know who remembers it, but there's like the iPhone 10 presentation, and during that WWDC, there's a talk about animations, and they show FaceTime as the example. You know when you have FaceTime on your phone, you have like the four corners where your picture is, and you can swipe it up, and you can swipe it to a different, and you can interrupt that animation, and all of that stuff works magically, right? I think this was UIKit Dynamics.

And so in SwiftUI, it turns out it's quite hard to do it if you're holding it wrong, which I was, and I thought I knew, and so I couldn't get it to work, and I couldn't get it to be interruptible, and it was always glitching a little bit, and at some point I heard that it could be the speed modifier. So what happens is, as you start an animation, and even now as of iOS 17, as you do a gesture, there will be a velocity in the system, right? Like how fast am I dragging?

What's the current velocity? And as you then start an animation from that gesture, as you, for example, let go, the system will pick up the current velocity, and put it into the animation. And if you then, for some other reason, animate to a different part, and you replace that animation that was running and not quite ready, it picks up the velocity of the running animation, and uses that as the initial velocity for the new animation.

And so the thing is, though, not every animation type can merge, and not every curve can merge. And so if you use the default animation everywhere, you're good. Then it works, because that's a spring animation, and they can do that.

But the moment, as I did, when you use .speed, it doesn't work anymore, because it cannot merge those two kinds of animations. And so in the end, when you write the code, and when you have it working, the code is very simple, but it's really easy to make a mistake and not know why.

### Denis
Okay, thank you. Thank you.

### Chris
Yes.