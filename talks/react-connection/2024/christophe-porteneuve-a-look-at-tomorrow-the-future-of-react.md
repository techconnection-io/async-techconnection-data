---
slug: >-
  /talks/react-connection/2024/christophe-porteneuve-a-look-at-tomorrow-the-future-of-react
date: '2024-04-22'
title: 'A Look at Tomorrow: The Future of React'
author:
  - Christophe Porteneuve
video: F4TS5_0ZLpw
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/F4TS5_0ZLpw.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
[Christophe]
This is a tiny talk, it's just like a closer of our conference. It doesn't look anywhere as good as Julian's. I don't look anywhere as good as Julian's.

So just a few thoughts about the future of React. So when I'm not emceeing conferences, I work obviously on the web, I've been doing JavaScript since JavaScript, and I've been doing React almost since React. I work at DrLib, which, yeah, I'm basically the boss of front-end at DrLib, to make a long story short.

And you might know me because of stuff like .js or prototype.js for the old enough among you. We invented the game that Jaquery won, basically, and PyWeb and Notes Called Paris, for those of you who attended those when they were last in, and the French React docs. So just a few thoughts about my thoughts, for what it's worth, on the future of React, React ecosystem, especially, like, let's say 2024, maybe mid-2025.

So obviously React's components are on the rise, and they're going to keep rising, and the API is likely to shift in breaking ways. I actually hope it does, because it's not really good just now. And I hope the documentation, even if that means a lot more work for me, the documentation is going to catch up, because right now it's very weird, and incomplete, and sort of like most valuable, minimum valuable products kind of way.

A lot more frameworks are very likely to adopt RSC, and I think that's important. It's not going to be just Next. It's going to be a lot more.

Remix is already doing a great work. I love Remix as well. Remix uses the web platform a lot more than Next.

Redwood just announced it, Redwood.js, which is actually pretty cool, and we fully expect more Amstrad frameworks to do that, and the related API will stabilize, and we'll probably see also increased usage of related, but not RSC-exclusive recent features. You might have seen stuff coming up in the docs about asset loading, for instance. So the fact that your React components, without the bundler, doing that work, and say that, oh, loading me means that you need to load this font, and this CSS, and that PNG, and that icon, and whatever, and inject that into the head.

And stuff that Helmet used to do is becoming internal. Same rising trend, full-stack type safety. So we alluded to that earlier.

The idea, everybody's using TypeScript, everybody and their cousin is using TypeScript now. Just look at the state of JavaScript surveys every year in December. Mostly TypeScript is well over 67% now.

Exclusively TypeScript is well over 40% now. Not just React, but the JavaScript system in general, and with good reason. And so people, we are developers, we are lazy, we want everything to be automatically done for us, and please don't make me read the docs.

So however good they are, and most of them, they're not. So that notion that I've got my type definition somewhere in some form, and I want everything else to automatically derive from that, and have that type safety, including really full-stack, from my back end to my front end in as automated way as possible, is getting traction. Whether your actual original source of truth is a JSON schema, is a GraphQL schema, is a Zod validator object or something.

Perhaps you're using dedicated approaches like tRPC, tRPC only works if your back end is actually known in TypeScript, or Deno, or what have you, it's a lot harder to achieve when your back end is something else. But it's fairly interesting, so we're going to see a lot more of that, I wager. Same about async behavior, and generally concurrent mode, concurrent mode features in React are still vastly underused, even if they've been fully documented and demoed in the docs for well over a year now.

So everything about suspense, everything about transitions, which actually have been stable for a while now and are actually really cool in terms of fine-grained control of blocking, non-blocking, high-priority, low-priority updates in React code, it's so easy to add in and it's very underused right now. The fact, you've seen that new hook called use, and it's basically throwing the rules of hooks by the window, it's actually, you can use it in conditions and loops, and you can pass it a promise, and it will automatically suspend when that promise is pending, and so you can use suspense as usual to orchestrate your waiting stuff. So even in client-side components, you can have some data fetching through the use, you can also pass it a context, it will do some fun stuff with that as well.

So I expect people to become more aware of that and use that instead of convoluted solutions more and more. React Compiler, so just remember that React Compiler might not ship with React 19, it might be later, they're already putting disclaimers all over this thing, it used to be called React Forget, please forget that it was called React Forget. It's React Compiler because that's what it does, and memoization is actually just the first thing that it does.

The opportunities that it opens up to actually have a compiler phase suddenly brings us on the same footing as some automatic magic that we see in Svelte or other stuff. If we have that compiler pass, memoization is the biggest pain point, so that's what we're tackling now, and getting memoization right is hard, as Charlotte's talk would have shown you, but it's a lot more that we can do besides memoization, so it's tackling the hardest thing first, and we're probably going to see a lot more really cool stuff when React Compiler goes in all our build tooling and dev tooling.

Tiny thing, but cool thing, you might have seen, so those slides are online, you'll be able to click that link, you might have seen a PR getting merged recently. Once we get React Compiler, actually translating our code, a lot of use cases that required up to this day props cloning when instantiating elements disappear, they vanish. In particular, the key and ref props stop having special treatment, they're dealt another way by the compiler, and that means that we can actually avoid 99% of the use cases where we had to do props cloning, so including deep cloning when instantiating elements, which means that element instantiation, which is a huge part of the rendering cost, becomes like 30, 35 times faster, so we can expect some little boost in rendering speed just because of that, which is kind of cool. I like when I don't have to do anything, and it just gets faster.

Finally, the end of Enzyme. Sort of a joke, like, that thing will never die, okay? So, really, thank you, Enzyme.

Anyone here has had to suffer through Enzyme written tests? This is a young community. So, thank you, Enzyme, for being there originally and providing us with the first non-run-of-the-mill React test runner approach to doing React component testing, but it did ruin our NPM install ever since React 16, and it sort of enticed us to write tests that are actually really tightly coupled to implementation details, because most of the Enzyme tests were written against the virtual DOM, so implementation detail rendering, not the actual DOM, and most of the Enzyme-based code bases are seen as a massive pile of legacy and depth now. So, obviously, if you are getting into React recently and you're looking at blog posts that are not with a date, first, DDoS that bitch, okay?

If you write any technical article anywhere, date it, okay? And put versions on it, like library versions and everything, so that people can know that it's not relevant anymore, and use, obviously, testing library, testing library selectors that are a lot more semantic-related and more resilient to change implementation details and stuff, and use stuff like Playwright or Cypress to do your end-to-end kind of testing. It's a lot better, or just VTest for, like, units and integration, and it's going to make you a lot happier and be a lot more maintainable than Enzyme, but still, nobody wants to get assigned that ticket to rewrite those Enzyme tests to RTL, right?

So they still linger, for some reason, and keep wrecking our installs. I don't think we're going to see a clear winner in the CSS and JS wars, because it depends, trademark, it really depends. Usually, the class is, everybody's been jumping on the tailwind bandwagon for, like, the app side code, perhaps because they're bad designers, perhaps because they have no designers, for whatever reason, a lot of the design systems are using more, like, discover that, hey, CSS modules are actually kind of neat, and sort of, like, a low tree-checking so that unnecessary CSS is not loaded if we tree-check the components that are the only ones needing them, and they provide some isolation, that they don't need a lot of tooling, and they're framework agnostic, so CSS modules are being rediscovered.

RSC has made traditional CSS and JS solutions harder, because they rely on, like, use insertion effect and stuff like that that do not work with RSC, like a lot of, like, the traditional hooks, but maybe you've seen some stuff called zero-runtime CSS and JS, where there's a, again, a sort of compilation phase, many options there, personally like Panda CSS, for instance, and those are links to especially, like, Josh Como, the ever-loving Josh Como wrote recently, like, a full-length article about RSC and CSS and JS, and if you're interested in that, I encourage you to read it and to subscribe to his blog, it's awesome. It depends, depends on your needs, depends on your app, depends on your team, but I would be surprised if we had a clear winner in that space.

And that's really all I have for my Nostradamus kind of productions for next year. Thank you very much for having attended this conference, huge round of applause to the organizers, to my