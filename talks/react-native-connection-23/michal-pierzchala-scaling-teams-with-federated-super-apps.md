---
slug: >-
  /talks/react-native-connection-23/michal-pierzchala-scaling-teams-with-federated-super-apps
date: 2023-06-01T00:00:00.000Z
title: Scaling teams with Federated Super Apps
author:
  - Michał Pierzchała
video: Br2dkgZtnic
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/Br2dkgZtnic.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/react-native-connection-23/michal-pierzchala-scaling-teams-with-federated-super-apps/slides.pdf
tags: []
year: 2023
conference: react-native-connection
edition: 2023
allow_ads: false
---

Hello, hello.

Can you all hear me?

I hope so.

I can hear myself.

That's great.

I'm already used to my voice.

That's a good thing.

It's a weird thing to hear yourself speaking.

So anyway, hello, Paris.

It's so great to be here.

I'm a second time here in this city.

I love it.

It's so, so nice.

It's such a vibrant place.

Yeah, really, really love it.

It also will be in my talk.

Anyway, you're going to see it.

So today, I want to talk about super apps and React Native.

So a few things about myself.

My name is Michał Micha Pierzchaƚa.

You can call me Michael, or it's @dymikey on Twitter, GitHub, and basically anywhere.

I'm a head of technology at Callstack, which means I'm working with our R&D and open source programs, and also close with our leadership.

I'm a co-contributor to Jest, to React Native CLI, to React Native Testing Library, and a few other projects but I've been more or less involved over the years.

So one of my favorite things about-- this is slightly clipped.

I hope it won't be that bad.

One of my favorite things about React Native is that you can ship your code really fast on all of the platforms at all times.

And unless it's like some exotic platforms out there, it should be all good.

Like, you can really, really quickly push your code and your features to your users.

But as your app grows and you add more functionality to it, it can quickly start to get more complex.

And you will end up shipping slower and slower.

So your leadership, your managers, will try to fill that hole with more developers.

Also, you will also, as a successful startup or a product, you will need more people to cover more use cases for your users, like internationalization, getting to new regions, figuring out some legal stuff, and all of that.

It all impacts the time you can push new updates and ship new code to your users.

So at some point, you could even find yourself in a team that quickly grew to 40, 50 developers.

And I mean front end developers working on the same app.

And they are frequently blocking each other's work.

So you start to think about, what am I doing wrong?

Like, I cannot ship as fast as I used to with this React Native, which was supposed to be so cool.

Now I have more people, and it's so hard to keep up the pace.

So I have a message for you.

You probably are a super app.

So what the heck is a super app, right?

Nobody really knows, but there are some ways to put it in some formal definitions, like this one.

Hope it's-- oh, it's actually readable.

So spending some time on improving the contrast worked.

So seriously, super apps are just big apps with loads of functionality.

And there's no rules here.

You can load this functionality directly from your app bundle.

You can load it dynamically from somewhere else.

This functionality can be related to each other.

It can be sometimes totally, totally something different.

So yeah, there's no rules here, no good definitions.

So I'll try to stick to that.

These are just big apps with lots of people working on them, lots of functionality that your users need.

And to some extent, I like to think about super apps as cities or organisms that live their own life, which one person or one team cannot simply control.

So you have to develop some kind of infrastructure to guide the direction where the city is going.

And by the way, this is Paris from the International Space

Station.

I think it's beautiful.

So now a typical super app will integrate a variety of services that are particular to relevant users.

But it's possible that not all features are relevant to every user.

So no single user will need all of them.

For example, this concept is particularly popular in Asia.

Apps like WeChat, for example, it's from China.

It integrates chat, payments.

It's a social network.

It will handle some kind of insurance for you.

And yeah, it can do basically anything in one single app.

There is also another Chinese app called Alipay, which handles similar thing.

It started as a payments app, and it evolved to an everything app, basically.

So you can even ride an Uber with it as a third-party integration.

There is also Grab, which is a pretty well-known app in southern Asia.

If you travel to Vietnam or Indonesia, you probably use this app.

It handles transportation, food delivery, digital payments.

And all these apps like to call themselves as an everyday everything app.

So look at WeChat alone.

Its feature set is massive.

Contacts, chats, social networking.

And also, its app size is pretty massive, because it's around 600 megabytes for iOS.

And a super lot of people use super apps.

And apparently, this is a thing in the east, right?

But guess what?

On the western side of the world, we also have kind of super apps.

We have Uber, which handles ride hailing, food delivery, everything around like riding and moving stuff from one place to another.

We have Revolut, which is everything around finance.

In Poland we have Allegro, which is everything around e-commerce and buying stuff online.

And Facebook, even Facebook could be considered a super app built around everything related to social networking with marketplace and dating all paired with this social, yeah, social thing as I don't have any better word for it.

So now that we know that we may have ended up in a super app, and we have super problems, what we can do about our time to ship?

And before jumping into solutions or quick conclusions, it's worth to realize that we are actually dealing with organizational issues, like extensive communication, sharing resources, onboarding experience, conflicts, and who owns what.

So similar to cities that grow and expand, it's time for us, hopefully, to organize and decentralize.

Decentralize ownership and deployments, because this is what's holding us back.

So I never really became an architect, although I wanted to like 10 years ago.

I don't really remember why exactly

I picked software development to architecture.

Maybe it was money, but yeah, at least now I can architect software instead of building.

So that's something.

So, organization of large teams is generally solved on a server with something called microservices.

Of course, it's not a silver bullet for all the problems.

But it has its upsides.

And since humans are great at copying from each other, we also have microservices on the web and we call them micro-products.

And the React Native core team encourages us to reuse the knowledge from one platform to another.

As Ricky Hedlon said or presented during the 2021 keynote at the ReactCon, where it used to happen.

For example, on Android in React Native, we have a view flattening algorithm which had to be ported to the C++ side of things when React Native was re-implementing stuff in the new architecture.

And it turned out that iOS got this thing for free.

So what we learned on Android side, we moved to iOS so that it's even more optimized.

It can use better technology.

And we're also encouraged to use web technologies for the mobile world.

This is how React Native came to be, right?

It's running JavaScript on our phones.

So maybe we could solve micro-pronouns, and we could build micro-pronouns for the native and solve our organizational issues there.

So to bring true micro-pronouns to mobile platform, we need a dynamic code delivery.

So on Android, we can handle that with something called feature delivery, which allows us to load native code from remote locations.

And yeah, it's not super encouraged by the platform, actually, and not super performant.

On both platforms, however, we have web views.

So for example, Grab or Uber are using web views to load whole applications, like Uber Eats or Alipay rendering Uber inside of it.

So this is way closer to loading our code dynamically from our app or for our app from a remote place.

But also we have hybrid JavaScript frameworks because guess what?

JavaScript is a dynamic language.

It can be loaded into memory and re-evaluated on the flight.

And React Native happens to be a hybrid JavaScript framework.

So yeah, we have all the means necessary to implement micro-frontends, like true micro-frontends that load our code dynamically from any location out there into our mobile app.

It's physically possible.

And to load the code, we need some orchestrator, and we need a bundler.

So React Native is known for having its own bundler called Metro, which is great.

For the last few years, it advanced so much,

I have so much respect to the team that's now bigger than ever, and it's shipping more and more stuff that we used to miss in the ecosystem.

But it only kind of supports async code loading.

I think it's there.

Theoretically, it's possible.

We would need to contribute that, I guess.

But on the other hand, there is Webpack, which has a first class support for async JavaScript loading.

So here I would really love to share with you that we implemented async bundle loading with Metro.

But guess what, six years ago we created a project for fun called Hull, which was an experiment on bringing Webpack to the React native world, because Metro at the time lacked symlinks and they make coloading and probably some other things.

And apparently there are developers that would like to use the same tooling and Webpack happened to be one of the most popular web bundlers out there.

So we had some really, really good success stories for Hull.

But it turned out it's not the best tool for the job, because apparently it did too much.

It was a Hull CLI, like an alternative CLI, that also integrated its own alternative bundler, Webpack.

And we had troubles upgrading it to Webpack 5 to support fast refresh, which Metro supported.

And it was amazing compared to hot module replacement.

And also, HMR wasn't super well working with Hull anyway.

And with Webpack 5 specifically, it came with this really, really nice feature that we really wanted to try and adopt in React Native world.

And this feature is module federation.

I told you that we solved micro-frontends on the web.

But what I didn't tell you is the obvious thing.

There is no single solution, and not the best one.

So at the same time, we believe that module federation is currently the solution to build micro-frontends that provides the best developer experience out there, at least for web developers.

So maybe it would be a really nice tool for mobile developers as well.

It introduces separate builds for the same app, allowing for more independent releases between teams and independent deployments.

It allows you to share code between apps, and it doesn't involve NPM in the process.

So the creator of Module Federation, Zach Jackson, also shares our experiences when working with big clients who couldn't keep up with the pace of development as they grew.

And he was also kind enough to speak at our podcast, the React Native Show, which I'll shamelessly plug here.

Feel free to watch it or listen on your favorite podcast platform.

So yeah, we had to do something about this whole thing, that we couldn't implement the Webpack 5 fast refresh.

So it turns out that we rewritten it from scratch with different ideas and different architecture in mind.

So Repack came to be, I think, like two or so years ago as a Webpack toolkit for React Native.

It's a successor of Hull.

It's for the advanced users, for people that really know what want to do in terms of architecture of their app.

And with Repack, we were able to fix all the problems that we have with Hull by shifting more responsibility into the users.

So we didn't re-implement the CLI anymore.

We integrated seamlessly with the plug-in and the comments mechanism that we were actually building as a React Native team, React Native CLI team, at the time.

So it was like a really nice collaboration between our teams.

And what's important, Repack supported module federation.

First, it was first theoretically possible.

Then we implemented this as an experiment.

And since version 3, it's a stable implementation of the feature.

So with Repack, we're-- oh, I didn't catch this lack of font.

Sorry about that.

But with Repack, we are able to create something what we like to call federated super apps, which are React Native apps for big teams powered by module federation, optimized for highly distributed teams, independent deployments, and delivering only the JavaScript that our users really need.

So thanks to Reapack, our app can still grow in functionality that's relevant only to particular users without having to pay the cost of the app size.

And at the same time, it allows for the teams to work independently on their features or so-called mini apps, even in separate repositories, the teams can choose whether to run the full app or run their mini apps in isolation.

And we found that most developers prefer the isolation because it's faster to iterate, and they can focus better on their job.

However, it's not required to work in separate repositories.

There are teams that thrive in monorepos.

In fact, we see like 50/50 split in the proponents of monorepo and polyrepos.

So with module federation, we can support both.

If you can handle all the upsides and complexities that monorepos come with in terms of tooling, you can freely use it as well.

As the teams here--

I call them team blue and team yellow.

They are part of the monorepo.

They can ship to a host application.

And there are team green and team red that can work in their full isolation, somewhere there in a separate repository.

They don't need to be a Git submodule.

And they can still build the same app with the same build system, thanks to module federation.

What's important here is that the teams are able to deploy their code independently at their own pace, without being blocked by the other teams.

And for the host app to be able to pick the versions that they're compatible with and that they want to load over the air.

And to ensure that the app loads the code that's not tampered by bad actors, repack allows you to configure a code signing for your chunks.

So it's like having CodePush, it works basically in a very similar way as CodePush.

You have the control and you have all the granularity with it.

So Repack signs all the JavaScript bundles for you and can unpack them safely, as it would be developed in a web browser.

So as web developers, for example, I'm from a web development world, who is there as well?

Yeah, so we have quite a lot of web developers and we take code signing for free because browsers do it for us with HTTPS and with -- in a mobile world, we need to handle it ourselves so we can -- for banking apps, for example, we can implement something called

SSL pinning to have this.

It works in a slightly different way.

However, it's not there.

If you want to load some remote code, you really want to sign it.

So with Repack, we make it very easy for you to do it.

So we could think about mobile development almost as being a web developer, just loading some chunks over the internet.

And don't worry about security.

And also, compared to CodePush, you don't need to worry about re-downloading your whole

JavaScript bundle, which can easily take from 10 to 40 megabytes.

This is the case of Discord.

You can check, Discord has a 40 megabyte JavaScript bundle inside.

And Discord is a React Native application, by the way.

So if Discord used this architecture, if it made sense for them, but it probably isn't, that is developed by two or four developers.

So it will be like overkill.

They could use this granular code splitting to ship the bug fixes and maybe some very small features to their users without waiting for the app store if it's critical.

So however, Repack is a bare-bones toolkit.

It won't handle everything for you.

You will need to write some of your tools around it.

Like, for example, picking a correct version requires a server that will serve the bundles that you can configure in a way, any way that you physically like.

You will also need to automate some of the deployments.

And also in React Native, setting up module preservation requires some slight runtime setup.

We have it all documented.

However, we realized that it may be not that easy to try this.

So what we've done is recently we open sourced a super app showcase.

So you can try it yourself.

It's a GitHub repository. clone it, run it, see how it -- what's the experience of running webpack, like dynamically loading everything for you, and if it actually makes sense for your team, for example.

So our goal was like a -- as easy as possible verification if this architecture works for me and if it makes sense to adopt repack at all, because otherwise it would be way more tedious and time-consuming task.

And if you want to adopt repack incrementally in your application, you can run repack init command which will handle installing all the necessary dependencies, create the webpack config and all of the tedious stuff that two weeks ago we would need to do manually, now

Now we have a command for this, so I'm really happy about it.

And after all is set up on the dependency level, we need to set up our Webpack plugin with-- our Webpack config with module federation plugin, which repack exports.

And we need to configure it for your host application and your many applications.

And for exposing apps from any application, we use the exposes keyword, which is standard for module federation setup.

We need to tell Repack where to get our mini apps from using runtime functions like other resolver.

And then we need to lazy load our imported mini app using suspense to avoid spinners.

It's also loaded from the remote.

So we should use a suspense and error boundaries here.

And voila, our mini-app is lazy loaded.

We can see that mini-app container is downloaded before.

However, the main navigation chunk is loaded when we are accessing this mini-app.

So it's not the part of your main bundle.

Your product shouldn't ship slower just because your app and your teams are getting bigger.

Repack and Module Federation can rewire your teams and change the way they work.

And what's most important, ship fast again.

Of course, there are gotchas.

It's not a perfect solution.

Repack is for big teams only.

This is what we believe at Callstack, at least.

We rarely see teams smaller than 30 developers, like front-end engineers working on the same app that would need this kind of architecture.

And such teams often have their own custom solutions.

So Repack exists so they can throw away, hopefully, their custom solution and outsource it to an open source library that Repack is.

You will need a dedicated infrastructure team.

Also, if you're this big, you probably already have your infra team handling dependencies, all the upgrading, all the management, speaking between the teams.

This is something that will need to happen to handle all the dependency hell that's going out there.

And there is no lazy loading of the native code.

This is like a platform's limitation.

However, we overcome it with JavaScript.

So any native functionality that your mini apps need to access will need to be a part of the host application that is there deployed to the App Store or Play Store.

And speaking of App Store, Apple will not be delighted by you shipping features without them knowing.

So be careful with that.

And to recap, super apps are just big apps shipping loads of functionality, features for everyone, usually statically or with web views.

Federated super apps are optimized for dynamic feature delivery and shipping only the necessary code that your users need. and code that renders fully native experiences because it's React Native under the hood.

They use repack and module federation to schedule all the organization and deployment and the building and it's all dynamic.

It's for both monorepos and polar repos.

And you can give it a try using our Super App Showcase repository, so you don't need to bother installing and tinkering with stuff yourself.

So thank you.

That's everything for me.

You can find me on Twitter.

[APPLAUSE]

Is Reback linked to a React Native version?

Is Repack tied to a React Native version?

We support what React Native supports, which is three latest versions.

And I think there are teams using

Repack on the React Native 64.

So we try to be compatible with the latest free versions of React Native.

That's the baseline.

However, if there is a good use case for someone that has something broken and they can't easily upgrade from an older version of React Native, sometimes we do that for them.

However, if you deploy your apps on Android App Store, you will need to upgrade your apps and React Native to the version 71 at least, because otherwise you won't be able to do it.

That's a rule from the Play Store.

They require SDK 33, I think, which is tied to React Native 71.

Okay, so you have to watch out also when a new version of React Native is coming out?

I mean, so there is nothing, I think there is nothing like from the private API of React

Native that we're using.

We're using public APIs.

So it should work like any other library.

So small things may break maybe, but they are rather unintentional and rather fixable.

> > Right, so basically, yeah, if a new version of React Native is released, you should not have to do anything to make it work.

> > Yeah, yeah, exactly.

We try to keep our tester apps on the latest version.

I think we should adopt canary versions of React Native to be sure.

React Native core team is doing amazing work on the releases process this year.

They're killing it.

So yeah, shout out to the React.dev core team for better release management.

- And another question then is, you talked briefly about caveats and stuff like this, but do you think in your opinion there are any major limitations to use repack?

- I mean, of course there are.

I think the better question would be whether you should use Repack or not.

And I believe that for most, like vast majority of cases, like I don't know, maybe 98% of the apps out there are 99, you would like to use Metro.

And Metro is great, like it's super integrated into React Native, it's faster than Webpack, for example, in many cases.

And it's just like one thing is, two things, it doesn't support module federation and it doesn't easily support dynamic code loading, you would need to, I think you would need to implement it yourself today.

And there are some ideas to have that in Metro and React Native.

Although it's a very niche use case.

So there's probably more important things to fix or improve in Metro itself.

So if you need to load some code dynamically, and you know that you really need to do it.

Or you need to have a finer control over how your teams release specific parts of your application.

So if you're like a super app or kind of super app, then Repack could be maybe a good idea for you.

And I would encourage you to try it, because these are things that Metro would struggle with.

Other than that, just use Metro.

Just use Expo if you're using any other app use case.

- All right, so we have one last question from Tico.

Did you have any issues with modules like Sentry because they've been working with federated apps on the web and using modules,

I mean they had an issue with Sentry basically because it was less compatible with federated modules.

- I don't think I have a good answer to this question.

I would assume this could be a question about source maps that can be, I mean source maps are really wild and there's no good specification around it and Sentry is doing a really good job still writing this idea and bridging all the different browser vendors.

But other than that, I don't know.

- Okay, maybe one last question, a bit less technical.

Do you think at some point users will get tired of super apps because those apps are doing so many things and we use like 2% of it?

And I think there is quite some data that shows that people want aggregated services in one place that's easily accessible.

So it's that -- I don't know if people can get fed with, like, extra functionality that they don't need to use, but if they feel like they can use, they can just do it in the app. it's hidden somewhere there or you can search for it and it's there.

At the same time, this setup with repack and module federation allows you to deploy the many applications separately to the app store.

So in a case like -- I think most of you can be familiar with Uber and Uber Eats.

They're like separate apps.

Uber loads Uber Eats as a web view.

So we can access Uber Eats through WebView, and if you enjoy this experience, that's great.

But if you want just to get your food and not get your driver with it, by the way, then you may just want to use a very scoped app.

And you can use both use cases.

So it's like the tricky question or tricky thing is to know your users and be able to figure out what kind of services and experiences they want.

Great.

Thank you Michaƚ.

Thank you very much.

[APPLAUSE]
