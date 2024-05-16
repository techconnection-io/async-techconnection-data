---
slug: >-
  /talks/react-native-connection/2024/mickael-dumand-top-5-metrics-you-should-track-to-improve-your-react-native-app
date: '2024-04-23'
title: Top 5 metrics you should track to improve your React Native app
author:
  - Mickael Dumand
video: Im8APhmdkys
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/Im8APhmdkys.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: '2024'
allow_ads: false
---
### Mickael
Hello, everyone. I'm happy to be here. As I said, I hope I will not have a son today.

Let's try. So I'm Michael, a freelance software engineer, and I started playing with React Native in 2015. Since then, I'm working on more than seven consumer apps, and this talk is an extract of what I learned along the way.

So generally, I try to have a data-driven approach, and this is definitely a picture of someone pragmatic. I live in Troyes. If you don't know it, it's the best place to be in France, so come and see it.

I remember the first prototype of React Native in 2015. It was on iPhone 5 and iOS 9. Android was not supported yet, and today, we have thousands of apps ranking in the top of Apple and Google Play Store.

So good job to everyone. The community is doing pretty well, and keep going. So looking at data, we've already seen this, but today, we have more than 2 million daily downloads on NPM, so let's continue these good trends.

As I said, I'm working on different kinds of consumer apps. As examples, there is Sephora in e-commerce, MPG, a fantasy football game well-known in France. I also work at Leuco, a new insurance connected to hardware devices, and currently, I work on Sush.

It's a social gaming app with a lot of animations. Pay attention. There is some Sushi animation in this slide, so I hope you are not starving.

From all this experience, I ask myself, technically, what makes a great app? So today, I think a great app is Reactive, an app that doesn't crash, an app without error, up-to-date, and download it fast. Let's see here.

Automuseum, download it fast. So this one, of course, is by looking at the app size. If we look at iOS, you can directly see the app size on TestFlight built, so you can inspect and directly see it.

And on Android, you can go on Google Play Console, and on the app size tab, you will see the size of your app. And Google is pretty good with this. There is some recommendation telling us to optimize your images or to extract larger files.

So it's good to follow that practice. OK, optimizing native size is good, but what about your JavaScript code? Actually, to inspect your JavaScript bundle, you can use this great command line, npx react-native-bundle-visualizer, and it will output an interactive table in HTML.

So if you never seen it before, there is a lot of information, but we will look step by step. So looking on the right part, we can see the percentage of unmapped. It's often something that we don't look, so we are looking on the left.

And it means it's not directly code-related, but can include image assets or JSON. So if you have a big percentage here, you know that you have asset optimization to do. And let's check what's inside the node then on the left part.

So if we look at this example, there is, for example, moment.js import that is taking some spaces. So moment.js is working good, but there is one issue with it, is the size of the bundle. So if you are using it, you can replace it with dgs, a lighter version, with the same level of features.

And here to help, I use import cost extension, so you can directly see the size of your package in the VSCode editor. So to remember, be selective when installing a library. There is this meme on the internet that is telling us that the heaviest objects in the universe are non-module.

So by compressing images and cleaning dependency, at Leuco we have divided the bundle size by two. And okay, app size is maybe not the most important thing for your user, but in general, less codes mean faster opening time. So it's really important if you are using over-the-air deployments, like CodePush or ExpoUpdates, this bundle, this reduction of bundle will really make the difference when you're making update to your user.

So app size is reduced. Can we take a break? Nope.

Let's see the next metrics, so how to measure up to date. Sure, to measure up to date, we will check app version. And let's see why it's important.

If we are looking at data, actually, we see a version can take eight days to reach 90% of active users, and it's coming from analytics in our amplitude here. And it's pretty okay, but what happened to the last 10%? We can see on our actual app that it can take several months to be updated with 20 version still active use.

So mobile apps are really different than web or backend on this point, and that's why it's important to notice and try to work on this. So there is no magic solution to fix this. It's really part of the ecosystem.

So the best thing you can do is to push a model to inform your user and redirect them to update. Now user are informed to update. Good job.

You can take a little break. And let's see how to measure doesn't have error. So obviously, it's the error counts.

And without it, we are quite blind to know the error impact. So it's really important if you want to investigate what's happening in production to measure it and follow it regularly. And to do it, let's create a simple logger module with one function here, the capture function.

This function takes a string, some params, and a level to group them by priority. Actually, there is different levels, the error, the warning, and the info. And we will focus on error to catch the most important things in the app.

Once you are creating your method, then you call your monitoring tool like Sentry inside with all precious information that are coming from there. And if you didn't know what to put in your try catch, actually, now you have your logger, and you call this in every part of your critical code. So then you can have your feedback.

The result of this is you can monitor in production with Sentry or other monitoring tool. And Sentry will add useful information like which release it happened, how many users are impacted, and much more. As a bonus, I like to send this information to amplitude also.

So you can add one more log event. And the benefit of this is you can really understand your user behavior when an error happens. It's not just about stack trace and a lot of technical information, but it's also what happened during the flow of the users.

So take your time on implementation because logs are easy, but the harder part is more to categorize them properly. So if you are not doing it properly, it can be unusable. So yes, it's really important to take the time to not creating too much noise.

And as a bonus, by combining with version, we detect regression. So when a regression happens, we can definitely target a specific version and investigate more what's happening. So we fixed all the errors.

Can we take holidays? No. You probably know the answer.

Nope. Because actually, the worst scenario for a normal engineer is application crash. So if you have a native crash, it's not something that will be handled by the logger.

So it's really important to check it. And how to measure it doesn't crash? Clearly, it's the crash free rate.

So looking here at Sentry, we can see the crash free rate is the percentage of time your application was used without crash. But there is two numbers. The first one is crash by session.

It's the percentage of session without crash. And the second information is percentage of unique active user without crash. So both are important, especially the latest one to know if the issue happened and impact a lot of users.

And let's see how to keep this number high. So to keep this number high, we will implement error boundary. We already talked about this before.

And the goal is to apply a fallback UI and avoid the application to be quit. So to make this happen, you need to implement a class component. So the old generation will know this pattern for sure.

And yes, this API is pretty old, but it's still the way to do it today. And we get the right state from error and component cache where you can call the logger we just created. So we can also get this information to our monitoring tools.

With that, you should have better crash number, but don't forget to monitor the number of error to be sure your application is stable. And once you have 99% of crash rates, we have done a good job. The benefits is to create some alerting, like daily alerting.

In Sentry, we can configure on the crash free rate here, a number like a threshold, a 97 number as a critical alert, a warning at 98%, and when it's resolved at 99, when it's above 99. As always, combining with version, we can also detect regression. So we can directly see the crash free rate by a release.

And if this number is decreasing, we will know that a new regression was introduced. So here we have 99% crash free rate. Maybe now these are holidays.

No, not yet, because actually the performance is the final boss when you are taking to some monitoring tools and working to improve your app. And there is a study from Google that is telling us that a one second delay in mobile load time can impact mobile conversion by up to 20%. This study is from 2017, but it's still valid.

And so it's definitely something we want to check. So which metric to check if our app is reactive? There is a lot of topics about performance, but if I have only one to check, I think the good one is time to interactive.

So let's see what is time to interactive. It's really the amount of time it takes for the page to become fully interactive. So it's patterns that is really coming from the web initially, but we can apply it to mobile.

And so it's really the moment where you click on your icon button, you have your splash screen, and then you can interact with your first element. When working on performance, I like to start looking at Android first, because there is much more cheap device with minimal resources than on iOS. And we choose Motorola E20e as a device for performance benchmark.

It was mainly based on the user base we have actually to check this. So now we have our device, let's see how to measure. We will use a flashlight that is a great tool that you probably know and developed by BAM actually.

And the good thing is with flashlight, you don't need to install anything on your app. So you install the CI directly, and you will interact with your app. Combining with Maestro actually, flashlight is really here to measure the data that you are taking.

But Maestro is a UI testing framework, another good tool that you should test if it's not the case. And you will configure it to interact with your app automatically. So the first thing to do is to create a YAML file where you will target the application ID, then you call the launch app, and you will just assert that your first text of your application will be visible.

Flashlight then will run your test 10 times and write the output in the JSON file. After the tests are running, it can take some one minute or depending on the test you will target, and then you can open the report. So I have done a test with the device before, looking at the first React Native in it, and we can see here the result is a score of 99 with the first version of React Native, and we have a time to interactive by near eight seconds.

So working on a little game animation, I've been benchmarking some the impact of animation, like there is two animation here, a small one that is 187 kilobytes, and the second one that is near 800 kilobytes with more complex stuff inside. And the result of that is that with Lottie, actually we have a pretty good score on the small file, like 82, with a 10 second time to interactive. And with the bigger one, we clearly see there is a drop of usage, mainly by the CPU usage that is more impacted.

We will see that just after. So we have done some benchmark. So we use Scotty, that is an alternative to Lottie, mainly based on the Skia Renderer.

So it's a young tool, but pretty promising. And here for us, with this animation, the results are not yet at what we expected. So we have a score at 68 globally, and an average time at 11 seconds.

And we can see there is a little improvement on bigger files. So we get from the score to 25 to a score of 32. But it was not the thing expected.

So we also try Rive, another alternative to do animation on mobile with React Native and native rendering. And here, we can see there is an impact on bigger files, like the score was from 25 in Lottie to 64 with Rive. And the time to interactive also is a bit aligned.

But we can see the CPU is really reduced on this part. On the smaller file, it's not that much, and there is less usage of the CPU. Another great thing with the flashlight, actually, is once you have done your measurements, you can compare the JSON.

So you take two JSON here, and you compare it. So you can really inspect the CPU usage. And then you can also check specifically the thread that is impacted.

So here, I've just chosen the UI thread because it's the most interesting one in animation. We don't want to block the UI. But if you have some extensive calls that are done on the JavaScript thread, you will see it on the MQT JS thread.

And here's a comparison. We have in red the UI thread that is in Lottie that is taking more CPU. And you have the UI thread of Rive that is in blue.

So we can definitely see the improvement. So from this benchmark, I recommend to use Lottie for small animation. Microinteraction is really working well when this is your usage.

Keep an eye on Scotty because it's young and promising, but not yet mature in my opinion. And use Rive if you have really complex animation and interactions that you want to push to your users, and especially on Android with restricted performance. So measuring is great.

But the most important thing is what we are doing from this measure. Actually, we have listed the app size, app version, error count, crash rate, and time to interactive. But we took action from it.

So from app size, we reduced the unneeded dependencies and assets. From app version, we implemented a modal update and detect regression. With error count, we created a logger dashboard to monitor the health of our app.

On crash, we avoided crash thanks to error boundaries and set up alerting so we can continue monitoring. And with time to interactive, there is much more to do. But here, we know how to speed up the app, mainly related to animation.

But what do we do when we are all busy building feature? Especially in startup, it's quite challenging sometimes. When you are focused on feature, you have no time for quality.

So from my experience, the thing I want to believe is that the best act to prioritize quality is to push for smaller interaction. So all the things I have talked before can be a roadmap integrated to your day-to-day. And taking it small by one and working on it to improve is really the way to do it and to fight for simplicity.

So believe me, it's easy to tell, but it's not easy to do. And I definitely think it's the role of engineers to discuss this with designer and product manager. The best option is often to simplify the problem we are working on.

So let's build React Native that are reactive, that doesn't crash without error, up to date, and download it fast. And now it's time for vacation. Thank you.

### Mo
Thank you very much. Let's head over to the Q&A corner. So I really liked your talk, primarily because it's very practical, right?

Just straight into it. And I'm definitely not biased because you mentioned flashlight very much, wink, wink. But no, this is really useful, and I do appreciate it.

So you talked about the unmapped section in the bundle visualizer. Just to kick things off, I'm curious as to what your experience has been dealing with that and trying to figure out what constitutes that. Because you mentioned it was assets and other stuff.

But sometimes library code also falls onto the unmapped. I'm wondering if you have any tips and tricks on how to detect what libraries. Because, for example, there is a certain cloud library SDK that has a lot of unmapped junk.

So I'd be keen to hear how you deal with that and how you handle that.

### Mickael
Yeah, I have more experience in the assets optimization, because actually on the animation, on the app for gaming, we have a lot of assets, and there is a lot of animation, actually. And so we use, I did not mention that, but we use Lottie optimized formats, where you can compress all this file. And I have not worked yet to optimize the unmapped part of this.

### Mo
Cool. All right. So a few questions.

Firstly, people seem to really like your animated sushis, so kudos.

### Mickael
It's because they are hungry, I think.

### Mo
I think so as well. We're going to have a lot of questions here, so, you know, I'm just saying, you might not get food for very long. Would you consider updating your code examples for generation 2 React devs?

Sorry? Will you use hooks? Sure.

Sure. Okay. Cool.

Glad we've resolved that, and that important question's been answered. Can you elaborate on what monitoring tools you recommend? So you showed Sentry as an example, you showed the great flashlight.

You know, what about Firebase? What are the tools, just like tool sets that you typically look at?

### Mickael
Yeah, I think Sentry is the most one for crash rate and error reporting. There is one drawback of Sentry that is I also talk about the size of the bundle, and Sentry has a big impact on this part. But actually, the tool is really good to monitor, so it's okay.

Except that I mentioned flashlight. Amplitude is really well. It's used by the product generally to monitor really the user base.

But if you use technically the tools, you can also configure some alerting in Amplitude. Yes.

### Mo
So this is a bit more on the web side, but if anyone's keeping up with the Core Web Vitals changes that Google is proposing and some of the things that are changing around, on the web, TTI is being, I don't want to say deprecated, but they're using other metrics like LCP, TBT, and INP to actually measure performance. Do you think that this concerns React Native devs in any way?

### Mickael
Yeah, at some point on the web, there is much more. I think on the web, on performance, Google is pushing a lot since a lot of time. And on mobile, it's really with new tools like flashlight and other monitoring tools, like you can do it in Firebase, for example, with real-time monitoring.

So there is an emergence of this tooling, but I think we are a bit late from the web on this part.

### Mo
It's just fundamentally different, I think. So like you said, they're just different paradigms as well. We're not dealing with network latency as much as on the web because we don't need to get the code to actually execute a lot of things.

I mean, offline support is generally there. So I think, yeah, some of it's not going to be applicable, but universal apps, it may end up being quite important. So we'll see.

And then just to wrap up, how do you create error boundaries effectively for native crashes? So in general, how would you handle that side of it?

### Mickael
Yeah, good question. Here, I just show a simple screenshot just to be explicit, but the good way is to keep the navigation as much as possible. So you can wrap it in your top-level routes, actually, but not the top level of your app.

And actually, it's not a good pattern to go too deep also because it will be really weird for the user to have the limited size of your application usable, but not the rest. So it's a balance between user experience and technical stuff.

### Mo
So I said final question, but there's two really good ones that came in, so I can't resist. One, just quick fire. So the first one is memory usage seems to be a good metric as well.

Question mark. And I guess the answer to that is Flashlight also has memory usage being shown, so you can monitor that. And then, over time, how do you monitor performance and bundle size?

Do you do it on pull requests or before releases? What's the process to stay on top of this continuously rather than on a snapshot?

### Mickael
Actually, what I've shown with Flashlight is more to debug on a day-to-day when you are working on feature and you want to test it directly. But for monitoring and be sure when you ship it to the user, we call this real user monitoring performance. And there is two options that I've used.

There is Sentry that has the tracing part. And combined with React Navigation, you can know the path of your performance by stack, like by screen. Or you can use Firebase that is also not measuring directly the TTI, but measuring the app starts in production directly.

Cool. Thank you so much.

### Mo
Really appreciate it. Thanks. Thanks.