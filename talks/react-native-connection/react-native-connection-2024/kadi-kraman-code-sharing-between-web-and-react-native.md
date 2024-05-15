---
slug: >-
  /talks/react-native-connection/react-native-connection-2024/kadi-kraman-code-sharing-between-web-and-react-native
date: '2024-04-23'
title: Code Sharing Between Web and React Native
author: Kadi Kraman
video: OQNDmej3sgE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/OQNDmej3sgE.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: react-native-connection-2024
allow_ads: false
---
[Kadi]
Bonjour. I'm Kadi Kraman, I work at Expo, and today I'm excited to talk to you about code sharing between web and native. So, for as long as I've been a React Native developer, which is several years now, there's always been this discussion about sharing code, sharing code between web and React Native.

Why are we so interested in code sharing in the first place? Well, if we look at the trend in the past decade from the so-called smartphone era, what's happened is the amount of time people spend online has increased overall, but in particular, it's shifted towards mobile usage. People spend more time online on their phones than they do on their desktops.

Moreover, when we look at what people actually do on their mobile phones, they strongly prefer using real native apps. So, only 10% of time using a mobile phone do people use on mobile web. And this tells us that mobile web is not enough for most smartphone users.

So, as a company, as a person looking to create your next online presence, really, you don't have too much of a choice between mobile and web. You kind of need to provide for both or risk alienating half of your user base. In a lot of cases, though, there is a significant amount of overlap in the feature set between web and native.

So, for example, for Spotify desktop, web and mobile, they all do the same thing. So, as a developer, it is very tempting and desirable to be able to build features once and run them on multiple platforms. Now, as React Native developers, we are in luck when it comes to code sharing, because we can already do it.

Always bet on JavaScript, right? With React Native, we are already building for two totally different platforms, a native iOS and a native Android app. And with React Native web, we can also build for the browser.

So, code sharing for us is already possible. It's really the nuance that needs work. When I say the nuance, I'm talking about things that can't be shared.

So, because we're writing JavaScript, we can run it on a browser with React. We can run it on a native environment with React Native, and we can run it on a server with Node. But there are areas on each of these platforms that can't be shared, such as accessing the browser window on the web, adding secrets on a server, or using mobile-specific features like haptics on mobile.

So, I'll put together my code sharing wish list. I want a single code base. So, not a monorepo, not an internal package.

I want to be able to build and deploy my code separately for each platform. I want to still be able to access all of my platform-specific capabilities, like haptics or native. And I want my app and website to look and feel befitting to a platform.

And finally, I want to be able to easily link between my web and native apps. Now, let's see how ExpoRooter v3 can make my code sharing dreams become a reality. On a very high level, ExpoRooter is an open source package, and it's a file-based routing for React Native.

If you've ever used something like Next.js, you're probably already familiar with file-based routing. But let me show you by example how the same thing can work for React Native. Here, I have a pretty straightforward user flow.

I have a stack of two screens, a home screen and a product screen. And when I click on view product, I'm going to open the product screen. With React Navigation, it would look something like this.

I'll define my two screens, a product screen and a home screen, and I'll have my app.tsx. For a React Navigation project, your app.tsx is the main entry point for your application. So, this is where I define the navigation container, the stack navigator, and I also describe how I want my screen to be laid out. So, in this case, in a stack.

This is how the same app would look like with ExpoRooter. Notice that we no longer have an app.tsx. Instead, we have an app folder, and this app folder will be the root of our file-based routing. We've also created our two pages.

So, we have our index page, which will map to the index route, and we have our product page, which will map to the product route. You'll notice that there is one more file there, and that is the layout file. And layout files are really the key to what makes file-based routing possible for native apps.

In this layout, I'm importing stack from ExpoRooter, and I'm defining that I want all the routes in this folder to be rendered in a stack. Notice that unlike with React Navigation, I'm not listing out all of my screens, because that information is already given to us by the file base. In most cases, however, you would actually end up listing the screens, not to list out what needs to be in the stack, but to provide additional options.

For example, the title for each of the screens. When it comes to navigation between the screens, with React Navigation, you're probably used to using the use navigation hook. You will call navigation.navigate, pass in a navigation object with the screen name, maybe some parameters, and off you go. With ExpoRooter, navigation is URL-based. So, every single screen on your application is defined by a unique URL. So, if you want to navigate by pressing a button, you could import link from ExpoRooter and surround the pressable area, the area you want to be pressed with the link component, and pass in the href to where you want to link to.

It's also possible to do this programmatically using the use router hook. What about dynamic routes? Say I wanted to have a product and product ID, with the ID being dynamic.

You can turn any folder or file into a dynamic route by surrounding it with braces. So, in this case, I've converted my product file into a folder, and inside this folder, I've added an ID route, which is dynamic, because it's surrounded by braces. And in this case, slash product slash 123 would map to this ID route.

Now, in my index.js, instead of linking to product, I'm going to link to product 123, and inside this dynamic route, I can access the ID using use local search params. The thing to bear in mind is that ExpoRooter is essentially built on top of React Navigation. So, everything you can do in React Navigation is doable with ExpoRooter.

However, you get a lot of extra functionality. Let's talk about creating web-specific components. As React developers, you've probably encountered having to create separate components for iOS and Android, and what do you do?

You add you can well, you have a couple of options, but usually, you could create a file with an iOS or an Android extension, which will then be bundled as appropriate. And you can do the same for web and native. So, you can use a dot web or a dot native extension, and then, when your JavaScript gets bundled, the correct file is getting pulled into the correct bundle.

The great thing about this is, because you know that your web-specific file is only ever going to be rendered on the web, you can add web-specific code there, such as HTML. When it comes to screens on your website and your mobile app, it often makes sense to have the same screens for both platforms, and it makes sense to have the same URLs. What doesn't always make sense is to have the exact same navigation.

So, to look at an example, so this is a two-tab bottom tab layout, pretty standard for native apps, and on the right, you see the same layout on the web. Now, this may be exactly what you need for your application, but sometimes, you may not. So, on the web, for example, we're not used to seeing bottom tabs.

We kind of want our screens to be scrollable all the way to the bottom. We want a header and we want a footer, and this is where our layout files come in handy again. In the layout files, I can simply check if I'm on a mobile or a web environment and render the screens as a stack or as tabs, as appropriate.

You can also use the same method to add platform-specific code. So, for example, you could add a header and a footer in your layout only for the website. I want to also show you a slightly more complicated looking example for file system-based routing.

So, this is rendering the slash blog route, and if you go, if you see, I'm starting from the app folder, and then I'm going into the home folder, but home folder is not included in the path, because it's surrounded in braces, so it's just a grouping, and then we go into the blog folder, which is included in the path, and we want to go to the index route, which isn't included in the path, so all of that long file system path ends up being just slash blog, and when you access the slash blog, the way that it gets rendered is that all of the layout routes get rendered in order from the outer to the inner one, and then finally the index file itself. Quick side note, because this comes up a lot, what about platform- specific routes?

We've seen that you can do platform-specific components, you can have a web component and a native component, so could you have a platform-specific route in your app folder? Could you have a web route and a native route? You can probably tell from the phrasing of this question that you cannot, however, it is not, it is a restriction within the app folder that you can't have file system-based routing that are platform-specific, however, this is not really a problem in practice, because you can get around it quite easily by redirecting away from the, with the platform that isn't supported, so for example, for this native-only route, I can check if we're on the web, in which case we redirect away to a fallback route. When it comes to server code in React Native, it's always been a bit of a pain.

React Native apps are inherently front-end apps, we are writing front-end code, we can't add secrets there, and it's always been difficult to figure out how to work on your, how to do your API requests, like where do you put your API keys, and really the only correct solution for that is to have your own API. You need to create your node API, for example, you need to have a separate repo, you need to deploy it, you need to manage it, and then use it in your application. From expr-router-v3, you can write server code directly in your React Native codebase, so this is only available in server mode, so in your app.json, you have to change the web output to server for this to work. After which, however, you can create server-specific code, you can write, you can write, you can create API routes, so in your app directory, any file can be an API route if it has plus API at the end, and in this API route, you can write get or post requests by exporting them as async functions, so, for example, I've added a get request here, which it doesn't, it's not very exciting, it just returns an empty array of products, and I've added a post request here, which reads from the request body and returns the product ID from the request body. Like I said, it's not a terribly exciting example, but I did want to show you that I can now access the get request in my browser and I can access the post request from my REST client. Now, we've gone through web, native, and server, and we've seen how you can create web, native, and API code in one codebase and keep it separate.

Everything else is shared by default, and think of how powerful this is. For web and native, you're going to inherently be sharing a lot more, because they're both UI-based, but even for server, you could have a utility function for passing dates, for example, which you can use on web, server, and native, and also in a TypeScript codebase, it makes sharing types incredibly straightforward. Now we've talked about all the platforms, how do we actually go about deploying these?

I won't go very deeply into how to deploy native apps. Suffice to say, deploy it as normal, but, for example, if you're using EIS, you can use EIS build platform all, or just submit to build your native apps and automatically deploy them for both stores. For the web deployments, you start by running mpx export export, and this creates the server-side bundle in your dist folder.

It creates a dist folder, which has all the server-side code necessary to deploy your website and your API routes. After that, you will also need an adapter, which supports the Expo router runtime on the server, so we have adapters currently for Express, Netlify, and Vercel. I've added a link at the bottom for the API route documentation, where you can see the actual code on how to deploy it, and a bit more examples.

But, suffice to say, we're actively working on the deployment side of things to support more platforms and make it a lot more straightforward. As you can tell by the beta ribbon there, this is very much work in progress still. We're actually working on it, but it's already available on SDK 50, and it's very much ready to be played around with.

Now, you can build for as many or as few platforms as you need to. As ever, you can build just for iOS, just for Android, or iOS and Android, or in our case, just for web. So, when it came to moving the Expo blog from Medium to our own site, we actually decided to do a bit of dogfooding and use Expo Router for that.

So, this is a website that doesn't have a mobile app. We are not even using a lot of native components. We're using Tailwind, we're using HTML, but we decided to use Expo Router to battle test it a bit.

It was a very interesting experience. We learned a lot. We learned what needs to be improved, and it's also proven to us that this is something that's worth doing and worth pursuing.

That's about it for me. If any of this was of interest, I would recommend you check out our docs. We have quite a lot of documentation about it.

We also have a Discord that has an Expo Router channel that you can join, and if you want to try out any of the examples that I talked about, if you use create Expo app with the tabs template, it will have the native and web already set up, and you can also play with API routes. Thank you very much.

[Mo]
Thank you very much, Cady. Would you like to come into the interview room? Sure.

Just grab this seat, and I'll pop around here. Awesome. So, great way to start the morning.

As Arthur mentioned, we're very passionate across BAM and Theodo about doing universal apps and co-chairing between web and mobile, so right up my alley in terms of the stuff that I'm very, very excited with, so lovely to have the chat with you. Cool. So, first question, and I'll kick this off myself, and then maybe we'll take some of the questions from Slido.

First thing that comes to mind is Expo seems to be building an entire almost framework, right? It does all of the routing, it does all of the building process, and a way for you to actually handle the submissions, and so on and so forth, and it's targeting web and mobile now. I'm curious to get your take on how much of what you're doing on the website is kind of competing with Next.js, and there's already existing paradigms and existing implementations with frameworks like Next, where they already have things like tree shaking and streaming and all of that implemented. How much of it is a catch-up game, and how much do you think there's a difference between what you're implementing versus what Vercel already has?

[Kadi]
I mean, I wouldn't say that we're competing per se, because we offer an inherently different product. I mean, obviously my example of building the Expo blog with Expo Router was a chance to battle test it ourselves, which is, you know, we try to do it anyway, but the main use case for Expo has always been to build mobile apps, so we are really, really, really good at letting you build mobile apps, and we are adding a web capability that is integrated into the existing experience, and Next.js generally just do a really, really awesome job, and we are often inspired by their feature set, because they've figured out what users need.

[Mo]
And so the current implementation of Expo Router is using Metro for web under the hood. There's a switch from Webpack to Metro, I think on version 49 or 50, if I'm not mistaken.

[Kadi]
I think it was. I thought it was 50, but...

[Mo]
Yeah, I'm not sure. So what was the philosophy there, if you're familiar with the decision-making there, and what have been some of the challenges of trying to get Metro to work on web?

[Kadi]
I'm not sure that I have a lot of answers to that, but I think Evan's done a huge amount of work to make things like front-end splitting possible, to make Metro a lot faster for web in specific. You know, you can use CSS in Expo Router, and there's a ton of features to have like Metro almost like catch up, but also, you know, be more feature-rich to support what we need.

[Mo]
Yeah, and Evan's done a great job, like you say. So very exciting to see what's coming out of that. Okay, cool.

Let's go to some audience questions. So firstly, let's just do a few quick round fire ones. Can you use Expo Router v3 with React Native version 68?

Somebody needs tech support, so please reach out to any of the folks at BAM. This is not marketing. No, jokes aside, can it be used with 68?

I don't know is a very valid answer here.

[Kadi]
I feel like it can't. There was something in SDK 50 that is important for Expo Router 3. Like there were some significant changes, so when you upgrade, I think you have to do.

[Mo]
I think it was the Metro config and the Metro runtime was customized, I think.

[Kadi]
Yeah, there was a few things, but basically the answer is you need SDK 50.

[Mo]
Cool. All right. Does Expo Router handle notification linking and universal links itself?

[Kadi]
It's highly integrated, so if you ever build universal linking, it's kind of when you set up Expo Router for the first time, it makes you choose a scheme, so it's highly integrated. So because you're in your file system already, everything's in the same place, then setting up linking between web and native is, well, the experience is the easiest you've ever had when you're used to doing it in native.

[Mo]
Cool. What about server-side rendering for Expo Router and Expo on the web?

[Kadi]
Yes. So that's one of the things that we are still working on, and it's very important, personally, like building the blog, that was like the main difficulty that server-side rendering right now isn't supported. So the components are coming and server-side rendering is coming as well.

It's just quite early days, so watch this space, but if you start now, you can be early adopters.

[Mo]
Cool. We've got a question about building for desktop platforms, and I think it's more Expo-related than Expo on the web, but basically the question is how do you see this being available for desktop apps, this universal vision of sharing between web and native? How can we extend that?

Does Expo have any plans to support, you know, Windows applications, Mac applications, TV we've recently seen you guys introduce? So what's the vision there, if you're aware of that?

[Kadi]
We've added TVOS. I don't think there's like a strong incentive right now for the native platforms, so it wouldn't hold you back there.

[Mo]
Cool. And last one, and this is an interesting question, which is how do you migrate progressively? So if I've started my application in React Navigation, and I want to introduce Expo Router to some degree in that existing project, is there a good way?

It might be something to go away and work on, if that's something that's of interest to people.

[Kadi]
So it's a bit tricky, because if you remember from the beginning of my talk, when we go through the example of the same thing in React Navigation and Expo Router, the main entry point of your application changes, so as part of adding Expo Router to your application, you actually, in your package.json, you change the entry point. So the main how you go into your app changes. I think it could be possible to render your app with Expo Router and then render your existing app within the index route, so you could explore doing that, but I haven't tried it personally.

[Mo]
You're playing with black magic, whoever submitted this question, so it's at your own risk, okay? Cool. Thank you so much, Kadi.

Big round of applause for Kadi Krammen. Thank you.