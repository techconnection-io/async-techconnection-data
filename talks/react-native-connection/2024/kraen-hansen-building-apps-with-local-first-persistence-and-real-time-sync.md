---
slug: >-
  /talks/react-native-connection/2024/kraen-hansen-building-apps-with-local-first-persistence-and-real-time-sync
date: '2024-04-23'
title: Building apps with local-first persistence & real-time sync
author:
  - Kræn Hansen
video: wMeMpt6vRSc
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/wMeMpt6vRSc.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: '2024'
allow_ads: false
---
### Kræn
I'm going to talk about local-first software, in particular, building apps with local-first persistence and real-time synchronization. My name is Kræn Hansen, I work for MongoDB on what used to be called Realm, but is now known as the Atlas device SDKs. Let's get into it.

So local-first is a term coined by Inc and Switch. It's an independent research lab. They published an article about five years ago about this term.

I'm not affiliated with the lab, but I read the article and I highly encourage you to go do the same. This local-first movement, and I believe it is a movement, it's picking up steam. We have talks about it, meetups about it.

There's a conference coming up in Berlin, unfortunately it's sold out, but basically I believe this essay, the document that was published, is one of these defining pieces of text that will shape our industry going forward, maybe the same way that the Agile manifest did for the Agile movement. It's pretty huge. This essay talks about local-first software, around seven ideals for building software.

These ideals are from the perspective of the user of a local-first app. First up, it needs to be fast, that means no spinners. I don't want to be waiting for the app while I'm thinking up new creative ideas.

Next up, it needs to be usable on multiple devices, that means I should be able to start working on my laptop, continue working on my tablet, without any interruptions. It should facilitate offline-first, so notice here how offline-first is a part of local-first. That just means I should be able to work without internet connectivity.

That could be in an airplane, but it could also be in a store, or a spotty Wi-Fi, spotty 5G connection. I don't want to be interrupted just because I don't have internet. It should facilitate collaboration, and that means not just going from my device to my other device.

It should also facilitate collaboration between my colleagues, my friends, my family, as I'm working with the content in the local-first app. It should support longevity, or what is called the long now in the article. That means what happens if the business that runs the synchronization that facilitates collaboration goes out of business?

How does the app handle that if the sync service is not available? Second to last, privacy or privacy should be built in by default security measures such as encryption, like role-based permissions, stuff like that. And lastly, user control.

You as a user of a local-first piece of software should be in ultimate control over your data and how it's being used. The article uses Google Docs, this idea about having files that you can rename and move around as one example of an app that facilitates this. This is very quick, the civilized ideals of local-first software.

Please go read the article if you're just remotely interested in this field. This is a very quick walkthrough. What I'm building on a day-to-day basis is these Atlas device SDKs.

I'm just going to go through a very quick introduction into it. We have this database called MongoDB and we have this cloud service called MongoDB Atlas. It's a multi-cloud developer data platform.

We call it an integrated suite of the cloud database and then data services on top of that. It should be able to facilitate and accelerate how you build with data. One part of how you build with data is moving data closer to where it's being used.

Sometimes where data is being used or generated is in your end-users' devices, so that could be a mobile phone or a desktop app or somewhere else. For that, we built this Realm database. I was a part of Realm before the acquisition, MongoDB acquired Realm some years ago.

Basically, we have this database that runs on-device and we have a synchronization protocol between the local database running on-device and the cloud. Yeah, I'm going to get more into that in just a sec. Yeah.

Oh, lastly, we have this Realm React package, which is built on top of the Realm database to give you a more reactive experience of interfacing with the database. Awesome. So, how do I believe Atlas device SDKs and Realm fits into these seven ideals?

So, first up, it's very fast. It's a local database running on the device. We use memory mapping and we provide synchronous APIs because it is very fast.

We actually have the ability to provide synchronous APIs and not just asynchronous APIs to data access and read and write. It is multi-device because we have this bidirectional synchronization. We call it flexible sync because you're able to flexibly select a subset of data that is on one device versus another device.

You can declaratively say what data you want to have on which devices. It is offline-first, again, because we have a local database. We also have what we call an edge server, which is like a near-tier or like a near-edge server that you can deploy.

Let's say that you're a stall, that you have individual devices for each of your employees and then in your back office, you have this edge server running where you can do synchronization with. That entire peer can be like the stall can go out of connectivity, but you can still continue using your apps and synchronize between devices. It facilitates collaboration because we have this synchronization protocol.

It's based on implemented around operational transforms. This is the same technology that powered the Google Docs, for example. We also have automatic conflict resolution, which means when I'm changing a piece of data on my device and my colleague is changing the same piece of data, we facilitate this automatic resolution of conflicts between those two states and they will eventually reach the same state of the data.

I believe we fit this longevity like ideal in the sense that we have the edge server that you can deploy in your local environment. So if the end service like the big cloud goes out of business, I don't believe it will, but if it will, you still have the edge server. We have an open protocol documented on GitHub.

We have open source SDKs and we also have a reference implementation of the server on GitHub. Privacy, everything is encrypted in transit and at rest, you can encrypt both on the server side and the device and just one more thing like with encryption, MongoDB has something called field level encryption that we don't support currently with the same protocol, unfortunately, but it is there like encryption at rest in the server. Okay, lastly, user control.

So because the Realm database is a file on the disk of the device, you can extract it from the device and you can open it using tools like Realm Studio, which is a UI, like a data browser for the database. It also has possibilities of exporting and importing JSON and CSV from the database file. Great.

So taking one step back, I think we could see local first as a piece of a megatrend that we see this idea about going from imperative to declarative, going from describing like the individual steps that an app needs to do to describing the end state that we want to have. One example of this, I'm going to go through a few examples of this. So like one of them is server configuration.

We see going from shell commands to doing more infrastructure as code using Terraform configs or Kubernetes, for example. Also like JavaScript module systems going from inline require statements to the more declarative ECMAScript modules is another example. On Android, going from the views, object-oriented paradigm to Jetpack Compose, for example, or on iOS, UIKit to SwiftUI.

We used to write jQuery, where we would be finding an element, changing some property, like changing the text inside the element to a more declarative approach, which we all know and love. And yeah. What about fetch?

What about data fetching? What is the state of the art in terms of declarative data fetching nowadays? When we look at the React Native survey and in the usage of the data fetching category, we can see fetch, like the fetch API, is very, very used.

Also small wrappers around that, like Axios, is also popular. TensorStack Query is increasing in popularity for helping some of the issues that are arising around fetching. And when we go over to retention on the data fetching, we can see that TensorStack Query is one of at least the most popular solutions to this problem about data fetching.

And it seems to be sort of the best thing we can do right now. But data fetching is really hard. And Tanner Lindsley, the co-author or the creator of TensorStack and TensorStack Query knows about this.

This is taken from their documentation, like a long list of all the problems that TensorStack is trying to solve. So I think when you don't control the location, this is the first bullet here, I know it's a little small, but when you don't control the location of the data of the service that you're fetching from, data fetching using HTTP might be the only thing you can do. Like if you want to interface directly from the app.

But I think that's not true for many apps and many like use cases, you actually do control both sides of that situation. Yeah, but there's a long list here, like the difficulties of interacting with asynchronous APIs, shared ownership. So this thing about data fetching, it doesn't inherently have solutions for conflicting data, for example, and how you resolve that.

Caching, deduplication, so I don't like fetch the same thing twice. Updating the state on the client, like how do I actually know when to fetch again? How do I don't underfetch, overfetch, yeah, all that stuff.

Pagination, memory management of something like this. It's really, really hard. So I want to be specifically like, I'm not bashing on TensorStack Query specifically.

I said that this is the state of the art. This is the best way we can do it. But I'm going to show how you can go about doing things in that library versus something like Realm.

So this is how you would go about setting up TensorStack Query. You import some like the query client and a provider and a use query hook from the React query package here. We initialize the client and we render our app providing the client into this client provider that will use the React context API to expose the client to the example app or example component.

We're going to try to fetch a piece of data in this case from the GitHub API. We import the use query hook here for the example component. We call the use query hook and we get back an object with an appending state, an error state and the data.

We have to specify a query key and this is to ensure that the query gets refetched if something on our client changes. Like this is a way of provoking a data, like a new data fetch. And we provided a query function, some asynchronous function that will return a promise of JSON or of data that we will eventually get back as the data property.

Yeah, and I think like this fetch will happen on mount of the component and when you focus the thing like the screen or the component, when you focus the app, sorry, it might as well get connectivity. If you're offline and you get connectivity, it's going to refetch and you can refetch on an interval. You can also like manually say you want to have this query fetched or you can invalidate the query key.

But these are all just heuristics like you need to know like when you want to do that. And that's why even though this is probably the state of the art in terms of like how declarative we can get with data fetching, you still have some underlying imperativeness in terms of like when do you want to fetch data in a smart way. Yeah, and we have this pending state where we need to show a loading spinner, which is super annoying if people want to interact with the app.

If there's an error, you need to show it and you maybe need to gracefully like refetch if you want to resolve the error. And finally, we're showing the data here. Okay, so how would this look in Realm React?

Setting up is a little differently because now we declare the GitHub repository schema in the app and we basically declare we have a name and a description and we pass that in as a schema property for the Realm provider and render the example component. We expose a use object hook in this case here that takes the repository like the class that describes the model and the primary key in this case, the RealmJS repository. It will return either an object or null.

If it's null, it's gone. It's not in the database, otherwise we can just render it. I think maybe the important thing here is to note that we don't have a loading state like we don't have the pending state and also we don't have the error like if there's an error occurring, it will happen synchronously.

It's going to throw so you can catch it with an error boundary, for example. And that's very rare like that something like that happens. We also have the ability to fetch more or get more objects from the database.

In this case, we have the use query hook from Realm React and we pass in again the class and we get back a collection. It's a collection of objects. One big difference is that this collection is lazily loaded.

That means it's not going to create any access to objects in memory until I actually start pulling objects from this collection. This helps a lot in terms of performance when you want to render, let's say that you fetch from a database or use query to get data from a database and you have like a ton of objects. You don't want to populate memory with that.

This helps in terms of memory management around like it alleviates some of the pain with pagination and stuff like that. Because it's lazily loaded, in this example, we have a GitHub repository. Let's say it has an owner with other repositories and you have like a chain of objects.

Because it's lazily loaded, you can just access the chain how deep you want to go and it won't like populate your memory too much. It depends on your access pattern. It's not going to eagerly use memory.

Awesome. Also, one thing to notice is that this is reactive. So the example component will re-render if data changes in a database, which is a pretty big deal.

It's not relying on heuristics. It actually has like a, if we're syncing, it has a connection with the sync server. As objects are streamed in, changes are streamed in, this will re-render the component to show the right updated data.

Yeah, so no pulling heuristics. And here we're showing the repository. A little more advanced, we can also search the database if we have too much data.

So here we provide a search term to the example component and we use the use query hook here to filter and sort the collection. It looks a little imperative here because we're calling filtered and sorted, but it is just like a build a pattern around declaring the subset of data that you want. Yeah.

Awesome. So what I've shown you so far is like, where does the data come from? I hadn't shown that.

So it was all local to this point. And now I'm going to show how to enable synchronization for your app. You need to have an app provider.

The app provider references an ID in the cloud service. You provide a user provider as well. This will ensure that all synchronization happens from an identified user.

And you can render a login component as a fallback to show like a login screen. And here we're enabling flexible sync. Okay.

Very quickly, just how do you mutate data in TensorStack query? You use the use mutation. It returns a function or like an object with a mutate function on that you can call to issue in this case a post request.

Again, you need to show the pending state, the error state, the success when it happens. And here we have a button to actually press to do the mutation. And this is great, but I think we can do better.

In this case, we expose a use Realm hook to get the access to the Realm that got provided into the example component. And here we're just showing a state of like, did it work? Did it not work?

We can show the text like the to-do was added. And here on the button, we do it a little differently. We just do a write transaction.

We call Realm to write. We create a task in this case, passing in the title. And because it's synchronous, we don't have to wait anything for this write to work.

Like if the write returns without throwing, it is in the database. And we can just set the success state, which is super powerful, especially if you're trying to, let's say, catch errors. In this case, we can just try catch the write.

If, for example, some task already existed with the same ID, it's going to throw. But then we can just like catch it and set, in this case, a message showing the state. Awesome.

So this was my talk. If you want to learn more, definitely go read the article on ingantswitch.com. There's also a Discord server.

If you go to lo-fi.so, you can find a link there. There's an awesome podcast that I encourage you to listen to on localfirst.fm. Also, the conference coming up in May. Unfortunately, it's sold out.

But I think there's some community tickets that you can apply for. And then, of course, our SDK. We have docs.

We have tutorials and information on how to use it. You can reach out on Cren Hansen. I'm Cren Hansen everywhere.

Thank you so much for your time and attention. It's a rare commodity these days. Thank you.

### Mo
Thank you, Cren. Please come along for the Q&A. All right.

So let's get the jokes away to begin with. Which one? I've been told there's rumors on the streets that you are able to pronounce a word that's in the Danish vocabulary that happens to also be in the Guinness World Records book.

Yeah. That is the longest word.

### Kræn
1993 edition. Yeah. How many characters?

### Mo
89, I believe. So can we get a drumroll from the audience? And then, yeah.

### Kræn
It's an occupation. It's... ...

Catchy. Yeah.

### Mo
Yeah. Very cool. All right.

Round of applause for that. All right. Cool.

So a few questions just while audience questions are coming through. And you can submit your questions right there in the live Q&A. So you mentioned edge services.

Just out of curiosity, what edge network are you folks operating on, and how many points of presence do you have access to?

### Kræn
So the cloud service itself is multi-region, and it's multi-cloud. Again, so it supports GCP, Azure, and AWS. That's one thing.

And then the edge server is actually meant to be what we call near-edge, and that means it's on your own hardware. So that would be some kind of server running in your back office, whatever you want.

### Mo
So it's not possible to run that on, let's say, CloudFlare's edge network?

### Kræn
It is possible. Anything that can run a Kubernetes pod. Okay.

Or a Docker container, I believe.

### Mo
Okay. Cool. You briefly mentioned conflict resolution.

I'm presuming it's using a CRDT-esque conflict resolution paradigm.

### Kræn
Well, some things, like the counter type I know is a CRDT, but it predates some of that work. So we use operational transforms, which is a little different in the approach. It's also maybe one of the, let's say, one of the limitations of Realm in that CRDTs is very good for peer-to-peer connectivity, where operational transform, like we have, it requires that you have a master peer, like the sync server or the edge server.

So it's more like a tree shape, so to speak, rather than like a graph of devices.

### Mo
What are sort of the weird edge cases in conflict resolution that, as a developer, we need to keep in mind? Is there some conscious thinking that needs to go to it as an app developer and some edge cases that we need to be able to look out for?

### Kræn
There's this discrepancy between when you're reading data and you're writing data. If somebody else does a write in between, how do you actually solve that? We do have some primitives, let's say, like the counter that we have.

It's like the ability to count up. If it was just implemented as a, I read from the database, and then you read from the database, you plus one and I increment it by one, and then I write and you write, then we're not going to reach the right semantic encoding of what we wanted. But if you use the counter, then that will actually help resolve stuff like that.

### Mo
Cool. So let's jump into audience questions. Maybe we can jump back to some other questions afterwards.

So really cool client-side demo. What does the server setup look like? So what's the other side of the setup look like?

### Kræn
It's a cloud service, so that would be, yeah, Atlas. It's just a UI. I'm not showing that.

But it's like a UI where you create an app and you get the app ID and you get to specify the schema of data. So all your clients, you can either be in a dev mode where clients can push schema changes, or you can lock down the schema to ensure that you have a proper schema, so to speak. And then you have your roles and permissions implemented on the server side, ensuring that I can override your data and stuff like that.

### Mo
Cool. There's maybe a question around clarification on what you do while the data is loading. Is there anything you can elaborate on that?

While the data is loading? While the data is loading on the client.

### Kræn
Well, so, yeah. So we do, as you open up the sync and you specify, I'm not showing that, but you need to specify a query that you subscribe to as a client. So you say, I want to have all the data that's relevant to me, for example, with the own ID of my ID.

Then you can listen for progress. You can have progress notifications on as that change is streaming in. And in that case, you would maybe show a spinner, like the initial load.

But from there on, you don't necessarily want to show. It's just going to come in and then the app is going to react to the change.

### Mo
Cool. There's a few questions on collaboration, conflict resolution. I think we've kind of covered that, so we can skip through.

### Kræn
So, yeah, I'm also an SDK developer, right? In the sense that we have a dedicated team writing the database in C++ and the server team as well. So the whole thing, maybe it's being handled on another layer.

If you don't trust me, you can trust them.

### Mo
No, I think we all trust you. And I'm not afraid to say otherwise if I didn't. Is there a way to use your solution and choose to sync the data with an on-prem MongoDB instance as opposed to using MongoDB Atlas?

And the reason for this is commonly with a lot of large enterprise companies, they'll have regulatory reasons where they need that to be hosted, quote-unquote, on-premise, whether that's on a private cloud.

### Kræn
I would say the Edge server is the solution for that. Edge server.

### Mo
Okay. Cool. I really like this question, and I think it's more of a practical question here.

If you had top three advices or a few pointers around going incrementally from an app that's not offline-first and slowly making it offline-first, what would that be? Or local-first. Or local-first, yeah.

### Kræn
Disable network connectivity as you're using your app and figure out what's broken. Basically, I think that and then go from there. Or just throttle your connection to see where the slowness is building up.

With any profiling, it's all in the details.

### Mo
And to wrap up, a very, very important question on database naming, pluralize or not. Yeah, I'm not going to go into that. Not going to dignify that with an answer.

All right, cool. Thank you very much, Kræn, and thanks for coming along.