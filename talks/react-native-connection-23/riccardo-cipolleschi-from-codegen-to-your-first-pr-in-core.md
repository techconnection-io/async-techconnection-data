---
slug: "/talks/react-native-connection-23/riccardo-cipolleschi-from-codegen-to-your-first-pr-in-core"
date: 2023-06-01
title: "From Codegen to Your First PR in Core"
author: "Riccardo Cipolleschi"
video: frkucOdc0E4
thumbnail: thumbnails/riccardo.png
slides:
tags: []
year: 2023
conference: react-native-connection
edition: 2023
allow_ads: false
---

OK.

Hi, everyone.

Thank you for being here.

Thank you for this conference.

I'm very happy to be here and to be able to connect with you in real life after the pandemic and stuff.

Today, I'm going to talk about how can you become a contributor into the core framework of React Native?

We're going to use CodeGen as an example, but it is just an example.

We'll see other ways to contribute.

First, mandatory slides about myself.

I'm Riccardo, I'm a software engineer at Meta.

I was a former iOS engineer, still an iOS engineer, actually, most of my work is on the iOS side of React Native.

And I'm basically working with the core team, trying to bring the innovation that we have internally in Meta that we are using, for example, in the Facebook app, also in the open source, so that everyone can benefit from them.

I'm also leaving some of my contacts, my GitHub profile, LinkedIn, Twitter.

I don't tweet a lot, so don't expect a lot of updates from my side.

And my Medium blog, where I write about iOS and Swift stuff.

So my heritage as an iOS engineer is still there.

I encourage every one of you to connect with me.

I love to talk about React Native or iOS and to hear your feedback.

It's something we really care about at Meta, so please do.

Let me help to understand the audience a little bit, and also I will need some light on the stage, on the room.

How many of you have ever opened up your R or contributed to the framework already?

Raise your hand.

Can I have some lights on the room, please?

Okay, I would say 25% more or less.

That's good, good number.

So, as you know already,

React Native is an open source project.

But it's not just an open source project, it is huge.

It's very big, and we are gonna see some numbers to justify this size.

First of all, the number of commits.

It has 27,000 commits, which is huge.

And I think it's kind of natural when a framework is eight-year-and-a-half old.

That's the first commit ever in the framework, 2015.

And it's pretty impressive that the framework has an age of eight-and-a-half years.

Most frameworks die somewhere before that time.

So we are still here, we are still working on that, and it's impressive.

It is used by 1.3 million people, which is a huge number, and it has almost 2,500 contributors, and you can become one of them as well, so the number will increase.

And it has, like, you can see that the latest stable release is 71, so there are at least

71 releases, more if you count the patches.

If you don't trust GitHub stats for any kind of reasons, we can look at the MPM one, which still says 1.3 million weekly downloads in this case.

A lot of people use React Native.

As Marek was saying before, some things happened during the past years that may have, like, could have broken React Native, but they didn't.

We are still suffering from the ripple effect of the Airbnb article, for example, and if you go on social medias like Twitter or Reddit, you can see questions like React Native is dead or nobody is using React Native or Meta stopped using it.

That's not true.

So just the myth busts this myth.

We are using it internally.

The Facebook app is one of the biggest apps that uses React Native.

We use it for Facebook ads and for the Oculus app, where if you have an Oculus, you can use the app to browse your games or to connect the Oculus and stream.

Meta is not the only big company that uses React Native.

For example, Microsoft uses React Native as well in many of their products.

And also smaller companies use React Native, not just big corps.

So everyone really can use it, and I'm sure that many of you are using it in their own apps.

This is a sample of app that they took from our website under the showcase section, and is a subset of the apps presented there.

And the showcase is a subset of the tens of thousands of apps that are available on the store, which are developed with React Native.

Like this week, a person from Expo tweeted something interesting as well on this topic, which like the first, of the first 100, if I remember correctly, apps in the food category,

25% or 22% are done with React Native.

So the framework is live, we are using it, we are developing with it, we are improving it every release.

And you can contribute to the framework too.

You should not be scared about the size of the framework because there are several ways in which you can contribute even if you don't have the full context of what happened under the hood.

One example is through the website.

Like this is probably the easiest way in which you can provide valuable contribution to the framework.

On the website, we have several guides that you can follow.

It's a little bit hard to keep them updated, so one simple way to contribute to that is to figure out, try them, and if something is wrong or outdated or you feel that we can do a better job explaining it, you can open up your against the website.

And this is the GitHub repository which bakes the website, so a PR that is merged here will end up in being released in the website in the next release.

Another way in which we can contribute to React Native but the ecosystem in this case is by bringing your own library.

As Marek was saying, one of the strength of the framework is the vibrant ecosystem that it has.

And if you have a use case that you think can be useful to others, you can create your own library.

On the website, we have a guide that you can follow to pack your library and publish it on NPM so that everyone else can use it.

And we have also the React Native dot directory website which lists all the libraries for React Native.

So when you publish it on NPM, you're gonna be also in our React Native dot directory website.

There's another way in which you can help us and it is by looking at the issues

And if you know the answer to that, try to answer to it.

As you can see, we have 1.7K issues.

And it's kind of-- we are trying to do our best to keep up with them.

But as we saw before, we have 1.3 million people using React Native.

So you can imagine how many issues people--

1 million people can open.

And it is a bit hard for us to keep up with everything.

So if you know something about one of the topics and you can help us answering there, it would be great.

For us, it's a huge help.

There is another way that doesn't involve coding directly, which is testing release candidates.

So yesterday we did RC4, today we are doing RC5 because we found a bug.

So this slide is outdated, although I tried to be as updated as possible.

But yeah, so one thing that we really need is for people like you that work with the framework every day to try and update their app to the release candidate and report what's not working in these discussions.

Only through your help in this case, we can really test all the use cases and make sure that the next release is actually stable for everyone.

So this is a super valuable way for you to contribute to the health of the framework.

Last but not least, maybe most interesting way to contribute for everyone of you here is by writing code.

ReqNative has code base composed of several languages, so we are pretty sure that we can find a way for everyone to contribute to the framework, either you are a low-level C++ developer or more front-end JavaScript engineers, there is for sure a way for you to contribute.

And we're trying to make it even easier by creating what we call umbrella issues.

And you can see the little umbrella denoting the umbrella issue.

But let's go a little bit into what is an umbrella issue.

So umbrella issues are ways in which we basically group together similar tasks to improve an aspect of the framework.

And we create them for different topics, like we used to have one for the React Native bot which helps with triaging issues, we have one to align the web styles to like our APIs to the web standards, and we used to have the React Native monorepamper issue which we closed last year and we are super happy about that.

If you want to go slightly deep into the anatomy of an umbrella issue, we are going to take

Codegen as our working example.

Codegen is an umbrella issue that I personally maintain.

We opened it in October last year, so if some of you are contributing to open source often already, you may know what Oktoberfest is, basically it's an event that happens every

October and if you contribute to at least four PRs, remember correctly, to any of the repositories that participate to the event, you get a badge on your GitHub profile.

This is a way also for you to boost your GitHub profile, your resume, and can help you, like, getting a better job if you want to change.

The core problem that we're trying to solve with CodeGen specifically is basically to improve the code base of CodeGen.

CodeGen is a part of the new architecture for React Native where people can create their own modules and components.

And starting from some JavaScript specification, which need to be typed, we are going use code to generate the native code, so this is a simpler way, it's a tool that allows you to create boilerplate code without actually writing C++ code which I think nobody really likes to write.

But the problem with the codebase is that it has been developed by different people over different -- in different times, so there is a lot of code application, we added the support for TypeScript in a later time, at the beginning we only were supporting flow.

So there is code duplication, things that can be put together, a lot of things can be simplified and the goal of this umbrella issue is exactly that, to leverage the help of the community to improve the code base.

And this is the second section of every umbrella issue, basically, the first, sorry, of every umbrella issue where we describe the context.

So when you start working on a task, you know what's going on and why you are doing what you are doing.

And we are trying to go a little bit deeper in the details of the code that you're gonna touch.

There is a second section in almost all the umbrella issues which is how to test your code.

What we think is really important is that for everyone contributing, it has to feel empowered of doing its best work.

And also, we want for you not to waste time in creating a PR that then we need to like kind of reject because it's not tested.

So we're trying to provide all the information that you need to write unit tests, to test your code, to see that everything is green on your side so you can be confident in pushing the PR and waiting for a positive review and merge it in the repository.

There is the third section which is a description of what we expect for you to like, when you want to claim a task, what you have to do, what we expect as a timeline before you open the first PR.

So just like logistics information, basically.

And the last section is the list of tasks.

In this example, you can see four tasks.

Two of them have been claimed and executed by a person.

We try to reward attributing the task to the person that claimed it with also the commit, where it landed.

So everything is tracked.

And there are also a couple of free tasks for everyone that are up for grabs.

So if you want to work on those, you can just claim them.

One thing that I want to stress here is that all the tasks are, we try to create them in a way that they are small, self-contained, and in several cases, like the first one here, there are similar examples in the code base that you can follow to implement your code.

So we're trying to really help you to be as successful as possible.

We're trying to give you all the tools that you need to execute perfectly the task that you want to take on.

But what does it mean in practice?

So what are the concrete steps that we need to apply in order to become a contributor following one umbrella issue?

And, again, like the code gen is just one example, there's other umbrella issue, more or less they follow all the same structure, so you can pick the topic that you prefer and you can work on that.

So the first part, practical thing that you have to do is to actually claim a task.

So to do that, you can go to the React Native repository, scroll the list of tasks, you find a task that you like, you read it, and you can start claiming it.

So almost all the tasks have some pointer to the code, following the principle that we really want for you to give, we really want to give you all the tools that you need to execute.

So by looking at the code, we can see that, for example, in this task, there are two pieces of code to parse something in flow, something in typescript.

They are very similar, like, they are basically the same code, just differ for small things, like how to get the name or how to get the node.

So it's a good thing to put them together in a single function, so if something changes, we don't have to change it twice.

Okay, I like this task, I want to claim it.

What do I do?

I simply, I put a comment in the issue.

After a comment is posted, someone from meta, in this case, myself, will assign the task to you, basically assigning it also into the task description.

So every other contributor that wants to take another task can see that, oh, this is a sign, I can't claim it.

If it's the first time that you contribute to React Native or any open source project in general, the process will require you to fork the repo.

There is a simple button on top of GitHub.

So just click on it, follow the dialogues, and you will end up having your copy of React Native under your GitHub profile.

So in this case, you can see that in the top left corner,

There is my username, which is also my handle on GitHub,

/recnative.

Next step, you need to clone the repo locally and run YARN to install all the dependencies that are needed to, for example, run the test.

And we finally can start writing our code.

So the IDE that we suggest to use for everyone is Visual Studio Code.

Of course, we are going to write JavaScript, so that's the best tool.

We can toggle the terminal, which something very useful to run tests and we as IS developers are not very used to that because it doesn't have it. And there is a go to file shortcut that we can use to look at our first file to modify. But oh, no. Red lines. We don't like red lines. Why is this

CodeGen is written in Flow, Flow is a type of dialect of JavaScript that Meta developed and open sourced as well, and we need a package for Flow to be able to use it properly inside

Visual Studio Code.

So let's install the package, it's called Flow Language Support, there are some instructions to set it up properly, and by following them, red lines are way up, disappear.

So, okay, we are up for writing the code.

So we go to the function, we create our function, and we use it in our call sites.

Now, again, the focus here is not the code base, like you don't have to bother reading that.

I'm not a JavaScript engineer and developer, so maybe there is some better ways to do that.

The point is that it's small. like the changes are very small.

And these are other couple of PR that I want to show you, highlighting this concept.

Like this is 11 line of changes.

11 line has been changed by this PR.

And just six files which are mostly imports and include similar, very similar PR.

26 lines, eight files.

So all the tasks that we try to put up are either very small or require a few code changes.

So you can be very confident that we will accept it.

We will not be rejected because it's a lot of code.

And no, it's a good PR.

It's easy to do, simple.

You won't face a lot of attrition in learning it.

The next step now is to test it.

We write our code, and we want to make sure that everything passes.

So to test, we use Jest.

Jest is a JavaScript framework to run a unit test, basically.

And this is the instruction to run it-- yarn Jest, React Native Code Gen, in our case.

This is how it looks when it starts.

So it parses all the tests inside the React Native Code

Gen package, and we can see the progress indication.

Everything is good.

So one thing that I want to highlight here is the number of tests.

CodeGen is very well tested.

We have 54 test suits and 2,500 tests.

So again, if everything is green here, there is a good chance that your changes are actually good.

And one thing that I want to highlight also for Jest is boosting your productivity.

By running Just Help, you can see that there is this bunch of watch instructions.

When we run Jest, which this switch turned on, what happens is that Jest is spawning a daemon, which is going to look at your files on your environment.

And as soon as you save one file that matches the pattern, or even not if you use watchful, it will rerun the interesting test for that file.

So instead of making a change, save, run test command, you just have to do the first two steps and the test will run automatically, which doesn't seem, but is a huge boost if you have to do a lot of changes because those small savings of time sum ups and at the end of the day, you will be faster and more productive.

Okay, everything is green.

We run our test.

We are happy.

We can commit our changes.

One thing that I want to highlight here is the branch syntax convention that we follow.

Basically, this is my handle slash the name of the feature that I'm implementing.

This is a nice and fast way to group together contribution from a single person.

So if I want to see what are my contribution,

I can just, they are sorted alphabetically, so all the Chipoleski slash things are together.

And then is the usual dance of GitHub, commit and git push.

We can then go to, like in this case, my copy of React Native repository, but it can be also yours, and there is this yellow box that we can use to create a pull request.

GitHub is pretty smart, so when we tap this button, it will already set up the pull request to target the main branch of React Native in the Facebook repository, meta repository,

So everything is already set up, and we also prepare it with a template that we need to fill.

One thing that is important to note is the changelog.

The changelog has to follow this specific format, because we have a tool that automatically parses the changelog and creates a pull request for us.

Why this is important-- in between releases, between '70 and '71, or '71 and '72, there were almost 800 comments.

So if we have to go manually through all those 800 comments to write down the changelog, it will be messy.

So please, when you contribute, follow this format.

The template also suggests you other keywords.

So everything is there.

You just have to spend a couple of seconds of attention putting down the right keywords.

Everything is ready. we can open our draft PR.

And when that happens, CircleCI, which is our provider for running the CI in the open source, will start running those tests.

One tool that we use is Danger.

In this case, Danger is telling me, oh, there is something wrong in your PR.

So we can look up and see what's happening.

And I can figure out that I forgot to run Prettier at the end of my coding session.

This gives also me the opportunity to talk to you about the script section of React Native, because the framework comes with a lot of scripts that you can run locally to speed up your development or to simulate some tests that happens in CI.

So in this case, we can just run yarn prettier to make sure that everything is aligned with our linting rules.

But there are other scripts that you can run, like flow, flow checks, or even you can try to test, run the same test that runs in CI with test CI.

So let's run prettier.

Let's see that it automatically update our code base.

So we can push again.

And as soon as we push a new commit on GitHub,

CI will run again.

At this point, let's suppose that everything is green.

So we can mark the PR as ready to be reviewed.

When this happens, we have tooling internally at Meta.

And automatically, it will ping some of us to notice us that, hey, there is a new PR. you need to review it because the contributor has spent some time on it.

You have to take care of that.

We review the code in this case.

And mostly, all the cases of code gen or the umbrella issues, we see that everything is OK.

So we approve it.

In some other cases, there are small changes that we suggest.

So it will be-- usually, it's pretty fast iteration when the umbrella issues.

And once approved, we import it in internal system, which is called fabricator as you can see here.

When imported, we run some other tests in internal infrastructure because as I told you before,

Meta uses React Native internally, so we need to make sure that the changes that we import doesn't break everything.

But when it's ready and everything is green also internally, we can land it and you will finally see your commit as top commit in the GitHub history.

And that's how you become a React Native contributor.

So now, what are future opportunities for everyone to contribute?

One is, again, improving CodeGen.

And in CodeGen, there is a lot of things to do.

I'm trying to keep the task list updated as much as I can.

This slide is slightly updated, actually.

I'm sorry.

We had like 140 tasks now.

Most of them are done.

We are in a weird state because we reached -- you need to tap nine times in the load more comments, so we are thinking about splitting and improving code in another, separate issues to basically go on with the work so it's easier to contribute for everyone.

So bottom line, keep an eye on these.

More tasks will come soon if you want to try it out.

Another way also still using issues from GitHub is to look at good first issues label.

These are issues which are usually small, self-contained, like the one that we already saw, but we cannot really put them together under a same umbrella, so they're a little bit spread across different topics, but they should be good for everyone to pick up and start working on them if you want to.

Another way to contribute is with the other issues, but not in the React Native repository.

For example, here is the CLI.

CLI is what we use to run React Native, and there are issues that you can take on here as well, but CLI is just an example.

You can really do that with WebView, for example, or any other components that you use.

Most of them, almost all of them are open source, so contributions that are as welcome as on the core of React Native.

Oh, wow, it works.

If you instead have a new feature that you want to propose, but you don't know from where to start, or you don't think that creating a PR from scratch is the good way to propose that.

There is this other repository, which is called Discussion and Proposals, where we try to collect all the RFCs, proposal in general, we discuss them before people can start implementing them.

So that's a good way to have higher level discussion for everyone to confront each other and find the best way to improve our framework.

Finally, this is a new umbrella issue, open a couple of weeks ago from one of my colleagues, Meta,

And it's on the CLI in this case.

So as you can see, we are trying to use the same approach, not just in the core framework, but also in other repository that we actually care a lot about because we need them internally as well.

The whole point of this umbrella issue is to improve the onboarding experience for React Native.

So when you start a new application, but of course, it has implication also on the upgrade story, great part.

So if you want to improve that part, because maybe you feel it as a pain as well.

I'm not looking at anyone in particular.

You can have a stab at those tasks and improve the life of all of us, basically.

So I have only one question for you.

Did I at least convince to try out contributing to the framework?

Okay, that's good.

Thank you very much.

Again, I'm Riccardo.

Connect on the various social.

(audience applauding)

I'm super happy to be here.

Thank you, Ricardo.

So Ricardo, you are also an iOS developer.

So do you mean it is possible to do both iOS and React Native?

Yes, definitely.

Kind of the trash question, obviously.

Actually, maybe out of curiosity, what moved you from iOS development to trying out to be part of the React Native Core team?

So first of all, I'm still an iOS developer, so most of my work is still on the iOS side of things.

I'm very interested in how to build iOS projects, and of course, this is one of the part of React Native, so that's the thing that attracted me into the React Native world.

On the other hand, this is a great opportunity not just to be focused on only iOS.

I think that in the software engineering field, are a lot of things going on and my experience is that if you expand like your horizon with other languages or paradigm, you can become a better software engineer in general.

So when I joined the React org, I joined that with the ideas in mind of being exposed to other technologies, how they work to become a better, more well-rounded software engineer, not to be super on the iOS.

- Cool, thank you for sharing.

And that was a super inspiring talk, I think.

I did have one question myself.

Like if there's someone who's maybe a junior developer who feels like, oh, they're not super experienced and they feel like maybe someone would be better to claim some tasks or to contribute to React Native,

What would be your advice for that person?

- Just try it.

I mean, the nicest thing of the React Native community, the open source one, is that it's super kind and welcoming.

And I really like the vibe, I guess, as soon as I joined the extended open source world around React Native, I was super well impressed of how everyone is welcoming you and excited about the framework.

The reality is that contributing to a framework to like React Native specifically in open source is a way for everyone to get better.

So if you are, even if you are a junior, you should not be worried about, oh maybe my code is not good enough or other people are more qualified than me.

The point is exactly that, like we are there to also help everyone to grow and become a better engineer.

So we learn a lot from the community as well.

It's not like a one direction only way.

So yeah, I mean, I understand that there is this first obstacle of like, from where do

I start, would it be good enough?

The reality is that even if it's not, we are working together on that.

So at the end, it will be good enough to be landed.

Fantastic.

So yeah, the answer basically is try.

One last question.

Yeah. what got, like the Umbrella project is super amazing, like it feels like, and when you say try, you don't just say try, you say like, oh, try, and we give you the tools to try and to go ahead and contribute and we make it like super easy. Like how did this initiative get started, basically? Because it's, I don't know if there's any other projects with similar things.

Okay, how it started.

So the framework is huge, as we saw, several moving pieces, and we try, we cannot really do everything ourself, also because in Metainternally we use it in a very specific way, which is different from how people outside use it.

Not that different, but there are differences.

So for us it's hard to have everything, to be able to cover all the use cases that everyone can encounter.

So we were thinking about, okay, there is this part of the code base which needs some care.

We don't really have all the resources to put that care inside that part.

Let's use the, let's collaborate with the community and let's make it sure that everyone can use a tool that it is polished, which we all need. and basically I was really interested in the code gen specifically, so I started drafting a few tasks that I thought, okay, these are simple enough.

Let's see if someone's interested as well.

It gained traction, and so I just keep doing that and creating tasks for everyone.

- All right, that's awesome.

- If I can add one thing, fun fact that happened last November or December, at some point,

I was involved in the release of 71, if I remember correctly, so I was a little bit short of time.

And all the tasks were claimed and almost done.

So the community itself came up with some other tasks to work on, which were like, OK, this is good.

Let's go.

It's OK.

Nice.

Thank you, Ricardo.

Thank you so much.

Thank you.
