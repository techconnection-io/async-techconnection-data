---
slug: >-
  /talks/flutter-connection/flutter-connection-2025/alicja-ogonowska-listen-up-mastering-ab-testing-and-feedback-techniques-in-your-mobile-apps
date: '2025-04-04'
title: Listen up! Mastering A/B testing and feedback techniques in your mobile apps
author:
  - Alicja Ogonowska
video: OCR_GU_fMLo
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/OCR_GU_fMLo.jpg
slides: null
tags: []
year: 2025
conference: flutter-connection
edition: flutter-connection-2025
allow_ads: false
---
### Alicja
  
Hello, everyone. Yes, now you can hear me. Welcome to my talk where I'm going to be showing you some A/B testing essentials for your Flutter apps. My name is Alicja Gonowska and I work as a senior mobile engineer at OLX. I'm based in Gliwice in Poland and actually I have some sweets from Poland. So feel free to reach out to me after the talk or during the party and you may get some. And as Wadim mentioned, I'm a member of Flutteristas community and there will be a Flutteristas conference streaming tomorrow on Flutter community YouTube channel. So don't miss on it. And I wanted to ask you, have any one of you ever done A/B testing in your apps? I actually see some hands. I was afraid that I won't be able to see anything, but I decided to ask the question anyway. So I'm glad to hear that some of you are already familiar with it. 

So basically A/B testing is exposing your users to different versions of the app to see which one performs better. And usually we have at least two different versions of the app or a feature with one of them being the so-called baseline. So something that you already had in your application and another version is a variation that you want to try out. And usually you are having some kind of remote values data source that will be distributing different values to your application, let's say A and B. And based on that, your application will behave slightly differently. Maybe the UI will be different. Maybe some flows will be changed. But what is most important is that your application already has those two versions implemented. And based on the remote value, you are differentiating what the users are seeing. And after that, you need to somehow measure, is it better or is it worse? And for that, you can use your analytics and track some events that are necessary to validate this kind of test. And after that, you can, for example, see that, okay, version A was definitely better. This is the winner. And the coolest part about A-B testing, you can mark this variant as a winner and automatically roll it out to all your users and you don't need another release. So no reviews, no waiting. Everyone will have the best version right away. 

And you may be asking yourself, doesn't it double the work? Because anyway, you will have to implement two versions of the code inside your application. And it's kind of true, but in return, you are making informed decisions because you don't have to rely on the guesswork. And sometimes we think we know what is best for our users. We think that our idea is just the best and it will make the app the greatest, but users may disagree. So automatically this saves you from making poor changes because even if your change turns out not to be so great, you can just finish the experiment, say, "Okay, that was not a success. Let's roll the better version to all the users." And ultimately you should be able to reach higher conversion rates because you are able to fine tune specific parts or flows of your application that you care about most. 

And how to design an A/B test? First of all, you need to define your goal, and it has to be specific and measurable. You can't just say, "I want my app to be better," but you can say, "I want more users to register." And then you need to hypothesize the change, so this is where you come up with ideas that will help you achieve the goal. So if you want more users to sign up, maybe the sign-up form should be more friendly to them or even shorter. After that, you create the variants and split the audience. So this is the actual implementation part. And then you need to release this app version, start the experiment and wait for the results. After that, analyze them and roll out the winner. 

And I'm going to show you a simple example. So let's say I have an e-commerce app where I want to make more users add to cart the products. And my hypothesis is that if the add to cart button will be more visible with more contrasting color, they will be using it more. But A/B testing doesn't have to limit to just UI changes. For example, a popular use case for A/B testing is the push permission prompt, and you can test out different flows or after how many app launches to show it to the users, so you don't have to limit yourself to that. And I'll be showing the example using Firebase A/B testing. And inside the application in my UI code, it's as simple as just using an if based on some use accent color call to action value that I'll be getting from a config. I'll show you in a second. And based on that, I can decide which color to use. 

And I also created an experiment config, which is some kind of utility class that lets you store all your experiments in one place and maybe even add some utility getters to get the value of the experiment more conveniently. And it's up to you how do you want to structure your experiments. In here I prepared examples for a boolean experiment or string one. So sometimes you can decide based on just a true or false value. It can be a string, it can be even a JSON. If you want to have a more complex config this is actually up to you. And after that, when it comes to fetching it from a remote config, all you have to do is at the app startup, you need to initialize it. So remote configs requires you to fetch and activate. And I'm also storing all the values in a map because it's easier for me later to get the experiment value based on the experiment type. So this is just some kind of utility code that you can use, but you can even just read it directly if that suits your needs. 

And you can't forget about analytics, because if you don't add your analytics events, then you will not know how does this experiment behaves. And since I was interested in add to cart event, I need to log it. And then in Remote Config, you need to actually create the experiment. So we need to select a name. You can also add some description. And you can target your apps. And unfortunately, a note that in Firebase, Android and iOS apps are separate apps. So you have to run two experiments for a Flutter app. And then you can also target your users. For example, you can select an activation event that maybe there is a precondition that needs to happen for the user to be eligible for the experiment. And after that, you need to select your goal. And there are some pre-configured goals or you just use your regular analytics events, also the custom ones. And after that you just select how you want to divide. What is variant A, what is variant B. So actually in Firebase it's not A and B, it's baseline and variant A and then B, C, D, et cetera, but it's just a naming. 

And when it comes to analyzing the experiments results, it's hard to mock up something. So I don't have the results of the experiments that I just showed you because it was just me testing my different phones. But I have some experiments from the past to show you how it looks like. And for example, in here I had a successful experiment where there was a very clear improvement and you can see that one variant performed much better. And then you have an option to roll out the variant to all the users. So it's just one click in Remote Config console and sometimes the experiments are not that spectacular. Maybe the difference will be really, really slight, like it's probably due to a random chance, but you can still decide something based on the results. And sometimes you just only started running the experiment. This experiment ran for like a few days and yeah, like you have to wait a bit more because remote config and A/B testing, this is not something that happens over a day. You need a bit more time. 

And there are also some other tools apart from A/B testing from Firebase, but they are mostly paid tools. So keep that in mind if you are a part of our organization, then probably you can use something more complex. And also many organizations use some in-house solutions. Like, for example, in OLX, we have our own analytics, our own A-B testing tools. So there was no point in showing you that because anyway, you won't be able to use that. But the general idea is always the same. And I also have some best practices for you to conduct a successful test. So it's best to test one variable at a time because otherwise you will be not for sure where are the better results coming from. Also, you should ensure a large enough sample size. So if you don't have an app with hundreds of thousands of users, feel free to split your audience in half and involve all the users in the test. And also it's important to leave a backdoor for testing. So as the CI/CD guys were showing you before with the feature flags, it's always good to have some kind of debug menu or at least a way to display what kind of variant you have right now, because otherwise you don't know whether it's an A/B test or a bug because, well, where is the feature? I don't see it. And last but not least, A/B testing goes beyond mobile apps and you can also test store listings. So in Google Play Store and App Store, you can select different descriptions or screenshots. Also, if you are using tools like Revenue Cat, you can check different pricings or even paywalls. And also most marketing tools offers you a way to A/B test push messages or in-app messages. So thanks a lot. Here is the link to slides. And if you want to talk more about it, ping me on Twitter, LinkedIn or Blue Sky. I'm basically everywhere. Thank you.

### Vadym
  
We're going to start from this one. What would be the difference between ABExperiment and Remote Config when you turn on flag based on different ways?

### Alicja
  
I don't understand the part about different ways, but basically remote config allows you to do feature flags. Because feature flags for me is just, you know, turning something on and off. And of course, you can decide that you can turn it off for some people. But with A-B testing, you have like a goal in mind. So it's not a safety measure that, OK, I'm not super sure about this new feature. So I'm going to enable the feature flag for half of the users and see what happens. Because then you are just waiting for crashes not to happen, usually. And with A-B tests, you always have some kind of goal in mind. So this is the difference for me. I hope I answered the question.

### Vadym
  
If they are silent, I guess, yes. And then how to decide on when the A/B results are significant enough to roll out the winner?

### Alicja
  
Well, all the tools show you that, so I mean, if you will see the results saying that the difference is 1%, then maybe you want to wait a bit more and see if that actually changes. But if you see a result of 20% plus events that you are waiting for, then clearly this is okay. So the good thing is I recommend using tools that are designed for that, because of course you could do everything from scratch. You could have your own analytics, remote value distribution, and then you can do all the calculations on your own. But yeah, who has time for it when there are tools dedicated for that?

### Vadym
  
I believe that actually every company and each company have their own metrics. So, I mean, you can imagine the scale 1% in a scope of Google or Meta will be huge. 1% in the scope of a smaller startup, it's not that much. It's your company and your data analyst to decide, or maybe you, because if you don't have a data analyst, but that's my opinion.

### Alicja
  
Yeah, I agree. I would say that A-B testing is great for huge apps because, as you mentioned, 1% can often mean millions of revenue increases. But even the smaller apps can try out A-B testing and see how the users are interacting with the app. And maybe for you, the changes will be much bigger.

### Vadym
  
Yep. Here then, what's your favorite tool for A/B testing and why?

### Alicja
  
To be honest, I still recommend Firebase A/B testing because the issues arrive when you want to do more complex tests, like mainly with the result analysis. It falls short when you have to check some more complex events or parameters, but it's a great way to start. Also, because many apps already use Firebase, already use remote config. So it's quite easy to get started and start your first experiment. And also quite easy to ask your company to start doing that because it's free.

### Vadym
  
Yeah, whatever free is really good in the beginning, but then as I'm also speaking about some kind of architecture, try to keep it on the edge. So not to dive deep into your application, not to like have really strong connections. And then how do you handle unit and end-to-end testing alongside A/B testing?

### Alicja
  
Okay, so usually I have some kind of overrides, so I create either a service or whatever you call it so that it's easy to set up the mocks inside the test and then you can test for the different variants and that's it.

### Vadym
  
I hope that's answered your questions and at least we're saying thank you, Alicia. Thank you. Thanks for sharing this.