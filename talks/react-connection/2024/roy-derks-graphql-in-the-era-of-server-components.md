---
slug: /talks/react-connection/2024/roy-derks-graphql-in-the-era-of-server-components
date: '2024-04-22'
title: GraphQL in the Era of Server Components
author:
  - Roy Derks
video: d0vugg96PME
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/d0vugg96PME.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
[Roy]
So, my talk will be about GraphQL and the era of server components. There's been lots of discussing around GraphQL, do I need it, do I don't need it, and then there's the same sort of discussions around server components. So, a bit about me, my name is Roy, I used to work at a GraphQL start-up called Stepsen, and then we were acquired by this small company that you might know as IBM.

I've also been doing lots of things in the, well, ever since I started coding, and a lot of different topics, a lot of different sort of start-ups I built and created, and then besides those things, I also created content. So, maybe you saw some of my books about React or GraphQL. So, if you have any questions about those things later, then please let me know.

And I also tried to create some content on YouTube. I don't make any money out of it, so it's just for educational purposes. So, I'm going to ask again, who of you has ever used GraphQL?

Okay, that's not that bad as Christopher made me think it was, so that's good. And then I think a follow-up question, like how many of you work in a company with, I don't know, over 50 developers? Some of you as well.

Okay, well, that's good to know because as you'll learn in this talk, maybe if you work at a small start-up, you don't even need GraphQL, or maybe it didn't even appear to your mind to look at this technology. And then a follow-up, who of you has used server components? Doesn't have to be production, but just try it out, maybe even in a code pen or whatever, and see if you like it.

Okay, that's good. So, there's been much debate about both technologies amongst developers. I saw a ton of memes.

I also saw a ton of blog posts about people who have opinions. I have opinions myself as well. This entire talk is opinions.

And hopefully, after this talk, you'll have your own opinion. I mean, don't take my opinion as the absolute truth, because it isn't. And other opinions aren't the truth as well, they're opinions.

So, you have to form your own opinions, and I'm just here to help you learn. So, the first thing I saw about server components was actually this picture, like someone trying to make a SQL call directly from their UI. This is something I don't really feel I want to do.

Maybe it makes sense to do it at some point, but for me as a developer that is known to write APIs, write frontends, bring them together using fetch calls, calling a server from a UI doesn't make sense to me. Maybe if you use SQLite, it makes sort of sense. So, this is the debate we mostly see about server components, and I wonder if developers actually need it, or it's something that larger companies feel they need because they have a million concurrent users.

And then GraphQL has, well, similar discussions, where a lot of developers might say, you don't need GraphQL. And if you need GraphQL, also, it depends. Like with all technology, it depends.

It might suit your company well, it might suit your team well, because, well, maybe someone in your team really likes GraphQL. If I would join the team, I would probably tell them, I want to use GraphQL, even though it doesn't make sense. And that's because I'm used to it, I know how to write it fast, and it makes sense to me.

It doesn't mean it makes sense to you or makes sense to other people in your team or company. So, you always need to compare these technologies. You need to think if they make sense to you, to your project, to your team, or to maybe the vision of your department or whoever is in charge of making sure you get time to work on code.

So, if we want to compare, or if we want to see what's the need for GraphQL in the era of server components, maybe you think we need to compare GraphQL and server components, because they're in the same sentence, and maybe I should compare them because they're both... Yeah, maybe they're both the same thing. I don't think they are, but maybe they do.

I'm from the Netherlands, and in the Netherlands, we have a saying, like, comparing... If you want to compare things that don't make sense, we say it's comparing apples to pears. I mean, they're both fruit, but that's about where it stops.

They both have small seeds in it, and they grow in a tree. That's sort of the things they have in common, but there's many differences, and you can use them for different things. They're not the same sort of fruit, even though you can both eat them.

So, to my opinion, like, comparing GraphQL to server components is something similar to this. It doesn't mean that we can compare use cases, but we shouldn't compare the technologies one by one. So, GraphQL is an API specification telling you how to interact with APIs.

That's why we like to call GraphQL the query language for APIs, and server components are for rendering HTML or UI server-side. So, even though you can say they're both APIs or specifications, and they like to do things server-side, they're not the same technologies, and they shouldn't be compared one-to-one. And to figure out if we can match use cases and see if maybe using them for a similar purpose makes more sense, let's have a look at GraphQL's original intent.

So, GraphQL is quite old. It was designed in 2012 already, and there's a really nice documentary about it. If you Google GraphQL documentary, you'll find it.

They had a problem at Facebook because they had a lot of users. They had old mobile phones, mobile phones of really low bandwidth, and they had different applications running on different systems. So, they were looking at an API specification that would make more sense to them rather than building a ton of different APIs or changing the API requests, or actually the response, for different use cases and for different applications.

So, one of their needs was they wanted to reduce transactions between front-end and back-end. And this is something that you can also say of server components. You want to reduce the amount of transactions between front-ends and back-ends, or maybe you want to reduce the amount of data that's being trafficked from your back-end to your front-end or the other way around.

So, if you think of this application here, it's a mobile application. It fetches data from three different REST APIs and it shows all the data on a single screen. If you're doing this, you maybe wonder why shouldn't I have a single API request that gives me all the data I need?

So, in GraphQL, this is something we call underfetching. You don't get all the data you need from a single request, so you need to do a second or a third, and GraphQL solves this. And before I'm going to show you how it solves this issue, I'm going to show you another issue that is quite common.

And this is where you're sending all these requests to different API endpoints and you're getting a lot of data. Like, each of these endpoints will give you maybe 10, 20, or 30, or 40, or even more lines of code. And it's not really code, it's JSON.

So, you're loading all this JSON into your mobile app. And if you think back in 2012, it was pretty hard to load all this JSON in a mobile app with not even 5G. Maybe we had 3G or maybe we had less than 3G.

So, this is something we call overfetching. You're fetching too much data. You don't need all the data.

Maybe you only need 2 out of 100 of the fields you're getting in your application. So, we have underfetching and overfetching. And this was the original intent of GraphQL, like solving these issues because data wasn't as cheap as it is today and the phones weren't as fast as they are today.

So, reducing the amount of transactions and reducing the amount of data that's being transferred between your backend and frontend was a valid use case for GraphQL. GraphQL solved this by having a single endpoint, so you don't have to send multiple requests anymore, and flexible data structures. So, you as a developer, you're able to request only the fields that you need and thereby making sure that your response only includes the field that you actually wanted instead of all those fields that you didn't want to have.

So, it works like this. And I'm going through this a bit fast because I'm hoping you heard about GraphQL. It's been around long enough, but still, I always enjoy refreshing your memory as well.

So, GraphQL is all based on a schema. And this is something that a lot of REST APIs don't have. They don't have a schema.

Maybe some of you are using OpenAPI, but I'm assuming most of you don't. So, the first moment you find out what information is available from a REST API is probably when you actually send a request to the REST API and look at its response. For GraphQL, you would have a schema, and in the schema, there are definitions of all the data that's available and then of all the ways you have to extract this information from the GraphQL API.

So, the schema describes the data structure and it describes the way to retrieve the data, which could be queries or subscriptions or mutations. Then whenever you send a request to the GraphQL API, you define your operation. In here, you define which fields you want and only the fields that you want.

And this is very useful, and I'm going to tell you why it's useful later, but it's most of all useful because this makes sure that you don't request more data than you actually need. So, you're not filling your UI with all sorts of fields of JSON that you won't be using anyways. And then you can set parameters to make sure that you only retrieve specific IDs or titles or whatever you put in there.

And then your response format is always the same as your request. So, this is quite handy because, like I said, most of you probably send a request to a REST API and then only when you look at the response, you know what data to expect. And it's the same for me.

Most REST APIs I work with, they have docs or they have maybe, hopefully, open API specifications, but more typically, they don't have any of this. So, the predictable return results is, for me at least, a really handy part of the developer experience. And this also brings me to the second intent of GraphQL.

And this is helping you to reuse your data. And this is useful when you have multiple applications, you have multiple use cases, you maybe have multiple backend teams or multiple frontend teams consuming your data. And if you would need GraphQL for data reusability or for data anyways, it really depends on your use cases.

So, let's assume you have a single API, you have a single application. Could be web, could be mobile, could be whatever. In this sort of one-to-one use case where you have one API and one web application, you probably don't need GraphQL.

I maybe won't even use GraphQL here. I'm, well, next to really liking GraphQL, I'm also a TypeScript fan. So, I would probably look at something like TRPC here.

And this is where you would define all your data and types pretty similar to how in GraphQL you define your data in a schema. And then you'll be able to create type-safe requests from your application. And this is a good way to make sense of your data because that's something GraphQL does as well.

It helps you make sense of the data you have available and improving the developer experience by having a schema for your data. So, in this use case, I might not use GraphQL because you have a one-to-one relationship and you're not getting the full benefits of having the GraphQL schema. So, whenever you start adding more applications in a mix, maybe you have a mobile application that does somewhat similar things as what your web application is doing.

And maybe you also have like an admin app. And this admin app could be as simple as the example we saw from Airbnb. You have people renting the apartments and then you have people renting out their apartments.

They have a similar application, but it's slightly different that it might have slightly different data needs. And you don't wanna be spinning up different backends for all these different apps. So, GraphQL is good at giving you a single API for these end-to-one use cases.

Because if you don't spin up one API that you can reuse and you need to filter out data, you need to normalize or you need to combine it, I start to worry like where is the heavy lifting gonna happen? It's probably you like front-end developers in your React app messing with estate management, messing with normalizing data, probably writing the same functions as that a mobile developer might be writing to filter out or combine data in their own applications. Because if your backend is a unified backend, but it spits out a lot of JSON and you need to filter and combine it, you're putting a lot of heavy lifting on your front-end teams.

So, you need to process it maybe up to three times or maybe more, maybe you have 50 applications using the same APIs. And this is something I saw happening. So, I introduced GraphQL at the city of Amsterdam.

So, the city of Amsterdam has quite a large open source department. And we had about like 200 different APIs giving you information about the city. It could be traffic, could be available permits or parking spots or garbage collection.

And all these APIs were consumed by like over 20 different clients. And they all had slightly different data needs. And before they were all doing the processing on normalizing of the data on their own.

When we introduced GraphQL, they only had one API to call and it didn't have to normalize this data and combine it. So, GraphQL solved this end-to-end problem where you need to combine data from different data sources and you need to normalize and filter them in all your different clients. So, this is a pretty popular use case for GraphQL where you would use it instead of having to build all these different, well, sort of normalizing state management setups in your different applications.

Or also, if you have been using GraphQL and you are a part of one of those companies that has more than 50 or 100 different developers, you might've been using GraphQL in a setting like this where different backend teams all create their own GraphQL APIs and then one big GraphQL API pulls it all together into a single setup. And this is something we did at the city of Amsterdam as well and that I've done and a lot of different companies helping them to make sense of their data. Because if you use GraphQL like this, you don't only get the benefits on the front-end side of reducing traffic, but you can also reuse all your data across different clients.

So, this is pretty useful as a front-end developer. And if you're only working on one front-end, you maybe don't see these kinds of benefits, but they are definitely there. Because if you remember the schema, you would have one schema that would serve all these different applications.

So, in your top app, you might be using product and you only wanna show a title and a thumbnail. And maybe in a web app, you wanna show all these other fields. You wanna show reviews or more than just a title, or maybe you wanna show offers if you're building a marketplace.

And all this data is available in your GraphQL API. So, any client connecting to it can make use of the available fields there. So, when every front-end can reuse data from a single endpoint, you're gonna save a lot of time long-term.

But the important thing to emphasize is it says every front-end. So, again, if you're building a single front-end, you may be better off with your PC or server components or maybe no API at all, because you can just build it all in API routes if you're using something like Next.js or Remix. And in this case, where you're building these sort of different front-ends that consume the same back-end, GraphQL can act like a BFF.

And this is not your SpongeBob best friend forever BFF. I hope you all have a BFF or at least a couple of them. But this is a back-end for front-ends.

If we think back, if you have all these different front-ends and you're building functions to normalize data and to make sense of the data, you're almost building small back-ends inside your front-end apps. And this is something I feel you need to prevent from happening. So, this made a lot of sense in 2012 when GraphQL was first designed, and it still makes a lot of sense today.

And this is one of the reasons why we have server components, because we have back-ends. The back-ends might not give the data in a format or shape that we want to, so we need a place to normalize and filter and combine data. And of course, you want to reduce the amount of transactions between a front-end and back-end to keep performance high and limit the amount of bandwidth that we need.

So, you can also say that server components could be BFFs for all your different APIs. And then again, if you have all these different front-ends, you probably don't want to be writing server components in three different places that end up doing the same thing. So, if you have multiple back-ends, please don't try to do the same thing in each of your front-ends where you're trying to filter data and combine it.

So, it makes more sense to have React server components maybe as your single API, where you would have a database, you have some services which could be REST APIs, and from your front-end, you're using server components to create the UI on the server and then send it to your front-end. But then again, you might end up doing something like this where you skip your back-end as a whole and build everything in server components, which could be good, but maybe look at your PC if I were you and you're using TypeScript. So, GraphQL has some other upsides, especially when you're using GraphQL clients.

So, they can help you with caching or state management or any of the things you're now doing with different libraries. And some of these libraries are more heavy than other libraries. Personally, if you use GraphQL, try to use something like Relay because it really transforms the way you're using GraphQL and brings it to a higher level because most of these libraries, they just treat GraphQL like any other API, whereas Relay is really helping you get the most out of the reusability of GraphQL.

With GraphQL, you can also generate TypeScript types from your GraphQL schema. So, if you remember the schema, it has all the types that are available for my back-end. It has all the ways to extract data from this back-end.

And one thing I can do with a set of open-source libraries is generating functions to call this data in a type-safe way. I can also create typings for all the different fields that I have in my schema. So, if you have REST, you typically cannot do this, meaning that you need to write all the types yourself, which could be fine, but there's no way to automate this unless you have an API specification.

And then the final thing I want to share with you is how GraphQL works together with AI. You might have seen the GraphQL schema very briefly and you know there's types in there, there is ways to extract data in there. And this is actually quite useful because the GraphQL schema gives you all the information you need to interact with a GraphQL API.

This means that if you're building something with an LLM, the LLM can read the GraphQL schema in the same way as you can read it because the schema is pretty much natural language. So, let's assume you're trying to build a system where you ask a question like, when will my package arrive? You pass this to the LLM.

The LLM cannot make sense of your question. Look at the GraphQL schema. I can maybe match package to a way to extract package information from the GraphQL API and do the function calling for you.

So, this is something I'm working on at the moment. If you want to know more about the cool things you can do with AI, then make sure to find me at the after party. But GraphQL is pretty good at this as it gives you a way to see what's in the schema.

So, to recap, the biggest outtake is don't compare React server components and GraphQL. You can have similar use cases. You can compare the use cases but don't compare the technologies because there's just too much that you can't compare for both.

I have one slide here showing you why. So, GraphQL is really good if you want to reuse your data, if you have multiple frontends, multiple backends, and you don't want to create all these functions to normalize and combine and filter data over and over again. So, it's declarative, meaning that you have the schema, there's lots of tooling around it to extract information.

And as this is mostly natural language, AI can also make sense of all of this. And you can't compare them because, well, server components are for rendering server-side UIs, HTML, and GraphQL is for building APIs. So, they serve similar use cases, but they are very different.

So, with that, I'd like to thank you and I hope to say hi again.

[Christophe]
Thank you, Roy. Please come along. I don't know if Simona is around.

Yes.

[Simone]
Yes, of course.

[Christophe]
Good. So, I've got a number of questions from the audience. I'm actually going to probably wrap three in one because they're like different takes on the same underlying question, I think, when someone asked, how can we handle scaling large applications with GraphQL?

Someone said, does it make sense to use GraphQL as a solo dev or small team, which you partially addressed. And someone said, how do you deal with the potential overhead of using GraphQL? So, this seems to me like three sort of ways of expressing the same question.

[Roy]
Yeah. So, my biggest advice would be if you really like GraphQL, use it, because, well, if you like technology, try to use it as much as you can. You really only get the upsides if you either have multiple backends and you're trying to federate them.

So, that's how you call it when you have microservices and you combine them into a GraphQL schema or when you have multiple frontends that need the same data, but they need it in a slightly different way. And then if you want to scale this, then I really look at Relay because Relay will help you to not only handle calls to the GraphQL APIs, but it'll also help you to handle the data flows in your application in a nice way that is really better than making a call to a GraphQL API, because maybe you know, maybe you don't know, GraphQL is usually served over HTTPS. So, calling a GraphQL API is like calling a REST API.

The request is just slightly different. And a lot of GraphQL clients, they just do the REST way of calling GraphQL over HTTPS without the benefits of the data flow. So, I'd say a combination of make sure you have multiple frontends or backends and then using Relay on the client to make sense of this whole technology together.

[Christophe]
Yeah, because Relay is one of the techs for doing GraphQL on the client, but it's really focused on like scale resilience, I guess, in terms of complexity.

[Roy]
Yeah, definitely. And there are some good talks giving like different conferences about does it make sense to use GraphQL without Relay? Because like I said, it's just HTTPS usually.

So, you send a request over HTTPS and you get your data back. So, in the frontend, you don't really get all the advantages of GraphQL. You just load less data.

[Christophe]
Which isn't nothing, right?

[Roy]
No, it's a good upside. Exactly what you need is already a pretty good upside. Yeah, but if that's the only upside, then you might think our team knows how to do REST and how to scale it, so why should I even think of GraphQL?

[Simone]
How would you tackle the most advanced use cases and some of the biggest issues of GraphQL like the fact that you are actually posting versus getting in those scenarios?

[Roy]
Yeah, so that's a good thing to distinct. You can retrieve data, but you can also mutate data using GraphQL. I think the upsides are bigger in retrieving data.

Well, probably most of you have used GitHub. So, GitHub has both a REST API and a GraphQL API. So, I would always advise if you're trying out GraphQL, have a look at the GitHub GraphQL API because it's pretty big and it gives you an idea of whatever you can do.

But most of the big companies use GraphQL in some shape or form now. I was booking a ticket to fly to a conference in, what was it again? Oh, it was in London a few weeks ago and I got an error in the page of the airline and then I looked at the network request because I'm a developer when I see an error on the screen, I open a network tab and try to figure out and they were actually using GraphQL.

So, it's everywhere and you might not see it as the user of the website but just open a network tab of your favorite products and see if they're doing GraphQL requests because there's a high chance that they're using it.

[Christophe]
Yeah, most of the Fortune 500 stuff use it at least internally. Even many of the prominent web names use GraphQL at least for their internal API, sometimes for the public API. And when it comes to GitHub, the REST API is actually their v3 API.

So, several years back and their v4 API, which was released like five years ago, is exclusively GraphQL and it's a lot better usage-wise than the REST API. So, if you want all the GitHub API goodness, you're going to have to do GraphQL.

[Simone]
Okay, what about caching GraphQL responses?

[Roy]
Yeah, so caching is always an interesting topic everywhere. So, caching GraphQL is slightly different from caching REST APIs and there's multiple places where you can cache. You can cache on your backend and you can also cache on your frontend, so on your client.

So, a lot of these GraphQL clients that I showed, they will help you do caching similar to how you can do caching with Red Query, for example. It's slightly different because you're caching either operation level fields. So, these are like your queries to retrieve data.

You can also cache types. So, maybe you have a type that is occurring in different places and maybe one request returns products, another returns products as well, but somewhere down the tree. You can still cache those if you're caching on type level.

But caching is always tricky. I think there is, what's the saying? There's like two things that are hard in life, like naming and caching validation.

[Christophe]
And not by one errors.

[Roy]
Yeah. All right. All right.

Thank you very much. Thank you, Roy. Yes, thank you all.