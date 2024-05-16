---
slug: >-
  /talks/react-connection/2024/skander-ellouze-exploring-performance-patterns-a-deep-dive-into-usequery
date: '2024-04-22'
title: 'Exploring Performance Patterns: A Deep Dive into useQuery'
author:
  - Skander Ellouze
video: 0hxrDDIphhA
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/0hxrDDIphhA.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
[Skander]
As you may have noticed, I'm replacing Charlotte, who could not be here, to present her talk about React internals. And I won't be speaking about the React library, but rather about another commonly used library when we develop with React, which is the React Query Library, also known as the Tanstack Query Library. Before getting started, I will just introduce myself.

My name is Skander. I work at BAM.tech, where we develop mobile applications using native frameworks, the Flutter framework, and, of course, mostly the React Native Framework. So for our React Native applications, most of the time, to not say always, we use the React Query Library.

And for those who don't know the React Query Library or didn't hear about it or didn't use it before, the React Query Library is a library for fetching, as the official documentation presented, it's a library for fetching, caching, and updating asynchronous data. And it's a part of the larger library, which is the Tanstack Query, which handled asynchronous data for other frameworks than React also. So when dealing with asynchronous data, we usually want to handle three states.

The error state, the loading state, and the success, or also known as the data state. And for that, React Query offers the useQuery hook, which is very simple to use, as you can see on the right part of this slide. So we call the useQuery hook with our asynchronous function.

And then we get the isErrorState, isFetchingState, and the data state. And after that, we can map the state with the component that should render. So as we can see, it's very simple.

It's declarative, and that's why we love it. But that's not the only reason we love it. We also love it because it's very performant.

And in the next minutes, I will try to present one of the many optimizations patterns that React Query used to optimize its useQuery hook. And I have chosen this pattern because it's very efficient, and at the same time, the technical explanation is very simple, as you can see, as you will see. So let's start with a simple example.

We'll be using a simple React application with two components. The first component will use a useQuery with an asynchronous function to display a loader while fetching, to display data once successful, and it will also display a re-fetch button to start the query. We'll also show a second component, let's call it component B, which will do exactly the same but doesn't show a loader.

And when we want to compare performance, we will, of course, record the number of renders for each of these components. So let's code it. This is the same code I showed before.

This is a simple useQuery with an asynchronous function as a query function. And as you can see, component A and component B share 99% of the code. The only exception is that component A will get the isFetching from the useQuery result and pass it to an UI component to show a loader.

So now that we have our components, let's start the query. So at the left, we have component A. We will click on the re-fetch button and we will record the number of renders.

As we can see, when we fetch, we show first a loader, then the data. And we have only rendered twice. And this is perfect.

We can do better when we want to show a loader than the new data. On the right, it's component B. Remember, component B doesn't show a loader.

So when we click on the re-fetch button, we simply show the new data. And yes, it rendered just once. And again, it's perfect because we can do better to show the new data gate.

When I first showed this to some developers, I had two reactions, two types of reactions. Some were surprised and mind-blown. And they were curious about how did React query achieve that.

And others were not really surprised because they thought that it's natural, since we don't use the isLoadingState, that component B does not re-render. In fact, yes, it's natural, but this is not how React works. Because React will always re-render no matter if your state is used or not.

And I will prove it. And for that, let's create our custom useQuery hook. UseQuery hook in a simplified version, of course, is just a useState to store the result and a proper asynchronous data handling where we set the isFetching before starting the query and then we wait for the query to be finished to set the data state and the isFetching to false.

Now, if we replace the React query useQuery hook with our custom useQuery hook, we can see that component A will always re-render twice, but this time component B will also re-render twice, which is not good, since in the case of component B, we just want to show the new data. We don't want to show a loader. And it would be better to re-render just once.

So I hope this proves that React is not smart enough to detect if the state is used or not to re-render or not. So for the next minute, our mission would be to have the same behavior in our custom useQuery hook as the React query useQuery hook. So we want to make sure that component B will only re-render once when the query is fetched.

So let's sum it up. What we have seen is that React query is capable of detecting if we need the isLoadingState and do extra work if it's the case. We have observed that with the component A and component B experience.

And if you want to reframe that, we would say that when we get the isLoadingState from the useQuery hook result, React query will execute some extra work. And now I have highlighted the keyword, which is get. And as many of you may have guessed, the trick behind the React query useQuery optimization is JavaScript getters.

And this is called the tracking pattern. Don't worry, I will explain how it's done. For that, let's improve our custom useQuery hook.

And this time, we will not be using the useState to store the result, but rather a new hook that I coded myself, which is the useTrackedResult. And what is the useTrackedResult? The useTrackedResult is 40 lines of code to make sure that the result is updated only if some tracked key has changed.

And to do that, first, we initialize the state with JavaScript getters. So as you can see, we initialize JavaScript set empty, which is called the trackedResultKeys, and which will store all the keys that are tracked. And by tracked key, I mean the key for which we will re-render once the value has changed.

And when initializing the result state, we will use JavaScript getters, which is the syntax object point defined property and the passing getter function. And once the key is accessed from the result, we will store it in the trackedResultKeys. And then when we want to update the state, we will check if any of the tracked keys has changed before setting the new result.

So in this case, we have declared the variable shouldRender. And as you can see, we will check if the new result key is equal to result.currentKey. We have used isEqual just to make sure that it's referenced, it's passed by reference. Now that we have created a new custom hook, we can check if it really performs like the React query use query.

We can see that for component A, it's the same, but it was the case before. And for component B, this time, when we fetch the data, it re-renders only once. That's good.

Sorry. This is also how it's done in the React query library. And as you can see, it's really the same syntax, which is object point defined property and passing getter function to track the properties.

Great. Before concluding, I just wanted to point out that this is great, and this improves the performance of our applications, but it requires some effort. In fact, you should never restructure the result of your React query.

And the reason is that if you do so, you will get all the keys, and therefore all the states. And this will cause unnecessary renders, since for React query, you are tracking all the keys. And this particular error can be avoided using the OSLint plugin from React query, which I don't know why is a lot less popular than the React query library.

And I hope with this talk, I have convinced you to download it and to use it in your project. Before ending, I would like to acknowledge Dominic Dorfmaster, which is the maintainer of the Tenstack query, and the author of a great blog, which is Tekadudu. And he wrote an article about React query render optimizations.

It may be two years old, but it covers a lot of render optimizations, such as the tracked queries, which we have seen, but other optimizations, like the structure chaining. Thank you for your attention, and I hope you enjoyed the talk.

[Christophe]
Thank you, Skander. Please come here.

[Simone]
We will ask you very, very bad questions. It's your...

[Christophe]
What is the atomic number of zinc?

[Simone]
630, by the way. I have a different question. How does it feel to wake up in the morning and say, okay, I'm going to have a boring day as usual, and then ending up speaking at an international conference with millions of people in front of you?

More online.

[Skander]
Online, yeah. It's at the same time stressing, but also very cool.

[Simone]
Cool. Is tracking... Sorry.

How do you activate or deactivate tracking in React query?

[Skander]
In React query, tracking is by default enabled, I think at least for React query version 4, and maybe for version 3 or so, I don't know. And if you want to disable it, you can pass a prop for notify on change props, and you can list the props that you want to be notified when they change. Typically, if you want to be notified when the query fails, and you don't get the error state, you can pass on change props error, and you will be notified when it fails.

[Christophe]
All right. You mentioned in your closing slide that external resources, resources really from the TK2D and everything, for further explorations and further optimization pathways. Is there one of these that you're particularly interested in that you'd like to mention?

[Skander]
Personally, I love the structure sharing, because for those who don't know the structure sharing, it is equivalent to replace deep equal, and by replace deep equal, we will just... If we fetch the query, and just a key has changed between the first query and the second query, React query will keep the reference of the first object, and will change only the reference of the key that has changed. Why is this very cool?

It's because when we use useMemo or useEffect or something like that, we will not cause any other...

[Christophe]
Yeah, you'll keep referential identity, and so you'll have less re-render because of that.

[Skander]
Yeah. So, you can optimize your useMemo or useCallback.

[Christophe]
Or your future React code when React Compiler does that for you.

[Skander]
Yeah.

[Christophe]
Okay, cool. And have you seen... Oh, we got questions coming in.

[Simone]
Cool. Awesome.

[Christophe]
Go ahead.

[Simone]
Okay. All right. Do you have other ideas or...

Sorry, scenarios in which this solution can be helpful, apart from pure itself?

[Skander]
Usually, this will be very good for large states. But at the same time, large states should not exist. So, I think as a temporary solution for large states, it will be very cool.

But the long-term solution would be to split the state into atoms by using Jota or something like that.

[Simone]
While you are waiting for refactoring, you can at least introduce that as a local optimization and then proceed to a larger-scale refactoring. Yeah.

[Christophe]
There was a question about, do you know other packages that use the same trick, like tracking, so essentially getters or proxies to achieve the same kind of thing?

[Skander]
Honestly, no. But I would be curious.

[Christophe]
I think Vue does it. Vue reactivity in Vue 3 uses ES proxies to do that kind of thing in computation tracking.

[Simone]
Yeah, I think...

[Christophe]
Some signals libraries do that, too.

[Simone]
Yeah, I think so. Yeah, I was thinking about that. Yeah, I think most...

I'd say most reactive frameworks libraries use that. All right.

[Christophe]
Thank you very much, Skander.

[Simone]
Okay. Thank you very much, indeed. Thank you.

[Christophe]
A big round of applause for Skander. This was his first talk. Hopefully, not the last.