---
slug: /talks/frenchkit/swift-connection-2024/lena-stoxen-everythings-cooler-in-space
date: '2024-09-23'
title: Everything's Cooler in Space
author:
  - Lena Stöxen
video: vn6TQvOdSQY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/vn6TQvOdSQY.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Lena
Hi, it's so nice to be on stage here today. I'm really nervous, but we'll see how this works out. This talk was quite long, but I cut some slides, so I'm thinking we're good.

Anyway, my title is Everything's Cooler in Space, and as I was later told is that a lot of people now assume that it is about space, space. I meant like personal space and like spatial computing, so it's not about space, space. I'm sorry to disappoint anyone here.

With that, let's get into what I'm talking about today. So I want to talk about first who am I and what do I want, and then we're going to look at augmented reality on different devices, for instance, the Apple Pro, the Apple iPad versus the Apple Vision Pro. Then we're going to look at AR anchors versus anchors, 3D modelling, ECS, and then some closing arguments.

So we have a lot to do. So first of all, who am I? So my name is Lena Matthäus-Stöcksen.

I live near Hanover in Germany. I'm a student at Volkswagen Commercial Vehicles, and by now I've won the Swift student challenge three times. I have my own website.

Thank you. I have my own website because I felt I'm a web developer. I can make my own website.

That's not that difficult. Under fancygoose.dev, and I have my own app called the Assembler. There is a QR code in case you want to download that.

If you don't know what Volkswagen Commercial Vehicles does, we do that car, for instance. I also like sushi, and I like dogs and birds. And that thing there, that's when you spend an hour calibrating the motion cap sensors, but then you don't calibrate it against the world origin, and that's when you end up looking like that.

So let's get into what do I want. So for the Swift student challenge this year, I came up with the idea of this app. Does anyone here know the movie Inside Out with the little spheres and the little humans inside your head?

I thought it would be cool to have something like that with your own memories, like your friendship memories that you made with your friends. So I decided to create this app. I made some spheres because I'm not good at 3D modelling, and a cube that rotates around them when you select them.

You can see some information up in the corner. And these spheres are like anchored on real-world planes, so like a table, a chair, or a floor. To get into some of the terms here, we have interaction, which is an orange, yellowy-ish here, we have the virtual objects in green, we have anchors, which are like digital representation of real-world objects in blue, and we have the real world in the really dark blue.

So what I want to do is this app already runs on my iPad, as you've seen, but I have ambitions for this. I want this to run on a Vision Pro. The thing is I don't have a Vision Pro, so it needs to also still run on my iPad, and I want to test it on my iPad, and because I'm a bit insane, delulu, as they might say, I want to have this as one codebase where I also do not need to change anything about my existing codebase.

It's basically a cross-platform dream I'm having here. So I'm thinking it's augmented reality. It's all augmented reality.

That's all the same, isn't it? We have this on iPad and that on Vision Pro, and that doesn't look too different, right? So I'm thinking this should be really easy.

Nothing to do should work out of the box. So I copy all of my files into Xcode because I created the original apps and Swift Playgrounds on my iPad. I copy it into Xcode, I click run, and it works, and then I click I want to add the Vision Pro on targets, and then it doesn't run any more, and now it doesn't build any more, and there is a lot of errors, and Xcode is screaming in pain, and now I'm thinking, well, what if this isn't easy?

And because of that, I'm looking more into what is the iPad versus the Apple Vision Pro. I use AVP and iPad as shorthands here. iPad is really any iOS device, whilst the AVP is the Apple Vision Pro.

You might know that. So basically augmented reality is very different on both of those devices. So I made a list with some concepts.

So basically on my iPad, I use UIKit. It's a UIKit app because I thought that's easier to make. You use, you ask for a camera permission to figure out whether the user will let you use augmented reality, then you instantiate an AR view, or I'm doing that in a UI view controller, and you're using ARKit sessions to find anchors in the real world, like find real world objects and planes, and I'm using RealityKit to make my 3D models.

And on Apple Vision Pro, it's a bit different. Basically what you would do there is you would have a Swift UI app, and you would not need camera permission because you can't get access to the camera if you're not in an enterprise development. So that's why you there only need tracking permission to find the anchors.

Also, you're using a reality view and not an AR view, and you're using ARKit session and providers here for discovering real world objects, but you're still using RealityKit for the models. So basically what I need to do to make this cross-platform is all of these need to line up and match. So first of all, we're getting rid of UIKit.

I think that's easy, that's why we're just doing this, we're just getting rid of it, changing it to Swift UI, easy, done. Next we have the camera permission. That's just an info.plist file that we need to adjust, and easy, done. Next, we're running into an issue because I still use a UI hosting controller to use the AR view from UIKit, and on the Vision Pro, I use Swift UI and RealityKit's reality view. So currently, I'm using this, a UI view controller representable. I don't like using this.

Why? It's a feelings-based thing. I just do not like it.

So I want to change over to reality view, because since iOS 18, as Apple has told us in .24, they said, oh, this is an iOS 18, an iPadOS 18. So that's great. We've got this thing checked.

Now to my thought about I don't want to change so much code. This is what my code looked like before. This is all the things I'm deleting.

This is all the things I'm adding. So I think I'm really on target with not changing a lot of my code here. It's working out of the box really great.

So next we have to look at anchoring, because that's one of the issues that we're running into here. The moment we start to remove UIKit and ARKit, we have the feeling of, but, like, what about the real-world objects? So we're going to look at anchors versus AR anchors.

And you might think that sounds kind of similar, but it's not. We have anchors on Vision Pro, which are only on Vision Pro and not on iPad, as you might see, and on iPad, we use everything that has an AR prefix. So we have AR anchors, AR plane anchors, AR world anchors, whilst on Vision Pro, it's anchor, world anchor, plane anchor.

So it's different. And as you might expect, these are not compatible at all. And something that I wrote in my CFP said something about, at dubdub, Apple released the unification of RealityKit and ARKit, and I might have said that, but I might have not read correctly what they wrote.

What they wrote was we're uniting RealityKit, not we're uniting RealityKit and ARKit. That is something distinctly different here that we need to keep track of. So basically, this is, by the way, it's a feelings-based chart again.

Basically, we have iPad and we have Apple Vision Pro, and ARKit is very different on both of them and not compatible with itself. And we have RealityKit in the middle, which is unified between both platforms, so you can share the code you've written for that. Something that I want to go to, what I've also been told is where the direction is kind of going is this, where we have ARKit and RealityKit unified on both devices.

Sadly, that's not the case currently, and we are remaining stuck with this version, which is kind of sad, because now we only have two options. Basically, we use a different code for anchoring and then use like a hashtag if to figure out whether this will compile on an iPad or whether it will not compile. And I'm not a big fan of that, but I've seen it in a lot of sample codes, so this might be the best way to go.

Or other option is we're using RealityKit's anchor entities, because as I said, RealityKit is unified between the devices, so their anchor entities run on both devices. With that, we can anchor things. But why is that not the option that I would choose?

Basically, again, feelings-based charts. We have AR anchors and anchors from ARKit. They are like in an async stream handed to you as you discover them, as the user like moves the device or moves their head around the world.

And you get a classification as tables or walls, chairs, things like that. ARKit is like offering you quite a lot of information about it. The tracking with them is really good, and they get updated continuously as the user moves around and there's more information available.

I really like using them. The thing is, they're not testable without a physical device, so you can only test them if you have a Vision Pro, and that's where we're back at my issue. I don't have a Vision Pro.

I only have an iPad, so that's why I also can't use them, apart from the fact that they're not like interoperable and I need to write different code. That's why we might use anchor entities. The thing is, anchor entities, their placement is kind of random, and I've been told by an engineer that they're just not as good, and which is also what I feel, because has any one of you seen the simulator for Vision Pro?

They have like a coffee table, and then there's another like two-story shelf, and then there's a TV on top of there, and for some reason, not like a good framework, it would choose the coffee table as the first anchor. No, if you ask it for a plane anchor, it will give you a plane anchor on the two-story shelf on the bottom shelf, so you have to zoom in every time. You only like using them.

The tracking on them is quite okay. I just do not like using them. But the nice thing is they're testable in the Vision Pro simulator, and so they are actually quite a good option.

They're just, again, not as detailed. You don't have the classification. But they are an option.

So I'm going to list them here as this is what you can do. Next, we will have to look at our 3D models, because, basically, when you do 3D models, you have multiple options here. Either you can import models from somewhere else, like a 3D modelling software, or a library, or any USDZ file you can create, or you can create something yourself in code with RealityKit.

What you would basically do is you would use a mesh and a material and a model entity. The model entity takes a mesh and a material and an array of materials, and, with that, you can build your own spheres. This one, for instance, is an orange sphere.

And something that I came across when I looked at this was, why is that called a model entity? And I said anchor entities. Are anchor entities different from model entities, and what does that mean?

So that's why I came across ECS. And ECS stands for Entity Component System. Now you might realise something.

I'm a genius. That's just like my title! I know.

It's an awesome title. I've put a lot of thought into this. Apparently, more thought went into the title than in reading the full announcement for RealityKit, but, yeah, maybe.

So let's look at what is an entity. Basically, everything's an entity. So we have model entities for our model content, and we have anchor entities for representation of 3D objects in the real world.

And then there is also entities. So, entities are basically hulls. So it's a bit like an instance of an empty class.

You just have a hull that's living somewhere, and you can do things with it. But how do you do, for instance, properties? For that, you would fill them with components.

So you have an entity, and you can create a component and set a component to it, and then the component has all of the properties that you would need. So you can have a component that has properties, like I have a rotation component that I created that has a state, but it doesn't have to have them. They can also be empty.

And basically what you do is you set components onto the entity, and you can only ever set one because they are like the holder of states, so you can't have multiple, because, for instance, if you have two model components, which of the models do you want? So that's why you can only have one. And if you add another one, and there's already an existing one, the existing one will be overwritten by the new one.

For components, I said you can create your own ones. If you don't want to create your own ones, you don't need to. There's a lot of components already there.

So there's, for instance, model components, physics components, billboard components, accessibility or hover effect or point light components. You can also make your custom ones, but as I said, there's a lot of standard ones, like a lot, a lot of them, and that is because I said that entities are everything, which also means for the components, entities can be anything. So our entities can be something like an anchor or a model, or they can be lights, audio that's playing, or they can be a camera, and all of that is what you create by adding components to them.

And to be back at all, what is an anchor and a model and an entity? Basically, entity is like the base, and an anchor entity just guarantees that there will be an anchoring component on this, on your entity. And a model component guarantees some things you need for 3D modelling, like a model component or a collision component, physics body, things like that, all the fun things you need.

And all of entities have transform components because you need some place to have them. They do need a 3D place and space, and they have a synchronisation component which allows for some animations and stuff. So that's why all of them have them.

So as I mentioned, there are some components, and we're going to look a bit closer at one of them. Billboard components. So a billboard component is, as it reads here, a component that orients an entity instance so that it continuously points towards the active camera.

Basically, that looks a bit like this. They will always face you, and you can't walk around them and see other angles. You would use that for things like text, because if you have a view with a text, you wouldn't want necessarily that the user can walk around them and see the side, because on the side, the text would be one pixel thick, and it would be just gone.

So something that I asked myself when I read about that component is, so the billboard component is the one that turns the object, but there are no functions in components. Components only have properties. What about the functions?

So billboard components do not actually turn the object, and it's a bit difficult to say this component does this, because a component doesn't really do anything. The components, that is what systems are for. The third part of our entity component system, architecture, it's not an entity component system if you want so much, but basically, you would have all sorts of functions in your system, and basically, components have a corresponding system, so a billboard component might have a billboard system, or whatever component you have might have a system that is like correspondingly named, and the systems are the ones that then perform the action that you want to do, and custom components and custom systems, when you make them yourself, you have to register them with the global system of RealityKit, and I've seen in sample code where you only have to register the system and not the components if the system is named, and if the component is named in the system, but, from what I've understood, you have to register both. I'm not sure here the documentation doesn't go into very much detail on that.

So the basic takeaway is here that components do not perform anything, the systems are the ones that do. The components are more like supplying the information to do so. And systems basically filter which entities they act upon.

So, a billboard system might, for instance, look at all of these entities in our scene, and it would look, oh, I only need things that have a billboard component, so it would only look at these three, and it would act upon them, and it would make a query and then get all of these three objects, and then iterate through each of them, and you can do some transformation or whatever, or maybe your billboard system says it doesn't matter that there's only a billboard component, I also need a model component, because why turn something if there's no model with it? So it might also only see these. I don't know that.

I haven't worked on the implementation. I'm guessing it will use all of them, but, anyway, basically, what a system looks like is this. It's really not a lot of code.

It might look like a lot, but it's not. Basically, you have a query where you specify what kind of components you're looking at. You don't need to have a query.

You can also look at all of the entities in your scene, but it's a bit nicer if you specify some sort of components that you're looking at, because, generally, you don't mean all of the entities. You only mean specific ones. And you need an initialiser.

You don't need to do anything in there, but you need one. And then the only function that you have is the update function, and in that function, you get this array that the query returns, and you iterate over all of the entities in that. And that can look, like, visualised.

I'm always trying to draw out what I'm reading, so this would look a bit maybe like this. So you might have entities that have different components on them, and you might have model rendering system which looks for model components, or you might have a fish flocking system that looks for fish flocking components, or you might have a rainbow colour system which only looks for entities with a rainbow colour component. All of these run again and again and again at each rendering cycle.

So, basically, because they run very often, you do not want to do heavy work in them. You can create serious lags by doing that, and you don't want that, because the only reason why you should be using an ECS system on a Vision Pro is, or in augmented reality, is because it is more efficient. And you kind of lose that if you yourself introduce lags into the system.

So the basic steps when you want to make something in RealityKit is you start with creating an entity, and then you add components that you need for that entity. And then you're adding your entity to an anchor, or you're just like keeping it in space, which I've seen in a lot of samples where they use cross-platform. They only, like in a lot of Apple samples that are cross-platform, they only use the entities and do not anchor them to anything at all.

So they just float in front of you in space. And then you change components, for instance, based, well, you change components, or you change the state inside of components based on user input, and you let the system do the rest. If you want to know more about this, there are some good samples to look at.

For instance, Apple has a great sample that's called Underwater. There they have fish that are doing, like, some flocking, and there's a fear and a greed system in there, I think, and they have like a small, what are they called? Like a person that's underwater in like a suit.

So you can breathe. What? A diver.

Yes, thank you. English, not my first language. Anyway, you can also check out the spatial drawing sample that was released this year by Apple.

It's going more into depth about extrusion and metal shaders, which are also kind of cool to use, but I don't have time to talk about them, and also I haven't been, I haven't tried metal, so I can't tell you anything about metal shaders. So you can also look into the community more if you want to find out more about how to build something for Vision Pro and how to build something with RealityKit and ARKit. For instance, you can look at Matt Pfeiffer's RealityKit experiments.

He has published a lot of gists on GitHub about things that he tried, for instance. This is a screenshot from something that he called a 3D printer reveal of, I think he used a low-level mesh for it and low-level texture to basically create the shape in an animation. He has a lot of these low-level mesh and low-level textures.

You can also look at Polo's Jumpfinity, which is a nice game, I felt, for looking at what you can do even if you only have simple shapes in your game and if you don't use complex 3D models. I also really enjoyed looking at Matt Haney's app ideas on Twitter. He had this idea of tasks that grow in your space as you do not do them until they encapsulate everything.

And as well as an app for did I lock my door, which I think is genius because I always walk past my car and I'm thinking, did I lock that? I need to press it again and again. Did I lock my car is a real problem for me.

Now, at the end, I want to look back at my cross-platform dreams from the beginning. Did I reach my goals? My basic problem is no, I didn't reach my goals.

As I said, I've changed a lot of my code already, so I couldn't reach that issue. But even then, my problem is I can't really do it cross-platform because the platforms are just too different. You have a different feel of the UI, which maybe you would have said, oh, yeah, that was clear from the beginning.

You should have known. Maybe I should have known, but I wanted to try anyways. There's also a lot of difference with interactions that feel natural in the device.

On iPad, tapping something might feel natural, but on Vision Pro, you might do something else. On iPad, you might not want to move something and zoom or whatever, but on Vision Pro, it makes it much easier if you can grab the object and bring it closer and turn it and do things with it, what might not feel comfortable on iPad. Apart from that, the anchors are also, again, they're too different, not unifiable, and that's something why, even though I did all of this to have an app that runs on both, I decided to go back to this and do something completely different for both platforms.

Because even though this is both kind of AR, this is where my cross-platform dreams are kind of sadly ripped apart, because, again, they are very different, and I would recommend developing for either or with different code bases, because a lot of the trouble I had, you're not going to face if you're doing this, so I can only recommend doing that. Now you might say, yeah, but why are we doing augmented reality? Is there really any people using this?

Not a lot of people have a Vision Pro, as I've heard from some people. Basically, I think it's an easy creativity starter. It's really easy to get started with augmented reality and do something small, do a proof of concept or work on something, and, in my opinion, everything really is cooler in space, whether it's a Lego set or an exploration of a solar system.

It's just a lot cooler when you see it in 3D than when you see it on a page or something. I think augmented reality is not really about how good your 3D modelling skills are. It's more about how you can work within these boundaries if you're not able to model something yourself.

It's more about the creativity. And I can show you something that I've been working on. This is what the app looks like on Vision Pro.

Basically, the spheres now rotate in an orbit around you, because I thought that's a cool animation, and they open separate windows when you click them. Yeah, with that, I'm good on time, I think, and I want to say thank you all so much for listening, and I hope you had fun.

### Denis
The main question remaining is, did you, by any chance, get into contact with someone at Apple and have an explanation on why there are three different implementations for the same thing, actually, based on three different platforms?

### Lena
No, not really yet. Maybe in the future. Who knows?

No, but I've talked to some people about the problems with it, especially the problems with anchors and testability. I suggested something. You know that a lot of people have a really new phone with a lighter sensor and everything, so that, in my opinion, you could kind of mock it with an iPhone, and then you could at least test whether the anchors would appear somewhere.

Same with iPad, because a lot of the anchors could, in my opinion, theoretically work there. I don't know that. I'm looking at it from the outside, and I'm not looking at the, oh, this is how that works on the back-end.

Maybe it doesn't work on the back-end. I can't say that.

### Rob
The systems all work on components, right? They reach out and would modify their orientation like the billboards. It seems like multiple could mess with the same component.

Are they ordered?

### Lena
So they don't fight. You can order systems. Basically, the systems run one at a time behind each other, and you can add a dependency to say first system A, then system B, then system C, or system C can only run once you have system A and B, and you can do things like that to make sure they don't fight with each other.

But, yes, you can do, well, it's not what you're really supposed to do, but you can, for instance, say I only want to look at, I have a system that, like my rotation system, that I don't need a component for that because I don't care about state, for instance, so I just want to rotate all entities all the time, and I just want to look whether they have a model component, and you can do that and then look at model components, because you're not really changing the model component.

You're changing something of, like, the orientation, and that's more changing the entity. So they don't necessarily fight with each other.

### Rob
Yeah. That was wonderful. Thank you so much.

### Lena
Thank you.