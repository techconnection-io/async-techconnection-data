---
slug: >-
  /talks/react-connection/react-connection-2024/mo-khazali-building-complex-uis-with-a-server-driven-react-app
date: '2024-04-22'
title: Building complex UIs with a Server-driven React app
author: Mo Khazali
video: hub__0Gbr6E
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/hub__0Gbr6E.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: react-connection-2024
allow_ads: false
---
[Mo]
How are you all doing? Everyone's well fed? Yeah?

Awake? Cool. So I've worked at a French company for the last three years, and what I've learned is that the French love to have extended lunch and coffee breaks.

So the fact that I have an audience at all is actually, I'm very thankful for it. Today we're going to be talking about building complex UIs with a server-driven React app. So nowadays when you put server-driven and React together, people seem to always think that that means RSCs.

Now the React community has been dealing with a bit of a split over RSCs for the last couple years, and if we were to draw a Venn diagram of the community, roughly there's the people who are excited about RSCs, there are the people that are sick of hearing about RSCs, there's React Native devs who are confused about RSCs, and so these people, this group, are here thinking this is an RSC talk. This group has skipped this talk thinking it's an RSC talk, and this group is just confused. Regretfully or happily, I am going to confirm that this is not an RSC talk, so effectively what that means is this group is disappointed, this group is also disappointed, and this group is confused.

Basically what I'm trying to say is I excel at disappointing, so you're all in for a ride. So let's jump into it. Server-driven UI.

We're going to look at how it works, when you should use it, and some of the challenges around having a server-driven approach. Let's imagine we've got an e-commerce store. This is a typical layout that you might see in an e-commerce store.

So at the very top we've got a banner with some information about sales or some contact details. We've got a header with a menu, some offers at the top, and as we scroll down, there's going to be a grid of products, and then we'll see some featured categories, followed by just some basic static landing page-y stuff like testimonials and a footer. Now, this is a typical layout, and if we wanted to look at what the code would sort of look like, it would be something along the lines of this.

This is very standard React code so far. So we have a home page, which is just a component. You'll probably know the style of whether I like functions or consts.

And then within it you'll have a banner, you'll have a header, offers, recommended products, featured categories, testimonials, and the footer. All is fine and well until a PM comes to you and says, can you swap the offers and featured categories section? We've actually run some experimentation, and we think that the orders should be switched.

Not a big problem. You go ahead, remove those two components, and replace the order of them. And you deploy that, you push that, and all is well and done.

A few days pass, that same PM comes to you and says, hmm, you know, having that banner above the header doesn't make a lot of sense. Could we just move them around? So could we flip them around?

So once again, you go into your code, same component, it's not much work, but you just have to go in and manually change this every single time, reframe the orders, and then do another deploy, push it, and those changes will be reflected to the app and the order of the layout. A few weeks pass, and the PM comes back again, and at this point, you're just shivering every single time he approaches you. And he says, the banner gets annoying after the user has seen it once.

Can we turn it off for logged on users? A little bit more of a complex request here. So what you do is you go ahead and you change some of the code, and you add a const that gets the users with, like, a user hook that you may have, and then it basically checks to see if the user is not logged in, and then only it displays the banner and will change the banner logic to dynamically render that, only if that Boolean is fulfilled.

Fine, a little bit extra work, but all is fine and well. So then another week passes, and this PM comes back to you and says, you know what, actually, we've decided internally that we want to be able to personalize everything, the orders, the recommended products, the offers, everything needs to change around, and I want to do this on a per-user basis. And at this point, your house of cards of a code base starts to shatter and fall apart, and you are angry, considering getting a new job and resigning.

Now, what if I told you that there was actually a paradigm that could stop all of this madness and stop all of the stress that you've been going through? It could be good for something like this in this use case, and that paradigm is exactly server-driven UI. So the idea with server-driven UI is that you allow the server to define the layout of the page.

That lives on the server side, and effectively, it describes the layout as you would in JSON. So that example on the far right there, you've got the component, and then it lists what props that component needs access to. So for the banner, you have some information around contact details.

For the header, you have a menu prop that's got an array with different routes and their URLs. And so you create a layout component that receives this JSON and effectively renders the page in any order and variation that that JSON is. So it's flexible and amenable to any changes within the JSON layout.

So in practice, what that means is we start with a components.ts file that imports the different components that live within your code base and creates a map of them, saying the string banner that comes from my JSON backend or comes from the JSON response that's coming from my backend or my CMS maps to this specific component in my React code base, and the header maps to this specific component, and so on and so forth. And this component map feeds into a render components function, and this render component will take in a config and effectively look at the config map and determine what component it needs to render and then pass the props through.

And then when you've got that JSON response coming from your API or your CMS, we get the JSON response, and then we use a loop to go over the JSON data and call that render component to render the entire page, and that's all being done dynamically. So when you put these two together, what you end up with is the final layout of the page, and that is dynamic and it's flexible to what's coming from the backend or the CMS and doesn't require you as the frontend developer to change it. It's all being handled by the CMS. So this is nothing super new or special, and this can come in different shapes and sizes. So a common approach is to use it for the entire page, right? So you can lay out the entirety of your page and do that via JSON and control that by JSON. But it can also be used for sections of your page, so a small dynamic changeable section of your page.

Or it can be done for individual components or even parts of components. And all of this is good in theory, but it will probably be leading you to think, well, what are the use cases where I should actually use server-driven UI? And I think the best way to answer that question is to look at who's using server-driven UI in production today and try to get some inspiration about the reasons that they've gone for this approach.

So a few key users of server-driven UI include Shopify, Airbnb, and Lyft. So let's start with Shopify. Shopify chose server-driven UI specifically for their Shop app.

So for some context, the Shop app is an app where it kind of acts like Amazon. Every single... A bunch of different store vendors will come in, and they'll create a store of their own, and then they can list items and sell them through this single app.

And so it means that users can go in and purchase from a single place, effectively, for a bunch of different brands. And as the Shop app grew, Shopify realized that high-selling vendors with many products have different requirements to smaller stores with only a handful of products. It doesn't make sense to have the same layout of a store for a top-selling clothing company that's got hundreds and hundreds of products and some bestsellers and some offers in different categories, and use that exact same layout for a small boutique shop that's being run from someone's garage that might have five products.

So they needed a bit of flexibility there. And then at the same time, business stakeholders decided, we want to personalize this and run A-B tests, and they were also slow at releasing. So those were the three primary reasons why they wanted to go for server-driven UI.

Airbnb, on the other hand, had a problem where their applications across web and mobile had different user journeys. So Airbnb had to support a guest platform, but also the host platform. So most of us have been using the guest platform, but really, there's also the host platform.

And it's largely using very similar API components and primitives, but effectively, they wanted to be able to share as much of that layout as possible to reduce rework, because maintaining two separate platforms is quite costly. And separate to that, they slowly were introducing new features like experiences. And they were, by and large, very similar, but there were still subtle differences, and they wanted to be able to manage that in a scalable way.

They were having slow development cycles, so they wanted to expand that. They wanted consistent UX across different platforms, and so that's one of the reasons they went for server-driven UI. They could have gone for React Native, but that's a different story.

And they wanted to reduce the client-side maintenance overhead. And lastly, Lyft. So Lyft has a slightly different story, which I think is an interesting approach.

Lyft found a small portion of their application that was quite dynamic and was changing with fast user requirements that were coming in. So they started off, Lyft has a service where you can rent bikes, very similar to other products like Lime and Dot. And so Lyft started out with scooters, actually, and then slowly but surely, bikes got introduced.

And so they wanted a way where they could change the layout and change some of the flows within just a single component, which is that bottom sheet component that you can see. And so they started off with scooters. They added a little bit of variation for the regular bikes and then the docked bikes.

And only that small component started off as a server-driven UI. So they went from small to large as opposed to large to small. And they expanded that, and they isolated it to certain features or capabilities and slowly expanded when and if they needed it, which was lower maintenance as opposed to a full migration.

And they wanted to reduce app updates and increase developer velocity, right? So really, the common reasons that we're seeing is you have a lot of different layouts and variations. You want to go to market quicker.

You want to be able to release features quicker. Maybe you have some user personalization needs, and you want to support consistent UX across different platforms. In some cases, your marketing team might need A-B testing, and requirements are changing fast.

So those are kind of the common themes. And for you, if you see these things happening within your project, it might be a sign that you could use server-driven UI as an architectural paradigm on the front end. Now, when you take the complexity from the front end, from the client side, and move it to the server, because that's the fact that we were removing it, what that also means as a side effect is that you have lower front-end complexity, which means you basically have less JavaScript code, and that results in better performance for the client side because you're taking down the amount of JavaScript that you need to ship to clients. That's great, right?

But this actually leads us very nicely to the challenges section, which is by taking complexity from the client side and moving it to the server side, you do have lower front-end complexity, but you inherently have higher back-end complexity. So I refer you to the law of conservation of energy, which states energy cannot be created or destroyed, only converted from one form of energy to another. We've all seen this in, I'm presuming, high school, if everyone follows the same educational curriculum, which we most definitely do not.

But a variant of that, which I really like, is the law of conservation of complexity, which says complexity in an application cannot be reduced beyond a certain point. It can only be shifted from one part of the app to another. And so this is a spin that I quite like, because this complexity in any app will not just magically go away.

You can move it from one part, shift it to another part, and try to balance the scales of complexity, but it will require you to adapt and handle that in your own way. And so this leads nicely into these challenges. So firstly, testing and predictability.

You've added a new layer of JSON API responses that need to be tested, and you have a schema that you need to make sure that the server is conforming to. And so you'll need to add a layer of testing to support that. And as you add more and more server-driven UI to your application, there's more surface area for edge cases to occur, right?

So there's almost like an upward trajectory of different combinations, right? The more flexibility that you have to pair UI element A with B with C, and all of the different permutations of that, there's more possibility for weird edge cases to arise. And so as the amount of server-driven UI increases, there's more surface area for errors, and hence you need to make sure that you're testing and accounting for all of those.

Bruno, who you may know from N26 and different conferences, he put it really well, which was that they use server-driven UI at N26, which is a challenger bank here in Europe. And the main challenge that they face is that it becomes a black box in terms of the front-end code. You're receiving JSON responses, and they're being rendered programmatically and systematically.

So you never know what's actually being rendered just by looking at the code. It's dynamic, and it's largely dictated by what comes from the server side. So it is adding a bit of complexity and can make DevX tricky, but you need to do the right testing and architect your app for the edge cases to be able to account for that.

And what do we mean by saying architecting your app for the edge cases? Well, there's two levels. There's one on the component level, which means that you need to make sure that your component is flexible in terms of the data that it will receive from the JSON.

It's handling things like internationalization, and the flexibility of the styling is probably the biggest one, which means as the layout changes, does the component make sense being displayed and rendered in different scenarios? Does it conform to the different styles, let's say if you render it in a row or in a column? Does that flexibly change and adjust the styling, and so on and so forth?

But also on a layout level, you need to consider the different combinations of components together as well and make sure that the ordering and the layouting makes sense and know at what points to add restrictions and not go for a fully server-driven approach. On the other side, you've got caching and offline support. To have offline support in your apps, you're going to need to cache the server-driven UI responses because your UI is being orchestrated by that JSON.

So then the question arises, what do you cache? Do you just cache the layout or parts of the data or all of the data? And then there's a question of how efficiently you can cache that.

How and when do you invalidate that cache? So do you invalidate it on internet connection? How much of that data do you keep?

How much of it do you override? So there's a lot of questions around how you design that cache. And if you do allow the user to change the state offline, then you need to sync that state back over to the server.

So that's a little bit more complexity added there. And then there's error handling the cache misses. So what if, for some reason, the cache has gotten purged?

How do you recover from that? How do you make sure that the app fails gracefully when there is no cache for it to render any of the UI or parts of the UI? So these are all considerations that you're going to need to think about.

And a really cool project and a great blog article that I would recommend you read is Project Lightspeed, which is about the re-architecting of the Messenger app by Meta. So previously, the Messenger app grew in terms of size. And that client code base became very, very complicated.

And there were different teams coding it in very different styles. And it wasn't extensible. It was slow.

It was clunky. If anyone used Messenger back in 2017, 2016, everyone remembers how clunky it was and how bad it was. And so the idea was, what if we took the majority of the logic on the front end and shifted it to a SQLite server that lives on the client?

And that coordinates with the back end. And all of the UI state and the styling of the UI is stored in a database in terms of how the layouting is done. And so this is a really good example of server-driven UI done right for the right reasons to reduce complexity at a very large scale.

So as we've been talking about code bases grow as well, one thing you need to consider is a lot of JSON is being passed around now because you're storing so much data in JSON and sending it out of the wire. So as the size of your pages and components grow as well, so does your JSON response payload size. And so the natural answer for anyone that's been doing server-related React will be, well, could we stream the UI or the layout to a certain degree?

So let's look at the streaming example and see how this would work. If we go through basic server-side rendering without any form of streaming added in, roughly with a server-driven UI approach, what we would have is we would have a long time to fetch some data. And then we would render those components and the layout on the server.

We'd send it to the client. That would load the code. And at some point in that process, it does the first contentful paint.

Then we run hydration to make sure that it's interactive. And only then we'll have the TTI. And so that's a long time before you have your FCP because you've got a very computationally expensive JSON object to calculate before you can even start to render on the server-side and send that over to the client.

So that pushes your FCP quite far out into the future. And then the TTI is also affected as a result. But what if we went with streaming?

So let's start with the streaming example. And we say, let's assume that we don't send all of the data or we don't fetch all of that data to start with. We just render the basic layout.

So none of those props being passed. We just render that on the server-side. And we immediately pass that to the client.

And we load that JS bundle and hydrate. And at some point here, suddenly the FCP is occurring. So that's significantly better.

And then in parallel in the server-side, we'll fetch for the different data for computationally expensive components. And then we'll render each of them when they come through, load the JS, hydrate, do the same for component B, and then go through the same process for the final components. And once all of that is completed, we'll have our TTI.

So what does that mean in effect? Well, if we look at kind of a graph, as the size of pages and components grow when you use streaming, it really kind of stays constant. It marginally increases, but it's not very noticeable.

It's quite negligible. But if you're using basic SSR, that number can increase quite significantly. And the same with time to interactive.

There will be a growth in time to interactive, in the sense that your streaming time is limited by the slowest loading component that you have, because they run in parallel. And your TTI is achieved when your final component that needs to be computed is ready to run. But that is significantly better than not using streaming at all.

And so in practice, what we then need to do to have this with a server-driven UI is we'll need to take the JSON API and slim it down. And what we'll do is we'll make a smaller JSON without the actual component data, just saying here's the layout with some base level styling to almost get a skeleton working. And once that's done, we'll render the components.

And within each of these components, we can actually look through and see within each of these components, they will be responsible to fetch their own data. So the offers component, which is a computationally expensive component, will fetch its own data, maybe make a database call, and return that once it's ready. Now, this may seem slightly familiar to you guys.

So I lied. There is a little bit of RSC in this talk. And this is a little awkward.

You see, it turns out that RSCs and server-driven UI kind of go hand-in-hand with one another. They fit very well together. And it's all part of a story where RSCs almost complete a part of the server-driven UI story.

It's a subset, and it's a part of tooling that allows you to optimize server-driven UI and make it highly performant and efficient. And I think Evan put it really well, which is RSC is just a small part of the universal server-driven UI story. So I'm very excited to see how RSCs and the use cases for RSCs morph and evolve over the next few years to fit within a larger server-driven UI paradigm.

And this is a pattern in which the whole story can be seen more holistically, rather than just looking at RSCs in isolation. Thank you very much. And that's my Twitter and LinkedIn, if you want to stay in touch.

[Christophe]
Thank you, Mo. Please come in. Can I have some light on the?

[Mo]
Am I not allowed to sit on this one?

[Christophe]
You are very much allowed, or requested. To sit on that one? To sit on that one.

Can I have you? Oh, there you go.

[Simone]
Yes. OK. Everywhere.

All right. So let's start with some harsh subject, which is about Crane, who's going to talk tomorrow. So you're going to have a fight tomorrow on stage, probably, or not.

Oh, I see what you mean. About, I'm just quoting. So less client-side code leads to better performance, as you said.

But is that really true? I mean, what if we go through spotty connections, or have the classic mobile issues?

[Mo]
I mean, that's going to be a restriction anyway, right? So there's a balance that I think you need to play in terms of those core features, and especially if we're talking in the mobile world, those core features that live on the client at any given point, versus those features that live on the server, as an example, and know where and how to cache it correctly. And I think that's where the caching functionality comes into play.

It is a trade-off. So what are you optimizing for? Are you optimizing for latency?

Or are you optimizing for code execution? And I think trying to optimize for network availability is a losing battle, because it's highly dependent on the user's state. So what you should be optimizing for is for the actual performance and how small you can make what you're shipping over the wire, so you're not reliant on the network anymore.

[Christophe]
You're going to combine both, though, anyway. You can optimize for execution when you have a reliable network and do some service worker-based specific caching.

[Mo]
And that's where the caching story comes into play.

[Christophe]
Yeah, definitely. I have this question. You're a big React Native fan, which is your biggest home, basically, in terms of tech.

[Mo]
That's where the heart is at.

[Christophe]
Yeah, exactly. So how do you say that what you just discussed sort of translates in the React Native world?

[Mo]
I think it's far more interesting in the React Native world, actually. In some capacity, this approach makes a lot of sense for React Native apps for a few reasons. Firstly, in the React Native world, contrary to the web world, you have restrictions on the frequency of how quickly you can release because you've got the app stores fighting you at any given point.

And so this is a really nice way to circumvent that process. You can do that in React Native with over-the-air updates, but I think this is a way to iterate very quickly as well. Beyond that as well, I think that a lot of these complexities that we've discussed, there's a few paradigms that people are talking about on the React Native world, which is quite interesting.

Some people are saying, can that server actually run on the phone? Where does that server need to exist? And how is that rendered?

So there's a lot of interesting questions happening in that space. And I'm excited to explore that a bit further. But it's very tied into the whole RSC conversation on React Native, which, like we said, people are seemingly confused about for now.

[Simone]
A third, maybe last question. How does end-to-end testing work in this case?

[Mo]
I think end-to-end testing becomes quite important. I mean, there's a few approaches you can take. You can either mock the JSON that would be returned from the API and assume that that's correct, or you would need to.

So the testing story, in the ways that I've seen it, becomes having heavy API tests running on the output of APIs given a certain input in. Obviously, that's reliant on what the PMs, quote unquote, are changing. But you can add some level of flexibility to make sure that certain things are adhered to.

Let's say you don't want to necessarily lose components. You have the set of components. They can be rearranged, but you don't want to lose them.

Or you don't want your header to be beneath your footer. So you can encapsulate a lot of that logic inside of API tests and fail them there. And then in the end-to-end story, it's a question of what your philosophy is, I think.

Do you want to run end-to-end tests with actual data coming from the JSON APIs? And if you do, well, there might be some risk in terms of things changing there. But maybe you want to catch that, right?

So it's a question. But I think the whole end-to-end game at the end of the day is dependent on whether you want to use real data or not. And that's a story.

Whether or not you use server-driven UI or not is just maybe amplified by the fact that you're using a server-driven UI paradigm.

[Christophe]
Thank you very much, Mo. Thanks for having me. Mo Gazzelli, everyone.

Thank you.