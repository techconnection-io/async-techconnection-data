---
slug: "/talks/react-native-connection-23/tommy-nguyen-raising-the-bar-our-journey-making-react-native-a-preferred-choice"
date: 2023-06-01
title: "Raising the Bar: Our Journey Making React Native a Preferred Choice"
author: "Tommy Nguyen"
video: hlhnAqEtpmY
thumbnail: thumbnails/tommy.png
slides: downloads/dev-xp-at-ms.pdf
tags: []
year: 2023
conference: react-native-connection
edition: june-2023
allow_ads: false
---

Hi, everyone.

I'm Tommy.

I'm a principal software engineer at Microsoft.

You may also know me as Tito64 on GitHub.

That's my avatar right there.

It looks way bigger than I thought it would look like.

I started out putting React Native in Outlook Mobile, but in the past years, I've mostly dealt with developer experience in React Native.

So at Microsoft, we have React Native in a lot of apps, including Word, Excel, PowerPoint, not just the apps you see here in the showcase, and not only on these platforms. also on Windows and even Mac OS.

And in fact, you can find React Native on Xbox.

And my role in all of this is to be invisible, which is kind of ironic since I'm standing on a stage talking to all of you right now.

But I promise this will make a lot of sense later.

Well, actually, I can't really promise that, but bear with me.

So two years ago, we introduced you to the Microsoft Galaxy.

Microsoft has many monorepos, similar to how a galaxy has a lot of planetary systems.

And every team has different needs and different setups.

And so some of the teams are focused on delivering specific features that are going into many apps, mostly hybrid apps.

There are some teams delivering full apps.

And then there are teams that are delivering frameworks for said apps.

And so trying to align everyone on the same set of tooling, on the same set of setups, it's super hard, let alone getting them to agree on the same version of anything.

And the hardest part is maintaining that going forward.

So to prevent our teams from drifting apart, we need the dark matter that binds everything together.

We need tooling.

And so we've made a bunch of tools, and we open sourced them.

So in our next kit on GitHub, you'll find all the stuff we're using internally at Microsoft.

There's plugins for Metro, presets for all the tools that I'm sure you're familiar with.

And since everyone has different needs, we made sure that all of these tools are standalone, which means that you can choose and pick the packages that you care about or are interested in and adopt them into your own setups.

But we also have an all-in-one solution, which is basically a drop-in replacement for the CLI that sets all this up for you.

As an example, one of the more popular tools we made is the tree shaking plugin for Metro.

And this started out as an experiment using ESBuild that we saw great results with.

Internally, we have seen savings up to 50%.

But the community has also shared their results with us.

For instance, Renoir here saw their bundle go from 18 megabytes down to 4, which is quite insane.

And the reason for this is because they were using Font Awesome.

And well, it includes all of the icons.

And one of the things we've put a lot of effort towards is making React Native upgrades easier.

I'm sure most of you are familiar with how painful this can be.

So this is the diff for upgrading from 68 to 71.

I don't know about you, but that looks super intimidating to me.

And imagine doing this for every example app in the whole of Microsoft Galaxy.

That's insane.

So one of the tools we made to make this easier is the React Native test app.

React Native test app is an example app in a package.

You add it as a dev dependency, and it allows you to effortlessly upgrade or downgrade

React Native without ever having to touch any native code or project files.

So the diff you saw earlier gets reduced to this.

So basically, you just bump the numbers, and you're good to go.

[APPLAUSE]

Thank you.

So over the past year, we've added support for 72, which means that now, with the latest version, you can upgrade all the way up to 72 or downgrade all the way down to 64.

We've made it easier to enable new architecture,

This is just a build flag, and then you don't have to deal with any boilerplate.

Just turn on the flag, rebuild, and it's on.

We have added support for Expo config plugins, and we even have an experimental app mode, meaning that sometime in the future, we're hoping that this will be the baseline for a React native app.

But even with this, you still need to know what numbers to put in your package.json, right?

What version of CLI or metro is required for React Native 71?

What about reanimated, async storage, web view?

Well, we got a tool for that as well.

We call it align-deps.

Well, we called it DepCheck first, and then we kind of renamed it because it was conflicting with another tool also called DevCheck, which caused a lot of confusions.

Basically, you run this one command, yarn align devs set version 71, and then it fixes up your package.json for you.

So here you can see that it bumped async storage.

It bumped React, React Native, React Mac OS, React WebView, et cetera, and the Babel preset.

And we continuously update this.

We keep it up to date, make sure that everything runs smoothly, even with the latest version of React Native.

And when all of this just works, I'm doing a good job being invisible.

When you bump to the latest React Native version, when you enable new architecture, when everything just builds and nothing breaks, invisible.

[LAUGHTER]

On a more serious note, though, our tools are not perfect, obviously.

But the community, you, have been super patient with us.

And so I just wanted to spend this one slide to say, thank you for being awesome.

So for the past couple of years, we've been focused on developer experience.

We lowered the barrier to entry with smarter defaults.

We made it easier to set up and enable advanced scenarios, especially if you're in the monorepo.

And we've made it easier to upgrade with tooling like AlignDepth and React Native Test App.

And all of this while making it still possible for you to adapt all of the tools to your own needs.

And this is super important to us.

And we will keep on reducing the friction wherever we see them.

But we keep getting feedback that this is not enough.

There are two things in particular that we keep hearing.

And one is, I already have some React Native code.

Now I want to put that into n number of apps without having to pay the integration cost per app.

And the second one, I already have some React web code.

Now I need to bring that code to native within the next week.

So what we're hearing is, increase developer velocity.

We want to move faster.

And while you can solve the second case with a web view,

I think it comes with limitations, and it doesn't exactly solve existing React Native code.

To solve both scenarios, we need to talk about web native convergence.

Web native convergence boils down to a pretty simple idea, idea, make web code work in native.

So for instance, in this example here, we have a button that, when clicked, returns the battery level.

Now what would it take to get this component working in a React native app?

Well, there are a couple of issues here, right?

For starters, there's a call to navigator.getBattery.

This is just a standard web API call, but for React Native, we would have to find the correct native module to access the battery state on a device.

And the other issue is that this component returns a button, which is an HTML element.

So in order to get this working, we would have to fork this element, fork this component, and also bring in a native module.

But wouldn't it be great if this just worked as is?

As a matter of fact, there's an RFC that plans to tackle the HTML part.

It was written by Nicholas at Meta, and he's proposing a way to bridge WebInnative with something he calls strict DOM.

And strict DOM is basically just a subset of DOM, CSS, and HTML.

It's a really interesting RFC, and I recommend that you check it out.

But the short version of this is they want to incrementally reduce the difference between web and native, with the end goal being able to run React DOM directly on native with little to no changes.

And we're hoping to collaborate with Meta on achieving this vision.

But what about the use of web APIs?

Well, just in case you're not familiar, web APIs is a set of well-defined, standardized

APIs that will work in any supported browsers.

What if we implemented this for React Native?

And that's basically what we're proposing.

Sounds like fun, right?

In fact, I don't have a cool demo for you, unfortunately.

We're just getting started.

We have some code to generate the interfaces that need to be implemented.

And there are over 1,000 in total.

After filtering out deprecated, experimental, and modules that we don't really want to focus on right now, we still end up with around 200.

So we still need to figure out which modules we want to focus on first.

And with so many modules, we want to make sure that it's pay for play, meaning only the modules that you use should be included in the final app bundle.

And we're doing all this work in our next kit, meaning that someday all of this will be open source.

And yeah, that's our grandmaster plan for solving developer velocity.

So we made a bunch of tools to improve the developer experience at Microsoft.

Everything is open source, and we hope that you will also find this useful.

And if you do try them out, we'd love to hear your feedback.

However, this is not enough.

We need to also increase developer velocity.

And we're proposing a new tool called developer velocity. And we're proposing to solve this with web native convergence by enabling web code to run directly in a React Native app. And there are two parts to this. There's the user interface for which there's an RFC and we're hoping to collaborate with meta on this. And then there's the standard API and we're just getting started. It may take a while before all this becomes ready. But imagine the day you can just write React code and it would just work across web, Android, iOS, Mac OS, Windows, whatever you want to target. That is the day we become truly invisible. Thank you.

[ Applause ]

All right.

Just one more thing.

[ Laughter ]

If you want to learn more about this, there's a link to the blog post, which contains past talks and a lot more stuff.

If you're interested in diving into our tools, there's the links to the documentation, the repositories, and finally, there's the link to the RFC for React DOM.

And with that, I'm finally done.

Thank you.
