---
slug: /talks/frenchkit-2022/michel-andre-chirita-from-app-to-game-development
date: '2022-09-30'
title: From App to Game Development
author: Michel-André Chirita
video: HLz0Cfkaiew
thumbnail: https:/async-assets.s3.eu-west-3.amazonaws.com/thumbnails/HLz0Cfkaiew.jpg
slides: >-
  https:/async-assets.s3.eu-west-3.amazonaws.com/slides/talks/frenchkit-2022/michel-andre-chirita-from-app-to-game-development/slides.pdf
tags:
  - SceneKit
  - GameplayKit
year: 2022
conference: frenchkit
edition: '2022'
allow_ads: true
---

Hello everyone again. So now I will talk about the side project I've started two years ago.
To give you some context, I have been a developer for more or less 20 years. But since 10 years I've only worked on iOS applications and I wanted to explore something different. I wanted to build a game, but not any game. I wanted to build a game for iPhone and iPad with artificial intelligence with real time online playing without any backend. With one hand... no, we can stop there [laughs]. So I ask myself is it possible to make all of these only with Apple frameworks as a solo developer during my spare time. And the answer is yes, this is the result I was able to do pretty much all the feature I had in mind but with some tough moments and some good surprises today I'll share with you five learnings from this experience.

First we talk about things I thought it would have been easy but haven't been so, at least in my experience. Also, things that could have been more difficult and some architecture, artificial intelligence and online media playing. But first my story needs a hero to help me illustrate it. So please welcome our Hero (Ndèle). And... The other guy. let's start with the first learning: easy things that are not so much.

One thing you need to do when you make a game, same as for applications, is to adapt to different devices and to different screen sizes. Even if `SKView` is a subclass of `UIView`, there is no autolayout in SpriteKit and no other magic tool to handle different screen sizes: you have to handle it by yourself depending on how you want your UI to scale.

Then maybe you'll want to have a drag and drop picture which is pretty common pattern in games. Same, there is no built-in method to handle drag and drop. You have to implement it by yourself, using `UITouch`. Yeah... I would recommend to make a state machine with the four possible states and use the `GKStateMachine` implementation built in GameplayKit.

Next, we'll talk about a bouncing ball. There is a physics engine in SpriteKit which simulates real world movement, collision, gravity, friction, etcetera. It's pretty cool but I had some difficult times figuring out why the exact same code produced two different results on two different devices. What's the difference? The answer is that scaling the scene size to adapt to a bigger screen affect the mass, which in my example changes the ball behavior. So with all objects, the exact same position size, scale and physics parameters, SpriteKit physics can be deterministic and you'll have the same results each time you run your code on any device. In conclusion, you probably won't find every feature you're looking for included in SpriteKit; deal with screen sizes from the beginning, check on every screen format, adapt to your needs and think about accessibility. Make Robin happy: the minimum touch and read size. If you need drag and drop, use a state machine, check all the touches and use the physics body if you need to contact detection for the drop position. At last the physics engine has deterministic results if you carefully control all the parameters.

Learning 2: there are also a lot of nice building blocks making things a lot easier than I thought.

When you are used to making animations, this is something you should like. Here we are changing some UI actions like moving, scaling, rotating and it's so easy and nice. The physics engine is also pretty powerful and cool. Here we are simulating one object that follows the other one anywhere it goes. It's also so easy and very fun and yeah, you should try it.

Matchmaking with GameKit is also a very good example of difficult to build feature, yet very easy to implement. You can reuse the given UI or build one custom made by yourself in a few lines of code.

There are many more nice building blocks. I can't go into detail today, like entities and components for all composition, agents, goals, behaviors for autonomous movement... For example, for enemies moving automatically controlled random values with setting a source and a distribution or graph path obstacles for path finding and many more. To conclude, there are a lot of nice building blocks in these frameworks and most of them are very easy to implement. I will strongly recommend to explore the documentation to avoid reinventing the wheel by yourself.

Learning three: architecture.

The most basic way to architecture game is to tie everything together. But as you can imagine, it's not a good idea. First we'll split the display and the logic parts, then we'll define what are the scene events that are sent to the logic layer, basically the user actions, and what are the actions that will be displayed in response.

Let's have a look at the implementation. First, we need the state describing at any moment: the game, time, the score, the character, position, other key information. We'll use a `struct` for that. Then we'll make an an `enum` for all user inputs, like when the hero, or its opponent, is moved; and we'll add all additional information that is needed to evaluate the change: here, the new position. For each new event received by the logic layer we need to evaluate how it impacts the state and what is the result to display. For example when the hero moves, the state has to be updated to reflect the new position. The change of position triggers the display action that is sent to the UI layer. Same for all the events. And finally we check if the new state reflects a victory for one of the players: in that case, we send a dedicated display action.

Next, we'll do the same thing for the UI part. Now we have an an `enum` for all the actions that can be displayed:s it contains all the things that th UI can handle. Here, we are updating the UI by animating the nodes with `SKAction` moved to a `CGPoint`. Same here. Finally, it will present the "game over" menu when there is a winner, of course.

To conclude this part, I will strongly advise to separate the game logic and the display layers. Use the global state and `enums` for defining all interactions. This will make your code more readable and testable and it will greatly facilitate integration with features like artificial intelligence or online multiplayer.

Learning 4. Let's talk about the artificial intelligence.

Basically AI will need to make a decision tree like this one, in which you can see an initial "State 1" and all the possible actions that may happen from there for each action. There are there are resulting new states (2, 3, 4) that can represent a victory or defeat. The goal of the AI is to find the shortest path to victory like this one, in my example.

GamePlayKit offers two strategists that will handle this slightly differently: MinMax and Montecarlo. MinMax will try to explore every possibility. There is one parameter setting your depth limit. It will return any victory path found in this range. Montecarlo will seek a compromise between exploiting choices that look promising and exploring nodes. It applies the concept of large numbers to randomly filter some of the possibilities and it also has some parameters to define limits.

To sythetise, MinMax will have better results but is generally slower, Montecarlo should be faster but also has less good results.

For the implementation we'll bring back our previous architecture and we'll add a new AI layer which will ask for the current state and send back in return the selected update, hopefully leading to victory. Let's have a look at what information the AI will need from our states. First, the state will need to confirm to `GKGameModel`: this will ask to implement variables telling the strategist who are the players and which one is the next play, then it needs a score for the player and if there is a winner then, as we've seen before, you have to provide all the possible actions for this current state. Then describe how to duplicate the state and finally apply the update the strategist wants to evaluate next. Once we have the state, all we need to do is to ask the strategist what is the next best move for the active player.

To conclude that part: it's super easy to integrate an AI with the right architecture. The performances depends of course on the complexity but it may be fast enough for real time gaming: you have to choose wisely when and how to run it. Use `GKMinMaxStrategist` when the decision tree is not too big, else use Montecarlo.

Learning five. Let's talk about building a real time online multiplayer feature.

GameKit supports multiple ways to do it. The probably first solution we'll think about, is to have a hosted server. All the clients will connect with it to send their inputs and get back updates. In this case, each client acts as a dumb display terminal. The inconvenience, of course, is that you need a custom back-end which may be quite expensive to build and require some specific skills. You can also choose a peer-to-peer solution where every client connects to all the others or the ring peer-to-peer to peer where each client connect to the next. It may be cheaper but also less robust, less scalable and less secure solution; and the obvious problem is how to handle conflicts as there is no one source of truth. The player hosted client-server model solves this by designating one of the client as being also the host. To improve it, we can opt for hybrid player-hosted client / server solution where each client has its own embedded logic service (local server) for very fast processing without waiting for the host; but only one remains authoritative in case of conflict or when one single source of truth is needed, for example, for generating a common random number shared by all the clients.

Now, let's have a look at the architecture. We can now very easily include a multiplayer service between the display and the logic, which will send and receive events to and from the other players. The implementation of exchange online information is very easy. We just need to send an event to our multiplayer service, then encode it and call the same function on the `GKMatch` object which, has been provided by GameplayKit during the matchmaking phase to receive events. There is a `didReceiveData` from remote player function in the `GKMatchDelegate`. It's where you can decode the received data and use it to update the local state and display. Of course you have to limit the payload size. This is why we only send updates and not the entire new states. Doing so, the connection is fast enough for real time games.

We need a good network connection of course, but you need to handle edge cases like connection errors and conflicts... and then you can add some magic: if each client is only displaying the remotes events received, and if you want a smooth animation, you need to exchange a lot of data. This can be solved by adding some interpolation between positions. You can do this, for example, by animating very slightly objects between two received positions. If you want to go further, you can do as major games like _Call of Duty_ by implementing predictions. There are many ways you could do this depending on your gameplay and needs. But one simple example consists at guessing the movement of the object locally and immediately in response to the last received input. You can do this by calculating the vector between the last known positions; and this only works if most of the times the prediction is not too far from reality, and that correcting it with the remote values doesn't have a too visible impact on the game experience.

To wrap up this part, multiplayer connectivity can be easy to implement; real time is possible but with limitations and I will recommend to first concentrate on robustness and then optimize and add smoothness. Edge cases and optimizations are most likely to be the biggest difficulty and the most time-consuming.

We are getting close to the end of my story. So to conclude, solo game development only with Apple frameworks is possible. SpriteKit, GameplayKit and GameKit offer a lot of building blocks but not everything I would have hoped. With the right architecture, AI and online features are very accessible. And there are nice problems to solve. And, last, it's fun!

I hope you will try it and have fun with game development. Thanks for listening. And thanks to the organizer for inviting me.

And last thing, if you want to try my game, you can use this QR code. [It's available in the App Store](https://apps.apple.com/it/app/versus-arena/id1542795843?l=en) and it's free. Thank you.

Greg: So I've been following this project like for years.

Mac: Actually, you have been the first tester.

Greg: We talked about it like dozens of time and I've always been impressed by the fact that you kept on working on it. So how did you find the will to keep on working on such a large project?

MAC: So, first, I think my family and my friends helped me a lot. They supported me to encourage me to continue and work on this project. And I think you have to be curious, you have to like it because you will want to work at a friday night or each weekend or of course. And maybe you can tell a friend you will yeahXXX. Do speak at a conference so you don't have a choice: you have to finish it. _[Laughs]_

Simone: When making predictions for online multiplayer, does does tiOS provide you with building blocks or you basically have to do that?

MAC: You have a lot of ways to do predictions and there is no building a block to help you. But there are simple ways like a vector, it's very easy. Just three points. No, you don't have another building block to help you for that.

Simone: How much time in total?

MAC: It's a little bit difficult to say because it was at first six months of more than full time then one year and a half during my weekends and my holidays and some evenings. I think it's somewhere around maybe one year full time.

Greg: What's the state of the project now?

MAC: So it's live, it's available on the App Store. It's only a first version. I think I will continue, I will keep iterating and do adding some features and something, but it's available so you can try it and leave a review. Five star hopefully!

Simone: So you learned love lots of frameworks and techniques. Which of them are applicable to normal app development?

MAC: Yeah, it's a good uh good question. Uh I think all of these are very easy to use inside any application because it's an Apple framework so you just have to import the framework and it works. I can think to maybe SpriteKit Particle Emitter, which is the same thing as the UIKit counterpart, but it has more options: so maybe you can use it. Maybe you can do animations with nodes as we have seen it. It's very easy, much easier. So if you want to have a Gamification or something in your, in your application, maybe it's possible. In fact you can do it, but you have to ask yourself if it's the best way or if you can do it another way.

Greg: If you if you had to do this project once more, if you restarted, what would you do differently?

MAC: I think I will try Unreal Engine. Or Unity [laughs]. No, no, I will do the same because it was very interesting. I learned a lot of things, so no, I wouldn't change anything.

Simone: We have another question: you have been working on this project for kind of a long time but I guess you took some pauses. Um how do you kind-of documented the project so that yourself from the future will be able to understand what you did in the past?

A: Good question. So I don't have like unit testing or documentation. Yeah, I don't have anything. In fact, I maybe have some comments in some tricky parts but no, I don't have any documentation. Thank you for the question.

Simone: I think we said no talks about no testing! [Laughs]

Greg: Maybe you do some PRs to yourself like to review your own code! [Laughs]

A: Yeah, exactly. It's difficult, very difficult for me!
