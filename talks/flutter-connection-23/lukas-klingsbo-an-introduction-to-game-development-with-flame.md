---
slug: >-
  /talks/flutter-connection-23/lukas-klingsbo-an-introduction-to-game-development-with-flame
date: 2023-06-02T00:00:00.000Z
title: An Introduction to Game Development With Flame
author: Lukas Klingsbo
video: fVEEp1vsakY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/fVEEp1vsakY.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/flutter-connection-23/lukas-klingsbo-an-introduction-to-game-development-with-flame/slides.pdf
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

Last talk.

Can you please just stand up for me?

Everybody?

I can't see you really, but yeah.

OK, and on three, everyone that can do a small jump.

One, two, three, jump.

Awesome. Now maybe you will be able to remember something from my talk to get some blood going.

All right, let's get started, because I heard that Esra really wants her beer.

How many in here have heard about Flame before? Raise your hand.

Quite a lot. And how many have actually used it?

Not as many, that's good, because this is an introductory talk, so for those who have used it, you probably know most of the things in here already.

Yeah, as I said, this is an introduction to game development with Flame, and who am I to hold such an introduction?

I am Lucas, or if you hang out on social media or within the Flame community, people usually

I'm part of the Flame Engine core team and also part of the Bluefire open source collective just like Henan.

And I used to work at Dice before they became part of the evil conglomerate EA.

But I didn't really work with game engines there.

I worked as a backend developer.

And to many people's surprise, I am not a gamer.

And I'm also the organizer of a conference in Stockholm called Flutter and Friends, which

I will say a few more words about in the end.

So enough about me.

What is Flame?

It's like the most popular game engine for Flutter.

And I used to say that it's also pretty much the only game engine for Flutter.

But now there are alternatives popping up, like River, for example, you can use as a game engine.

There is an old one called Sprite Widget, too, but that one isn't really maintained anymore.

And Flame is just a Flutter widget.

I will talk a little bit more about that later.

We have 7,800 stars on GitHub, and that is to compare with Dart that has 9,000 stars on GitHub.

That doesn't mean that we have a lot of stars, but that means that you really should go in and give Dart some stars because they really deserve some more stars for all of their effort.

Yeah, three thousand commits, seven hundred and sixty forks, hundred and sixty contributors and it's been four and a half years now since it was started by a guy called Luan.

And a few days ago, we released version 1.8.

And we're starting the planning phase of version 2.

So people, when I say that, oh, we are making a game engine in Flutter, people are like, why are you making a game engine in Flutter?

It's way too high level.

But for the purposes of our game engine,

Flutter is actually perfect.

You have direct access to the graphical context of the underlying platforms.

And very high and nice rendering performance, and mature ecosystem, and the USP that we get straight out of the box, multi-platform, and you get all the nice debugging tools with that, like Hot Reload and Hot Restart.

So it really is great for our purposes.

So as I said, Flame is just a widget.

So you can put it anywhere within your widget tree.

So your whole app doesn't have to be a Flame game.

You can have maybe a little Easter egg somewhere that it's a Flame game.

Or maybe you want to do a cool animation with Flame.

It doesn't even have to be a game.

And then you just put the game widget somewhere inside of your normal widget tree.

And to get started, this is the base boilerplate code that you need. you create a flame game instance and extend it.

Like, you don't even have to do that nowadays.

You can just throw in children at it, but I won't show that today.

But usually you want to load some assets and things like that.

And those ones you can load in this onload method, which is one of the lifecycle methods that we have.

And meanwhile, you're loading things in here.

You can show a loading screen with the game widget.

That's pretty handy.

And if you don't want to have barely any Flutter at all in your app, this is all you have to do to start your Flame game.

So you just have your Flutter main method, and you start your game directly with the game widget in the root.

So even people that don't know any Flutter, they can jump aboard Flame directly if they want to. but usually we recommend to use some Flutter, too, because it makes your life a lot easier for building menus and stuff like that.

And usually in the Flutter community, not a lot of people have toyed around with game development in these lower levels.

But a lot of game engines, or pretty much every game engine, have something called the game loop.

And the game loop has one update method and one render method.

And the update method, it takes your app from the last state of your frame to what it should be showing on the next state of your frame, on the next frame.

And then you render that with the render method.

And then apart from this, you can also get input from other places.

There are lots of different ways to get input in Flutter.

So Flame has this kind of a game loop.

And we're using that.

We don't only have one update and one render method, as I will show later.

We have something called components in Flame.

So in Flutter, you have the widget tree, right?

And in Flame, you have the component tree.

And within a component, you have one of these update methods and one of the render methods.

And like I said, you do the logic in update and the render code in render.

But a lot of the time, you don't even have to do anything in render because we have lots and lots of components already prebuilt for you that handle the render code for you.

But usually you have to do something in update if you want to have some logic in there.

And this DT that you see here, that you get in, double DT, that stands for delta time.

And that is the time since the last frame was shown.

And depending on the frame rate of the device, this DT will be like, I think Craig said that too, it's like 16 milliseconds for 60 FPS.

And then you have to take that into consideration so that your player doesn't run faster on

170 FPS devices compared to 60 FPS devices, for example.

And just like with widgets, components are highly composable, so you can add as many components as you want to other components.

And they will be like following that, they will be dependent on that component.

So for example, if you imagine a dash that is your player, maybe you want to give that dash a sword or something, then you can add a sword component to dash and then you don't have to care about the placement of that sword when you have initially placed it on dash because it will move around with dash.

And the base class for a lot of our components that are visible on screen is called position component and in the position component we have a position, a size, a scale and an angle.

So something you usually need to show something on the screen.

And all of these are vector 2 and people that haven't done math for a long time, they're like, oh, vector 2, that sounds really scary.

But it's just a tuple with X and Y in it.

So it's really simple.

And these are some of the position components that we offer out of the box.

Like a sprite is for people that are not used to game development, a sprite is basically just an image.

So a sprite component is just an image that you show somewhere on the screen.

And we have the sprite animation component, which is of course like an animation showing on the screen.

And our longest named component so far, the sprite animation group component, which is a set of animations that you can change between the animation depending on some state.

So for example, if you want your dash to be running, it has one state, or if you want it to be showing a jumping animation, it has one state, and so on.

And then we have things like a parallax component if you want to have some depth in your background.

And a text component and shape component.

There's lots and lots of components that are already prebuilt for you.

And it's also pretty easy to build your own components if you want something specific.

So this is what a sprite component would look like.

Like you probably wouldn't want this for your player, for example, because it's just completely static. want it as a stone in your game or something.

You have the sprite animation component and you can have it moving a little bit.

And the sprite animation group component, I spoke about how you can see it moving from one state to the other and you can have as many states as you want.

Very handy.

And yes, Flame is very modular.

So we have the core package in the middle, just called Flame.

And that one you can build a game completely fine with just that one.

But usually you want some audio in your game, for example.

You want some QQ sounds when you're shooting and some whatever sounds you have in your game.

So then we have something called bridge packages.

An example of that is Flame Audio, for example, which bridges to another package on Pub called

Audio Players, which is one of the biggest packages for playing audio in your Flutter app, and Bluefire is also maintaining that one.

Or if you want to have a physics engine, for example, then we have Forge 2D, which is a box 2D fork, so then you can use Flame Forge 2D and you get some custom components for that.

And then we have, I think we have maybe 15 to 20 different virtual libraries that are on Paloma.

So you can check those out if you want to extend the flame.

And some other notable features, we have a camera component and a viewport.

So the viewport can look however you want to.

So maybe you want to play the game from within a submarine.

Maybe you want a circular viewport.

You want to have a multiplayer game on the same computer, and you can have two cameras or two viewports besides each other so you can play at the same time at the same computer.

So that's some really powerful stuff built by a community member called Pasha.

And then we have collision detection, so you can add hitboxes anywhere to your components so you can see where different things collide with it.

And effects, that is kind of our-- it's mostly used for animating and moving around components.

But you can use it for anything that you want to change a component over time.

So that's also a pretty powerful system.

And then we get a lot of gesture and input handling directly from Flutter.

But we are also making it a little bit simpler to use this within Flame.

And if you've heard of sprite batching or how to draw atlases, we have that built into and if you want to draw lots and lots of things on the screen at the same time, then you don't want to draw them once.

You want to draw all of them at once.

And we have particle systems and a physics engine, as I spoke about before.

And we have built in debug mode, which is a real lifesaver.

Any component, you can say debug mode equals to true, and it will show some debug information live on the screen.

Or you can set debug mode true on the game and all of your components will show the debug.

Now hopefully some of you, even though you're craving the beer, it's like, how would I get started to create the game, though?

So a nice thing we have every time anyone makes a new feature in Flame, they also have to create an example on examples.flameengine.org.

In that repository, it's like a little bit like WidgetBook, but very scaled down to where

We show all of the examples for Flim.

You can go in there and just click around to see if there's anything you need.

And then of course we have docs for everything too.

And there are some short tutorials in the docs.

And there are lots and lots of unofficial tutorials on YouTube and on Medium.

But make sure that you don't look at a tutorial that is very old, because then there might have been breaking changes since then.

And if there has been breaking changes, you can look in our change log where there are always migration instructions between versions.

And when you get stuck, we have an awesome Flame community, and if you're hanging out on Stack Overflow, you can just tag your question with Flame and we will answer it, or you can write a GitHub issue, and the Discord here, that is where this great community that I

That's where they hang out.

And we usually have lots of events, like game jams.

And we have something that we call

Flamecon, which is like a little online conference that we have every now and then.

I can really recommend joining that.

Yeah, that's it.

And yeah, as I said earlier, I'm the organizer of Flutter and Friends in Stockholm, is a conference which has a bit more of a social aspect to it.

So check out that site.

Or if you talk to me later, I will give you a code that you can use on the site to get your tickets cheaper.

Yeah.

That's it.

Any questions?

[Applause]

> > I know that.

So we guess you learned a lot while coding Flame.

Which one of those learnings do you think that make you a better Flutter developer overall?

This question, it actually made me a worse developer.

Because in Dart, it's really expensive to create objects.

So a lot of the time, you have to make sure that you reuse objects when you're building a game engine, and the code becomes horribly much worse to look at.

But then, like in my day-to-day coding,

I also think about all these performance implications of creating objects, which can sometimes make my code less readable.

But more performance.

So you have any performance tips for Flame developers?

Don't create new objects within the update or render loop, because when you create things in there, it will create at least 60 new of those objects every second.

And the garbage collector will be very busy.

And then when you have a lot of components, it will be thousands and thousands of objects created every second.

Last January at Flutter Forward, it was announced the support of 3D in Shutter.

How about supporting 3D for Flame?

Yeah, so a lot of people thought that because they showed some 3D on the screen, that meant that they have 3D support in Flash Blaster.

And it's quite far from the truth, to be honest.

But they are working on it.

And we're getting more and more support.

But until we have full support on all platforms, we're just experimenting with it pretty much.

So Impeller is bringing some stuff that we couldn't do before, but we still need a lot more things to get access to more things from the hardware to be able to properly do 3D.

So you're planning on this, but no roadmap to announce.

Yeah, exactly.

I mean, we are in tight collaboration with Google, too.

They ask us what we need.

But it takes a long time to do these things.

It's quite complicated.

Of course.

And maybe our last question about, can you actually use plain Flutter widgets inside a Flame game?

Yes, that's a very, very common question, actually.

So we have these components, as I was speaking about.

And people are trying to add widgets where you add components.

But that's not possible because they work very differently.

But we have a system called overlays where you can put widgets on top of your flame game so you can build a menu or you can have some heads up display somewhere that are built in with normal Flutter widgets.

And so either you use the overlay system directly, you can look that up in the docs, or you use something that we call the router component which can bring up and down overlays for you. All right. All right. Thank you very much. Thank you. Thank you.

And thanks for a great conference. It was so much fun. Thank you. Thank you for being here.

Actually we enjoyed a lot. All talks and yours as well. And thank you for being last. It's not an easy place.
