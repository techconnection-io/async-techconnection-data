---
slug: /talks/react-connection/2024/francois-zaninotto-single-page-apps-are-not-dead
date: '2024-04-22'
title: Single Page Apps Are Not Dead
author:
  - Francois Zaninotto
video: H-_fyb2scC0
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/H-_fyb2scC0.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
### François
It's a pleasure to be here at React Connection. I'm here to talk about our web apps and more specifically about the merits of the single-page application architecture. First a few figures about myself.

I'm a software engineer. I work at a company called Marmolab that I founded 11 years ago. I started contributing to open source a long time ago and I've never stopped since.

I'm the lead developer of React Admin. I'm French and I live in Nancy. You can follow me on LinkedIn, but since I'm here, please come to talk to me in person at the break.

Let me start with a question. How many of you have started a new Rack project in the past year? Yeah?

Quite a bit. But if I ask you which framework you chose, the answer will probably be very diverse. The React docs advise you to use Next.js, Remix, or Gatsby. In the past, the same docs suggested using Create React App, and third-party frameworks like Redwood or Astro are already quite popular in the Rack community. And finally, you can use React without a framework with bundlers like Vite or Parcel, although the Rack docs explain this is a result for unusual constraints. So the choice is not straightforward, and the two most recommended frameworks, Next.js and Remix, have some issues. First, they both use file-based routing. This convention lets you define a folder hierarchy that translates into routes. And file-based routing implicitly encourages developers to place components in the folders of their page, and shared components outside of the route hierarchy.

This Next.js app uses many conventions to define only four routes. It doesn't contain any Rack component yet, but it's already confusing, in my opinion. My experience is that file-based routing is great for simple apps, but it quickly gets messy for larger projects.

To their credit, both Next.js and Remix let you redefine routing to use your own conventions. But what's the point of using a framework then? Well, Next and Remix are not only about routing.

They are also server-side rendering, or SSR, frameworks by default. They encourage you to put the business logic and the database code in server functions, as in this Remix example, using the loader function. The lifecycle of these server functions is not the same as the lifecycle of Rack components, so it kind of adds to the complex mental model of Rack rendering.

And this means that, upon navigation, users have to wait for a server round-trip to see the screen change. By default, that means that React apps built with Remix or Next behave a bit like the apps we used to build with PHP or Python. I mean, the apps I used to build with PHP or Python.

I don't know about you. They were not that snappy. That's far from the user experience of desktop and mobile apps.

I call these frameworks PHP and JS. From that point of view, server-side rendering frameworks represent a step backwards in terms of navigation performance. And it gets worse when you introduce React server components in the mix.

This new feature lets you define components that will only render on the server-side, contrary to regular components that can render both on the server and on the client-side. In theory, you can mix client and server components the way you want, but in practice, you can only use server components up in the component hierarchy because they are very limited. You cannot use useEffect, useState, or useContext in a server component.

And on the other hand, as soon as you need browser APIs like scroll navigation or preferred theme, it must be in a client-side component. Choosing between client and server components, where to put the boundaries and how to make them communicate adds another layer of complexity. And the problems are not only with the developer experience.

Server-side rendering also affects the user experience. When the server renders a React component, it sends the HTML to the browser, which renders it immediately. The browser then downloads the React code and re-renders the component to add interactivity.

This is called the hydration process. It's not instantaneous. This means that there is a slight delay between the moment the user sees the content and the moment they are actually capable of interacting with it.

This delay feels like a bug. The application looks okay, but it's not responsive, and UX specialists call that gap the uncanny valley, and it's a big issue for SSR frameworks. So there is no free lunch.

All the rendering techniques from server-side rendering to client-side rendering have their pros and cons. Don't try to read that slide. There's too much text anyway.

But I think both Next.js and Remix solve a very specific problem, the initial load time, at the cost of a slightly degraded user and developer experience. What bothers me is that their rendering model, SSR, is the de facto standard for new React apps, even though it's not a good fit for many cases. And finally, as I said, Next.js and Remix.js are unopinionated. This means you have to make a lot of choices when you start a new React project. Should you use app router or pages router? Should you manage the state on the client or on the server side?

Should you use server components, server actions? Honestly, even after ten years of React development, I find this liberty of choice a bit overwhelming, and I sometimes envy the Svelte or regular developers who have a clearer path to follow. So, as you might have guessed, I have mixed feelings about these two React frameworks.

I think it's a good idea to challenge the status quo and to try to find a better way to start a React project. This is what I'm going to do in this talk. Sorry.

Yeah. So, before I start, I would like to define what I mean by framework. When I compare Next.js and Remix.js to other server-side frameworks like Ruby on Rails or Spring, one key difference strikes me. The other server-side frameworks implement a design pattern. It can be, for instance, MDC for Ruby on Rails or Django. In other terms, they choose a proven solution to a common architectural problem.

And they provide the best implementation they can for this pattern. In contrast, Next.js and Remix are more like a collection of tools that provide a router, a bundler, a way to handle forms, but I can't see the underlying design pattern. In my opinion, they are a bit shallow.

So let's get back to the roots and explore a few of the design patterns that apply to React development and see if we can find a better way to start a React project. And as my main inspiration, I invoke the two grandmasters of software architecture, Martin Fowler, the author of Patterns of Enterprise Application Architecture, and Eric Evans, author of The Domain-Driven Design. Both books are must-read for any software architect.

One of the main learnings of domain-driven design is the notion of bounded contexts. In order to make sense of a large code base, it must be divided into independent units that only communicate through identified interfaces that domain-driven design called domain boundaries. In React, we're lucky.

The very notion of component allows us to build a bounded context and encapsulate the logic for a given feature. The interface is the list of props. So React gives us bounded context for free as long as we can serialize props.

The limit is that we should not use prop drilling, where components pass their props down to their children because it blurs the domain boundaries. In this example, the user menu in the bottom needs a user prop and only the topmost component app has this user. So it has to pass it down to a child, in this case top bar, which will pass it down again to the user menu component.

Instead to respect the domain boundary, I'd rather pass a user menu element to the top bar so that it just has to render it. This avoids what I called God objects, which have a very large number of props and too many responsibilities. This is a form of inversion of control.

That means it's the responsibility of the parent to set the dependencies of their children, and the design pattern for this inversion of control is called dependency injection, and it's a must-have in most applications. Dependency injection is very useful for generic services, for instance to fetch the API, to store user preferences, to get interface translation, etc. This pattern is natural in React because we can use context for dependency injection.

A parent element, for instance the application shell in this example, can create a context for general propositilities like the user service, no? All its descendants can get the user from this context. Another key learning from domain-driven design is that the code should be primarily organized according to the business domain.

So if you build an e-commerce app, for instance, your code should be divided into folders for customers, products, etc. How these features translate into database queries, whether the code should run on the client or on the server, all this should be seen as secondary and hidden behind some kind of adapter. The app routes are an implementation detail.

They should not dictate the organization of your code. The way you persist data, the way you handle forms, all that belongs to the infrastructure layer and should be separated from the business logic. So how do we put all that together for a React project?

We should move services out of components, use context for dependency injection, encapsulate logic into hooks, and organize code by feature, not by route. This is in direct contradiction with the constraints of server components. Contexts don't work in React server components.

That's a huge limitation. In my opinion, until RSCs provide a dependency injection system or until they provide use context, they cannot really be used for large-scale applications. This also means we lose the main benefits of Next.js and Remix, so we can't use server components or the current generation of SSR frameworks. What can we use instead? Well, there is an architecture that allows all these constraints. The single page application architecture.

That's right. It's the good old SPA, also known as client-side rendering. A static server delivers the application code and the API delivers the data.

It's the client's job to render the interface and to handle the interactions. This used to be the default architecture of most React apps before Next.js and Remix, and it's still a valid choice. And it's the only one that allows us to organize our code by feature, to use context for dependency injection, and to hide the infrastructure behind an adapter.

But we all know that single-page apps are bad for SEO and first-load performance. That's why Next.js and Remix were built in the first place. But let's take a moment to examine these two assumptions.

First of all, load performance. Single-page apps need to download the application code, execute it, then fetch the data from the server and render the interface. So the app requires two round trips to the server instead of one for SSR. Many people advocate it's too slow and that you should do server-side rendering instead, but modern tooling like tree shaking and lazy loading allow us to reduce the initial bundle and you can display a skeleton screen while the app is loading. YouTube does exactly that, and it's not a particularly slow app. So yes, 100% of the users have slow internet, 5% at a time. And on mobile, latency makes things worse.

But the initial loading time of single-page apps isn't really an issue with modern tooling. But of course, this doesn't work if you need SEO. Client-side rendered apps are not well indexed by search engines.

And even though the Google crawler has been executing JS since 2021, it still penalizes long time-to-interactive. This, in theory, forbids the usage of single-page apps for SEO-intensive apps like e-commerce. But in an e-commerce app, not all sections require SEO.

The cold part, like the project details, do need SEO. But the hot parts, like the cart, the list of recommendations, they don't need SEO. So even if we can't use an SPF for the entire app, we can still use it for some sections or some islands of interactivity.

Next.js recently introduced partial pre-rendering to do exactly that. But you can use any tool to generate static pages previously. So I'd advise to use something faster than Next.js to do that. And many apps don't require SEO at all. Think of a dashboard, an ERP, a B2B app. In my experience, most of the apps I've worked on don't require SEO.

So why should we use SSR for them? So in conclusion, I think that the single-page app architecture is still a valid choice for many React apps. I think the popularity of Next and Remix comes from the fact that they are simply the best tool chains to start a new React project.

But if we could find a single-page app framework that follows proven patterns, that offers great productivity and the liberty to build the app the way we want, we could very much improve the developer experience. It turns out I'm the creator of such a framework. It's called React Admin, and it's open source.

It's built with Vite, React Router, React Hookform, React Query, or Tanstack Query, and Material UI. It allows you to build single-page apps on top of REST or GraphQL APIs. It follows the principles I've just described.

It's already pretty popular with more than 20k stars on GitHub, and it's not a new kid on the block. It's been around for the past seven years. React Admin can be seen as a starter kit with only four components, Admin, Resource, ListGuesser, and EditGuesser.

You can bootstrap a working app for an existing API. This example uses a feature called Guessers, which generates CRUD views based on the API response. Here is the result, a working app with a list page and an edition form for these four resources, complete with optimistic rendering, relationships, a mobile version, et cetera.

Hear me out. It's not one of those fake demos where the code on the slide is a tiny part of a very complex app. This is all the code that is necessary to run the app shown in the preview screen.

You can scan the QR code to launch this app online and check for yourself. React Admin doesn't need a gazillion root files. The eight routes of the app are defined by the resource components, so React Admin uses a central router configuration, and it uses React for that.

React Admin encapsulates the logic into hooks and puts the infrastructure layer into services, as in this example that renders a book edition form. It leverages the use edit controller hook. This hook fetches the API for a book record based on the URL parameters, and it creates a save callback that will trigger a mutation on the API on save.

Forms are complex in React, but this complexity doesn't get in the way here. The simple form takes care of initialising the form values based on the record fetched from the API. It takes care of form validation, submission, and it handles errors correctly.

If you look at this code, it's 100 per cent business logic and presentation, and zero per cent fighting against the tooling, when there is not a single use effect. I won't show you the directory structure because React Admin doesn't mandate anything on that subject. It just follows your imports.

I have one final slide to give you a glimpse of the developer experience of a true application framework. This CRM app is built with high-level building blocks provided by React Admin. All the common features of web apps like notifications, bulk actions, filters, even a Kanban board, they come for free with React Admin.

You can customise the look and feel. You can replace any framework component with your own. React Admin never gets in the way.

One huge advantage of single-page apps over server-side rendering is that an advantage I didn't mention before is hosting. You can host a single-page app on any CDN for free. This screenshot shows a note-taking app with local storage and an AI auto-completion called Writer's Delight.

It is hosted on GitHub pages. Even if you mention it on Hacker News, it will never suffer the hug of death, so please mention it on Hacker News. The reason I mention it is because I think it explains why many sponsors of the SSR architecture don't want you to know that single-page apps are better.

The goal of Verso, the sponsor of Next.js, is to hook you into SSR so they can charge you a high premium for their pass. If you ever read a bad critic about the SPA architecture, look at who is writing it. They might have a hidden agenda.

Here's my advice. The single-page app is back from the dead, and it's your best friend. If you're starting a React app, in 90% of the cases, you should use an SPA.

If you need a framework for that, try React Admin. It's free, and it's built on the shoulders of giants. Thanks a lot for your time.

### Christophe
Thank you, François. I've got some of the best speaker photos I've seen in a long time. So that was not controversial at all.

The guy starts up the RSC track with, okay, so RSCs suck, you know? I know some people in the audience who are big on clean design and everything, and they're like, oh, yeah, dependency injection, and bounded context, and I'm like, yeah, context, and then everything re-renders a gazillion times because people misuse them. But we have some good questions.

Do you want to get started?

### Simone
Yeah, sure. Well, actually, the first question you actually answered about why you think there is this push for Next.js, but you more than answered that in your talk, and actually maybe you want to close this conference down. Thank you very much for that.

Anyway, you mentioned you can marry SPA with server-side rendering where needed without Next.js and Remix. How would you go about that?

### François
Sorry, come again?

### Simone
Sorry. You mentioned that you can marry SPA with the SSR without Next.js and without Remix. How would you do that?

Do you have any recommendations?

### François
Well, yeah, you can use any server-side rendering framework and send rendered HTML, and then with React 19, I think, or React 18, you can have many routes for React applications inside the same page, so you can just add components, islands of interactivity like Astro does, but you can do that in React, and you can totally use, I would say, like Ruby on Rails, Django, Symphony, whatever you want to render the HTML page, and that's what many people are doing, and I think Next.js is reinventing this server-side rendering for static pages, but it's been done in the past with much success, so there's not much to reinvent here, I think.

### Christophe
Yeah, people haven't waited for Next to keep rendering stuff, HTML the old way, and just sprinkle interactivity with React.

### Simone
Totally, totally. A question that actually is interesting from a product point of view, is React actually a framework or just a tool to admin as an admin panel? I know the answer, but I think that the name might be not clear enough.

### François
I think it's a framework, but many people put different meanings behind that word, so to me, it's a framework in the sense that it gives you the backbone of your application around which you will build your app. The difference with a collection of tools would be that the collection of tools, you can extract the tools and replace them by another one. With React admin, I think it's very hard to remove that backbone because it handles routing, it handles form submissions, layouts, et cetera, et cetera, so it's very core of the UI logic, so the only thing is you have the backbone, and you add some layers of flesh.

### Simone
It's not an admin tool, that was the question.

### François
It's not an admin tool.

### Christophe
I think the original perception was very much using React admin for a quick and easy way to your back office kind of screens, like admin panel and everything, but you're seeing it as having evolved more towards really like a scaffolding, including for the user-facing pages.

### François
Yeah, exactly. We see many B2B apps.

### Christophe
Perhaps it's in need of rebranding, rebooting.

### François
Yeah, we're not very good at branding. But yes, it's used for many different apps, including customer-facing apps, not B2C apps, because usually these apps require SEO and pre-rendering, but for all the B2B apps, we have so many users.

### Simone
I think it's worth mentioning that React admin is actually one of, so it's kind of your own project at some point, and some personal projects at some point get stuck, and they eventually die, and you actually made, I think, some people leave about this.

### François
Yeah, so it is a sustainable open source project, and it's a great joy to be able to say here that you can bet on React admin today, and there is a team paid to maintain it for the foreseeable future, and we don't have to reimburse any VC, because we don't have any VC, and we're already sustainable. But it's easier said than done. This is something like my eighth open source project.

All the previous ones have failed in terms of sustainability, so this sweet spot of having something that you have the liberty to develop yourself, but you're also paid to do it, is really hard to attain.

### Simone
Anyway, congratulations for that.

### Christophe
Thank you very much, François. François Zaninotto, everyone.