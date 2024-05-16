---
slug: >-
  /talks/react-native-connection-23/monica-restrepo-testing-apps-at-scale-how-shopify-manages-testing-and-qa-of-its-mobile-applications
date: 2023-06-01T00:00:00.000Z
title: >-
  Testing Apps at Scale: How Shopify Manages Testing and QA of Its Mobile
  Applications
author:
  - Mónica Restrepo
video: dpO-3OoPZNM
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/dpO-3OoPZNM.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/react-native-connection-23/monica-restrepo-testing-apps-at-scale-how-shopify-manages-testing-and-qa-of-its-mobile-applications/slides.pdf
tags: []
year: 2023
conference: react-native-connection
edition: 2023
allow_ads: false
---

So hi, everybody.

As they announced, I'm Monica Restrepo.

I work as a software developer at Shopify, and I'm obviously very excited to be here.

I'm happy that you guys also came.

And thank you to the organizers for just putting this together.

So many aspects, as you know, of developing mobile applications are hard sometimes.

And this is dependent of our experience and how comfortable we are with code bases and languages and such.

And they vary, right?

Like what we consider difficult or not.

But there is one thing that is very common and everybody agrees on or majority agrees on when it comes to developing, and that is obviously testing.

Yeah, so today I am going to act like your mom in the context of obviously developing applications.

And I'm going to tell you to write your tests and also to set up a good strategy when it comes to testing at your company or if you're a freelance developer or anything, to do it on your own, but just do it.

I am going to specifically talk about the importance of testing for your mobile apps, what makes testing complicated, and then just talk a little bit about our experience with testing on Shopify.

So while I would say many aspects of developing might get hard, we always wish that we can just write code, push it directly to production, have our apps there, and only iterate over our application just to make it better and just level them up.

But the reality, obviously, is that many times our code that we write is just buggy or just introduces regressions and so on.

So testing is important.

And one of the main things why testing is important is because it ensures high quality of our code base and our applications.

Reliability and obviously maintainability.

Self-testing code is a key part of continuous integration and continuous delivery.

And one of my coworkers at Shopify put it in one of his blog posts.

You aren't really doing continuous delivery and continuous integration if you don't have self-testing code.

And I think I couldn't agree more with this.

The biggest benefit of testing your code and having unit tests and everything in place or just having a strategy is not only being able to fix bugs and just fixing things that are broken, it's also giving confidence to your developers to make changes.

And this is very important because if nobody wants to touch the code base, I don't think there's a way to actually make an application; right?

I'm pretty sure if you have ever faced applications that have, like, very -- either complex or old applications, and they have certain parts of them that are like a magic box where everybody is like, it works, just don't touch it.

Because every time you touch it, something breaks, and nobody wants to do this.

This happens a lot with, I don't know, like bridging and stuff like that, where it used to be,

I think.

So having the confidence for your developers to be able to make changes and know that there is a backup plan to let them know that something is going wrong with the code is very important.

You don't want the amount of things that go wrong with just one fix to increase over time, or people like patching things just to account for bugs, when you can just write one unit test and just make sure that every time somebody touches that part of the code base, it behaves the same because the tests are going to tell you that something is wrong.

In relation specifically with React Native, testing is important because of the multiple things that React allows us to do.

One of them is because it is a cross-platform framework.

Obviously, it allows for cross-platform features to be implemented.

And you obviously want your tests to make sure all platforms, or at least the main ones that you're using for your application, work fine.

And yeah, so you just want to ensure that the app behaves consistently across all of them.

There is also the fact that it's a component-based architecture that relies on this type of architecture.

So you want to ensure that components function correctly in isolation, but also when they are integrated with other components.

So unit tests, I think, is the perfect way to define the type of testing you want for account for this type of architecture.

We also have the-- let me see.

Yes.

So we also know that React runs in JavaScript runtime.

And testing really helps us catch any issues related to the JavaScript system over it all, such as type coercion or just asynchronous behavior.

Equally to all of these, performance is obviously important.

And we want our applications to perform in a wide range of devices, which means they need to perform in a wide range of hardware are in different configurations.

So testing allows us to identify bottlenecks and optimize our applications for performance.

And finally, obviously, UI is very important when we want to test our applications.

And just not to test them, but just in general to engage with our users.

So ensuring that there is a consistent UI across our applications and that none of our changes affect that UI is one of the most important parts of testing mobile applications, but especially React.

Because it helps us verify components are rendering how they are supposed to be rendering.

And things just look the way they are supposed to.

So OK, so what makes testing complicated?

Why is this a problem?

So the same cross-platform differences that I was talking about before as being a blessing for React kind of become some sort of a curse when it comes to testing. because we need to make sure that we account for changes that we're making to the code base and the way they are going to behave in each of the platforms that we are targeting.

So testing needs to account for this cross-platform benefit of React.

So we ensure that we have a consistent user experience on all platforms.

We also know that many of the applications that use React are hybrid applications, which means they use native modules, making it also hard to test because you need to focus a lot on the interaction between JavaScript code and native code.

And obviously, you're required to test in separate platforms as well.

Asynchronous code is one of the reasons why, again, text can become complicated.

Most of all applications rely on networking, requests, and stuff like that, animations, and just like timers and things like these ones that are asynchronous.

So testing this code can be really complex at some times, because you have to account for promises, for callbacks, and timers, and things like these ones.

And especially if you want your application and your test to be deterministic and reliable, which is the ultimate goal of all tests.

Again, a variety of devices and configurations.

So you obviously have to account for everything that happens amongst the different configurations and hardware.

And I'm not going to dive deep in this one, because I think I've already mentioned it.

React Native obviously use a combination-- oh, I'm sorry.

No, this was this.

So going back to testing UI components, it becomes tricky, especially at the visual part of it.

So because the computers don't have eyes, so it's very easy to have a silent regression, or just things that are very noticeable for the user.

And if we don't have tests that test-- if I'm being redundant-- these type of UI changes, it's going to be-- our users are going to be the ones to see them, right?

And we definitely want to avoid these things.

Test and third libraries is obviously also something that gets complex with time, and that's because of the dependency that we have in their APIs, their code, and all of these things.

You definitely want to make sure that every time you integrate a library to either speed up your development process or to, you know, implement something within your application, you also account for testing the behavior of these third-party libraries that you're you're using are just dependencies so things don't break, especially if they are not kind of like your responsibility to maintain. So now let me go over some testing tips in general before I move on into what is kind of our strategy at Shopify.

So you might be familiar with some of these ones, but one of the most important things when it comes to testing is to keep your test units focused.

This means you don't want to test multiple components in just one test.

You want to make sure they are separated so you can test the behavior of them in different scenarios.

You also want to test behavior and not implementation.

And this is very important.

As an example of this would be, for instance, a button that changes color or something like that.

You don't want to test the logic behind this process, but you just want to test that the style is being applied to the actual component.

So you want to test that the color change and know how you got to that point.

You want to test also for accessibility.

This is a very important topic in many aspects of mobile development.

But when it comes to testing, you want to make sure that those features that you are creating to make your applications accessible are well tested, so you don't either forget about them, and they just break, doesn't exist in your app anymore, or you just make them worse for people who really need to use your application in different conditions.

There are some countries, I'm not sure if in Europe, I'm assuming yes, because that's always the case, that are really good at enforcing this type of regulations for including accessibility in everything.

But in this case, for instance, in the case of the United States, there are regulations that actually enforces mobile applications to have accessibility features included in them. to test them so you don't risk your application being in trouble.

So we want to keep the tests organized.

And then even though this might seem trivial, when adding unit tests to your applications, you are always adding more complexity to your application overall.

So the amount of files just increases, the amount of things that you have to account before when you are getting into the codebase for the first time is bigger or even when you are familiar with the codebase. So keeping your tests organized is important. Ideally you want to do it by groups and, you know, like classes of like behaviors that you want, you know, the tests to be for in the application. Always test edge cases. Always I think is a little bit of a strong word for this because edge cases are just cases that are not covered.

But at least if you have a creative enough group, you need to think for the things that you normally wouldn't think, if that makes sense.

So you want to make sure you are covered for edge cases.

I guess a very common example is just making sure that your application -- how does it work when there is no Internet?

You want to account for these things and also have the test that guarantees that if you change something, your application is going to still behave the same when someone doesn't have Internet. Just as an example. And then this is kind of a preference, depending on the organization, but I think -- and we kind of agreed on this, using test-specific data is a good practice overall. And it kind of, like, guarantees reliability and your test to be repeatable. And this is because testing data is data that you have kind of like make and molded according to the things that you have and you want to test. Versus if you test with production data, which is also important but not as important as we're doing with test data, test specific data, you might not have variances in the input and the output in this case versus production.

Okay.

So how do we do it at Shopify?

We have through time kind of like adopted or kind of understood that unit testing is

-- end to end testing and test driven development is one of our basis when it comes to testing our mobile applications.

And I dare to say that it comes for pretty much all of our products, our tech products at Shopify.

Unit testing and TDD allows developers to ensure their code, obviously, is in place to be shipped to production.

And so bugs aren't hitting the users, right?

And as our ambition for scaling our mobile applications has increased, and also our development velocity, we have found that on many occasions that even with a bunch of things in place, like about-- what is it?

19K screenshot, your needs and functional tests for iOS,

Android, React Native, we still sometimes fall short to test everything.

And we have, obviously, bugs and regressions that are just shipping to production.

So this has made us kind of intensify our intentions to improve the testing strategies that we have at the company.

So we obviously have adopted end-to-end testing as a way of testing across various units to make up our applications in the way that most closely resembles the user experience.

And these user-based scenarios part and the user experience is, I think, the focus of what testing is, or one of the key takeaways of this talk today.

Because you don't want to test for engineers only and for developers that are putting code into the application, you want to focus on whatever you are delivering to your users.

So we realized that the longer we go without end-to-end testing, the more code we are shipping out, but the more code is coming back to us so we can fix it.

So then this was slowing down our process with creating new features and just evolving our applications.

For end-to-end testing, then, so we started working with the screen object model, which derives for the page object model.

And what this is is a design pattern that is-- and I'm talking about the page object model, which is the pattern of this thing-- is a design pattern for testing that focuses on UI and just end-to-end.

And then it has the mobile version, which is the screen object model.

And we have adopted it.

The idea with this is that you divide the application into modules and screens as needed, and then abstract object recognition and actions on those objects from the test level.

So just pretty much ripping away the functionality that you offer to your users, and then just being able to test it.

And this has allowed us to go with a more functional testing strategy rather than just a hierarchy-based one, which allows us, again, to have our test to be reusable in multiple scenarios.

Another thing that we really like to focus on is testing the tooling that we use for testing.

So we leverage tools like BrowserStack, Snack, and Apium.

Let me see if I have--

Okay.

So here I was going to show a quick giphy of one of the implementations that we have with APM.

But it's okay if I don't do it.

I can't just put it up without interrupting the presentation.

Basically what I was going to show is some demo of how we use the app.

And in this case, it was just to verify that every time the user taps into one of the buttons that we have in one of our menus, we use APN to verify that everything renders correctly and there are no regressions where we are introducing changes.

So again, that's talking about tooling.

Then we also strive for creating tools that facilitate our own internal process for testing.

And when we don't have them out there in the public,

We are currently working on React Native Testify, which is a snapshot type of library that helps us test UI.

I think I have a video for this one that's good.

And basically in this example that you're seeing, this is basically testing one of the banners that we were supposed to display for the user in the app and then making sure that

The screenshots after the changes, the new changes were introduced within the app, kind of matches the screens that we have previously loaded.

And we know they were corrected in regards to that banner component.

So yeah, I know it's pretty fast, but that's basically what it's doing.

Another part of our testing strategy at Shopify is top hiding.

So manual testing of all of the PRs that we want to ship into production is part of our culture at Shopify.

So we have called this process top-hiding.

And this comes from back in the days when GitHub didn't allow for a PR review system.

We leverage this tool in the mobile infrastructure as well for this one.

So we can make top-hiding easier, especially when it comes to mobile for all of our developers.

So basically we created tooling that provides a seamless and integrated and interactive experience for the developers, or contributors, to call them better.

So we built a desktop application for Mac that is called Top Hat and that lives in the system menu bar.

So under the hood, the way it works is we have the Top Hat application exposes a lightweight

HTTP web server that we link from our PRs in GitHub.

And this is because GitHub right now doesn't support custom URL schemes.

So then in the Shopify mobile repository, we kind of like integrate this to the continuous integration pipeline.

And then the pipeline itself, we use a bot that helps us create pipeline artifacts, which are just like build-ready type of artifacts that will help us then test our applications in the future.

And then we store those in Google Cloud Storage buckets.

So that makes it easier for us to retrieve the build artifacts in a later time, which is the objective of this tool for top-hiding in this case.

So this means that we basically reuse the builds for iOS and Android applications and also for React Native for this purpose of top hatting. And then GitHub -- the GitHub bot just give us the opportunity to download both of the builds for the case of iOS and Android just from one click. And then I don't know if you'll be able to get this for you to show.

I was going to show also how does the top-hiding app look like.

But basically it's just imagine the continuous integration part of your repository and then you have the option to just click what type of application you want to download and instead of having to go through build times and all of these configurations locally in your machine, you just have it there opening the app for you so you can do tests faster.

We also obviously use manual QA.

And I'll show you what-- that was for the video that I can show.

We do manual QA, obviously.

And this is pretty much the users that are involved in mobile development at the company are the ones that are testing our applications in low-end Android and iOS devices.

So we are sure that we cover all scenarios for those users that are using these types of devices.

This is because simulators and emulators are generally a good strategy to test the logic behind the code that runs our application.

But they are definitely not good indicators of performance, right?

Especially when it comes to lower-end devices.

So that's the purpose of ManoAQA.

So yeah, while there is still a lot of work from us and from the React Native ecosystem and community in general to do in terms of testing applications and just having libraries out there that make it easier, testing our mobile applications is our way to strive for getting better every time, not only the products that we ship, but also investing in things that might benefit the community in the future.

Our idea with testing is everything, and pretty much everything we do at Shopify, is that if we can make our development process or an experience more enjoyable, faster, and just better in general, we can continue focusing on making commerce better for everyone through our tech products and, obviously, our mobile applications.

And that's it for me.

Thank you.
