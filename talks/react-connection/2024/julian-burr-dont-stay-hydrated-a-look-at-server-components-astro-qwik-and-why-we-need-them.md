---
slug: >-
  /talks/react-connection/2024/julian-burr-dont-stay-hydrated-a-look-at-server-components-astro-qwik-and-why-we-need-them
date: '2024-04-22'
title: >-
  (Don’t) Stay Hydrated – A Look at Server Components, Astro, Qwik and Why We
  Need Them
author:
  - Julian Burr
video: l9wnzLKjjIE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/l9wnzLKjjIE.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
### Julian
I'm going to talk about server components, they have been mentioned here and there already. I'm not going to talk much about the what they are, how to use them, et cetera. I'm going to focus more on the why.

Why do we need them? What problems are they trying to solve? A disclaimer up front.

This is not going to be a talk where I'm going to tell you you have to use React server components and if you don't, you're stupid, you're missing out, et cetera. We've already heard there's room for single page applications, there's so much nuance to how to solve your specific problem with the context of what are your requirements, what are your team, what app are you building? This is really more an attempt to give you context on, again, the problem that React server components are trying to solve so that you can go away and hopefully make a more informed decision whether or not you need them for your project.

With that out of the way, I think to understand hydration and to understand why it's problematic, we have to take a little step back and look at the history of web rendering, where we came from, how we got to where we are today, and where the future is likely going to lead us. And if the clicker is working, it is. Let's start at the very beginning.

This is like the mid, late 90s, where we were writing mostly good old plain HTML. Some of us were. Sounding like an old person.

So this is plain HTML, so it doesn't really matter if you're writing static HTML files or if you generate that HTML on the server with PHP or something like that. For the browser, it all feels very similar. The browser makes a request to the server, the server responds with HTML, the browser renders that as UI, and that's pretty much it.

Like it was simpler times, and the focus was really on that transferring static information. And then JavaScript came along. And with JavaScript, eventually libraries like jQuery that made it much more accessible for us developers to add dynamic stuff to websites, web applications.

And when I say dynamic, I primarily mean the introduction of event listeners, so suddenly we can react to user behavior and users clicking on things, users scrolling, all of that kind of stuff. But I'm also talking about application state, as we heard earlier today. Before it was like kind of tedious going forth and back on the server.

Now we can actually deal with that on the client with JavaScript. But what that actually looks like from a user experience, it was still very similar. So when the browser does the request to the server, the server would still return a bunch of HTML.

And then additionally, it would return a JavaScript file, multiple JavaScript files. And those JavaScript files would specifically target elements on the page to make them dynamic, to add event listeners, to add state. So it would need to be downloaded, it would need to be parsed, and then to be executed.

Once that's done, it actually injects those dynamic elements. And in a way, you could already call that hydration, because we're injecting dynamic parts into the static HTML. But at the time, we were much more conscious about what if the user doesn't have JavaScript enabled, for example?

I know, crazy, crazy thoughts. But it was really more used as a, could we still go static first from a mindset, and then we use JavaScript as a progressive enhancement. So in this example, we would just usually hide the buttons on the carousel, for example, until the JavaScript is loaded, until the buttons actually do something so that the user experience doesn't look broken for users without JavaScript.

So mindset is static first, JavaScript as enhancement. Then the early 2010s came along, and collectively, we apparently decided we don't care about that anymore. So we went all in on JavaScript, this is where single page applications and the frameworks like Angular, React, Vue started popping up.

And what that basically meant was two things. One, it enabled us to build dynamic large-scale applications a lot easier. In my opinion, this is still to this day the biggest step that we've done forward from a developer experience perspective when it comes to web development.

From a user experience perspective, like we already kind of heard slight hints on that with different opinions, but what it meant from a user perspective was the browser requests a page, the server returns, but the page is still blank because the server just returns an empty shell. And then a bunch of JavaScript with it. And that JavaScript, again, needs to be downloaded, needs to be parsed, needs to be executed.

That takes time. But then once that's done, the page is there, and it's already interactive, it's already dynamic. Because we've done it all in the client, so we can already attach event listeners, etc.

So this is great from a, once it's loaded, it's interactive and all good. But that initial load, especially the larger your application gets, and if you don't deal with the code splitting and tree shaking and all that, it just gets worse and worse. It doesn't scale very well.

So we might have overdone it with the everything is JavaScript. So we decided to try to go back to the server. Which is like a natural response, okay, there were good parts to that server, so let's try to get back to it.

But importantly, we kept clinging on to those client-side frameworks, kept clinging on to React in our example. And what that means is those frameworks were built for client-side rendering, they were built for that single-page application feel. So the idea was, and metaframeworks like Gatsby and later Next.js popularized it, is the idea of server-side rendering and static site generation. And I'm going to talk about them in the same way, because they're essentially the same just at different times, at build time or at request time. The idea is you run a Node.js server, that server runs all your JavaScript to create that initial HTML, so the server doesn't respond with an empty shell, but with that initial HTML, which is great. And then we just need to inject the dynamic parts, right?

But the problem is your bundler doesn't know what is dynamic and what is static. Because by definition, we're still using a framework that was built in a way that everything could be dynamic. So the bundler has to ship everything to the client, has to essentially run the same code that we just run on the server, again, to build that copy, that virtual copy of the DOM that then renders into HTML, just to inject those dynamic parts.

And this is essentially what we call hydration. And this is usually what you see next when you're in dev mode. But jokes aside, I hope with that you can see how inefficient a lot of that part is of server-side rendering and then having to hydrate the whole thing again.

I hope you can also see with that slight look back into history where that problem is coming from, that we've changed from a static-first mindset, even with the introduction of JavaScript, we're still static-first and JavaScript as an enhancement, if you will, to suddenly everything was dynamic. And even with server-side rendering, static is the afterthought that's patched onto the end. So this is where server components come in.

Server components give us primarily a way to tell the bundler what is static, only needs to be rendered once on the server, and then we don't need it anymore, and what is dynamic, what actually needs to be shipped to the client and needs to be hydrated. This is why the approach is called partial hydration, because hydration is still going to be a thing, but we are actually explicit about what needs to be hydrated. The other thing that server components do, and I think is even more important, is it forces us back into the mindset of static-first, and dynamic as an opt-in, or rather, you opt out of the static behavior as a developer explicitly.

What does it look like actually in action? So let's imagine we have, like, a simple demo application here. It's like a search for movies.

You can type in whatever you want. We take that search term. We go away to a REST API or GraphQL API.

Fetch any matching results. We render those. The user can click on any of them, and we, again, go away to an API, fetch the details of that page, and we want to render that.

For the sake of this demo, we also want to have a like button, so we want to keep track of what the user likes or doesn't like, but we don't want to build a back-end architecture around that, so we're happy to just store that on the client in local storage, for example. So we have all of that. For the purpose of this demo, to compare server-side rendering with React server components, I'm going to use Next.js' old server-side rendering model and compare it to the new app product. I want to be very clear that server components are not exclusive to Next.js. They're a React feature. Next just happened to work very closely with the React team and happened to just release this new app product very recently, so just to keep that in mind. So for anyone who's used Next before, this will look very familiar.

We're just looking at the details page here, and the main things are at the bottom. You can see get server-side props, so that's your way to do stuff on the server, fetch the data, and then inject that into the page component. And then in the page component, we might want to do some data manipulation.

So I'm using Moment here mainly for the meme, but you probably want to do some data-forming stuff even if you use, like, a lighter library. But there's other use cases, like here we ‑‑ our API is returning descriptions and reviews and stuff as markdown. So we have to transform that markdown into HTML that we can actually render.

Those libraries are usually very heavy, and we can see the effect of that in a moment. The like button, try to keep it simple, so it has a click handler that just sets a state, and then we persist that state with the third-party library that deals with the local storage. To see the impact of that hydration thing and the bundle not knowing what's static, what's dynamic, we can go to the dev tools.

So there's two parts of the dev tools that are pretty interesting for us for this particular case. We probably want to take a look at the network panel. The network panel obviously gives us a list of assets that we load and the size of them.

So that's interesting for us. We can see here there's a bunch of JavaScript files. There's a bunch of JavaScript chunks.

And some of them are actually pretty large. So if you look at chunk 2, chunk 3, they're very sizable. To see why that is, in dev mode, a lot of people don't know that the sources panel can be really useful because Webpack and other bundlers, they expose what Node modules they're actually bundling with the application and what they're shipping to the client.

And here we can see that Node modules folder is full. It's packed. And that's not too surprising.

Node modules is that black hole in web development. But it's really annoying because especially the big dependencies like markdown, like moment, we know we don't need anymore. We know it's only needed to render the data that's static.

But it's still shipped to the client. So how does it compare to server components? If we change the code, we've already seen some snippets here and there in earlier talks.

Server components by definition only run once on the server. So we don't have to care about lifecycle methods. We don't have to care about anything else.

So they can be asynchronous functions and we can fetch data within them. This is great for multiple reasons. But one thing that I want to call out that I don't have time to actually go into, a huge difference from a user experience here is compared to the service head rendering, the service head rendering, the get service head props is blocking the response of the server.

So whatever you're doing, the server hasn't responded yet and has to wait for that. And then it responds with that full HTML. With React server components, it uses suspense under the hood.

So this is actually not blocking. It will still return while this is loading in HTML with the fallbacks, if you define any fallbacks. And then stream in, Mo mentioned it with, like, out of order streaming.

This is the power of suspense and I think it's magic. It will stream in those elements when they're ready after the server already responded. But the rest of the component still looks the same.

So we still do the date formatting, we still do the markdown to HTML rendering and all of that. And our like button, like I already said, it actually has a lot of dynamic parts to it. It has an on click handler, it has state, it has a use effect, it has local storage that it tries to use.

So this definitely has to run on the client. We can't run that on the server. So all we really need to do to make sure that that runs on the client is add that directive to the top of the file.

So we're literally telling the browser at the bundler, this needs to be shipped to the client and it needs to be part of the bundle. And again, we can see that effect in the network panel and in the services panel. So this is server side rendering as it was before.

And if we compare to that, the numbers don't matter, don't look at the numbers. But I want to focus on two things. One is the actual HTML, the document, has also gotten half the size now.

And this is because next.js and get server side props, it will include all the data that you're injecting into the HTML response as JSON. For React components, we don't need that because it's all encapsulated in those components. And then there's a lot less or fewer JavaScript files that are a lot smaller.

So that's kind of like what we expect with what we just discussed. But there's also like a new JavaScript file that I at least quickly want to mention, that RSC equals hash kind of stuff. And that is the out of order streaming from React server components, where it streams in stuff that you suspended where you're fetching data or other things.

And if we look at the sources panel, we can see why those JavaScript files are much smaller now. This is, again, server side rendering and then React server components. It looks a lot cleaner.

So yes, the next dependency hides a lot of that noise. So there's like React and routing and all that stuff in there. But most importantly, we see that the markdown and moment and all those big libraries we know we don't need, they're not there anymore.

So it's just a really good way to see how partial hydration can deal with a lot of those bundle size problems. All right. As mentioned in my intro, I want to do a quick comparison to some other frameworks.

React was by no means the first library to look into hydration and how to fix that problem. There's a lot of other libraries and frameworks out there. We already heard about Astro earlier.

And another very popular one is Quick. So I want to look at it from two perspectives, mainly from a developer experience perspective. How does it look like in other frameworks, how to do the same thing?

Astro is a good example because it's also trying to do partial hydration. So it's very similar to React server components. But you can already tell, like, it looks very different to React.

It looks more similar to if you ever used knockout.js in the past, Vue, Vue 2 at least, or just markdown itself. That's where it came from, static side rendering. And essentially, you split up the file by purposes.

The top of the file is your server stuff. Only runs once, only on the server. And this is where you do the data fetching.

This is where you prepare the data. And that all gets injected into your renderer. Second part is your markdown.

So what actually renders the website. And then the third part is the script tag where you can do all the dynamic stuff. So here's where you add event listeners and state and all that.

And some of you might cringe at this hard split of concerns. And I'm with you, like, it's nice to have everything in one place in React. But I think it's really interesting and really good because it really tries to give you the best of that old system of when we had, like, PHP and jQuery, where you have the strict concerns of, like, static and dynamic.

But it gives you in one framework, in one file, in one language, which I think is cool. Compared to that, QUIC looks much more like React. So much more familiar.

And it goes even a step further. So like I said, what we've seen before is partial hydration. QUIC promises zero hydration.

And I say it with quotation marks because I don't think there is such a thing as zero hydration when you have dynamic applications. But they go further by trying to not only reduce the amount of hydration that you do, but also defer that hydration for as long as possible so that you only really hydrate what is needed instead of the whole page all the time. There's two things I want to point out.

One is the QUIC has a concept of that server-side only. They call it resource. So the use resource will only run on the server only once.

And basically, through static analysis, it will exclude everything that you use there in your client-side bundle. And then most importantly for that, deferring your hydration, it goes extremely heavy on the code splitting. So every closure, every function will end up in its own bundle.

So in this case, our useQuickHandler will create its own chunk, its own little chunk. And that way, we have full control over when we load that. So if you want to go extreme, you can only load it once the button is interacted with.

In a more likely use case, you only load it once the button is visible on the page. All right, to wrap it up, I'm probably already way over time. Our server confirms the future.

I'm ready to fight for that on this stage. Personally, I think 100%, absolutely. So the mindset shift back from dynamic everything to think about static first and dynamic as enhancement, I think, is going to be the future, and it's necessary.

Do I think React nailed the API and the developer experience for React server components? 100% not. And I think that's fine.

They are, with other frameworks, the front runners to try to change the way we do things back. You can't nail that in the first attempt. So looking at other frameworks, like Astro, like Quik, many others, I think it's really encouraging to see, we're going to evolve.

We're going to find that sweet spot between developer experience and user experience. And I'm really excited to see what's coming in the next year or two. And I hope you are, too, at least after this talk.

This is the GitHub repo with the slides. And the demo app, I actually did create that demo app in various frameworks to compare how things work. And yeah, thank you for listening.

### Christophe
Thank you very much, Julian. Please join us. OK, most of us have slides that look like crap compared to that.

So jealous. Those slides were like proprietary technology, like custom SPO or something?

### Julian
That is, yeah, custom web form.

### Christophe
I liked how the shape of the computer morphed, and you went through a round robin of all the browser names.

### Julian
I don't know if you could tell, but I spent way more time on that than on the actual talk.

### Christophe
Yeah, that happens. That happens.

### Simone
The best talks are just visual.

### Christophe
Fortunately, flights from Brisbane are long.

### Simone
Actually, I think you win the prize for the best slides, at least visually. I mean, content, of course, was good. And I think you're the first participant at the conference, since you come from, I mean, you are cheating in a way, but you came from Australia.

### Julian
Yeah, if anyone was hoping for like a cool Australian accent, I am very sorry. Actually, German, I just live in Australia.

### Christophe
But you don't have that German speaking English thing where the lamp was delicious, you know what I'm saying? So yeah, it throws us off. So yeah, so one question is actually not a question.

It's like gorgeous slides, we can all agree. And so there's a question that I think you sort of answered, which is like, do you not, OK, that's like there's, so please agree with that guy, he seems feisty. Do you not think that RSCs are sort of a copy of islands in Astro and stuff like that?

### Julian
100%. Like, they're trying to do the same thing.

### Christophe
Same concept.

### Julian
It's just React's approach to it. You can see it in other frameworks as well. Vue has that island concept, and Astronaut has that concept.

Even adopting that terminology of server components, which I kind of dislike because most of us can agree, like server components is not a great name for what they're trying to do. It's very misleading. But yeah, there's other, like Astro heavily on that island, and you can use whatever framework under the hood is trying to do the same thing.

### Christophe
Yeah, it's pretty popular, too, growing.

### Simone
Would you actually use, so what would you be the best flavor of Astro, like adding React or not for your components, let's say?

### Julian
It really depends, like, I hate to say it, it depends. It depends on your use case. It depends on what stack you're comfortable with as well.

### Christophe
What was that? Personal code aesthetics.

### Julian
Yeah, yeah, 100%.

### Christophe
Subjective.

### Julian
It depends on your team. Like, what is your team most comfortable with? Personally, in my side projects, I like that, what you just mentioned of like Astro and then using those React islands to do whatever you need.

But just because I love React and the concept of Astro, of like actually being very explicit about static, dynamic, it's great. The one thing about Astro that I would say is you suddenly realize how nice it is to have, like, event business and stuff within the JSX in React because Astro itself, it makes it very tedious. Again, it's back to the jQuery days where you have to have your selectors and then add, like, on click and then that.

And it's, this is where we're at right now. It's like a trade-off in developer experience to get the user experience right. Somehow we will eventually find the balance, I think.

### Simone
Let's introduce some politics here. No, I mean politics, developer politics.

### Julian
Let's go.

### Simone
Yeah, exactly.

### Simone
Let's talk about Trump. No, no, seriously. Is there a world in which actually in the future, I mean, a no Next.js solution will be the default in your opinion?

In no Next.js. I mean, a project without Next.js for server components.

### Julian
I hope so. Like, nothing against Next.js. I do agree with what's been said here before that with big companies like Bacel backing it for their own reasons. But they still do a lot of innovation and a lot of stuff.

But I hope, especially like comparing it now to Astro and Quick, I hope that competition will just naturally grow into something where it's more diverse again. Remix is doing an amazing job. I love Remix.

One thing I didn't get time to talk into is how server components encourage you to use the platform more. It's a meme by now, but I actually think it's really important. The whole thing of like, oh, you can't use state anymore in server components.

You can. Use the URL. Store the state where we used to store it when we were server first.

And I hope, yeah, there's going to be competition around that. And hopefully it's not going to be a monopoly of like one framework once in a while.

### Christophe
Yeah, there already is. Like, we have Redwood and Shopify does their own thing. Yeah.

And then Remix. And well, through Remix, I would say better. And this actually ties in.

Another question was you said, and I couldn't agree more, that React didn't nail the API for the concept of server components, let alone the name. So do you think it's up to React, as in like React core, to iterate on that and improve that? Or should that sort of be left?

Is it the purview of the frameworks around React? We saw this like notion that I found a bit toxic that true React is more like Next is the true React, something which I find dangerous.

### Julian
Yeah, I agree with that. So I think it's probably a mixture of both because the point of the frameworks is to abstract stuff out. So if they want to name it something else, they should totally be able to do that.

But given that server components are a React feature, I think they will, I'm sure they will listen to a lot of the feedback that we have now with the early versions of Next. And yeah, keep evolving that concept. I don't know how easy that is, because like once you're logged in, it's probably hard to completely change stuff.

### Christophe
And also half the React core team has been co-hired by Vercel at this point.

### Julian
But yeah, we don't want to, that's the politics part.

### Simone
Yeah, I think we are making it clear that Vercel didn't sponsor this conference, and so we'll do everything we can against Vercel. No, it's not true. We can cut this in post-prod anyway.

### Christophe
Someone has to pay those devs to do that R&D and iterate on top of it for sure.

### Simone
All right.

### Christophe
Thank you very much. Thank you so much, Julian. Julian Burr, everyone.