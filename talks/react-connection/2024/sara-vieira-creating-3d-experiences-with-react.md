---
slug: /talks/react-connection/2024/sara-vieira-creating-3d-experiences-with-react
date: '2024-04-22'
title: Creating 3D Experiences with React
author:
  - Sara Vieira
video: frtdTH2d_HY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/frtdTH2d_HY.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
### Sara
I'm here to talk about 3D on the web. So Rachel did useful things during their pandemic. I tried to learn Blender, and I failed miserably.

But now I get to do talks about it. So that's nice. Yes, I'm here to talk about 3D on the web.

And this talk is going to be mostly live coding. There's only three slides. So, yeah.

First thing, I'm going to introduce myself a little bit. This button is not working. So my name is Sara.

I am originally from Portugal. I am a developer relations at a company called Orama. We make search, and it's open source, and it's not related to 3D at all.

And yeah, I like football and bad movies and video games. Specifically old video games, which will come into hand in this. And I've learned to love the pain of doing things in 3D.

So yeah. So first things first. The software I use is Blender.

Blender is free and open source, and it's a 3D software. The reason 3D has a little no one tell me about that. There was a mouse there.

So the reason there's, like, an asterisk there is because Blender does other things. At a time, it was even a game engine. So you can do 2D and video editing and stuff like that.

I would not recommend you do video editing in Blender unless you really like pain. But you can. If that's your cup of tea.

Sure. Okay. Cool.

There's one very important thing that we need to know about Blender that I will get into it when we get into the software. So yeah. That's literally my last slide.

So I'm going to open up Blender, and this is a PS1 game case, clearly. You can see it right there. Right?

Okay. Let me turn on the textures so that it makes more sense. This is a PS1 game case, and this is the thing that we're going to export and use on an app.

The very important thing that you need to know about Blender in order to do some web stuff, it is not specifically about Blender, but it's about the different rendering modes. So there are two main rendering modes in Blender, for example, which are Eevee and Cycle. So Eevee does fake lighting.

Like it kind of approximates where lighting is going to go. And Cycle does ray trace lighting or path trace lighting. So this means when you do ray trace lighting, it means that every single ray of light will be calculated where it hits and where it goes.

And this means for things like this case, which is fake shitty plastic. You can see that in Cycles, which is this one, that kills my computer, you can see way more reflections on it. So this is very important, because the web does not use ray tracing, because ray tracing will kill your computer, everyone's Chrome, your Android phone, it doesn't matter.

There are ways to do it, but it's not good. So most of the lighting you see is faked. It's just an approximation of what the computer thinks the lighting is going to be.

And that is what game engines, most of them also use. When you see lighting in video games, and I mean all video games, not just old video games, like in modern video games too, most of it is fake. They don't know what the fuck they're doing.

And that's why sometimes you get weird glitches in shadows and stuff, it's because all of this is just math. It's not actually calculating the thing. Some Unreal, I'm getting way too deep, no one cares.

Unreal Engine 5 sometimes does it. Okay. There, I said it.

Yeah. So this is the case, and it's very important that there's a couple of things, if you are going to use Blender to export a model that you got from the internet or that you made it yourself, there are a couple of things that you need to know. First of all, select everything.

It is very important. Because if you don't, pain will come. Because then you're like, why does it only have my model here?

And then you have to go back. I mean, select everything you want. Only select the things you want.

And then we can go to file, export, and the main thing to export for the web is gltf. GLB and gltf are both formats that are very compatible with the web. Gltf is basically JSON.

No, it's not basically JSON, it's literally JSON. And GLB is not JSON. It's a binary format.

That's what the B stands for. I just realized that. Okay.

So if we click this, there are a couple of things here that you may want to change. So first of all, you can choose between GLB or gltf separate. So this means that it will give you two files, basically one with the textures and one with the JSON.

There is also a way that apparently they removed in the last version of Blender, which is sad, which was just imagine the most cursed JSON you've ever seen, that. So like you would put the textures as base 64 in a JSON file, and it was disgusting and I loved it. Also very important, there's something in data here that says compression.

Very important for the web. And also you want to include only selected objects. And then after that, you can export it.

You can use GLB, you can use gltf. It doesn't matter. So let's say let's export this.

Nope. No, actually. Do I need to export it?

I'm going to do it either way just to show the next step. Okay. So wait, no, I don't have to.

I don't have to. Just pretend I exported this. And I'm going to close Blender so it doesn't burn my computer.

Cool. This is the texture I used. Okay.

So next step, what I usually do is that I come here to gltf.rs. And basically what you can do here is you can drag and drop a gltf model or GLB and it will give you back React components, which is pretty nifty, you know? I don't know why I said it like that. So I have the file here, and I can go on public, for example, and I have a PSG.GLB, which is around 600 kilobytes. You can definitely make it smaller. I didn't really focus on that here. So you drag it in.

You don't fail at dragging it in. There we go. Then you wait a bit, and it's in 3D on the web.

That's my talk. To be fair, I did make this thing. So that could be my talk.

So basically what this does is that it uses a thing called gltf.gsx that was made by the Pomodoro team, and it creates this React fancy thing. Okay. So let's put this on an app, right?

So first things first, this is the app we have. So the app right now is I have a lot of data. That's why I work at a search company.

Actually the data came before the work at a search company. But this is a list of all the PS1 games that I could find covers for. And basically what you do here is that you can search for a game.

Let's say Tony Hawk, which is always my example, and then it will give you Tony Hawk's Pro Skated with a cover. But wouldn't it be cool, right, if instead of a PNG, or I don't fucking know what that is, instead of a straight up image, we had, like, a 3D thing of the cover. Because we have the model, right?

This could work. Okay. That's what we're going to try and do.

So yeah. These are I think they're about 1,000 games or something. The play button does absolutely nothing.

It just tricks you into thinking it does something. Okay. Cool.

So I have Vite running, and I have this code, which I can copy over. So you literally copy all of this, and you have to paste the PSX.GLB in your public folder in the case of Vite. Depends on what you're using.

Does Vite actually mean quick in French? Thank you. Yes.

To be fair, I lived in Germany. I'm used to this. Okay.

So if you're in Vite, you have to put it in the public folder. It depends on what you're using. But I'm going to guess you're probably going to be using Vite.

So public folder as a PSG.GLB. And now I have a model.jsx here. And right now it just says return null. We're going to paste this in here.

And it's very important, two things, is that you need to install 3 and React 3 Fiber and React 3 Dread. These are three packages that are very important into doing these things. So 3 is the base package that does a lot of these, you know, 3D stuff on the web.

But 3.js mostly is, you know, kind of like the jQuery of it. It's not really what you would want to use vanilla with React. In my opinion, with anything.

But and then there's React 3 Fiber which converts a lot of these three stuff into React components that you can use. React 3 Dread. It's just a beautiful thing that gives you helpers.

That's all it does. It's here to make you happy. That's it.

That's all it does. Cool. So now we have this.

And if we look at the app.js, I have a search. And I have a sidebar. And if something is selected, I open the game.

And the game right now just shows the cover. Right? That's it.

Let's delete this. Let's not talk about my choice of Tailwind. Because that's going to get us into a hole.

I like Tailwind because I'm a bad designer. Okay. So if I go here now and I reload this page, we are most likely going to get an error.

But it depends on what error. We got a syntax error. Because I did not export it as case.

Sorry about that. So we should just render this model. The only thing we did was that we added a� I am sorry about that.

We added a canvas. We added shadows to this canvas. And we just mounted this.

That renders the model. That's all we have right now. And that's beautiful.

Right? That is the most beautiful thing you've ever seen in your life. The background is just the background of the canvas.

That's CSS. It's not JavaScript. I can show you.

But it feels condescending to do that. So that block by client is a completely different thing. It's because of my ad blocker.

So right now, one thing that's very important about 3D in terms of anything, if you do video games, if you do Blender, if you do 3D on the web, 3D doesn't exist unless there's light. If there is not a light in your scene, everything is just black. Because that's the way the world works.

Unless you're a cat. In general, you cannot see in the dark. So that's why this just is a black dot.

So the first thing I'm going to add is some light. So I'm going to close these things so I don't get lost. We have a scene where we can add things, and this is just the actual model that we copied from the internet.

So first thing that I'm going to do, if I do this, can you still see? If I do this? Yes?

Oh, that's even better. So now we can see me screwing up in real time. So first thing I'm going to do is add some light.

And the saddest light you can add is an ambient light. So basically, you can think of an ambient light as imagine if the sun casted in every single direction with the same intensity and did no shadows. You're like, that's not a thing.

It's not. But that's basically an ambient light. So you can increase the intensity or anything, but an ambient light does not produce shadows.

And ambient light will always do like it's just basically imagine it as the sun. So we have some light. And can we get closer to it?

So let me add a orbit controls. And if I add orbit controls, we can do this. And we can see that it does indeed look sad.

There are no reflections, even though we know that this is fake plastic. And to be fair, to start it like this is just kind of sad. So one thing that I'm going to do is add a stage.

That's something that comes from React 3Dray. And it's a helper that helps you. Helper that helps you.

English. A helper that I'm just going to say the same thing because I have no other way of saying it. A helper that helps you like center a model.

So I'm going to come here, delete this ambient light. And around this, I'm going to put a stage, which comes from React 3Dray. I'm going to do this.

And if that one, I do need to oh, no, there's yes. So that looks way better, right? So what this stage does is that it adds some lights, and it centers the model in the middle of the screen.

And that's nice. That's exactly kind of English. Exactly what we want.

So let's do some changes to this. Like, for example, right now, let me push this over here so this moves a little bit. That's beautiful.

So right now, for example, I don't really like the lighting, and there's a whole different types of lighting that we can use, so I'm going to say environment, and one that I like is the forest one. And you can see that that looks nicer. That looks cute.

Crash boy. I've actually never played Crash Bandicoot. I played Spyro, though.

I don't know why I chose Crash Bandicoot for this talk. And let's also move the shadows a little bit lower, because they kind of look like they're on top of it. So that's something you can do by calling the shadows, then passing an object, then passing the position.

Right now, they are constantly at 0, 0, 0. Without this. Reload this thing.

Oh, they are not at 0, 0, 0. That's beautiful. So if I do 1, where are the shadows?

In the shadow realm. We're going to pass false and create our own shadows. That was my intention all along, and I just didn't do it.

Okay. So let's add some contact shadows, do this, and give it a position of 0, okay, minus .2, and 0, and we should have some shadows, unless this thing is not cooperating with me. Something is wrong, and that's not supposed to happen.

Did I type forest wrong? Sometimes I do that. No, I did not.

Shadows false. Okay. So if I remove this, and I remove this, you know what?

We're going to keep it that way. Because I am not sure how this screwed it up, but it did. So yeah, we're going to do that, so that I don't die, and you get to see the end of this talk.

Cool. Okay. So that's cool.

We have crash, but crash is not Disney's Lilo and Stitch, right? Right? Right.

Thank you. Okay. Cool.

I can't see anyone, so I need some, like, feedback. Okay. So we know that the case actually gets a prompt that is the URL.

So if I come here, and I console.log the prompts, and you know what I should also do? No, I already do. That's cool.

Good job, Sarah. I go to the info. We get the cover URL.

Okay. One thing that you should know that pained me to find out is that if you try to do this with anything you find on the internet, cores are a thing when you try to load an image from a fetch request. So I had to download all the images and pull them to my own server.

By my own server, I mean a call fair. I do it doesn't matter. Okay.

You know? Cover. We have a cover.

That's cool. How do we use it as a texture? So first things first, how do we even change a texture?

Not like that. You don't want to do that. We have here the cover image.geometry and materials.cover. So if I create a new material here, this is just going to use 3JS as material. So I say const cover image material equals new if I can type new physical material, mesh physical material. There we go. And now if I say color equals red.

Wow. I think there's coffee inside my it's not good. There we go.

And now if I delete this material, literally just paste it in here, that is not crash. It's also not Disney's Lilo and Stitch, but it's something. So there's a bunch of stuff you can do with this.

You can change the roughness. If I say roughness equals zero, then it's shiny red. If I say metalness equals one, then it's metal red.

You get the drill. That actually looks very sick. Looks like an emo band from the 2000s.

That's not what we want to do, though. What we want to do is basically put this cover, this cover that we get as the background image. So if we think about it, we have to turn this cover into a texture and then apply that texture.

Because the color, if I just do props that case, I think, that clearly did not do anything. It's very confusing when it's actually props that cover. It's very confusing because of the metalness, so I'm going to remove that.

That clearly did not do anything. That is not how I wish it was, but it's not. So we need to get this image and transform it into a texture.

And for that, we have a helper from React 3Dray. So const, I'm just going to call it cover, equals use texture, and this comes again from React 3Dray, and you pass it an image, right? So I'm going to pass it props.cover. And if I console log this cover, you can see that it's a texture. This means absolutely nothing to me, but the part that says texture, I know what that means. So I can try to use it. Okay, so let's try to use it as a map.

So it's not a color. If I try to use it as a color, I actually did not try to use it as a color, so maybe it works. No, it doesn't.

Okay, that's cool. That would have been shameful. If I try to use it as a color, that doesn't work.

What we need to use it as is a map. And if we use it as a map, then it works. That's cool.

Okay, let's put the roughness a little bit up so it's not as shiny. And we got something, right? If I change the game now and put metaglow solid, it works, and I can twist it around and stuff.

I think it's too close, so let's move the camera a little bit back, and you can do that in a stage with adjust camera. The default is 1, so this is what we have. I want like 1.2 or something. 1.3, 4. Yes, there we go. And now you can see that you can actually rotate this, and it looks cool.

Okay, what's the next step here? We shouldn't have to rotate it by hand. We should do some animation so that it does the, you know, the spinny.

You know. You know what I mean. Okay, so first things first, we need to attach something to the group that holds all of these components together.

It's literally called a group. You can think of a group as the same thing of a group in SVGs or just a div. It's just a div, basically, that you can do to like plop things in it.

Say let's create a ref, so const cover equal, I can't call it cover. I can call it cover group, equals use ref, like exactly like that, and then we plop the ref in here, and now we have a ref. That's it.

So what we want to do is we want to want every frame rotated a little bit so that it does a little, you know, the little, again, the spinny. You know what I mean. So use effect.

Wow, I am not good at typing. Okay. Why am I?

It's not a use effect. Ignore everything that I just said. You have to use a use frame.

So use frame comes from React 3 Fiber, and what it does is that it runs something on every frame. So assuming your computer isn't burning, it should be 60 times per second. In this case, it is 60 times per second, and I can actually show you that.

Okay, let me just do this so that no weird stuff happens, and if I come here and I just import some stats from React 3 Dre, we're going to get a little thing here that's 61 frames per second. So this thing will run 60 times per second, and that's actually what we want. We want it to rotate a little bit every time a frame passes.

So from this, we can get the clock, so it's the internal clock, and from the internal clock, we can get how much time has passed. So if I console.log clock console.log. Does this happen to other people? It's so annoying.

I'm not trying to be like, see? I'm also bad. No, it just keeps happening to me, and it's really annoying.

Console.log clock.getElapsedTime. If I do this, you can see that I get the elapsed time that has been in seconds since this thing started running. So that's cool. That's kind of what we want, because if we use something — let me just remove this before it goes insane.

If we use something like this, we can do a cute little normal spinny. So we can use the rotation. So if I do rotation.

Yes, I just do just rotation. That current, that rotation. So the next thing is that we need to know which rotation it is, and so Z is the one that does this, X is the one that does this, and Y is this.

So the one we want is this one, right? We want to rotate it like this, so we want the X. Actually, the Z is different in Blender and in every single thing you're going to use, but in the web, the Z is the one that hits you in the face.

Okay, so that equals clock.elapsedTime. And as I said, that is not the X. The X is wrong. That's the X, because it's the one that goes like this.

I said it right. I was like, this is the one that goes like this. That's the one we want to rotate, and no one corrected me.

Okay, and it's the Y. That's what I want. There we go.

Let's reload the page. And there we go. I think that's a little too fast, so let me just divide this by, like, two or something.

And that's nice. Okay, cool. So we got that.

There are two last things that I want to do, because I have no idea how long I've been on stage, and I want to do it for the vibes. So one thing is, no goddamn PS1 game is this smooth, right? Let's be honest.

So I added this component called an FPS limiter, and I'm going to add this FPS limiter to this. So FPS, what is it called? Components FPS limit.

Okay. FPS limit. I'm going to close this, and I'm going to import it.

I tried to not use TypeScript to be easier, and it was just so much harder. It's just, like, I haven't imported things manually, you know, since the before times. FPS limit.

There we go. And this absolutely does nothing now, so I'm going to put up the stats so that ... There we go.

The stats come up. Nope. Reload, maybe?

Maybe we have stats now. No, we have an error instead of stats. FPS limit does not exist.

What do you mean? What are you talking about? Rename, copy, rename, paste.

Export function, FPS limiter. Okay, of course, Sarah. What an idiot.

Obviously. There we go. So now if I reload this page, we have the FPS there, which is 201 frames.

We do not want this. We want, like, 10. So I'm going to pass it a FPS of 10, and look at that.

That's so janky, and I love it so much. It brings me back to my childhood. It's so janky.

Okay, that's cool. So now it runs very terribly, which is exactly what we wanted in this case. The other thing that I want to show you real fast is something you can do with some post-processing effects.

So you can ... There is something called React post-processing, and you can add something called the effects composer, which comes from React 3 post-processing. And with this effects composer, you can add several things.

Like, I can add a vignette, for example. And again, I'm not saying that this ... I don't know what the thing is in it.

But you can add a ... Oh, no, there is some vignette. It's not good, though.

But one thing that you can add is a pixel effect, and that's the one we want. So if I say, pixelation, and I say, okay, I want the granularity to be one, just so we can test it. That looks terrible, and I'm into it.

So what if I do five? Yes. That's juicy.

You know, fucked up my shadows, but it's juicy. Let's try to fix the shadows real fast, because it really bothers me when shadows look like this. Let me add a contact shadows, and put here, shadows false.

Shadows, and pass it as false. And now we have absolutely no shadows. That's cool.

Opacity, one. And let me look at my cheats. There is something here that I'm missing.

Nope. Actually, there is not. Opacity, one, position.

I can usually type faster, but today ... Oh, there we go. 0.2. Nope. 0.6. Yes. And the opacity at one is terrible. Let's do 0.4. Yes. Yes. That looks good. I mean, good is subjective.

But that fits what we want, right? Like, that fits the idea of a PS1 game. So let's see if it actually works, and switch to Metal Gear Solid, and it does.

We have like a cool 3D showing of every case that PS1 has to ... not all of them, but you know, most of them. So let's do Tony Hawk's again.

Tony Hawk's Pro Skater. And will you look at that? That's my boy, Tony.

Okay, let's do Spyro, just because I feel like ... Look at that. That's my boy, Spyro.

That's what I call everyone, apparently, now. Yeah, that's all I have for you. I hope you enjoyed this train wreck of a talk.

And yeah, thank you so much. If you want to follow me on Twitter, I will not call it anything else. You can at NikitaFTW.

And if you're wondering why Nikita, it's exactly why you think it is. My parents wanted to call me that. So thank you, friends.

Thank you so much. Okay, yes, 2Ks, and you can find this code at GitHub, at that URL, and yeah, thank you so much, and I realize that I actually cannot leave the stage, so this is actually kind of awkward now.

### Christophe
Thank you, Sarah. Who liked that? 3D, that's what we do every day, right?

Can we sit in the middle?

### Sara
Can I sit in the middle? Do you want to sit in the middle? No.

Oh, yeah, no, there's an X there.

### Christophe
Okay. You grab the mic. Thank you for that.

We're going to try and have just a couple questions in order to less delay your intake of calories, which is scheduled a bit further in the day. Do you have good questions in Slido?

### Romain
Not really. I think your talk was perfect, so ...

### Christophe
I don't think that's my ... Yeah, everybody was like, so when is the shadow coming?

### Sara
What the fuck is she talking about?

### Christophe
So anyway, what I was wondering about is like, okay, so yeah, COVID and everything, and trying to find a reason to grab the keyboard, but what got you interested in 3D specifically?

### Sara
Honestly, that's a very good question. So my dad, when I was a kid, used to do 3D renderings, but not cool renderings. He used to do buildings and shit.

So he used 3DS Max, and I don't know. I started seeing a lot of stuff about Blender and how it was easy to get started. That was a lie.

Blender is not easy to get started with. So I don't know. I think I've always also wanted to make games, so it felt like I should learn Blender, and now that I have the basics of Blender, I still do not make games.

So to answer your question, I like pain.

### Christophe
All right.

### Sara
Masochistic.js. Yes, that's why my keyboard is in Portuguese.

### Christophe
Oh, there you go. Well, this is a French audience, so we know what it is to hit three keys to do a curly brace. I have the three keys.

Especially on Mac, right? It's a choice. Like there's a hidden pipe in there somewhere, and at some point, your muscle memory ...

### Sara
Yeah, I can't change to American. I don't know why.

### Romain
For sure. So I like 3D, too, but I'm really bad at it.

### Sara
Same.

### Romain
But maybe I like pain less than you.

### Sara
That's fair.

### Romain
What kind of advice can you give me to start making 3D on web?

### Sara
First of all, there's a lot of free models online. Like if you go on things like Sketchfab and BlendSwap, BlendSwap has a lot of actual CC0 models. There is also this Dutch guy called Kenny that makes a lot of models that are completely free and CC0 for anyone to use.

So if you want to do Blender ... If you want to do Blender, sorry, if you want to do web stuff but you don't really want to do 3D in Blender or anything, there are many, many models that you can use. A lot of the stuff that I've done over the years in 3D has not used models that I've made.

So you just sometimes have to credit them, sometimes you don't. But yeah, that's a good way to get started. If you actually want to try and do some Blender, just go on YouTube and type Blender Donut, and there's this one Australian guy that does a donut in Blender for like 20 hours, and it's the most absurd shit that you're ever going to see, but you'll learn all of Blender.

So you have these, I would say, these two options. Sketchfab is a really good resource, by the way.

### Christophe
I had not seen the donut as a comprehensive feature set.

### Sara
It is absurdly comprehensive. It's absurd.

### Christophe
But it's going to be the best-looking donut.

### Sara
It is the best-looking donut you will ever see in your life. You also learn how to make the sprinkles, and you randomly generate the sprinkles, because Blender now has geometry nodes, which is something that you're like ... It's kind of like coding.

You can also code in Blender. It's Python. So there's so much in there.

There's so much. It's beautiful.

### Christophe
Okay. Okay, so just one more way of being creative with React, and we're going to have a talk later today by Mael Nisson about other ways to use React in areas you wouldn't think of. Thank you very much, Sarah.

### Sara
You're very welcome.

### Christophe
Feel free to talk to Sarah outside of the talk. She has plenty of great anecdotes for you.

### Sara
Ask me about the Berlin airport.

### Christophe
It's bad.

### Sara
I can leave now, right? Okay, thank you.

### Christophe
You are free to leave.

### Sara
Thank you, Sarah. Thank you.