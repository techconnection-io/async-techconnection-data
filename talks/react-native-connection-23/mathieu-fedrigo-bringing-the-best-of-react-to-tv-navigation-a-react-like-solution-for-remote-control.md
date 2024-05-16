---
slug: >-
  /talks/react-native-connection-23/mathieu-fedrigo-bringing-the-best-of-react-to-tv-navigation-a-react-like-solution-for-remote-control
date: 2023-06-01T00:00:00.000Z
title: >-
  Bringing the Best of React to TV Navigation: A React-Like Solution for Remote
  Control
author:
  - Mathieu Fedrigo
video: Asn1TmCH2b0
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/Asn1TmCH2b0.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/react-native-connection-23/mathieu-fedrigo-bringing-the-best-of-react-to-tv-navigation-a-react-like-solution-for-remote-control/slides.pdf
tags: []
year: 2023
conference: react-native-connection
edition: 2023
allow_ads: false
---

[Music playing]

Hi, thank you for welcoming us.

We're really glad to be here.

Thank you to the React Native Connection team.

Also, we are glad to be in Paris. It's a beautiful city.

We live here, so... [Laughter]

So today, we want to share with you our experience experience with React on the TV application.

We've been working on MyTFM, which is the video on demand application of one of the most watched TV channels in France, TFM.

So here's what it looks like.

So you should know that this is a TV app.

There are many things in common with a mobile and web app.

But there's one major difference.

You have a remote control.

So what happens when you press right, right, up, down?

What should be the focused component?

So that's the main challenge we had to tackle working on this.

It was quite hard, and we learned many things.

And we hope we can show you what we learned along the way.

A very short presentation.

I'm Pierre.

Mathieu is here somewhere.

You can check us out on GitHub or Twitter.

We both work at BAM, too.

To give you some context, so we did not know of this before working on the project, so you might not know either.

There are many smart TV devices on the market.

That's usually the devices you would use to watch Netflix on your TV.

So it can be either embedded in your TV directly.

You might have Android TV running in your TV.

It could be a little box plugged to your TV through HDMI, like an Apple TV box.

There are also HTML devices.

And you should know that this Android TV and Apple TV OS use the same tools as Android and iOS.

So let's give you an example of a simple TV app that we made.

So it's a bunny program TV app. definitely not AI generated. So we have two rows in this app so I'll show you what happens when you press the buttons on the TV remote. So I land here, no focus. If I press right on my TV remote I get to the first row, first program. Press right again I get to the second program, nothing fancy. If I press down I will not get to the second bunny but the first bunny of the second row because we are talking about rows so it's a classic TV component it can be well it could be a grid it's another component but it's a different behavior the grid would be second bunny press right press right if I go back up I'll get back to the second bunny of the previous row so we keep track of what programs we were on.

So those are the spatial navigation rules of a TV app.

So our goal with MyTFM was to deploy the app on all the platforms.

We want Android TV, Apple TV, and also some HTML devices.

The classic thing is having one code base per platform.

We've all been through this.

React Native is a great solution to have only one code base unified, but there's still a major difference.

We still have this TV remote to handle.

So how do we handle this?

We could use the native TV OS components.

It would work, but it's not multi-platform, really, because it's not available on the web.

There's no implementation of the TV stuff in our browser.

So we could use a custom navigation system in React.

That would be multi-platform, which is great, but it's also a hard problem.

So why is it hard, you may wonder.

Well, there are many edge cases of what should happen when I press a button on the TV remote.

Also, it's quite hard to keep track of where you are spatially in React.

So what we will cover is the expressive API we should have to describe this, how handle this logic and how we plug this out to React.

So first I want to tell you about the first iteration we had.

We faced many dead ends.

We had a first version with many -- a lot of impressive logic where you had to declare manually the components in a user effect, so we declared them in JSX.

There was duplication between the declarations, so you can imagine bugs.

We had very leaky abstractions, so spatial navigation logic dripping everywhere on the business code base.

It was really painful to work on.

So we had many bugs.

We could not handle dynamic updates, like adding content dynamically.

We could not have any layout we wanted.

So that's how we came to design a declarative API.

So Mathieu will show you that.

- Hey, so can you hear me?

Yes.

So thanks Pierre.

We want a better API.

We want a declarative API.

We don't really want to have to manually register each of those components into some kind of special navigation layout skeleton or something.

We just want to write JSX.

We want to build a simple React Native page.

And we want that by just writing the JSX, it makes it so that the navigation works.

That would lead to a much better developer experience.

So let's try to build this simple app and show what it would look like for some developer to do it.

I'll start with just two rabbits here.

Currently, it's only the design.

They are not focusable.

It means that we can't reach them with the remote.

The app is not interactive.

To make it interactive, we can wrap our program with a node.

A node is what we'll use everywhere to describe the spatial layouts.

This node means that the program is focusable.

It can also describe the layout of the element.

So this container node, the new one, is not focusable and it means that those two programs are in a vertical container, so they are on top of each other.

So now you can reach them by pressing up and down.

And of course you can make horizontal rows too.

So now we can go back and forth by pressing left or right.

So let me clarify something here.

The node is only there to describe the spatial interaction, not the style.

So if you want to put those two objects next to each other, you also have to modify the style on something like a view here, not on the node.

The node is only for spatial things.

And I think finally we have everything we need to build the page.

So I can add some titles for the two rows.

I can create a second horizontal node below with several programs inside.

And we only need to write this to achieve this simple app where you have this whole logic baked into the nodes and the components.

And maybe last precision, you see here that the title of the rows don't really need to be focusable.

I mean, I don't need to go on the title to do anything.

So here, the title is just a simple typography, no nodes wrapping it.

The nodes are only here to describe the spatial layout.

So let's get back to this spatial navigation problem.

As we showed, there are spatial navigation rules.

And the first thing we thought after our first iteration is it has nothing to do with React, so we should just separate it.

Once it's separated, one may wonder, is there a lib that's a library that handles the spatial navigation logic, which is very -- it's a common problem.

Well, yes, there is.

The BBC made a lib called LRUD.

It means left, right, up, down.

And how does it work?

So the goal of LRED is to represent a spatial layout using a data structure.

It's completely UI-agnostic.

You can use it for whatever framework that you can run JavaScript.

Its goal is to be generic.

Yeah, it's written-- it's small, but it doesn't matter.

So how is it represented?

You have a root element that has an ID.

It has an orientation.

You can say your content is vertical in the root.

It has children.

And each child has the same shape.

So an ID, an orientation, and its own children.

You have leaves that can be focusable, like the program 1, 1, program 1, 2, 2, 1.

They are focusable.

And you can also add unselect callbacks, like what happens when I select it with my remote.

And if you think this through, it's actually a tree.

Each node has one parent, and LRED is represented as a tree.

So just like React, so you can probably do something.

To sum up, you feed LRED with a layout description, some keyboard events, some callbacks.

And at the end of the day, we will return you who is currently focused, return you some events, and we'll call your callbacks when you want to select something.

So let's see how concretely we use Eluid.

So you can register an element using the register element method.

You give it an ID and then a direction, so the option that we saw earlier.

So here we have our root, direction vertical.

We can register a row, so call the same function.

Well, ID is row1.

This time, you need to specify the parent, which is root.

Also a direction.

And we register the programs.

Well, same as before.

Parent is now row1.

And you give it the focusable props.

And now we can send key events.

So LLD.handleKeyEvent, right.

We'll get the focus on the first element.

If I do right again, we get the focus on the second element.

And that's it.

Now that we have the engine for our spatial navigation all handled by LRD, Mathieu will show you how we can plug this to React.

MATHIEU RICARD: Yes.

So I showed you the API we want.

Pierre showed you how LRD works.

So let's plug it all together. as Pierre said, React is a tree and LRUD too.

So what we want to do here is to automatically create the LRUD tree from the React tree.

And so this imperative logic that Pierre showed with the LRUD.registerNode, we actually want to abstract this inside the declarative components, the nodes I showed you earlier.

So this way, when a node is created for React, we want to call this imperative logic and to register the node inside LRD.

So first thing first, let's set up LRD.

This is where it gets a bit more technical and this is also where we learn a lot of things, really interesting React behaviors.

So let's create this LRD class. we can register the first root parent element that will contain everything in the page.

Pierre also said that we have to feed LROD the remote events, so we have to call LROD.handleKeyEvent when needed.

We can have a look at the program I showed you earlier.

So let's dive inside what a node is.

In its most basic form, sorry it's a little cut on the bottom, a node is just something that returns the children.

It can have some props like, is it focusable? What's the orientation for focusable nodes?

The first step for a node would be to register something to LRD when it's created.

This is what it looks like.

You create a unique ID.

Inside the useEffect, you call LRD.registerNode() when the node is created.

As Pierre showed you earlier, if I want to register row 1,

I need to know what its parent is here, its root.

So we need a way to identify this node's parent.

Maybe the naive solution would be to do some prop drilling, but there's a better way here.

So our solution is to use context, and there's a twist, maybe something you didn't know about context.

This would be a basic context implementation.

You create the context.

You have a provider that passes the value root to every children.

And so when there's something inside root, like row1--

I mean, this code may seem a bit odd, but it simply means that row1 will receive root when using useContext.

But the thing is that it's not only one value that we want to pass in context.

We want each of those nodes to give its ID to each tilde one.

So maybe we could use one context per node.

And this is where we can use a key property of React context, which is that we can override the value of the context.

So here, row one uses the same context provider, but it overrides its value with row one, its own ID.

And now, its children, like program one, will receive row one when using useContext.

So, I mean, of course here, program one doesn't really see root anymore.

It only sees its closest parent.

But this is nice for our use case, because we only need each node to get its closest parent ID.

And what's really powerful with this nested context approach is that now we can nest as many nodes inside one another and they will always be able to get their closest parent ID when using useContext.

And of course, this also work if you put several rows inside root or several programs inside row.

Now that we know how nested context works, we can put it into practice.

If we go back to our node, I'm just creating the context at the bottom and I'm using the context inside the node so that it can pass its ID to its children.

You can also add this logic so that the node will get its parent ID by using this context.

Now it can call registerNode with its parent ID and hopefully all the nodes will be registered.

So it should work now, does it?

No.

So if we run the app now, we get this strange error, cannot find row 1.

And if we look at LLOD and debug it a bit more, we can see that it seems that some nodes have been registered but some haven't.

If you know why, congrats.

To understand why it doesn't work, we're going to have to have a look at the render and use effect execution order.

Listen carefully now because I'll ask you something later.

Let's say we have this root component with two rows and each row has two programs inside. all of those components look something like that so they log render when they're rendered. Can you guess the order of the logs which is the which which component will be the first one to call render? I mean this is the first the first render of the whole page so they all will be rendered at the same time but what's the first one that will go under?

Maybe by raising your hands, how many of you think root is the first one?

Maybe 10, 20 percent.

Good job, it is.

It's root, then row one, then program one, two, and then it goes back to row two, and so on.

So to understand this a bit more,

Let's have a look at the math behind this.

This is actually a tree traversal algorithm which is depth-first.

It means it goes as deep as possible before going wide.

It is also pre-order.

Pre-order means that it will execute the node's code, then it will look at the left path recursively, and then it will look at the right path recursively.

So this GIF may seem a bit strange.

Let's look at what happens step by step for our components.

First, it looks at root, and so it executes the code for root, which logs render root, and then it looks at the left pass recursively, which is row one.

And you start over.

You look at row one, you execute the code for row one, which logs render row one, and you look up the left path recursively.

And when you arrive at program one, who doesn't have any more children, you can execute the nodes code and go back to the last one you were at, which is row one, and go to the right path this time.

Same thing for program two, when all this huge left branch is dealt with, you can go back to the other right path from root, and so on and so forth.

So, I mean, this order seems pretty logical to me.

But another question is coming and I changed up the component a little bit.

So now it's not render, it's logging effects when the use effect is called.

And it's still the first render of the page.

Can you guess what the order of logs will be this time?

Is it the same?

Is it maybe the reverse order?

I mean, some of you will probably feel like it's not the same, so maybe by raising your hands, how many of you think program four is the first one to be logged?

Yeah, maybe a bit less people.

It's not, I'm sorry.

It's actually program one.

It's not the last order, and it's not even the reverse last order.

It's another completely different order.

This one I really didn't know at all before digging into it.

So if we have a look at the math, this is still a dev-first algorithm, but this time it's post-order, which means it will first look at the left path recursively, then the right path recursively, and at the end it will execute the node's code.

So, for our example, what it means is that it looks at root, but before executing root's code, so before logging the root effect, it will first look at the left path of root, which is row 1 and its recursive, so same thing for row 1.

Before logging effect row 1, it looks at the left path, program 1, and now that program doesn't have any more children, there's no left or right path, so it can execute Program

1's code which will log effect Program 1, comes back to Row 1, goes to the right path, so it looks at Program 2, then it can log Program 2, and then for Row 1, all of the children of Row 1 have been dealt with, so now it can execute the code for Row 1 and log row one. And then you continue this algorithm, you go to the right path from root, same order pretty much, four, five, six, and then for root, well, every children have been dealt with, you can log the effect of root. How many of you knew this behavior in React? Ah,

Good. I didn't.

So just to recap, this is the order for render and useEffect.

But if you remember what Pierre showed you earlier, when we register the row1 as a child of root, root needs to exist first.

Because you can't say row1 is a child of root if you haven't created root.

That's a limitation of LRD.

But the thing is, when you register the program with the useEffectOrder, program will be the first one to be registered.

And it will be registered before row1 is created.

So that's why we see this error.

It can't find row1 when it's trying to register program1 as a child of row1.

So that's why the app didn't work earlier.

What we want here is actually to use the render order, because it would work.

You would register root first, and then it's general.

And our solution here was to create a custom hook, which behaves like a use effect, but the effect runs during the render phase.

So it's a bit tricky.

Let's look at what it's like.

We called it "Use Before Mount Effect".

I mean, disclaimer here, this wording is strange, not exact.

We just really want the callback, like the effect to run during render, not during the effect phase.

But I think this wording is a good compromise between clarity and exactness. beforeMonth signifies for us that it's before the effect phase, before the component is already created during render.

And in its most basic form, this useBeforeMonth effect is just going to call the callback instantly, not inside the use effect, obviously.

And, I mean, you don't want to call this callback on each re-render, so this is where you would add some logic to only call it the first time.

And second big disclaimer, maybe some of you already think like this looks like a code smell.

It does look strange indeed.

We're using useRef and trying to call effects during render.

We only use this for special navigation.

Nowhere else in the app. but there's a big warning in the code.

All the developers know that they shouldn't use this everywhere, but for our use case, it worked really well.

And this is actually lacking some things to be more complete and to look a bit more like a use effect.

So we need three more things.

First of all, a way to deal with dependencies and to rerun the callback if the dependencies have changed.

And also a destructor, maybe also known as the cleanup function.

So inside the useEffect, the cleanup function is the function that gets called before the component is unmounted or before the effect reruns.

And usually it's where you handle any cleanup task, like unregistering the nodes in our case.

This is how you would do it.

Finally, we also need a way to call the cleanup function on unmount.

Sadly, when a component unmounts, we don't really know it during render, because when it unmounts, it doesn't render.

So we had to use a regular use effect destructor that gets called on unmount.

This doesn't guarantee the order of the destructor.

But in our use case, we don't care either because we have to create the node in the right order, but we can unregister them in whatever order.

So now we can just use our useBeforeMount effect instead of the use effect.

You know of any other way to achieve this order behavior.

You can come see us at the end

'cause we would be very interested in knowing it.

But yeah, sorry, for us it worked pretty well.

And so if we have a look at the app now, does it work?

Sadly, still nothing happens because we are missing one last thing, which is a way to keep track of which element is focused to show it to the user.

But now the nodes are well registered in the right order.

So to keep track of the focus state, we can just create a state and update it with the callback that LRUD gives us, the one that Pierre talked about in the beginning.

And we pass this information to the children with the child function pattern.

So this is what everything would look like.

This is how the program receives the focus information and updates the program layout, like for this red border.

Maybe the program is a bit bigger.

Some animations if you want.

And I guess that's pretty much it.

That's how we build this simple page.

We have a node that creates an ID, registers itself in LLD in the right order, and can give its children its ID thanks to nested context.

And I mean, the node is not used a lot.

Lots of the time, the developer, we only build this page.

And it works pretty well for our use case.

With this code only, you can achieve the example we showed you earlier.

- Well, Mathieu lied.

That's not really it.

There are many other challenges.

That's only for basic applications.

But we had many other things to handle.

We don't have the time to cover them.

Among them, you can think of handling the scroll, which you have too many elements on the view.

Handling pages off the top of each other with the right navigation.

Having a side menu that is common between these pages.

Navigating in virtualized lists, which was the hardest problem we had.

Even worse, having these virtualized lists refreshing their data and shuffling the order.

It was quite a struggle.

And handling the default focus, which was quite easy, actually.

But it is something to handle.

So what saved us?

Well, we came from something very imperative.

It took us three hours to add a simple button, because we had so many things to know with our first iteration when it came to adding a component in the spatial navigation.

There was no real proper abstraction.

You had many clunky declarations everywhere.

And just thinking an API that is declarative and embracing the React way, we came to something so much easier to use.

The code is readable.

It's purely declaration.

You barely even need to know that the spatial navigator exists.

So now, adding a button is just one minute.

You just add the button, add the callback on select,

And that's basically it.

And you cannot imagine the joy in our eyes the first day we saw this working.

It saved us so much struggle.

So thank you for listening to us.

It was by far the most interesting problem for us during our career.

And we hope we shared the passion to you.

We hope at least it intrigued you or you learned some stuff.

And we'll gladly take your questions and have a chat afterwards around the coffee.

So thank you.

Thank you.

[APPLAUSE]

Thank you, guys.
