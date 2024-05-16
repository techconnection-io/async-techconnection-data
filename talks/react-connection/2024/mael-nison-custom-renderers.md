---
slug: /talks/react-connection/2024/mael-nison-custom-renderers
date: '2024-04-22'
title: Custom Renderers
author:
  - Maël Nison
video: ya1byUuxHaI
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/ya1byUuxHaI.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
[Maël]
So thank you for being there to listen to my talk. Today we're going to talk a bit about custom React renders, which is kind of similar to what Sarah talked before in her talk about 3GS being used for React, but we'll go deeper into the usage that we can do of that. So my name is Mael.

I work at Datadog as a staff front-end engineer on front-end developer experience. And I have to admit that I'm not super familiar, well, I am familiar with React, but I don't use it every day. I'm not a product developer.

I don't build websites. In fact, one of my most popular websites is this one. No, don't laugh.

I'm sure that you have done the same thing as well. Anyway, one thing that I'm experiencing are CLI tools. I maintain Yarn, the CLI package manager for JavaScript.

And you may not know this, but we actually use React in Yarn. I know that it might sound surprising, but are you familiar with the command Yarn upgrade interactive? When you run it, it shows something like this.

And in order to power this, we are actually using React. This exact interface is powered by code that looks similar to this. So you can see it's raw React.

Before digging into how we managed to do that, we are going to talk a bit about how React works under the hood. It's very simple. Don't worry.

First, you have a state in your application. React gives you this state using the useState hook. You consume this state, and you produce some GSX in output.

This GSX is turned by React into a GS object, and this GS object is then diffed by React in order to extract the changes that occurred between one render and the next. So for instance, here we see that React notices that only the content changed, so it generates a diff that contains that only this one property needs to change. Then this diff is turned into a DOM call.

In this case, it's a getDomElement by .innerText. So this is very schematic. Of course, there is no getDomElement function, but you get the gist. We saw that React is able to turn something that is abstract, so the content property changed into something that is concrete, changed the property of the DOM element.

What if instead of the DOM, React could actually call something else in order to render to a different target than the DOM? That's what custom renderers are. For instance, here, if we were to assume some 3D space, we could tell React that the props.x property is now 100, whereas the props.y property is now 60, and I notice that there is a typo on screen. It is x and y. For instance, here we have an example with 3GS being used in order to render a React application. So it's not as fancy as PS1 case, but you see that those triangles are working just fine, and we can change their color using a cyan, for instance, using React.

That's the kind of thing that we can do if we were to render to a different target than just a raw HTML. How do renderers work under the hood? It all starts from one package, which is called React Reconciler.

It's a very advanced package, and the documentation is there, but it's sometimes a bit difficult to understand. We are not going to dig too deep into each function, but there is one thing that I think is interesting, is that you have a lot of functions that are very similar to what you would get on the DOM itself. For instance, you have the appendChilled function, which is translated into the appendChilled function from the DOM itself.

You have insertBefore, which translates into insertBefore from the DOM itself, etc. You have a couple of more complicated functions, which are specific to React. For instance, here you have a support mutation that instructs React about some specificities of your renderer, but generally speaking, you don't often need to worry about them.

They can be no-op in many cases, and it will work just fine, as we are going to see in an instant. One thing that is interesting, though, is that React custom renderers are intended to work with retained-mode rendering. I'm going to talk to you a bit about that.

You have two modes of render when you're rendering some information on screen. You have retained-mode rendering and immediate-mode rendering. Immediate-mode rendering is when you're basically sending all the commands required to render your application on screen each time there is a render, so each time there is a frame.

For instance, that's what WebGL or even OpenGL does. Each time you want to render something, you always perform the draw commands again and again and again. With retained-mode rendering, instead, you build some kind of trees, and the system has the knowledge of the objects that exist and can preserve them from one render to the other.

It's much more convenient to work with retained-mode rendering. But immediate-mode rendering is how some render targets work. So for instance, the canvas, WebGL, the terminal itself, although it's a bit different, all those are immediate-mode, which means that in order to make them work with React and with the retained-mode that it expects, there is some kind of work that is needed.

This is an example of a renderer that I wrote myself, targeting the terminal itself. Most of the code is about turning immediate-mode rendering into retained-mode rendering. This is possible by building some translation from a tree to a list of actions to perform for the render.

However, the React part itself is very small. So this is everything that I needed in order to make it work with React. So less than 300 lines of code, and it could integrate with React from a generic library to React.

As you can see, a lot of functions were no-op and didn't need to be implemented for the basic use case. It still supports updates, so when a prop's changed, I get the same change inside my application. I get a text node, so everything is working fine.

This is Terminosaurus, so it's a renderer that I wrote, as I mentioned, which targets terminal so that you can write terminal applications using just GSX. What does it look like in practice? You have your GSX script that contains the term div elements with a bunch of CSS-like properties like border, padding, padding right, font, text decoration, even click handlers.

And it gets turned into a terminal application. So here you see that we even have the scroll that works. We can have some text editor that is working just fine.

We can have a full text editor that supports Kodak Lightning, or even you can have just a bouncing ball that gets around on screen, and which is implemented in React. It's just this regular old application where you have a div and you update its position every frame. So what renderers are you aware of that works in production?

Because renderers are somewhat advanced use cases. Can we actually find them in the wild? There is one that you know for sure, React Native.

React Native is a custom renderer in a sense, because React by default can target the DOM using the React DOM package. That's why React DOM and React are separated. React DOM is just the DOM-specific part of React.

But React Native is another renderer that targets another render target than the DOM itself. So React Native is a custom renderer. And here, so it's technically React Native Web that I'm using, which is another custom renderer itself than React Native itself.

So React Native custom renderer. React PDF renderer is a custom renderer that allows you to target PDF files and to generate them using React. So each time you make changes to the file, it gets synced into the actual PDF that is generated.

You have React 3 Fiber that Sarah presented you before that allows you to use 3GS and actual 3D and put it inside your web pages. You can do complicated interfaces, or you can use it for a more subtle developer experience inside your apps. You have React Roth Fiber, which can be used in order to wrap SVG to turn them from clean SVG objects into things that look like they have been drawn by hand.

That's a custom renderer that is using the Roth.js library. You have a large list of renderers. It has been compiled on GitHub with a bunch of some experimental, some production-ready mix.

For instance, you have a React GTK, React QML that allow you to build native applications using Qt or using GTK, using Proton. You have a lot of options. However, a lot of those are very experimental, have been built as prototypes, and may not be used or may not be suitable for use in production.

But they still exist nonetheless, and if at some point you want to build yourself a renderer that would target a native environment, you can read their source code in order to figure out how they did it and how to replicate this in your own project. As you can see in the Terminal Service Library that I showed you before, building a custom renderer for React requires, most of all, to read the documentation and to try to understand it. But in terms of code, it's very light.

Now the question is, should you actually use renderer? In which situation is it a good thing to use them? In which situation should you avoid that?

Custom renderers have a couple of issues. First, they are retained-mode rendering only. So as I mentioned, if you are targeting something where you need to perform all the render commands before each frame, there is more work required in order to turn your objects into something that can render at each and every frame.

Documentation can also be sparse. So on top of reading GitHub, you sometimes have to look deep into the source code of the applications that you want to replicate in order to see how they used some AppEngine function, some commit update function, to see what is missing from your own implementation. And of course, not everything needs to be JSX.

One big advantage of React is that it can be used to enhance the interactivity of your application. Each time you make an update, it gets replicated on screen. So applications that get a lot of updates are more suitable for JSX than something where you would render once and be done with it.

In the case of PDF, for instance, we could imagine that it could have been possible to write a JSON converter that would take a JSON payload and convert it into PDF. There is no update that gets required. You don't need to have HMR. So you have to weigh the pros and cons of using custom renderers versus a more simple approach. However, custom renderers are also very useful for some very specific reasons. First, their usage is transparent. It's JSX in custom renderers, but it's also JSX in the rest of your application.

So you can merge the two together, and it works very well. For instance, what we saw with the Roth JS library, where you just have some SVG inside your application, you wrap it inside the Roth JS component tag, and it gets rendered through this React renderer. It also works well with the statefulness of React.

So if your application requires interactivity, then it's perfect, because React will properly diff the components that chat and will be able to reapply the new property and update the appearance of your application on screen, even if you're targeting something else than the DOM. It also integrates well with React libraries. So for instance, something that is using the standard React functions, like useContext or useState or useEffect, that's something that you will be able to use inside your custom renderer.

For instance, it could be possible to implement an application targeting 3GS, so 3D, but use Redux, Redux toolkit, in order to preserve the state of your application and to trace it across multiple pages. Because you could use a router, a memory router, inside a 3GS application. That would be possible, as long as it doesn't depend on the DOM itself.

That's doable. And finally, you have access to hot module reloading while you're developing your application. That's something that I implemented, for instance, in my renderer, in order to see live the changes that I was making in my source code directly inside my terminal without having to kill the process and restart it.

That's good developer experience. Thanks. I hope you enjoyed this presentation and how I talked about different tools.

If you have questions, feel free to ask them.

[Christophe]
Thank you. Please come over. Thank you.

Custom renderers. I love that. I was just curious whether you had, like, a particular favorite among all those...

Custom renderers? Yeah. Yeah.

Custom renderers you mentioned.

[Maël]
I really like terminals. I actually started to get involved in custom renderers seven, eight years ago, when they were very prototype, because I wanted to implement a custom renderer for terminals. And Terminosaurus is a modern version of this early work that...

[Christophe]
Because we have, like, Ink and React, Blast, and everything for the terminal.

[Maël]
Exactly. But before, we didn't have that. So when I started Terminosaurus, it was under a different name.

[Christophe]
It predates those.

[Maël]
Exactly. It predates them. I wanted to use...

To render on the terminal, because I was building a Game Boy emulator, and I wanted to build a debugger for it. However, it was too slow to have the debugger inside the browser, due to the DOM override. So I wanted to bring it to the terminal, but only Blast existed at the time.

I couldn't really implement the UI I wanted as efficiently as I wanted, so I decided to try my hand with this new, weird interface that allowed you to use React for anything.

[Christophe]
Okay. Cool.

[Simone]
Why going specifically with React renderers instead of other solutions? I mean, it's not the only framework library that supports custom renderers, is it?

[Maël]
Nowadays, you have other frameworks that start to use custom renderers. For instance, I think that VGS is supporting them. However, the custom renderers in React are very mature, and they are used in very significant production use cases.

So React Native, as I mentioned, is a custom renderer, so the React team is putting a lot of effort in making sure that they can do anything that the DOM implementation could do. So basically, it's more mature, so it better fits.

[Simone]
A question from the audience. Well, we actually answered the first one. And which renderer are you currently using with Yarn?

Yeah. Well, which one?

[Maël]
Which one?

[Simone]
I mean, so it's just a custom, specific renderer just for Yarn? It's not about...

[Maël]
For the interactive upgrade feature. Oh, so for interactive upgrade, we are currently using Ink. And if Terminus Ares continues to be a project I'm interested in, we are probably going to migrate towards it at some point.

Okay. Awesome.

[Christophe]
All right. Thank you very much, Manuel.