---
slug: >-
  /talks/react-native-connection/2024/aleksandar-andjelkovic-why-choosing-adaptable-technology-matters-strategic-advantages-of-investing-in-react-native
date: '2024-04-23'
title: >-
  Why choosing adaptable technology matters: Strategic advantages of investing
  in React Native
author:
  - Aleksandar Andjelkovic
video: UdiCLPq1T48
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/UdiCLPq1T48.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: '2024'
allow_ads: false
---
### Aleksandar
All these amazing people here in this lovely city and with such a lively React native community. So, let me start my talk with a quote, basically. You might think this is Dykstra or Knuth, but no, it's me and Chad GPT, just trying to convey into words, basically, you know, what is the importance and the permanence of the technology decisions we are making every day.

So, that's exactly what my talk will be about. I will tell you about the big bets the number of teams in Microsoft has made to use React Native on a number of important projects that are used by a million of people across the world and how it helped them move quickly and also have a strategic advantage as the technology moved and changed quite rapidly in the last period. So, I'll divide my talk into two parts, talking about adaptability and about the strategy.

And when I talk about the adaptability, I will talk about the technical reasons behind why you should use React Native. When, on the other side, when I talk about strategic reasons, I will talk more about the business and reasons lying behind why using React Native is the right choice for you. So, and the main purpose of this call is to give you all a set of reasons and considerations on your next discussion, where you're making the next big technology decisions, why React Native is the right choice for you, or maybe why it is not.

So, just a bit about me. Mo already done a great introduction. I'm a Principal Engineering Manager at Microsoft.

Previously, I was Engineering Manager at React and Meta, where I supported a team of engineers developing React and React Native itself. That was a great experience. So, adaptability.

So, you know, this is a super minimal diagram showing how React Native looks. And if you take it to the basics, you know, what React Native is, in fact, we all know, it's you use JavaScript to basically puppeteer native UI through a communication layer. So, let's make this a bit more realistic.

You don't just, you know, puppeteer native UI, you puppeteer native modules as well, Bluetooth modules. And on the other side, there is a part of JavaScript logic that you have in there that is dealing more with business logic, not with the UI itself. And we're going to extract that on the right-hand side there.

And we all call this a greenfield app. So, everyone know this, we all use it. And this is the first, basically, dimension of the adaptability of the React Native.

So, what happens is developers write JavaScript code, users see, and interact with the native UI. And, you know, this is the first way how we're speeding up and making development faster. So, if you need to target both Apple and Android, this is the fastest way to develop, basically, your application and go to market.

We all know about this. So, let's go to something more interesting. So, what happens if you want to roll out this application to other platforms?

Let's say, you know, roll it out to macOS or Windows. As most of you already know, there is a Windows and macOS port that was built by Microsoft. And much more than that, it's not just built by Microsoft.

We use it heavily in a number of our applications. We use it to ship Office on macOS, on Windows, working with a huge number of users using production. Windows also has, basically, part of the experience in React Native built.

The start menu is now built in React Native. So, a number of our experiences are using React Native on a huge scale. So, it's more than production-ready.

And more than this, if you want to use React Native on Vision OS, you can do that now, as well if you're trying to use it on large screens. Yes, there is this React Native TV initiative supported by Android that helps you do that. But, you know, let's go a bit further to more interesting areas.

So, let's say you have, you know, a team of native engineers, you have native applications, basically, and you need to develop a new feature. And the only person that you have, basically, in your team who can do work is one lonely React Native developer hero, basically. And what you can do is, yes, you can integrate React Native into a standard native application, and this is what we all in the ecosystem call Brownfield application.

A lot of you know this, but I just wanted to showcase this dimension of the flexibility, as well. So, let's go one step further than this and showcase some of the things we've done at Microsoft. So, let's take our Brownfield app, and let's simplify a bit this diagram, just to be able to showcase this more complex scenario.

So, let's say we have two applications where you need to share different parts of the user experience between them. For instance, you have a contact card that's used in a number of applications, or you have a project screen that's the same at both of the applications. So, you see that JavaScript code on the right-hand side?

What you can do is, yes, you can extract it into a separate code base, into a separate React Native module, and share it between these two applications. And, you know, certainly some of you try this. We are using this very extensively in Microsoft, because a number of applications share the same user experiences between them.

And it saves the amount of, you know, introduces code sharing, saves the time you need to maintain two different copies of the code. It is, you know, beyond useful. However, you know, it's far from simple in Microsoft's world.

As you can imagine, there are a lot of applications, a lot of different experiences that are sharing these components. And we call our environment, basically, many Monorepo environments, a bit of a misnomer. And if you want to learn more about it, there is a good talk done by Lorenzo and Tommy a couple of years ago, talking about how we are organizing our code base.

And more than that, there is a set of tools that we were developing generally for the community, but also for these more complex use cases that you can check out if you're interested in the RNX toolkit, or just watch another talk by Lorenzo and Tommy from last year, just talking about all the tooling that was built. So let's take it one step further. So let's say you have basically, you know, React Native standard Brownfield application.

And, you know, what's happening, if it is a Brownfield application, you usually would boot up React Native at the beginning. But what happens if the screen that you're basically using React Native to develop is not the first screen? It's like a couple of screens deep, and it's only used by a certain percentage of users.

So what can you do? You can modify the comps layer. And, you know, if you didn't already check out React Native Host, please do.

I believe a lot of you did. Gives you more flexibility to understand where you can initialize React Native communication layer. So you don't pay the price at the first load of the application at the first render.

So let's take a bit more realistic example where this is really useful at Microsoft. So let's say you have not one, but you have three different screens in the application that are in different levels of the navigation, at least different basically levels of depth. You can create these custom layers that are customly basically booted up on the layer level of navigation minus one that will boot up this screen, and they're tore down when you don't use them.

So you reduce basically the cost for the users that are not using them. And also this tailored basically layer enables you to do it more effectively than using a standard communication layer. This is even the final way you can modify React Native.

So let's say that you have a brownfield application, and you developed a new fairly code-heavy complex feature that is basically more on the backend side, much less on the UI side. And you want to port it to a different application. But that other application is a native application, and you don't have any React Native engineer that's available.

Basically you don't want to port, basically what is more important, you don't want to port the UI elements to React Native. You would just want to use native UI, but you want to trigger the logic in JavaScript or TypeScript. This is what we were working on, and this is what we are using internally in Microsoft.

We call it React Native Headless. And this is more realistically how it looks like. So what it enables you to do is enables you to connect native UI directly to the JS logic in the backend without the need to spin up the React Native UI layer at all.

And I cannot talk in more detail about it still because we still didn't open source it, but be on the lookout, there will be a talk in the coming months about it. So there's a lot of talking about flexibility of React Native, and I'm certain quite a few of you are aware of some of these dimensions, but I just wanted to put them in one place. But how does a real Microsoft application using React Native look like?

So we have five applications that are in the showcase, but they are not the only experiences that we use React Native for within Microsoft 4. And I cannot talk about a lot of them, but there are many more other experiences that use React Native for parts of it. So some of those applications are greenfield applications, like Xbox app is a greenfield application, while other ones are much more complex.

They are quite complex brownfield applications that have custom const layers like Word, basically. But they're working really well at this huge scale, so that is what is amazing. It's tested by millions and millions of users, and you know that this scenario works.

And that is the beauty of the adaptability of the React Native, that both of these scenarios are valid, and they are working in production in a huge scale. So it's not that if you do a brownfield app, you're just hacking it around. No, this works, and it works really well for us.

So that was about the technical reasons. But unfortunately, as we know, it's not only the technical reasons that drive the decision-making when you're choosing a new technology. A lot of the reasons that lie behind the reason, behind why you're choosing a new technology are strategical business reasons.

And here, I'll try to talk about them. And I divided all these cases into what I call good strategic reasons. And because I come from Microsoft, I created a three-letter acronym, GSR. Yeah, sorry, yeah. It's a very internal joke. So GSR number one, it's higher ability. This is an obvious one.

This quote is from McKinsey. Even in 2023, which was quite a tough year for our industry, the ability to hire the right talent is still the biggest problem for the companies to grow. And this is not just finding engineers, basically the number of engineers in the market.

You need to find the right fit for your company, for your culture, for the problems you're trying to solve. And that person needs to be excited about the problems you're trying to solve. So, you know, using the most used programming language helps.

Basically, tapping into this biggest pool of talent will help your company grow. And this is why, in Microsoft, React Native grew so much. It was hard to, and in math as well, basically.

It was hard to hire native talent at the scale that these companies needed. And this is why, you know, one of the reasons why we moved to React Native was for that. You know, there was talented new JavaScript, the new React.

It was easier to onboard them. Learning curve was lighter than going and learning the whole native stack, which is quite challenging. GSR number two, it's live.

So, you know, we all know this, but, you know, it's not, you know, it shouldn't be taken easily. React is now more than 10 years old, almost 11. React Native is almost nine.

And, you know, if you look at the JavaScript ecosystem, very few, basically, very few companies are, sorry, very few frameworks or very few libraries are alive at this mature stage. And even more than that, it's not just alive. It's very active.

It's been actively contributed to, you know, the idea of, like, changing the communication layer at this mature stage is very rare. And this is the effort we all know as the new architecture. So, I was there when, basically, we were rolling it out experimentally.

And it's close. We're close to a point where Meta will roll this out as a default. And having in mind how big of an effort this was to address some of the main concerns people have about React Native at this later stage just showcases how all of the, you know, companies, especially the core team, are still very invested in it.

So, GSR number three is the cross-industry synergies. So, this is an interesting one. You know, if you look at the ecosystem within the React Native, it's very meritocratic.

One thing that I noticed is, you know, you go to the Discord of core contributors, you will see people from, you know, who are basically not working in any company, people working in very small companies, a number of small partners that are very active in the React Native community, and the three big tech companies that are very invested. So, what this gives you ability to, if you're an active core contributor, I've seen people coming to the Discord with good ideas that are aligned with the efforts at Meta or basically Microsoft are trying to do, and finding a partner in these large companies or even smaller companies, and rolling out some of the features that you need on the React Native. And this is a very unique opportunity.

You cannot do that in any open-source project. And when you're a team on that, the GSR number four is because it's open-source. It's quite an obvious one.

But just being open-source, it's not a reason by itself enough. So, I'll try to break down why I believe React Native being open-source is a huge advantage. So, the first one is basically, if you go talk with your leadership, it's good to talk about the cost savings, of course, that you will do, that you will introduce using open-source.

There was this basically research done by Harvard Business School. The paper was published, I believe, in January this year. And it's talking about if companies that use open-source tried to develop this open-source in-house, it would cost them three and a half times as much money.

Of course, this is a big study. There are a lot of averages here. So, trying to do that at such a scale is a bit clumsy.

But thinking about it, that's a very true. In some cases, you will save much more. In some cases, a bit less.

But still, it's a huge saving of time and money. The second one is retaining control. So, this might not be a very popular one, and I know it might be a bit controversial as well.

But in some cases, you might need to change, the core of React Native might have some things that you need, and they are not able to roll it out as quickly as you need to. And this is what we needed to do basically in Microsoft when we were rolling out the Mac OS. We needed to fork out and make changes that are needed for the Mac OS, and now we are working to forking it back in.

But we have the ability to retain the control. We had the ability to develop and move fast. But by all means, this was not a simple, not a cheap decision.

So, I'm certain all of you are aware of it. But it's there. And the good thing is, even if React Native is moving in a direction that doesn't align with your project, you can fork as well.

Open source, reason number three. You are part of a big community. As you can see, I was really impressed how full this room was.

And the number of conferences we go to, it's great to see how big and lively the community is. But it's not just about the number of people in the conference, it's the number of downloads. It's also about the number of libraries that are being developed.

It's almost 1,400 libraries now. And these are just React Native libraries. And the number of them that are really well-maintained, you know, like Reanimated, a number of people that were here before me, have really well-maintained libraries that save you a lot of time if you're trying to roll out a feature in React Native.

And that is a huge thing, you know. It's a big and a very active community. So, the fourth reason is, you know, it is React.

And even in meta, we were trying to, you know, bring these two teams together. But it's not because the concepts are similar. This reason is more about, yes, if you're trying to hire someone and they don't know React Native, but they know React, they will be able to learn it easier.

But it's more than that. This is more of a case where you have a company that already has a React team. What you can do is you have opportunities to work with this team and create opportunity to synergize with them.

So, this is maybe more for the medium and larger-sized companies. This is what we've done in Microsoft with the Fluent UI. You know, there was already a team working on the React.

It was working on the React UI components. And then what we've done is we joined the team to be able to roll out the set of components we needed for React Native. You know, creating win-win opportunities in mediums to larger-sized companies is something that is really important part of working in that.

And React gives you this advantage. So, yeah, let's go back to our GSRs. GSR number five is using web code.

And, yes, you heard me right. You know, you heard about strict DOM and what's happening. But I just wanted to share more about it, too.

So, the idea is, even in Microsoft, a lot of the first experiences are usually built on the web because it's easier to iterate. It's easier to roll out. And what happens if you're trying to port, if you're trying to port this into the React Native application?

So, you know, at the moment, on web, you're using HTML controls. On React Native, you're using React Native controls. So, it's not a straight port.

You know there's a lot of work. So, this is where the work on the web API, basically RFC, as well as the React Native strict DOM, is basically, React strict DOM, sorry, is really helping. You know, and we know this is still not, you know, production-ready, but it is something that we are very closely looking at.

And, no, of course, none of these things come with the tradeoffs. We're all very experienced, you know, have enough experience in the industry to know each of these decisions come with a tradeoff. So, let me just talk you through a couple of them.

The first fact is, yes, it is alive. So, if it is alive, it does mean you need to keep up. If you need to keep up, you see where I'm going with this.

You know, you need to upgrade. So, this was 0.68 to 0.72 upgrade, as I remember. And this is just part of the pull request.

It's much, much, much bigger, basically. And, no, it's not easy. The good thing is, I know the amount of effort that Meta is putting to simplify the upgrades as much as possible, but in addition to that, you do have tooling produced by the other partners in the company, as well as Microsoft, that does help with simplifying the upgrade process.

And if you're interested, check out this talk by Lorenza and Tommy and learn more about the tooling that we are developing. So, the fact that you can integrate React Native into an existing project, it does mean that you will add overhead. And by adding overhead, it does mean you're increasing the app size.

We know that you're, you know, increasing the time to first render, basically. So, you know, we need to be conscious about these decisions. They don't come without trade-offs.

The good thing is that there is work. Of course, you know, both the work that Metro will be doing on Tree Shaking. In the meantime, Microsoft has done a Tree Shaker for Metro that will help you reduce the bundle size.

But on the other side, the work that's being done on the new architecture will help avoid some of this overhead. And the last one is, yes, you can integrate in an existing application, but that does mean that you disrupt the equilibrium of the team, usually, because if you're integrating into a native application, maybe your team is full of native engineers. And if they are, you need to get a very wide adoption across the team to ensure that everyone is aligned with the trade-offs coming with React Native, because React Native is not a perfect solution.

And even in Microsoft, we're not using it for everything. So, you need to understand that you need to get alignment from the people who will be working on it, both about the trade-offs, about the problems, because, you know, there will be problems when you start developing it. And when you hit the roadblocks, it's important that, you know, you made the decision very consciously so you can persevere through it.

If you're interested about, you know, everyone knows the Airbnb story and probably saw this article, but if you're interested in learning more about it and the reasoning behind it, I would definitely recommend Mo's talk from last year. It's really good to understand kind of how, if you read the text, you can see a lot of this, but Mo really processes it in a really well, in a really good way. So, yes, that was a lot.

I'm certain you know quite a lot of these things, but I wanted to summarize them in one place and just tell you how we are using React Native. So, let's recap it quickly. So, you know, React Native can speed up your time to market in a lot of cases.

It is incredibly adaptable, as we saw, and definitely we are stretching it to probably its limit, but even us didn't encounter a problem with the technology. It's much more about ensuring that we are doing it in a sustainable way. It can give you a significant strategic advantage, and we saw this when, you know, for instance, the big push for the Copilot was made, having some of our platforms made in React Native enable us to move faster, much faster than, you know, having in mind some of these codebases are more than 30 years old, which is very old.

And, you know, it does come with a lot of trade-offs, and, you know, some of them I did talk about, and you need to adapt all of these, basically, to your case. You need to think through, you know, what are the pros and cons, what are the importance, basically, the trade-offs that you need to think about, and what are your criteria, what are the things you cannot change, and make this decision having all of those in mind. So, thank you for listening.

If you're interested in more about what Microsoft is doing about the React Native, take a look at our blog, follow us on X, and I wanted to share a special thank to Lorenzo, without whom this talk wouldn't be possible. So, a lot of reference to his in most talks, but thank you.