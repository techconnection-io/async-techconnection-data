---
slug: >-
  /talks/flutter-connection/2024/maxime-rougieux-thomas-coumau-animations-vs-delivery-do-you-really-have-to-choose
date: '2024-04-24'
title: 'Animations VS Delivery: Do you Really Have to Choose?'
author:
  - Maxime Rougieux
  - Thomas Coumau
video: GkF-LO2CiL4
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/GkF-LO2CiL4.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: '2024'
allow_ads: false
---
### Thomas
We're going to talk about animation versus delivery, and do we really have to choose between those two? I am Thomas, a lead developer at BAM, and you are?

### Maxime
Yeah, I'm Maxime, I'm a tech lead at BAM too, and one thing that is very much important and the reason why we wanted to do this talk is that we actually love animations. And there's been a lot of animation talks in the past, and there's one reason we wanted to do another one is that we realized that we are not using them a lot in our application, even with the fact that we love them. So to understand that, let's have a look at what a classic feature delivery flow looks like.

Okay, it's very simplified, but you have product needs that comes from somewhere, then you have a design phase where you have some mockups, then us tech arrives and do some technical conceptions, then we develop it in the app. For the purpose of this talk, we're going to assume that those tasks are done by different teams or at least different people, which is usually the case, but sometimes you have product designers also. Let's say these are different teams, okay?

So now let's have a look at what is the classic delivery flow for an animation.

### Thomas
Yeah, so because we looked at our delivery flow for an animation, and we want to match it to the feature flow, so it will be easier to introduce in our apps. And the first flux we actually encounter is the fancy dev flux. Why is that?

It's because you're making your application in the dark and you said, oh, this animation could fit there. And you put it in your app, it's in production and nobody on your team knows it, but it's there. So let's go for it.

The other flux we encounter is the current flux. It's the, I'd like to speak to the designer, please, because actually you make the same animation, but you're thinking, is it beautiful? Should I ask my designer for it?

And you go for a designer and your designer is a really good designer and tell you, yes, it's beautiful. Make it in your app into production. Yeah, it's still better, but not the one we want.

But because the one we want is the God flux, because I believe it exists really, but I never really encountered it for now. But it's the product who said, yeah, I want an animation because it really could fit our products and we really need this. And they said, great, let's make it and easy.

We can make it easy and boom into production. So here are the different flow of animations we encountered during our lifetime at BAM.

### Maxime
Yeah. And yeah, so what's broken?

### Thomas
What's broken in this flux? Why can't we achieve the God flux? The first time I arrived at BAM and I tried to make animation, one of my mentors told me animation, it's easy.

You just have to, and then a bunch of others still don't understand to these days. So I understood that I didn't know how to make animations.

### Maxime
Okay. And so what do you do when you don't know something? You engage practice mode.

So that's what we did. We introduced a thing that we called Flutter UI Dodgers. Easy to understand.

It's a 45-weekly meeting where we take an animation that we found on internet, like on Twitter, Dribbble or any equivalent website. And then we split into multiple teams and we try to do it as fast as possible. There's plenty of animations that exist.

So we did a lot of them. Those are some examples of what we did. And so we wanted to show you very quickly a few examples of what we discovered while doing so.

So the first animation that is very easy to do and that you should go to when you want to do animation in Flutter is implicit animations. So basically, it's really simple. You all know the container widget, for example, there's plenty of them.

But there is an animating counterpart to a lot of widgets, for example, container. And so what you have to do is just use variables for your inputs to the container. And then you just replace your container with an enemy container.

You give it a duration and a curve. And then you could set states. And voila.

It works. It's very easy. It's magic.

And it's the easiest way to do animations. But sometimes you need to do some things a bit more complicated.

### Thomas
Because we love animation, but we also love skateboards. So what if I want to actually make a skateboard animation who can do flips, like front flips, back flips, any flips? Then my animated container wouldn't be enough.

So that's why we get introduced to animation controller. The first thing you want to do when adding an animation controller is to actually add a controller and also provide an extension with a single tickle provider state mixin. So this enables your widgets to rebuild on every tick of the clock.

Don't forget to dispose your controller, otherwise you would have some performance issue in your app, and we don't want this. Then you just have to add an animated builder to pass the value of your controller. And boom, that's done.

Not really. Because if you only do this, it would not get animated. You have to add some control over your animation.

So for example, a button who can just launch your animation on reverse, repeat, or just forward, or even pause it, if you want.

### Maxime
All right. That's already some of them. Yeah, so a bit more complex, of course, than the PC animation.

That's some of them, but there's a lot of ways to animate. We won't have time to go through all of them. But basically, we have already come a long way with Flutter UI Dodgers.

And so we made it. We know now enough to start animating with real-life scenarios. So yeah, some celebrations in order.

And so now the easy part is just to go back to our product and our designers and say, hey, we know how to do animations, so we can do it, right? Let's do some animations. And this is the response for our product.

Yeah, animations takes time. It brings no value. We won't do it, of course.

Ah, yeah. OK. So what do we do now?

This is the reality checkbox, as we call it. Basically, it's our product saying to us, yeah, stop screwing around. We've got work to do.

And yeah, let's go back to developing some real features. OK, let's have a quick look at this sentence and to understand what the actual problem is. There's actually two there.

One that it takes time, and the second one is that it brings no value. For the first one, I mean, everything takes time, right? So it's not really a matter.

And now we know how to estimate how much time animation takes because we've trained. We've done some dojo. So we know that in pixel animations, it takes between 10 and 30 minutes, and animation controller is harder.

So it's OK. This is done. OK.

The actual trickier problem is it brings no value because it's kind of beyond our tech scope to kind of know, even if we have intuitions about it, what brings and what doesn't bring value in an application. And so to help with that, we have to go to our allies, which, of course, there will be our designers, right? So let's ask our designers what they do about this.

### Thomas
So when we asked our designers, they told us, like, you just have to reflect on how do you judge that a feature is valuable in your app? And we have a framework which is called the minimum viable product, which is based on three different points, the viability of the feature, the desirability of the feature, and then the feasibility of the feature. And this is our expectation of this minimal viable product.

Everything is round, square, and everything is beautiful. But in reality, this is not what we really see. The features are really more delivery-oriented and the viability becomes a business viability only.

And we are not on what the user desires, but what is the minimum that is usable for the user. And here we don't see, like, any room for putting animation into it. So we reflected into another way of doing stuff.

And we arrived at the minimum viable product, which is based on four different points. The first two points are about pragmatism, how to add values that can be a business value or feasibility of the product, like to reflect on this pragmatism part. And then we want to add commitment of our users.

And so we are based on still the desirability, so what the user desires, but also the lovability, what will they love, which is kind of different. And to see the difference, we have this example. So if any of you took the plane to Paris, shame on you for the ecology.

No, I'm joking, obviously. But if you get put between those two planes, if we told you the plane on the right doesn't have 18 seats, but the plane on the left has, you would still choose to take the plane on the right, even if it has less features, but is more lovable.

### Maxime
Right, so a bit quick there, kind of shortcut, but let's say that all that we said convinces our product that animations are good. Actually, it's a very good way of convincing them. And then the flux is repaired again, right?

Yeah, so it's a bit of a lie, obviously. The flux that we just presented is not the actual one, the current one that we are using right now. The one we are implementing right now is more like something we call fancy designer flux.

Basically, the design team is now convinced, thanks to the MLP, that it's important to do animation, but the product, they still don't really understand that. But still, we are doing some animations now. Just, it's more like something like Rives, I'm sure you've heard about Rives, which is a way of doing animations with assets, a bit like Lottie did in the time.

I mean, it still existed. And so, this is now the flux that we need to build on, right? And so, we went from a broken flux, which we presented earlier, to one we can build on.

Now, we have to really focus, and this is our focus for the next month and probably a year or so, to try to collaborate more with our designers to help them know what animations we can do, what is easy to do, what is harder to do, and yeah, and that's how we build some awesome products. So, yeah, I think this is really cool. Yeah, that was very fast, actually.

Thank you, thank you. Thanks a lot. All right.

### Thomas E.
I think we can do the Q&A here. Thank you a lot for your talk.

### Simone
I have a very technical question for you. How does it feel, you know, to have a very relaxing Tuesday and going home and say, okay, I'm going to take a shower, watch a Netflix movie, and then being told by Guillaume, oh, you should be on stage tomorrow morning, like be the second speaker of the conference.

### Maxime
It's your duty, right? First, we hesitated, but we said, let's go for it. We had already given this talk before, the only constraint was the time slot.

I think we kind of made it.

### Simone
Yeah, yeah, definitely, definitely. So, let's start with the questions from the audience. Like, animations are hard to communicate about, of course, because it's not as easy as static design.

How can you improve, how can we improve sharing and talking about it without too much design effort?

### Thomas
Actually, we are putting in place, we are enhancing the dojos we talked about. Now, we are based on different animation or screens our designer gave us. And we try to implement the screen, add animation, give some feedbacks, say, okay, this took this much time.

It's too hard, so we just will remove it. Or this is good, and it's really easy, so you can pick more of this animation, it's a quick win. And so, we try to change our formats to this format, so we can have more feedbacks between both teams.

### Maxime
Yeah, because we are the best persons to know how much time animation can take. We are not the best persons to know what animations to do, because we are not really designers. And so, we have to, it's a collaboration.

You have to tell your designers, oh, this is easy, this is hard. They have to, okay, try to do this, try to do this. So, this is a collaboration that teaches us all.

### Thomas
Still in development. Yeah.

### Thomas E.
We have also a question about performances with Flutter animation. Do you see some performances issues? And if so, how do you make the choice between a lot of animations and a good performance?

### Maxime
So, as you may know, Flutter is a very good framework for performance. Still, there is some issue. It's a really hard question, because there's plenty of animation types.

The easy answer and the only one that fits, I think, is that if performances are an issue for your product, you should definitely measure it. And there is no, like, the real answer to that.

### Thomas
For me, the only thing is just, animation is just about three builds on the ticker of the clock. So, be careful of what you rebuild on every animation, because it could cause some issues of performance, obviously. And then, just to add, I think it's SNCF and Connect who told us at conferences that they were releasing a package to understand the performance of your devices.

So, you can just judge based on the device if you want to put this animation or not.

### Maxime
And you can use Flashlight, of course.

### Simone
Always. How would you... So, this is hard.

How would you unit test animations? That's a hard one.

### Maxime
Yeah, actually, we don't. Yeah, easy answer. I think the tricky part about animations, of course, is that it moves.

And most of our tests for UIs are static tests, like golden testing, for example. So, if you really want to test animation, I mean, you can take multiple goldens, but this is not something I would, yeah. I think taking one golden and seeing that the animation exists and is in any state, I mean, maybe it's enough to prove that, yeah, it's there.

So, I guess this is already something.

### Thomas E.
We have one question about the FlutterAnimate package. And how do you see the abstraction above all the Flutter animations basics that it gives you? Is it a good thing?

I think the question is, is it a good thing? Because it's a lot of abstraction.

### Thomas
I think it's a good thing. On one dojo, we tricked our different developers to tell them, do this animation in less than 15 minutes. And nobody could do it, even the senior developers.

And we told them, just use FlutterAnimate. And in three minutes, even the junior ones did the animation. So, I think if you want to add some value quickly and prove your products, that you can add animation to your app.

And also, we don't encounter any performance issues with it. So, I think it's a good thing to add. But if you want more control on your animation, just do the animation controller and use custom painters.

### Simone
Since you're an agency, Edmem, do you see value, at least, do you see how you could do to maybe share pre-developed animations across multiple projects or across different teams?

### Maxime
Yeah, there's not really an animation that fits every product. There's concepts that you can reapply. Like, for example, I'm sure you all know hero animations.

If you don't, you really should give it a look, because it's pretty cool. Which makes things move between navigation. I think that, yeah, mostly it's a reusing concept.

That's also why we do some dodges, because we know that it's the concept that matters and not really the animation itself, because it's really based on what the product wants.

### Simone
All right. Thank you very much. Thank you.

Thank you.