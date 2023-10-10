slug: >-
  /talks/${editionInfo.conferenceSlug}/${editionInfo.editionSlug}/${slugifiedSpeaker}-${slugifiedTalkTitle}
date: '2023-09-21'
title: Offline-First Mobile App Design
author: Avi Tsadok
video: V9Dcrnjg_n4
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/V9Dcrnjg_n4.jpg
slides: ''
tags: []
year: 2023
conference: swift-connection
edition: september-2023
transcript: >-
  My name is Avi.

  I'm going to talk about how to design mobile apps for offline.

  Let me introduce myself.

  So I'm currently head of mobile team at Million Payments.

  Million Payments is a fintech company.

  We deal with payments between small businesses in the US.

  And in my team, we've got an iOS team, we've got a backend team, and also an
  Android team.

  So I'm just waiting for your reaction about the Android, like the flutter from
  before.

  Besides that, I worked seven years at , Any.do, , which is a leading to-do
  list and calendar app, quite famous.

  I guess some of you know that.

  I've got 13 years experience of iOS since the iPhone 3GS, I think.

  And I've also published four books, currently working on my fifth.

  I want to start with some interesting quote.

  "The internet was down for 10 minutes, so I went outside. the graphics were
  amazing, but the gameplay was terrible.

  And I think that's emphasized how much we are connected to the network, how
  much it's important, and we feel reliable when we have a stable internet
  connection.

  So what use case are relevant for offline?

  So most people think about flying, because in flights we don't have internet
  connection in most cases.

  And we usually consume content, mostly Netflix, TV+, Apple TV+, but we don't
  fly every day, right?

  I mean, usually Americans fly something like 30 hours a year, something like
  that.

  So why am I wasting your time with offline mode?

  I mean, only for 30 hours in a year.

  So, let me tell you a story.

  This is story time.

  Four years ago, I took my daughter to a birthday party.

  It was in the basement because it's raining.

  And if you look close, this is me.

  And I'm not reading a book.

  I'm doing something much more useful.

  I'm opening Instagram, trying to spend the time, you know?

  But the problem is that the router was on the second floor, and the basement
  was not really having any 5G reception.

  So the reception of the Wi-Fi was almost there.

  So I was about two hours of trying to browse the network on my device.

  And you know, there is something that, we expect the Wi-Fi to work, but it's
  not really working.

  You see that it's connected, but you cannot access the network.

  So it's not a Wi-Fi, it's more than a Li-Fi.

  Okay, and a Li-Fi is really shitty, okay?

  Li-Fi is a problem, because when you don't have internet connection, it's very
  easy.

  You're just saying, no internet connection.

  Please check your connection later.

  But when you've got a Li-Fi, it's a nightmare.

  The next slide, if you're sensitive, please look aside, because the next slide
  is very terrible.

  We see this one, and this is a loader.

  This is a big loader, and we hate loaders.

  And why do we hate loaders?

  Because, I mean, I don't care about waiting one more second, but the problem
  is that I don't know what to expect now.

  I see the loader, maybe I will have some data in one second, five second, 20
  second, maybe it's gonna be 30 seconds, and then some timeout error.

  And user prefer, and they want good experience.

  How do I know that?

  Well, there is a fake research I made up four months ago.

  No, don't laugh, this is a real, authentic, fake research.

  And it turned out that 100% of the users prefer good experience.

  What do I mean when I say good experience?

  So good experience is usually performance.

  And when we say performance, we usually think about the A17 Bionic, and Swift
  optimizations algorithm.

  This is something I generated, it's not a real quote, but it sounds like
  something that you would hear in an Apple event, you know, with the A17
  Bionic,

  SOC and Swift optimization working with Harmony, experience a profound leap
  into the future.

  Okay, this is bullshit, I'm sorry.

  Why it's bullshit?

  Because the real bottleneck when you load the screen is the network, it's not
  really the CPU.

  And if we can remove the network, the bottleneck, that we have something
  really, really fast.

  How much fast?

  User will be able to use our app as fast as the speed of touch.

  So this is the ideal experience.

  And so when I say design an offline app,

  I usually mean, actually mean design an offline-first app.

  When we don't count on the network to have a stable connection, we just
  pretend it's optional.

  We just use the app.

  And if we have a network, it's a bonus.

  So what's the agenda?

  So we're going to talk about some basic principles.

  And we move to data updates.

  We're going to talk about something we call optimistic UI updates.

  And we're going to finish with CIDT, which is something--

  It's a concept that is more suitable for distributed systems.

  But we can learn a lot about it when we design a mobile app for offline.

  So let's start with some basic principles.

  And if we want to design an app for offline, that we need to understand why do
  we need a server.

  And there are a couple of reasons.

  Here are some of them.

  And the first one is we want to retrieve and update data.

  We want some centralized processing power.

  And we want to share some resources and collaborate with others.

  And I think that most times, we need it for data.

  This is why we need a server, to help serve to get update and to add some more
  information.

  And if we remove the front cover of our device, we can see there is some
  component over there that we can store data.

  This is our drive.

  I'm not sure that this is the right location.

  But anyway, don't do it at home if you're not technical.

  And we can solve everything there to support a better user experience.

  Well, you might say, oh, it's a cache, right?

  So there is a difference between a cache and a persistent service.

  A cache is something that we use to avoid recalculations and to speed up the
  user experience or make some temporary storage.

  That's fine.

  But a persistent store is something much more organized.

  It's a structured data storage.

  It has some great capabilities.

  We can add more data and components and instances.

  And it's there to stay.

  So basically, a persistent store is a code data, or Swift data, or any other
  database.

  So if we want the persistent store to be always updated with our server, we
  need to talk about sync.

  And the bad news about sync that is syncing is hard.

  It's very, very complex.

  And it's not complex only for us.

  Take a look at this screenshots for various and popular apps.

  How do we have when we don't have internet connection?

  Usually, we don't see information because they had to sync it.

  But the good news is that we have the flexibility to choose how much we want
  to go deeper into the syncing algorithm.

  So we've got several levels that we can choose.

  We can go some just offline first reading.

  We can just read, OK, not adding any new information.

  We can have some partial or full writing support.

  We also can add on top of it some real-time sync and collaboration, which
  makes everything much more complex, but it improves the user experience.

  So let's talk about Delta updates.

  Let's jump to Delta updates.

  You see, jump.

  It's the ball.

  And I think that the most important thing about offline reading and Delta
  updates is to make sure that our UI is consistent.

  When we see different screens in the app, we want it to be consistent across
  the app.

  For example, if I see the first screen here,

  I see seven locations.

  I want to make sure that on the middle screen, when I drill in, I will see
  seven locations.

  Because right now, I see six.

  And why did it happen?

  Because it's a different endpoint.

  So when you enter the next screen, we need to wait for the endpoint to return
  so we can update the data.

  And this is something that users don't like.

  And you know that.

  We see that in apps.

  When you see some information here, you navigate.

  And then you need to wait for it to update.

  So your eyes are consistent when you go offline or you don't have any stable
  internet connection.

  And we have many endpoints.

  It's not only three, right?

  So what do we do?

  So I'll tell you what we did at , Any.do, , which I worked seven years.

  We didn't have any endpoints. we had only one endpoint, which was a big sync
  endpoint.

  And when we have a big sync endpoints, we retrieve any update that we get for
  the server and then update our local DB.

  And when we do that, everything is consistent.

  Even if we don't have a stable internet connection, everything is consistent.

  How does it work?

  Well, let's say that we have a client and a DB.

  And we have two items on the DB.

  Then initially, we request some full sync.

  And then we return all the data.

  Then we save some timestamp locally on the client.

  The timestamp represents the most updated item.

  Then we want to get the new update items.

  We just send the timestamp to the server.

  And the server returns a new item.

  Yeah, that's there.

  So it's Michael, Scotty, and Dennis, by the way.

  These are Chicago Bulls old players, if you know.

  Michael Jordan, Scotty Pippen, and Dennis Wallner.

  And then we can save the new update every time a new player is added to the
  server.

  So Delta updates are great, but there are some things that we need to consider
  when we want to design and implement

  Delta updates.

  The first one is that the back end needs to maintain some time step for all
  the entities.

  And it sounds simple, but it's not, because sometimes an entity is related to
  another entity.

  So if you've got a list and list of items, and if you modify the item, maybe
  we need to update the time step of the list.

  We've got issue with some initial loading.

  I said that you need to load everything at the beginning.

  But what if you have too many items?

  You don't know what to do.

  So there are some things that you can do.

  For example, use pagination.

  You can load some of the stuff.

  You can change it to have some archived items and then load it lazy.

  And well, Delta updates are great and really increase the user experience.

  But I want to increase it even more, because there are many apps that are
  productive,

  And you need to create data offline and online.

  And then we have something that I call optimistic UI updates.

  Now, optimistic UI updates talk about how to add offline editing capabilities.

  And we call it optimistic UI updates.

  It's going to be OK.

  That's fine.

  We call it optimistic because we know that when we add something, we create
  the content offline, we don't need to worry.

  Whenever we get on and back again, we can just sync everything to the server,
  and everything will be synced fluently.

  That's why it's called optimistic.

  And we can perform any changes without waiting for the back-end confirmation.

  If you know, for example, the notes app on your app, when you type something,
  you don't need to wait for any confirmation for the back-end.

  You don't care if you've got any internet connection, because it just works.

  So this is optimistic UI update.

  And we assume that everything is going to be OK.

  If, for example, we have a list of ingredients, then we add something offline.

  When we're back online, we just send the entities back to the server.

  But there are still some things that we need to make sure.

  For example, if we create content offline, we need to take care of everything.

  It means that if we have a new list that's called work, and then we have two
  items that belongs to work, we need to establish all the relationships
  offline.

  We also need to create some unique IDs for the elements offline, because we're
  going to sync it to the server.

  The item created offline on the client, so we need to generate it myself.

  And there is also a thing that's called validation.

  If we created something offline and then we need to sync it to the server
  later, then we need to make sure that it passes any validation rules.

  And if something changes on the server, maybe we need to share some documents
  of validation rules with the server.

  So it's not that simple.

  But wait, it gets even worse, because now we have sync conflicts, right?

  Because we have two devices.

  We have maybe iOS and Apple, the Vision Pro, the lucky of you, the next year.

  And when we create a data offline, and then we sync it with another device,
  maybe we can have a sync conflict.

  What is a sync conflict?

  So let's say that the server has an item, which is a dog in this example.

  And then we sync it to both devices.

  Then the first device changes to a cow.

  And the second device changes to a cat.

  And then they both go online.

  The first one is device A. So it changes the item on the server to a cow.

  But then goes the second one, and it changes to a cat.

  This is called a sync offlink, because the backer receives an outdated
  version.

  So there are two ways, popular ways, to deal with it.

  And I guess that you know what it means.

  The first one is last. right wins, the server picks the most updated, the
  latest version.

  And the second one is the first right wins, when the server rejects the new
  version that it gets.

  Now, if you're lucky, you can try to merge stuff.

  For example, if you get two versions from different clients, maybe we can, I
  don't know, we can take the diff, we can do some diff and take the updated
  property from one device and the second one for the other device.

  But this also has issues, because we don't know if the reason that we don't
  have any change is because nothing happened, or maybe we change it and want it
  back.

  So in this case, maybe we need to maintain some updated timestamp for every
  field.

  And this is something that we didn't need to do, because we had to do that.

  And you know, optimistic UI updates are really amazing in terms of user
  experience.

  And they're very good for single user environment.

  They're good for non-collaborative editing, because once you have different
  users, it becomes really messy.

  And it's really good when your low update is right.

  So that was optimistic UI updates.

  Now let's talk about the problem that it holds and how CRDT can partially
  solve some of the problems.

  So we have issues with optimistic code update and just writing capabilities.

  And this is one example that can happen.

  You know Medium, right?

  The Medium, the blog site.

  So Medium has something called Claps, which is similar to Likes and Facebook.

  But the change is that you can, as a user, give more likes, more claps, than
  one in one day.

  You can give up to 50 claps a day.

  And if you have two devices, and you work with Medium, and you want to do one
  clap, additional clap, on second devices, so you gave one clap on device A and
  another clap on device B, then when you sync it to the server, you expect to
  see three, because you give one clap in each device.

  But the problem is that the server needs to pick one version, which is
  obviously going to be two, because two versions are true.

  And this is just one example.

  If, for example, we want to update some list that's represented by a ray.

  So we've got one list on device A, we add orange.

  And the second device, we add mango.

  And then we want to sync it to the server, to have something like apple,
  banana, orange, and mango.

  And we need to pick one version so we get rid of the mango.

  And text editing is even worse, because we lose words that we type.

  For example, if we say hello Paris in device A and hello smiley on device B,
  we want to say hello Paris and smiley, but we need to give up Paris, and we
  like Paris.

  So we can't give up Paris.

  And the reason that it happens is because we are syncing entities to our
  servers.

  We create or modify the entities offline, and then we sync it to the server.

  And that causes issues, because the server receives two entities that collide,
  and it doesn't know what to do with it.

  So that's why we have something called CRDTs.

  Now, CRDT is not something that comes from the mobile world, but rather from
  the distributed system world, when we have different systems with replicated
  databases.

  And we want to sync all the databases without even needing a server for that.

  And Sanity works instead of sending entities or instances, we send messages
  about the change.

  For example, instead of sending the list of fruits, we just send a message and
  a mango to the list.

  And instead of sending the number of claps, we just send a message, increase
  the counter by one, or add string pairs to index six.

  And CRTD has two rules.

  The first one is we don't care about the order of the messages.

  We can send the messages in different order.

  And remember that because we're going to have an issue in short.

  And the second is that we can send duplicate messages, and it's going to be
  fine.

  It needs to be very, very stable so that all the clients and all the databases
  are going to be replicated exactly.

  This is an example where we have four devices.

  It's four people, actually.

  And device D is offline.

  And then device A has a change.

  Fill a cell number five with blue.

  Then it's sending to the back end.

  So we got one message.

  And device B retrieved the message, and it can update it.

  And then device B fill send number 9 with green, and then it send it to the
  server.

  And A and B--

  A and C, sorry-- are being updated.

  Then device D is back online.

  It reads the messages, and we can apply it to its database.

  Now, working with CRDT is not just changing form entities to messages.

  It's much more than that.

  It's a really different mindset.

  Because when we work with that, we need to be very, very consistent between
  the replicated databases.

  When the user, for example, adds some item in its user interface, we don't
  just insert a new item to the database.

  We create a message, and then we apply it to our own database.

  We apply the message.

  And the reason we do that is because we want to have the same behavior when we
  get a message from the back end or when we create it from the user interface.

  We want it to be the same every time.

  Then we create the message.

  We save it locally.

  So we need to think how to do that.

  It's not a business logic entity, right?

  It's just for syncing.

  And then we need to ship it to the server.

  So OK, we get it.

  I mean, do we still have conflicts?

  What do you think?

  Of course we do.

  Otherwise, I won't ask that question.

  So even CRDT is not perfect.

  And let me show you one example.

  And it really depends-- this example really depends on the algorithm that you
  use for CRDT, because CRDT has something like eight or nine popular
  algorithms.

  But let's say that we have two devices with the word "hello," and then we add
  "hello, universe" on one device, and "hello, world" on the second device.

  And then we sync it to the server, and we expect to see something like "hello,
  universe, world," or "hello, world, universe."

  It depends on the algorithm, but you can choose whatever you want by
  alphabetically or not.

  But instead of that, you get something like "hello, and never mind, you know
  what I mean.

  It's not something that we can read, and the user gets it, and then he needs
  to delete it and write it again, and it's not something that the user will
  like.

  And the reason why it happens is because when we work with syncing text, for
  example, that we use boundaries of zero and one, because we want the
  flexibility to insert characters between other characters.

  So we use some friction values to do that.

  And then we had two devices with the same friction values.

  Everything goes fine, unless we add some more data, more text.

  So on one device we added universe, and the second device we add world.

  But it's different lengths, so we get different friction values because we
  need to generate some values.

  And then we sync it and we try to reorder the letters, and this is what
  happened.

  Now, you may say, OK, this is something that won't get to production, right?

  So Google Docs had this bug many years ago.

  Of course, they fixed it.

  And this is something that can happen with just messaging.

  What else?

  Let's say that we are re-ordering items.

  So if you remember, we said that there are two rules for CRDT.

  The first one is that we don't care about the order of the messages.

  But we don't have a move operation on CRDT.

  So what do we do?

  We create two messages.

  It's delete and insert.

  But since we don't have any order restricted, we can set it with whatever
  order that we want.

  So what can happen is we can delete twice and then insert twice, and we get
  duplications.

  And I think that the last example is maybe the most fun.

  We've got, I don't know if you can call fun for sync issues, but let's go for
  it.

  We've got two devices with some hierarchy of employees.

  And in the first one, the left one, we did the change.

  We moved Alice to be under Tom.

  Tom is the manager of Alice, which is, I mean, this is a valid operation,
  right?

  And on the second one, we moved Bob to be under Alice.

  Now, what will happen when we sync it?

  So Alice is the manager of Bob, which is the manager of Tom, which is the
  manager of Alex, which is the manager of Bob.

  So we've got a cycle.

  And it happens even when two operations were valid.

  And I think that's emphasis how much complex syncing is when we try to do it
  offline.

  Now, let's have some summary of what we talked.

  There's something called Li-Fi.

  OK, now that you know that.

  We talked about some offline reading.

  We talked about optimistic UI updates.

  We talked about conflicts resolution.

  We talked about CRDT basic and some edge cases.

  And there's one note that I hear every time

  I speak about offline that I want to tell you.

  We've got great solutions today for offline.

  We've got Firebase that can sync everything.

  You don't need to do anything of that.

  I'm not saying that you need.

  We've got Cloud Kit that can do many stuff for us.

  And well, there is a reason why I'm talking about it, even though you don't
  need to do anything of that.

  I don't see you because of the light, but please raise your hands.

  Developers that are more than 9 or 10 years developing iOS.

  Oh, OK. I'm in a good company.

  So, yeah, if you remember, 10 years ago, everything was much more complicated,
  right?

  We had, instead of Core Data, we used SQLite. I remember that.

  Then we moved to Core Data, and now we have Swift Data, which is much more
  useful and much more simple.

  And we had to animate, use the commit animations before we had the blocks.

  Actually, we didn't have blocks on the days of Objective-C at the beginning.

  And everything was much complicated.

  Now we have dozens of tools that can help us, a framework that can help us
  produce much more useful and effective code.

  And everything is much simpler, which is great.

  Which is great.

  We need to continue with this direction.

  But there is a price for that.

  And the price is that we are starting to get away from the basics, from the
  infrastructure.

  And I think that if we want to be better developers, better programmers,
  better iOS developers, we need to understand how things are working
  underneath.

  We need to understand what are the challenges.

  Because when we know more, we're going to be much better in solving new issues
  and new problems. problems. So, thank you for listening. That's for start.

  [ Applause ] Now, so, this is a QR code for a feedback for my talk. And it is
  a little surprise. I will pick randomly three people who answer the feedback
  and they're going to get a print copy of my latest book, the Complete iOS
  Interview Guide.

  So I encourage you to answer the feedback and maybe get a present from this
  conference.

  Thank you.

  [applause]

  Thank you, Avi.

  One quick question I had to start with.

  I started working on mobile things a long time ago.

  About what? about mobile things, mobile apps a long time ago and we already
  had before the iPhone on PDAs, things like that. We already had
  synchronization issues, offline issues. Why is it still such a complicated
  topic nowadays?

  Well, because nothing has changed. We're still thinking issues. By the way, if
  you remember iCloud was a nightmare a few years ago, in syncing issues, it
  just got stuck.

  And we had issues at any door when we synced many data, and it was without
  even the CRDT, just regular data.

  And the problem with syncing is that small things can just break your sync.

  It can bring you to a state where nothing is happening.

  It's very easy and very difficult to test it,

  Because you've got so many edge cases.

  You saw here, there was edge cases that I didn't give you an answer because
  the talk is too short for that.

  But if you Google in YouTube CRDT, you will find stuff that are really, really
  complex.

  And every small issue can break-- just break into sync.

  It's not that a small data is not syncing.

  It just stops the sync.

  That's the problem.

  - Okay, from what I get, you said there are many implementation of CRDT, and
  from what I get, the kind of issue you might run into really depends on how
  you interpret the difference that are applied.

  And so in the end, isn't it related to the core of your application?

  And so my question is, is there a possibility to have like a library that is
  generic enough?

  Or if you need to implement CRDT, are you doomed to go from scratch?

  So I just said that there are libraries for that.

  The most famous, I think, is Firebase.

  It does that for us.

  A Cloud Kit you can use.

  I don't know.

  But someone told me that you can use Git for that.

  But Git is also not suitable for text editing.

  So I don't know if someone can tell.

  None of it. There is a library that can solve text editing issues between
  devices.

  But for all the others, you can use Fab as a Cloud Kit fluently.

  We'll take a question from the audience, from Simon actually.

  Are there any cases of apps that should not adopt an offline-first approach?

  Should not?

  Ah, should not.

  Yes, so I always said that in Adobe we did that,

  In my company, I work in a FinTech company, and it's payments.

  So it's very, very hard to do a payment when you're not online.

  So you can't do that.

  And payments, it's also some regulations and legal issues that you can't do
  because you are not online and we've got some engines that check.

  So I think that FinTech world is a problem.

  By the way, not only for payments, but also for retrieving data.

  So the things that are sensitive, like crypto and fintech, stuff like that,
  are problems in offline mode.

  So we need to be more careful over there.

  Do you have a last question?

  So the question that's wondering, how can you convince your back-end team to
  move away from REST and towards CRDT.

  And so the question is also, how much work should you plan when you need to
  move from one way of working towards the other?

  So the question is from REST to CRDT.

  You talk about optimistic UI updates, actually, when you say go to that.

  So one of the best things about moving to optimistic UI is when you get rid of
  many endpoints, because you have one endpoint.

  And this is very, very--

  OK, so it's decoupled the work between the client and the back end.

  This is what happened, because you don't need as a client the back end for
  every small task.

  You can just generate and change everything on the client and just sync the
  stuff to the server, and the server doesn't need to know about it.

  On the other hand, it requires more work from the back end size to set up
  everything at the beginning.

  But I guess it's much more fast after you do that, both for the back end and
  the client.

  Thank you, Avi.

  Thank you.

  [APPLAUSE]
allow_ads: false
