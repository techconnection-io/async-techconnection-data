---
slug: "/talks/flutter-connection-23/dominik-roszkowski-from-network-failures-to-offline-success-a-journey-of-visible-app"
date: 2023-06-02
title: "From Network Failures to Offline Success: A Journey of Visible App"
author: "Dominik Roszkowski"
video: e5aOsY6N8Cs
thumbnail: thumbnails/dominik.png
slides:
tags: []
year: 2023
conference: flutter-connection
edition: june-2023
allow_ads: false
---

How is everyone doing?

Did you enjoy the day today?

Yeah.

It's hard to see you, so I hope that you're all smiling.

And I welcome you to the talk that's going to be maybe somewhat related to the previous one as well.

I'm going to tell a story of some findings that we have acquired over last year at Visible.

And I hope you kind of like the title, because together with my friend Chad GPT, we came up with From Network Failures to Offline Success as a wrap-up of what happened along the journey that we had in the last few months.

So for those who don't know me, I'm Dominic.

You can call me Dom.

And I'm a Flutter GDE, which is a fancy name for just a person that speaks about Flutter a lot.

And currently, for almost the last year,

I've been building, together with my colleagues, a product called Visible.

This is an app that's aimed for people that struggle with long COVID and chronic fatigue syndrome and similar conditions.

And we try to help them with managing their illness.

And probably once a year--

I don't know-- I try to write something on my website.

So if you're into this kind of cadence of blog posts,

I kindly invite you to check my blog online.

So before we dive in into the particular topic that I want to share with you, let me tell you about the app itself.

So Visible is a symptom tracker, and we have a wearable integration where we have a Bluetooth band.

And I'm wearing one with me as we speak.

So for instance, it's going to record my heartbeat for the presentation.

And then I'm going to just see how much I exerted myself in this last half an hour.

But in general, it's aimed for people that have much worse situation in life as we normally have.

So they need to actually track how they feel every day.

So this is like a journaling app along with the wearable integration.

And it aims to help them in some way.

And that's the business statement.

But when it comes to the app itself, it's mostly mobile first.

And we kind of focused on the mobile app.

We have a very thin layer of back end, almost no code back end, you would say, or like low code back end.

So opposite to, for instance, Flutter Flow, where it's like low code app.

So we have low code back end.

So we kind of had to learn a lot of the things along the way when it comes to the back end.

But the important part is that we have a GraphQL Hasura-based back end.

So we wanted to utilize all of that from day zero.

So we kind of went all in into the GraphQL subscriptions, mutations, and queries, and stuff like that.

So it was kind of an easy way to work with.

And I didn't join at the very beginning of the app.

So we inherited the code base, the base state of the app from a contracting company.

And it was quite naive.

Everything that was happening in the app was just calling the APIs, querying the data from the back end, and stuff like that.

So everything was kind of tightly coupled with the network.

But we were building this for a couple of months last year, and in December we decided to just go with a public beta.

So we released the app, and we didn't do any marketing.

We had around 100 founding users that would use the app even before the beta, and they would share some feedback.

And then we just published the app, made a couple of blog posts and Tweets.

And the community itself, the Long COVID community, kind of quickly started using the app and making judgments in December.

And so how did it go?

And I'm super happy to say that actually it went super well.

Like in just first week after launch, we went to like thousands of users and we had like 70,000 sessions every week, which was like completely unexpected for us.

Like, it went bananas completely.

We didn't know-- like, we weren't prepared for this kind of scale.

And as I mentioned before, we didn't have a real back end.

So it was also a bit scary.

But at the same time, I think we learned that the back end infrastructure nowadays is prepared for much bigger loads.

So even though for me, as one of two developers working on the app, it would seem scary, but in fact, it was kind of-- like, the back end didn't have any issues.

And I must say that since then, six months after the launch, we've been steadily growing.

There was, of course, a hockey stick at the beginning, like typical startups have.

But then we were steadily growing every month.

And people tend to stay with the app for many weeks.

I mean, this is also a bit of the condition with long COVID is that you have to live with that.

So it seems that it's a success story from the very beginning.

But the title spoils it a little bit.

So we actually had one big problem.

This problem was making us very anxious.

And when you open any of the crash reporting tools, you would see something like that.

And I specifically crossed out crashes because some of the crashes that are reported were just flatter errors that were reported as crashes.

So nothing serious.

But still, it would be like thousands and thousands of exceptions daily.

So essentially every user would have some exceptions every day.

And that was very tricky.

And I mean, of course, like at the beginning, you kind of think, all right, just some network exceptions, nothing really serious.

And as a really solid good developer team, we made our effort and put a lot of error screens in the app.

So any time anything failed, we would have an error screen, right?

Because this is what you do, right?

But of course, once we started receiving them, we knew that something's off and we have to just start tweaking them.

And there was a couple of issues that we identified.

Again, it's going to be maybe something obvious for people that work with bigger apps, but for us at the scale, it was quite interesting to see that.

For instance, we would -- like, when you open the app on the push notification or a local notification in the morning, there would not be Internet right away, especially on iPhones.

And this might mean that, for instance, the Firebase token that we need to call the API would not refresh.

So it would snowball, and then the request would fail.

And even with some retrials and stuff like that, it would still kind of fail.

And that's one thing.

The other thing is that we would have a lot of GraphQL subscriptions.

And in some conditions, like these all separate subscriptions would randomly fail.

And of course, we would try to retry and reconnect.

But still, it would be very tricky to handle and reproduce and then fix in the development environment.

And frankly, I would blame myself for that.

We were a little bit too optimistic about all these retriers and timeouts.

So it was kind of a realization that maybe we were doing things a little bit too naively.

And again, that's something that you probably learn only when you actually do a real product with real users scattered across the world.

And so one thing that is very--

I think for us developers, we need to be aware of that.

We typically tend to test our apps on a good Wi-Fi connection, maybe 5G like here.

But most of our users are still going to use 3G or even worse connection in some rural areas, in an elevator, in a parking lot, places like that.

So it's important to have this in mind and not -- like, myself, I would test offline mode with just turning on airplane mode, which is not actually, like, it doesn't reflect real conditions.

So we started patching things up, like, really, like, went all in to trying to fix these issues.

So we added a lot of the things, like, retries, connectivity checks before any action would happen.

We would use GraphQL caching, restarting the connection, optimistic updates.

These are all terms that if you ever use libraries like GraphQL or Ferry, they all have this as, like, things that are, like, built in.

So you can have cache built in into your GraphQL client.

You can have optimistic updates.

So whenever you call a mutation on your GraphQL endpoint, you may have some response immediately, stuff like that.

But we started adding these things and we were expecting that it was going to work so well, but actually, because, for instance, our WebSockets were pretty chatty, they were sending a lot of messages, any time anything changed, it would still have some possibility to make an error, just because of the scale of that, it was very chatty, there was a lot of messages being passed on and just the number of connections meant that there was going to be some network exceptions.

And this also meant that we had a significant bandwidth usage.

So probably using the tricks from the previous presentation would let us realize that we have a huge battery impact and battery drain because of that.

And I mean, still people would use that, but at the same time, it meant that we are -- like, the app was not like the good citizen on your phone.

And just to maybe give you some background, let's talk about architecture, quote, unquote, because, I mean, this is just a simple setup.

So the app itself can -- maybe it's not simple setup, but it's straightforward setup where we have just a few layers of different stuff.

And you may recognize this from some of the block library documentation.

So at the top, the frontend layer is just qubits and blocks managing the state here and there.

Then the important, I would say, later part is the repositories where we just convert or pass the data from underlying clients like GraphQL client or a lot of client that we have here that connects with the band.

So this is like a pretty straightforward setup.

But separating all of these into these layers kind of makes -- will make sense in a second.

So knowing that, we decided that we're going to just change a little bit.

So to reduce this chattiness and the impact of the WebSockets and stuff like that, we decided to add a little bit of a secondary caching in the repository layer.

So we just went with the behavior subjects for different sets of data.

So for instance, whenever you would update your user, your observations, like your symptoms, it would be immediately available on the behavior subject.

So no need to do any GraphQL mutation, no need to wait for the subscription to refresh, stuff like that.

And it kind of worked well.

And then on top of that, we also added hydrated block, which is like a library on top of a block library that lets you cache the state of your blocks.

So for instance, when the app starts up, the previous state is retained.

Pretty cool stuff.

And I think if we would use RiverPod, which is like a caching framework in some sense, it would also provide similar possibilities to cache the request or provide the most recent data to you.

But we are in the block ecosystem, so this is the way we went with.

And I mean, it kind of worked, but we were kind of expecting, like, talking to our founders, it's going to work fine, let's just wait for the next release, but I mean, we still had some issues.

So for instance, this is some of the intercom messages that we were receiving, and they kind of didn't stop.

So after this release, with these updates and stuff like that, we were still getting a lot of the complaints from our users.

And it was mostly about the connectivity, like things like seeing error states, not being able to use the app, being stuck on the splash screen, which is related to this token refresh issue.

And we're seeing things like that in our crashlytics.

And maybe some of you have already seen this exception, connection closed before a full header was received.

There's a couple of issues about this on Dart issue tracker.

And it's a thing that I think no one I know knows how to reproduce and fight.

And the other one is even more strange, which tells us just that the app was not able to resolve the host.

So DNS didn't work.

So it means that there was no internet connection at all.

And we know from just observing the internet status or connectivity status that the Internet should be there.

So these kind of exceptions were very cryptic and we kind of ran out of options how to fix them.

And the important piece of that is that if it would happen randomly in different places, it would be probably much better, but it affected our critical path in the app.

The critical path in the app, as I mentioned at the beginning, is that user would open the app in the morning, maybe the first thing in the morning from the notification, and

And they would need to do their morning check-in.

And if it fails, then probably the user will not come back later to fill it in.

So it was very important for us to make sure that this path, this critical path, works best.

And we knew at this stage that the approach that we took may not work.

And, like, we even found that, for instance, this is a common issue on iOS, that, like, the Wi-Fi just disconnects overnight.

And I'm not an iOS user.

So it was new to me, but maybe iOS developer would spot it instantly that, like, for the first few seconds or minutes after you open the phone in the morning, you just don't have

Wi-Fi.

Maybe you haven't put it in the charger and stuff like that.

And it's a known issue for years and you just have to deal with that.

And we learned these and more issues that were affecting our users and we just decided that we just need to take a new approach. a step back and just look at the architecture from a different point of view.

So this is the moment when we say, all right, let's make the app offline first.

The current approach is quite naive, quite simple, so everything is tightly coupled with the network and what we need to do is to make the app and decouple it from the network connection.

And frankly, I had this idea how to build this for several years already, even back

Back in Xamarin days, yes, I was a Xamarin developer.

If there's any, please blink now twice.

So back in the Xamarin days, we would kind of use this approach, like offline first app where a thing back then, we would have a local storage and we would just have like some kind of queue of actions that would be then replayed.

Some folks would even use even sourcing for that, which is fancy architecture pattern for like additive incremental -- starting of incremental changes.

And I know that many of the frameworks, like React Native and Jetpack and iOS, these topics, this offline first approach has been solved several times already.

So we are kind of reinventing the wheel, which I think is quite a good thing, just going through that, especially on a real production app with real users, thousands of them, and trying to optimize it to time to market.

We didn't want to optimize for cleanliness of the code or number of tests.

We are a startup, so we optimize how fast we can deliver new features to our users.

So first thing that you need to think about when doing the offline mode is local storage.

Basically, you no longer want to rely on the data from the HTTP client.

Even if it caches the data, like GraphQL may have a hive storage, hive box storage.

It may give you the response that it recently had.

It may even give you some structured data, but it still only kind of caches the fraction of the data for a particular request and it may be invalidated.

So you essentially need to have a local storage, some kind of database.

And there's many options on the market, Couchbase, ObjectBox, Realm, SQLite, ISAR, and all of them have some traits.

I'm not going to get deep into that.

But if you look at the first three, they are all no SQL databases.

And for us, we had already a really nice Postgres database on the back end.

And the easiest approach was just to mimic that in the app.

Especially because it just reduces the cognitive load.

So we went with SQLite.

It was a proven choice on the market for many years, again, back in Xamarin days.

And it works cross-platform.

So it can be accessed not only from Flutter, but also from the native part of the app.

So we have a lot of the integration on the native side, for instance, foreground service that connects to the band.

So we wanted to access this database from this site as well.

And in the future, maybe we're going to have an app for Apple

Watch.

So it also would be nice to access this data from the Apple

Watch extension.

So SQLite checks all the boxes.

And on Flutter's side, it can be accessed from a separate isolate.

Not every of the options that I've shown before supported this at the time.

So for instance, reading a big chunk of data would mean that you would just have junk.

Like for a few milliseconds, you would just have to-- the UI would just stop.

So having a separate isolate means that even with big reads or big writes, you don't have any junk, which is a really nice thing to have.

So the thing that may be interesting is that what about the models? we have some database modeling, our Postgres database.

But we don't necessarily need all the fields.

We have some permissions.

You should not be able to maybe read creation date of an object.

You should not be able to read other users' objects.

So we just went-- we tried to mimic the back end, but just make it a little bit simpler, make the cognitive load lower.

An important factor here that is very worth understanding is that we started from the back end first, right?

Like, back end was like the source of truth.

And now we can move the balance towards the app.

So now the app will generate a lot of the objects that then will be synced to the back end.

So important thing to think about right now is who decides about the IDs of the objects?

So like before, it was the GraphQL back end assigning the IDs or database assigning the IDs.

And now you may be able to work with the app with no internet connection, so there is no one to provide the ID.

So we have to come up with a local, just a redundant local ID that's going to be assigned by the mobile client.

So we just -- typically you just go with the UUIDs because they are kind of -- they will not repeat.

And another thing is that why we didn't want to do the NoSQL, because we wanted to kind of embrace the relationship.

So a user may have different observations.

These observations may relate to the symptoms and symptoms may relate to health conditions.

So having these relationships just be the same as in the remote database makes our life much easier because we can just kind of write SQL queries locally, which, again, is not a big deal, especially with chat GPT.

So you can -- are fine with that.

So you don't have to worry about this. like skipping the classes and you don't have to deal with that.

So for instance, one of the example tables would look like that.

This is just a note that the user can add.

This is a drift definition.

So for SQL Lite on Flutter, you would have -- you may use, for instance, drift library.

And here, like, we have the remote ID, but we also have the UUID that would be defined by the local client.

And in our case, the primary key is going to be the UUID because the ID may not be defined until we get information back from the backend.

Another important factor or topic that you have to embrace or do while implementing offline first approach is just some kind of queuing mechanism for user's action.

So before, action would mean that you would have a GraphQL mutation and some response from that.

But you have to decouple this right now.

So now we're going to go into like a really fancy diagram that I tried to explain everything in.

So let's say we start with the morning check-in, so this is the thing that you do every day in the morning, and you may have like your sleep rating.

The sleep rating is going to be saved through the observation repository just to the observations table.

Nothing fancy, but the important thing is that we just save it to the local database first and suddenly we don't care about the network here, so we can just let the caller know this qubit, right?

Everything is safe, move on, you don't have to wait for anything.

So now the loading state is not necessary anymore because it's already saved.

After that, this repository needs to make sure that we have some track record of what just happened.

So we have a separate table, this is just for the client, where we just keep all the actions as some kind of entities.

Synchronization tasks.

And these tasks will be picked up, they have some metadata, like what kind of object has been added to what table, stuff like that.

It's just a description of that.

And we decided to not keep the copy of the object that has been saved because it's in the different table, because we only care about the final form of that.

We don't care about the diff between the previous version and the current version, like the event sourcing.

We just only care about the information that, hey, there is a new observation with this and this ID.

Make sure that it's uploaded to the cloud.

So then another thing, and it's like single drop qubit, just for the lack of a better name, that's going to pick up.

And thanks to the reactiveness of SQLite queries and debouncing of that, we kind of respond to all the new tasks being added to the queue reactively.

So every few seconds, if there are any actions, they are going to be picked up by this thing.

And then reusing the previous implementation, a mutation is going to send it to the cloud.

So this is a really nice approach.

And it decoupled the--

I would say the app part of the app, like the user-facing part of the app, from the synchronization.

It may seem obvious.

As I said, it's reinventing the wheel.

It's been done thousands of times before, but finally doing that in a real application with dozens of features.

It's not that we have only observations that need to be saved that way.

There's many, many more features that have been built over a year.

And after the observation is added, it gets immediately-- after it's saved to the cloud, we know the ID, we know the last update date, we know the final form of that.

Maybe if somebody else modified this, there might be some validation logic on the back end.

We have the final form, so if anything changes, we save it to the database, and anybody who was subscribing to that now knows what's the final form of that.

And finally, after everything is done, we mark the task as done, as successful, and we know that the process is finished and the task is going to be pruned in a few days.

So that's the kind of the very simplified flow.

And for every action, you would have to define your own handler.

And it's kind of irrelevant how it's done.

It's the important part is that you have to kind of think about all the possible actions that may happen.

So essentially, every mutation that we had in the app now became its own action.

And as I mentioned, thanks to that, you can do optimistic updates.

So we don't have to await anything anymore, because everything is going to be-- maybe

We have to wait because it's still a synchronous process to a database, but it happens in a fraction of a second, in milliseconds.

So you don't have to put loading states or anything like that.

And so for instance, here you have a morning check in, and after you rated your sleep, you can see the sleep immediately.

You don't have to wait.

You can do this completely offline.

You don't have to worry about that.

And the cool part is that if you want, you can use the app with no internet connection indefinitely.

But of course we want our users to be able to synchronize the data with the cloud.

Which is quite cool.

And it affects all the parts of the app.

So suddenly, like, everything in the app started to feel snappier.

Like you don't have to wait for anything.

Like in human scale.

So updating the user, updating the observations.

Sending the data, like, saving your health condition, details, notes and stuff like that. started to be much, much smoother and people actually noticed that when we asked them about this.

And for developers, we wanted to have some insight how tasks are being processed.

So for instance, here you can see the task even finished before I was able to talk about the slide.

So there's a task and it's pending because it was just added and then it's in progress and then it's successful.

And we have this table and we can just read the table on the device and know what the the current status of a given task.

And if it fails, it's going to be repeated eventually.

And the idea is that that is going to be finally sent to the cloud.

And the topic that's kind of natural, like extension of what we have, is that we also want to do the synchronization not necessarily only when the app is in the foreground.

So we also have, not on a production just yet, but in a TST version of our app, a background synchronization.

So every time a user connects the device to the charger or a nightly, the synchronization will happen to just make sure that the latest back-end data is on the device, and also that the user's data has been sent to the cloud.

A topic that also often is mentioned during this kind of offline first approach is conflict resolution.

And we are super happy to say that in our case, we actually don't have to worry about this.

Our app is like a single user app, so we don't interact with other users.

Not like, for instance, in Monday.com, when there is maybe dozens of people modifying a given entity.

So for us, it was not a big deal.

And it's mostly additive.

Like, people only add data.

So even deleting the data is not a big issue.

Only a few things can be deleted.

And we just handle that through dedicated Cloud Functions so that we always make sure that it happens in a transaction and the user is aware that something has been deleted.

We don't have soft deletes, so that's kind of approach that we took.

And it works quite well for the few things that need to be potentially deleted.

And I think that you have to mention when talking about conflict resolution is conflict-free replicated data types.

This fancy name is for very specialized structures that help you operate when you have multiple sources that can modify the data.

It's a way more complicated topic than what we want to cover tonight.

So again, one thing that's worth mentioning-- in our case, we just have last write wins, right?

So I need to mention here a really great example of how company and a team approached offline first mode, which is monday.com.

They have made an amazing presentation a few years ago at DroidCon.

So if you would like to kind of understand ideas behind offline first, not for such,

I would say, complex simple case, maybe -- I don't want to say simple, but like such a normal case as ours where we have a single user application, but for an application that that potentially many people can modify a given entity, and it may be also edited from the back end, like not only from the mobile client.

I highly recommend this, and you can look it up in the notes that I'm going to share at the end of the talk.

So did it work out?

Did our approach help us solve this issue?

The title spoils it, but yes.

And we had, like, immediately after the release, we had less exceptions.

And the important part maybe was not that there's, like, less exceptions, but finally we brought back the visibility into how -- like, what are the other issues?

We didn't have this noise anymore of network exceptions coming from different mutations and different queries.

So this was very helpful.

And I mean, every day there is, like, kind of more visibility into the actual issues that our users encounter.

And there's another good thing that happened.

As I mentioned before, we have this low code backend, which is a bit costly, I would say, when it comes to bandwidth and data throughput.

So thanks to that, we no longer had these chatty WebSockets, our bill dropped significantly, to the level that we no longer have to worry about it.

So all this effort that was put into that was worth it.

It was paid off in a monthly bill.

So it's a thousands of dollars thing.

So it's really, really cool to see your idea actually affecting the bills of the app.

So that's pretty cool.

All right.

The topic could be covered in much more detail.

We could go deep into the code, but for today I just wanted to show you the general idea, something that actually sparked me to actually try it out, try it for myself.

I remember when I was coming back from the DroidCon two or three years ago and I was just doing this, trying to implement the same thing that Monday.com did, just on a plane, so I didn't have Internet connection, so that was the best possible way to just try it out.

And since then I was always hoping that finally one of the products that I'm going to build will have this approach included.

So I'm happy to say that it works.

It's out there in production, serving thousands of users daily.

And it's kind of unlocked a lot of the possibilities right now because every new feature that we add right now just relies on this simple principle.

And it just works.

And I think that's the best thing that kind of came out of that.

Thank you so much.

I hope you enjoyed.

The notes, there are notes to this talk if you go to the website, my name.dev offline, you're going to find some links and presentation slides and stuff like that.

I don't think I posted these slides just here, but they will be there.

And another thing is that, as I mentioned, I want to kind of explore this idea of kind

I'm doing a little bit more realistic apps with Flutter, so probably I'm going to share some more details in the upcoming months, some samples and stuff like that.

So if you're into that, feel free to follow me.

And definitely, I invite you to chat about how you would approach this, and maybe you have some cool ideas.

Thank you so much.

And I think that's going to be all.

[APPLAUSE]

[Applause]

Who wants to start?

> > Maybe I'll start with the question from Twitter.

> > Awesome.

> > So the first one is not directly related to offline, but just an insight from you.

Which GraphQL package would you recommend for development regarding how it can handle offline off-court and caching?

> > So there's a couple of options on the market.

And I don't want to say that one is better than the other because they are doing an amazing job.

I'm personally using GraphQL library and there's a whole ecosystem around that.

And the folks behind that are a super fun team and I happened to met them before.

There's also another one called Ferry.

I used this preliminary just to test it out and it's catching up with GraphQL and I think it has superb support as well.

So these two I think are one of the best out there, but of course there's probably more implementations of that.

Alright, thanks.

A question from Craig, who we saw just a few minutes ago on stage.

Can you say more about what made retries insufficient to fully solve connectivity issues?

Not sure if I...

Yeah, I mean, actually, can you say more about what made retries insufficient?

Retries.

So retries were kind of tricky because it's like a snowball effect, where essentially the first request, when it fails, maybe because of the token being invalid, like the token tries to be refreshed.

And if the token is not being refreshed and Firebase has this issue that sometimes it just doesn't refresh until you restart the app,

I mean, hopefully it's going to be fixed.

But it happened to us several times that the token would not refresh.

So the retries will not solve that.

And only the next time the user would launch the app, the token would be fresh.

So we kind of had to not rely on the Firebase as a source of truth anymore.

That was a tricky part for us.

And also, if you have a retry and you make the user wait longer than necessary, and maybe they are in the elevator or they are in the parking lot, where it will-- in the sense of this request, it will never reconnect to the network.

Like, if it's going to happen a minute later, it's too late.

And you just see a loading spinner.

And if you show any kind of real user, they are impatient.

They will just close the app and restart from scratch, so this retry is not going to work.

And if a user is dissatisfied on the first run or whatever, they will just not use the app.

So that's the tough reality.

So we have to give them the impression that everything works and there is no retrials.

Speaking about what you're saying about, yeah, basically it's UX and spinners, how do you actually make it so that people understand that their app is like stopped syncing?

So I mean, like, of course, when you have a network error, the person sees that, like, in the very minute they test the error.

But on the longer term, how do you make sure people understand that there is a more widespread sync issue?

Yeah, so if something like that would happen,

I mean, again, potentially, they should-- in our app, they would not have any issue whatsoever, because you can use the app almost indefinitely.

And on the next update, we can make sure that we resynchronize everything.

We show some special screen-- we put a special screen telling the person, hey, make sure to have internet connection.

We're going to synchronize it here, stuff like that.

But on a daily basis, it doesn't really matter if it's going to synchronize today or tomorrow, because it's like a local journal.

Of course, if you would have more like back-end logic that needs to work on the user data.

And for instance, in our case, we send the heart rate samples to the back-end and to process them later.

So this is important for to sync for us.

So in case of the heart rate updates, we have a different synchronization process that's like a little bit designed in a little bit different way, a little bit more resilient, so that it will happen several times in different conditions and eventually the data is going to be there.

I don't have a perfect solution for this, so I think we're going to learn this the hard way.

If it happens that we have some users that they will never synchronize, we'll have to work with that.

Thank you. Is there a way to automatize tests to check that your app is offline compliant and that when you implement a new feature, then it won't break?

Or do you have to do it manually, as you mentioned?

So yeah, testing is tricky.

In my previous role, when I was working in a consultancy, we put a lot of effort on tests so everything would be tested.

In my current role, as a second-- there are two developers in the project.

We almost don't have any tests.

I must say this.

We have maestro tests, which are great, and they cover the use cases of the users.

But in fact, I think it's just the trust in the other person and just making sure that changes are reviewed.

They are small.

Someone said it before, don't keep long-living branches.

So we embraced feature flags.

We used a paid service for feature flags and just make sure that the code is committed to the main branch as quickly as possible

If something is not complete, it's just behind a feature flag.

And this way, our founders, our designer, are able-- is able to just see the even unfinished feature in some kind of test condition.

So that's the way we do it.

And we have a separate environment where we can test things like that.

So we can embrace the fact that, again, we accept the trade-off.

We don't have automatic tests on the code level, but we have a really decent QA pipeline and a couple of master tests for critical paths.

- Okay, those remain an open issue if somebody wants to investigate further.

Thanks.

I wanted to ask also about your database on the front end.

How do you handle change of the schema?

Do you have migrations running on the front end?

And how do you synchronize it with the back-end model, even if it's not completely the same?

Part of it should be synchronized.

Migrations are a really interesting topic whenever you work with SQL database.

And again, we didn't have any issues right now with that.

So we had a couple of migrations.

And SQLite with Drift on Flutter, they support migrations easy well.

So if you add a column, you just have a nice call to add a column.

If you have a table, just deal with that.

And we can assume that the data is synchronized to the back end anyway.

So we can even do migrations that are distractive.

So you just drop the database and start it from scratch.

And hopefully, it's going to happen overnight, so people don't have to see a loading screen when they open.

But if they wouldn't have a synchronization overnight, they would see the loading screen just for a few seconds. and then it should work just fine.

A note on the migrations.

Some tools, like I think ObjectBox and Realm, they have automatic migrations, which is amazing.

I mean, if SQLite had automatic migrations, it would be splendid.

But you just have to be aware that whenever you change your models, you just have to add another line for the migrations.

And probably in a few releases, we're going to do just a destructive migration. when we're going to start from scratch so that we don't have this line by line changes, version by version.

And when it comes to the back end,

Hasura provides a really nice way to keep your definition in code.

So anytime you want to modify your model on the back end, you can do it through their console, and it generates SQL migrations for you.

So they are being applied to the real Postgres database, and they might be a good guidance for you as a mobile developer, what kind of migrations

I need to apply on the mobile site as well.

So it's like a versioned and checked out into the GitHub repository and deployed automatically to the Hasura.

Right, I think we learned lots of stuff.

Yeah.

Do we have time for a couple-- there's a couple questions?

OK.

One more?

Yeah, one more.

One more from Samir.

We can stay here until like 11 PM.

I hope I'm not going to answer questions until 11.

We'll put you in chains to stay here.

We'll apply to the client.

Yeah, just bring some snacks.

And beer.

Did you have any security layer for the offline data?

Yeah, it's encrypted.

So it's encrypted.

I'm not going to say how.

But it's encrypted.

But anyway, on iOS, it's not a big deal.

You can have an unencrypted database, because it's just confined to your app anyway.

On Android, on a rooted device, it may be a little bit more easy to access that.

But still, it's users' data, so even if they get access to that, that's fine.

But definitely, like, we encrypt the hard-trade data so that if it ever gets leaked, like, you will not be able to even distinguish this from gibberish.

But we don't gonna say, we won't gonna say how we do it.

At least here.

MD5.

Ah, crap, you found it!

It's the fastest, man, so...

No, just standard encryption on the SQLite, yeah.

Well, thank you very much.

Alright, thank you very much indeed.

Thanks a lot.

Thanks Dominik.
