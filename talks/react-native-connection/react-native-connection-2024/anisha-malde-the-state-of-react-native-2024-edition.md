---
slug: >-
  /talks/react-native-connection/react-native-connection-2024/anisha-malde-the-state-of-react-native-2024-edition
date: '2024-04-23'
title: 'The “state” of React Native: 2024 edition'
author: Anisha Malde
video: o4kxwOCsDOg
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/o4kxwOCsDOg.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: react-native-connection-2024
allow_ads: false
---
[Anisha]
So, thank you, Mo, for the introduction. I'm Anisha Malde, and my current state right now is about 40% Croissant and 60% React Native Developer Advocate. My own journey with React began in 2017, and the first four years were spent as a developer at the digital agency part of IBM.

As a result, as many of you who may work at agencies know, you work on a variety of projects, and our tech stack was usually more or less the same, where for state management, we would usually end up using MobX and Redux. When I joined Amazon, however, my role changed from building those production-level apps to React Native demo apps for Fire OS, and so thus, so far, I've actually managed to get away with just using the context API. However, recently, as Mo mentioned, I've been helping him with his initiative of bringing React Native to the big screen.

If you haven't already seen it, please check out ReactNativeTV.dev, because there's some really cool content on there. So as part of that, I've been trying to figure out which state management to use for my React Native Fire TV demo app, because, as you can imagine, the Fire TV device is not as performant or powerful as your iPhone, and you have to optimise for performance wherever you can. I quickly realised that, from my time at IBM, there's a lot more options, and everyone is very, very opinionated, and I just didn't know where to start.

So I did what every normal developer does, and I started procrastinating, and I came across this image in a tweet by Lee Robinson, and, as you can see, with a few of my own additions, after the introduction of Redux and MobX, there was a period of time where there wasn't really any major state management libraries in the ecosystem, and it wasn't really until the introduction of Hooks that we saw a resurgence in innovation in this area, with libraries like Zastand gaining popularity only in about 2020.

And in my opinion, the introduction of Hooks was a significant milestone, and it did open up all these new possibilities, unlocking new patterns for developers that inspired them to rethink how to approach state management. So then about three weeks in, while in the bathroom, because that's where we all do our best thinking, I realized something else, and that was that the introduction of Hooks didn't just change the options available in state management, it also created a divide in the way that React developers, and I guess hence React native developers, approach state management. And this realization sparked my curiosity, and so I procrastinated some more, and I put all my findings in a love letter, like any normal person would do, and it looks like the community found it somewhat interesting, so if you're interested, you can check it out here, but I thought I'd share where my procrastination led me to, and as much as I'd love to stand here and recite the love letter to you all, I think I might get a bit too emotional. So instead, here's what I hope you'll take away from this talk.

First, how the different learning journeys shaped each generation's perspective to state management, how we can bridge the gap between them, state management options in 2024, insights lessons and guidelines that will help you make a more informed decision, and finally, the impact of the new architecture and React 19's features on the options that are available in 2024. So let's jump in. In 2019, with the release of Hooks in React 16.8, the way everyone learned React changed, and hence React native changed. Prior to Hooks, functional components were largely just used for simple stateless rendering, while class components handled the more complex logic, like state management. But with the introduction of Hooks, functional components gained this ability to manage state and side effects, and it significantly altered the way applications were built and state was handled. And justifiably, like, at the time of writing, and I'm sure you heard Rachel yesterday, the Hooks docs assumed that the reader was familiar with class components, and that's changed now with the new React docs.

However, those learning React post-2018 probably didn't prioritise learning class components because the React ecosystem was shifting to a functional component approach, and if you didn't come from a computer science background and you learned React post-2018, you probably never even saw what a class component looked like. So this left little incentive for those developers to learn React the old way, and, as a result, it ended up with those two generations learning React in a different way, and I like to call it the two generations of React, the class component generation, and the new gen of React devs. And here are some of the, I would say, things that divide those generations.

So class component gen of React devs learn React with the class components. They like skinny jeans, they use self-deprecating humour to cover up their existential crisis, and they show off their Harry Potter knowledge. And then the new gen of React devs learn React with functional components, where mum or dad jeans, and I don't know what these are, so someone please explain them to me, have an absurd meme-based sense of humour and show off their Snapchat, streaks, and TikTok.

So raise of hands, who falls into the first category? Okay. I can't really see, but a few of you.

Who falls into the second category? Okay. Who's just confused?

Okay. So let me explain. This is just a little joke that inspired my article title, because as it just so happens that the year that Hooks was released is also around the time that Gen Z was most likely starting their jobs, and so I drew the conclusion that most, and I'm not saying all, so most of Gen Z likely learned React from a Hooks-based approach, so that's why my article is like Gen Y to Gen Z, so the point is it doesn't matter whether you fall into each category of the other things, either you learned React from class components or you learned it from a functional Hooks-based approach.

And each generation has a different approach to React and state management. So now I'm going to explain each difference and how it came to be. First up, we have the new gen most likely didn't learn the React lifecycle methods, and I think this is one of the most significant differences, because for the class component generation, managing state meant you were forced to think about the nuances of state by understanding those lifecycle methods, because these lifecycle methods provided clear entry points for initialising, updating, and cleaning up your state. That Hooks abstracted away. So let's look at an example, and this is what a class component looked like, and some of you may have seen this, some of you may not, but as you can see, each phase of the component lifecycle had specific methods, so for mounting, you had componentDidMount, for updating, you had componentDidUpdate, for unmounting, you had the equivalent componentDidComponentWillAndMount, and so you were forced to logically think through each phase of the lifecycle and implement your state management logic accordingly. So you knew how to, for example, put clean-up operations in componentWillAndMount, whereas developers who never worked with class components might not think through the component lifecycle in this way, and hence might overlook that logic when writing code.

Next, the new generation loves using Hooks. So, as mentioned, in class components, you had lifecycle methods like shouldComponentUpdate, and that allowed for this manual control of component re-rendering, which encouraged developers to think about performance optimisation, whereas now we have Hooks like useCallback and useMemor, where those optimisation techniques might not be as intuitive, making it harder to identify the most effective way to use these Hooks.

And similarly, when coming from class components, you required a deeper understanding of that component lifecycle and how it related to rendering and updating, so you were able to understand more when to touch the DOM or when using things like useRef. So let's look at another example. So in the class component, shouldComponentUpdate compared the next state props with the next props value, and in this example, you can see it's comparing the previous product ID and the new product ID, and determining whether the re-render is necessary.

In the equivalent functional component, the useMemor hook memorises the result of an expensive computation, in this case, compute requirements, based on the product dependency, and this memorised result is re-computed only when that value changes. And then you have the useCallback hook, which memorises the callback function handleSubmit based on the product ID dependency, which indirectly is, I guess, what helps determine if the re-render is necessary. So as you can see, it's not as intuitive of just saying, like, hey, re-render when my product ID changes.

And then we've got testing became, I think, maybe easier? So the step-by-step nature of class components meant you were, like, encouraged to think, again, through those component lifecycle methods, but you also had to mock those lifecycle methods, whereas now testing components, it's easier, especially with the help of React Native Testing Library. So, for the class component gen, maybe testing might seem like a no-brainer, whereas for the new gen, it might be sometimes an afterthought.

And again, I've got an example. So here's what an old test looked like with enzyme. So the enzyme example checked whether the wrapper.state, so the enzyme checked wrapper.state, and it checked the component's implementation. As you can see, you've got wrapper.state, whereas now what we test is the user interaction. Like you're testing the user interaction. Here's the example React Native Testing Library.

So you don't care about the implementation details. And this is what I mean by testing became a little bit easier. Before you're testing whether state was implemented in the correct way, you would explicitly test the state in various stages during the component lifecycle.

And there's actually a great blog by Coolstat that talks about how we move from enzyme to React Native Testing Library that goes into a bit more detail on the plus side of things. And finally, the new generation tend to jump to state management libraries. So prior to hooks, integrating Redux into React apps was a pain, and it required a good understanding of the Flux architecture and a lot of boilerplate.

So even though with hooks, the process of integrating Redux and I guess now RTK has become much easier, those scars of the past do serve as a reminder of the complexities that can happen when reaching for a state management library. And so I think this makes the class component generation less likely to reach for those state management libraries. I do think this also caused another pattern, which was class component gen still reached for Redux due to familiarity, whereas the new generation of devs might be more comfortable with the newer, lighter libraries.

Again, let's look at an example. And this is what Redux looked like before RTK, and this is what it looks like after RTK. And you can see the code is a lot simpler, and you can set up a store in a couple of lines of code.

Okay. At this point, you're probably all like, okay, cool story, bro. Why does any of this matter?

Or how is it specific to React Native? And I think if you're going to take away anything from this talk, let it be the content during this slide. So first, it's clear that the different learning journeys shaped each generation's approach to React, and I guess then React Native development, which has led to this pattern of common issues we see when handling state.

So now that we understand those issues, we can help bridge that gap between each generation. So for the class component generation folks sitting here, it's things to look out for and advise the new gen on. And for the new gen, it's things to be mindful of, and it might be an explanation for those coding best practices that the other generation is always asking you to follow.

And how is it relevant to React Native? Well, performance optimization, our favorite topic. You want to limit performance overhead of the React Native JS bridge, and we do this by understanding techniques that avoid those unnecessary re-renders, that minimize state updates, and reduce our app bundle size.

And this will help ensure smooth performance, because we have so many more form factors to think of, and not all the form factors have the same, you know, performance that you might expect on a Mac M1. So let's look at each generational difference I talked about, and some techniques to help mitigate and ensure that we are optimizing for performance. So for the first one, they didn't learn the lifecycle methods.

So avoid storing unneeded state. Storing unneeded state can lead to unnecessary complexity, which ultimately leads to a performance overhead, which means more places for bugs, and it's not a good story. And this can be mitigated by avoid storing state that can be calculated from other state values and props.

For example, if you're storing full name, calculate in the render from the first name and the last name. Enforce immutability, don't transform data in state. Transform the data while rendering, and keep your state as the source of truth.

And next, watch out for duplicated state, or deeply nested state. So this example, make sure you're using IDs to store the users, the posts, and the comments separately as slices of state. Don't nest that state object.

For they love using hooks, let's work on understanding our hooks. Separate concern. Don't put all your logic in a single use effect.

Separate related logic into custom hooks, for example. Watch out for multiple use effects at the same time, because multiple use effects with many dependencies can also lead to spaghetti code and performance issues. Watch out for the missing dependencies in use effects, because if you don't know, you should, but this can lead to very unexpected behavior, like infinite loops.

And make use of the cleanup returned by use effect to avoid memory leaks and properly handle those component unmounts, like cancelling listeners. And finally, don't overuse hooks, like use memo, use callback, because using them as premature optimization techniques can have the opposite effect. Sorry, that was not the last point.

Enforce immutability. So avoid direct state mutations. So for example, if you have something that looks like state.count, increasing it in the state, set state directly from props, or setting state directly from props, that's not great practice. I would create a new object and then mutate the state there. And there's a great talk called Using Use Effect Effectively by David Kay, which I really recommend. I think he did it at one of the React Advanced Londons, and he talks a lot about how to use use effect way better than I can in one slide, so check it out.

For testing, it became easier. So even though it became easier, maybe we still need to think about it and keep our components concise. So keep components focused on a single responsibility.

Refactor complex logic into hooks or utility functions. Make sure your components aren't too large or coupled or nested. Follow principles like unidirectional flow, atomic design, and decoupling components.

Favor composability over inheritance. And if you want to learn more about this, the legacy React docs actually have a really good page that I think they've removed. So if you want to check it out, check it out in this link.

And finally, pass dependencies into those components, into functional components from the outside, rather than having the component create or manage its dependencies internally. And finally, pretending to jump to state management libraries, understand your options. So some general advice, don't stick everything into one context.

This is going to slow your app down, so you're going to have re-renderings happening all the time. Red down your state into smaller, more manageable contexts that are specific to different parts. Not every app needs a state management library.

Understand when to use a state management library. And finally, be intentional with state organization and tooling. And this is the initial reason I wanted to do this talk, because when making my state management library choice, I wanted to be more intentional.

And so I started looking at the options for state management in 2024. And on the client side, we have five options, Recoil, MobX, Redux, or RTK, Jirti, and Zestand. And on the async state management side, we have TanStack and Apollo Client.

And Software Mansion's State of React Native 2023 survey shows the usage of each of these libraries from 2023. And two things to note. So the async management options aren't mutually exclusive from those client-side state management options.

And another thing, Redux and RTK are what MST, so MobX State Tree, is to MobX. So hopefully we can see a rise of the use of MST in the following years, because I think it really does simplify how to use MobX. So this is what I learned.

These are the usages of these. And as you can see, Redux is at the top, followed by TanStack and Apollo Client. But because those can be used together, it's still quite a drop to Zestand, MobX, Jirti, and the rest.

So next, I classified these state management libraries based on their core architecture and how they handle state updates, as I found that those things directly impact, first of all, their usage, their scalability, and their performance. So this is what I came up with. I put each library into four categories, decentralized versus centralized.

So this indicates whether the library follows a centralized single global store or decentralized, whether it's a component or independent store approach. And then we have mutable versus immutable. So whether the library enforces immutability or allows direct modification of state.

The state management model. So for libraries that follow the Flux architecture, or ones that use observable data stores, and ones that observe state, ones that split state into tiny pieces of data called atoms. And finally, state machines.

And then whether the flow of data was unidirectional or bidirectional. And now you might be thinking, like, why did I do this? Well, I found this really helpful, because I could see which libraries had a similar mental model.

And ultimately, it was to help me choose the right state management library or approach. And so first, I want to give you some general advice. First, only reach for a library if you have a clear use case.

Next, consider the project size, complexity, team expertise, and performance requirements. And this is where my table should be taken into consideration. So for example, centralized libraries may be easier to manage initially, but as the project scales, you might want to rethink this strategy, because those centralized libraries can be harder to maintain.

So that's why I made that table, where it's like, fine, that initial choice may look good initially, but when we scale, when we're thinking about performance, that choice may change. So having that mental model really helped me think through the options. Next, for React Native specifically, things like bundle size, DevTools, are even more important factors to consider.

So fine, the library may be, you know, smaller or less complex, but if it has a massive bundle size, that doesn't really help me with my task of optimizing for performance. So it's something I need to think about. And DevTools, like, we all need to make sure that the DevTools help us debug, because it's just not fun.

And finally, Ola from Callstack has a fantastic book called Simplifying State Management in React Native, and she kindly shared this cheat sheet with me, which outlines some of the use cases for those libraries. So to summarize them, Jyota is really good for component-centric apps. Well, first of all, let's start with Redux, sorry.

Redux is, well, RTK is good if you have a large app that needs state from many different places. So it has a significant amount of state that needs to be accessed and modified in multiple parts of your app. And then Jyota is good for component-centric apps.

Voucher is really good for data-centric apps, because it leverages the proxy API, which allows for direct mutation of state. Recall is really good for derived data, because it uses the concept of selectors, which are functions that calculate derived data based on atoms, and then they can automatically also track dependencies and recompute those changes when those dependencies change. Zastand is really close to React's mental model, so if you want a simple API that's close to how we think in React and React Native, that's a really good choice.

And MobX is really great for state that needs to be reacted to in real time. And finally, and I'll admit I added this at dinner last night, we have LegendState, which is great for performance, but if you want to know more about that, please find Mo, because he knows more about it than I do. And an analogy that I saw in the Jyota docs was actually Jyota is like Recall and Zastand is like Redux.

So if you're thinking of options between those two, they're quite similar in the way that you implement them. So that might help make your choice easier. And finally, I think I wanted to share what I learned and the pros and cons and sort of my learnings along the way.

So firstly, Zastand, Jyota, Vow2, Recall were all really lightweight options, like coming from MobX and Redux, I was surprised at how easy it was to install these libraries. Zastand works great with 10 stack, so if you've got a lot of async state management, it's a great option that works together. Jyota has really simple syntax and solves a lot of those issues of context re-rendering.

So if you've got an app which has a lot of state that keeps needing to be re-rendered, that's a great option. RTK still has a lot of boilerplate, and the learning curve, if you aren't familiar with Redux, is still quite high. RTK, Zastand, Jyota, Vow2 are all compatible with Redux dev tools, so if you're used to Redux dev tools like I was, these are great options.

Recall, Jyota, and Vow2 have automatic type inference, and I put a star on this one because I'm not sure if other ones do as well, but this is what I gathered, so if anyone wants to correct me on this, please feel free. And finally, I found Vow2's docs a little bit confusing, I don't know if anyone else did, but another great article that goes into the options some more is this one, so check it out as well. So that brings me to today, and the only factor that was left to consider, which is what is the impact of what's happening in 2024 on my options?

So the new architecture supports concurrent rendering and features that were shipped in React 18+, which means now you can use features like suspense for data fetching, transactions, and other React APIs in React Native. So in this case, Jyota, Vow2, and Recall are all designed with concurrent rendering in mind, and they all leverage React Suspense, so they're all very well positioned to take advantages of all those performance optimizations that are offered in the new architecture. So if you're creating a new app, this is a really big factor to consider.

Additionally, with the new React concurrent rendering features, following those best practices for state updates is even more important to avoid inconsistencies, race conditions, and stale state, because libraries that enforce immutable state updates and provide that clear, predictable way of managing state will be beneficial in a concurrent rendering environment. So while those options in that table may be great, there are still things I needed to consider that were happening in 2024. And finally, the introduction of React 19 and the new React compiler, which was called React Forget, for those of you who might know it as React Forget, marks a significant shift in how developers are going to optimize their React Native applications.

So with automatic memorization, the need for manual use of useMemo, useCallback is going to be greatly reduced. Like, it's not going to go away, but it's going to be reduced. And simplifying the code and improving performance might be less manual than it is right now.

So who knows? In 2024, we actually might end up with three generations of React devs, and I'll have to redo this talk. So thank you so much.

If there's three things I want you to take away, let it be, number one, be kind to that new generation of React devs. It's not their fault they didn't learn class components. Number two, be intentional with your state management choices.

So don't just go with what you're familiar with. Like, try, I know it sounds hard, but try and be intentional, because this will greatly help with performance optimization. And that is what's most important to us as React Native devs.

And finally, when making your choice, consider not just the past and the present, but also the future, because the changes in React 19 and, you know, the new React, I think React Native 0.74 was just, like, announced today as, like, the new stable version. So all those things are going to have a massive impact on the choices you make today. But that's it for me today.

Thank you so much.

[Mo]
Thank you, Aneesha.

[Anisha]
Come on out. It's really bright.

[Mo]
Yeah. You guys are non-existent here, by the way. So, yeah.

Okay. Cool. So, you started off your talk talking about almost software architecture, which I thought was an interesting take to have, particularly because over the years I've found that a lot of issues that we oftentimes face is because we are afraid of traditional software architecture principles.

I was having a very interesting talk with Morgan, who's going to come on later this afternoon and talk about something totally different, but we had a very interesting conversation around this, where terms that you mentioned, like separation of concerns, are tabooed words that will get you egged and tomato-throwns at you. So do you feel like this is part of the issue here? The state management library is one thing, but, like, have you found that you've seen resistance around, like, employing traditional software architecture principles and maybe that's part of the issues around performance and stuff like that?

[Anisha]
I don't know if I can speak, because I don't come from a traditional software, I didn't study computer science. All I know is, like, what I've seen in the evolution of React, and it's that if you, for example, like me, you didn't come from a computer science background and you just learned JavaScript and you just learned React and then you just learned React Native, you may likely have never seen, like, you know, object-orientated programming. You may have always just known, like, functional programming.

So I think, like, React does try and teach you some of those things, like, you know, separation, separating concern, immutability of state, but it might not be something someone thinks about naturally, which is why I brought it up. So don't throw eggs at me.

[Mo]
You can target your eggs at me, because, yeah, I deserve it. Katty wants to know which state management library you ended up selecting at the end.

[Anisha]
Yeah, good question. So I still haven't, because I, like, procrastinated.

[Mo]
Don't we all, Aneesha.

[Anisha]
I will be releasing a repo on my slides. If you check out Amazon app devs on GitHub, I'll be putting the libraries sort of that I visited. So, like, Joytai, Recoil, Justand, and Valtio examples there.

So eventually. Give me a couple. I wanted to have it ready for this talk, but I think I was still trying to get everything in my head together before I, like, published it and made it sure it was very readable code.

[Mo]
Cool. What are some good examples of projects that don't or shouldn't require a state management library?

[Anisha]
So, yeah, I think it depends. Definitely ones where you don't have complex state, like, be intentional, right? If you have a clear use case, that's when you should go for it.

So, like, for example, if you have a lot of async data fetching, then you might want to think about, like, just using, like, 10 stack or GraphQL. You might not need a client-side state management library, but if you've got, like, a lot of components that require state, then you might want to go for something like Joytai, because it's quite component centric and doesn't cause those re-renders.

[Mo]
And that's a really important point to add on, which is especially in the React Native space and in the TV space far more than anything, and shameless plug here, go to ReactNativeTV.com or RNTV.dev, as Anisha said, and go learn all about TV on React Native. I have no shame. But really, it becomes super, super important to optimize, because it's not like the web where you have just a single flat view hierarchy and a single screen that's subscribed to state changes.

You have a bunch of stacks, and something might be rendered on a part of the stack, and you can't see that, and that's triggering re-renders, which slows down your app. So, super important, and I'm glad you mentioned that. Cool.

We're a little bit behind on time. I'm going to finish with just this one question. People have asked, what generation are you?

So, how about we do a little quiz? We can't really see you. Maybe we need to move back into the center, but we'll do that.

[Anisha]
It's not fair. I look like I'm 15.

[Mo]
And we're just going to limit this to React generations. So, first or second generation, maybe we get the audience to vote first what they think, and then you can reveal. Wait for me to balance it out.

So, Anisha, audience, who thinks generation one versus two? Raise your hand for generation one. That's majority, I think.

Generation two? Minority?

[Anisha]
Yeah, they're correct.

[Mo]
Generation one.

[Anisha]
So, I mean, how would I know about classical politics if I wasn't? That would, no.

[Mo]
Good research.

[Anisha]
Yeah. Good research.

[Mo]
What about me, I guess? Just to be fair, generation one. Do you guys all think I'm a second generation?

Really? Just sad. Second generation?

They're confused. They're confused. Yeah, they're confused.

I am indeed a.

[Anisha]
You wear skinny jeans, but you also, I don't know.

[Mo]
I don't wear skinny jeans. Thank you very much. I've never touched TikTok in my life.

Thank you very much, Anisha. Thanks for coming along. And a round of applause for Anisha.