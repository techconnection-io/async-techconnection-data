---
slug: /talks/frenchkit-2022/zamzam-farzamipooya-cloud-functions-to-the-rescue
date: "2022-09-30"
title: Cloud Functions to the Rescue!
author:
  - Zamzam Farzamipooya
video: DdGfFkOz9gQ
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/DdGfFkOz9gQ.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/frenchkit-2022/zamzam-farzamipooya-cloud-functions-to-the-rescue/slides.pdf
tags:
  - Other Languages
  - Back-End
year: 2022
conference: frenchkit
edition: "2022"
allow_ads: true
---

0:00:26.3 Zamzam: Hi, everyone. Okay, so my name is Zamzam. I'm an iOS engineer. I've been doing iOS for the last seven years. I've worked in Iran and in Denmark. And now I work as a tech lead and senior iOS engineer at a company called Veo Technologies. It's based in Copenhagen. And I'm here to tell you about Cloud Functions. So, Grady has said the functions of a good software is to make the complex appear to be simple. And to me, that's exactly what Cloud Function is doing. So as a mobile engineer, we all had our share of having these problems, having to call multiple APIs just to load one page, or handling a lot of business logic client-side, or keeping local data on the client for some reason, and the list goes on. Okay, so how many of you in the audience have wished to be able to do some back-end work in order to avoid doing these things client-side? Wow, okay. [laughter] Okay, yeah, great. I've been there myself.

0:01:38.4 Zamzam: So one of the usual blockers, at least these were my blockers. I didn't know where to start, or I didn't know what dataset to choose. And as Maxim said yesterday, it's actually quite important. And I didn't know how to deploy or maintain a back-end project. And to be honest, it all seemed way too complex. So that's where Cloud Functions come to the rescue. What is Cloud Functions? So Cloud Functions is a serverless framework. It runs on event triggers. You can... So the code is stored in a Google Cloud Panel, which means that you can update your business logic without having to give an update to your app. You don't have to do any maintenance. So the Firebase automatically scales up computing resources to match the usage pattern of your users.

0:02:33.4 Zamzam: It's private and secure. You can deploy it with one line of code. It integrates very well with Firebase Cloud Messaging and other Firebase systems. So if you wanna build a notification system with some business logic, you can use this. And you can run intensive tasks like machine learning tasks that you don't want to run on your client. Also it integrates with third-party APIs. And there's a lot of integration that you can use with Cloud Functions. They've recently released the Version Two, which has a bunch of cool features. Some of them are that you can execute more than one request at a time. New trigger types are added, like Crashlytics velocity alerts. And it should be functions can have a one-hour timeout. Previously, it was nine minutes.

0:03:28.0 Zamzam: So a quicker start, you can use a Google Cloud Panel. So you can go in, and it has... I know that maybe you cannot see all of the steps. But it's basically some steps, and you can finish it within five minutes. You can just deploy a "Hello World" function. Everything is done through Google Cloud Panel, so you don't actually have to install anything on your machine. And you just get to know how it's actually working. But what I would suggest is to use Firebase CLI. In order to do that, you need to create a Firebase project or use one that you already have. You need to install Node.js and Firebase CLI on your machine. And you need to initialize your project with JavaScript or TypeScript. Oh, I know, don't sweat. There's nothing that a Swift engineer cannot handle. So you can do all of this with these, basically, three line of codes in the terminal. So let's write function.

0:04:27.5 Zamzam: The first step is that we're gonna write some code, we're gonna test it, and we're gonna deploy it. A bit too optimistic for a flashlight talk, but here we go. So when you run a Firebase init function, you just... It will create a folder for you. The structure is you have a project directory, and inside that there is a function directory and a source directory. And then you get to this file, `index.ts`, which is the main source file of your code. So everything that you're gonna see in the next slide is gonna be in this file. So TypeScript code. So this is actually a Cloud Function, and I'm gonna walk you through it. It's actually a callable cloud function, which is not exactly as a normal cloud function. The main difference is that you can call it directly from a Firebase app. And if you are using Firebase authentication, or FCM tokens, app tokens, app check tokens, you don't have to send it anymore. So the SDK will take care of that for you.

0:05:35.2 Zamzam: So as you can see, the data is the part that you receive as input from the client, and the context part, there is the authentication information that you get. So in this function, I'm expecting to receive a name, a family name and a birth year from the users. And then I can do some error handling. This year, I'm just expecting to receive a name as a string, and it shouldn't be empty. Then I have some business logic. So this function, what it does is that it checks to see if the user has a legal age. And as you know, it could be different within different countries, and it could change over the years. And you can come and change this at any time without having to worry to give an app update, or force update your previous versions. And this is the return object. It's a JSON object. And it's a combination of name and family name. And the Boolean saying if thes user has the legal age or not. So that was it. See, that not that bad. So let's test it.

0:06:43.4 Zamzam: The first step is that, save your code. Not all the IDEs have autosave like Xcode. I learned that the hard way [chuckle]. You navigate to your function folder. And after that, you just run NPM run serve, which what it does is exactly like Command+R in Xcode. So it builds your project and it starts the emulator. After you run that, you see some logs and then you see something like this. So on top you see the URL that your cloud function is running on your local host. And then you see, the URL for the emulator UI. And here you can see what emulators you actually activated. So the emulator UI will look something like this. And as you can see, I'm, using Firestore and Functions, for this emulator. I'm not using anything else. Now, I'm gonna test it with Postman or any other things you would use for testing APIs. I'm giving it the data that I define, and then as you see, I'm receiving the JSON object, a full name, and is legal.

0:07:55.7 Zamzam: So, to call functions from mobile apps, you have two options. The first one is to call functions via https request, like any normal request that you would do. The second option is that the callable function, which is what I showed you, you can call it from your app with cloud function SDK, and I'll show you how. So this is Swift code, yay. So now you see that, I'm not gonna tell you how to add a Firebase project, a Firebase to your project. I think like most of you have done that. But you need to add the Firebase Cloud Function SDK through SPM or CocoaPods. And then, here you can see, how I'm actually calling the function. And as, Tunde showed you yesterday, it's using async await.

0:08:47.0 Zamzam: And it's like how you would call a normal Swift function. So `userIsLegal` is the name of my function. And I'm giving it the request object and the response object. I'm calling the API and I'm waiting for the result. So the very cool thing about this is that you can actually use `Codable` Object. So I'm using `Encodable` and `Decodable` for a request and response object. So basically everything else in your code could be the same as you would call any other API. You can see logs in the emulator, you can see other things, but like logs is part of it. And now, so we've so far, we have written and tested our cloud function. So now let's deploy it.

0:09:35.4 Zamzam: So you can deploy it with this line of code, that's actually it. And then when you run that, after a few minutes or maybe less, you'll see something like this, that deploy complete. And that's basically it. You don't have to do anything else. After that, you can go to your Firebase console, and there is a function tab over there, and then you can see a list of your functions and like some brief info about each one of them. And you can get a more overview in Google Cloud panel, but Firebase also shows you some information.

So this was like only a fraction of what you can do with Cloud Function. But what I would suggest, if you're interested, there is a lot you can do with Firebase triggers like Firestore. You can run unit tests for your functions. You can run functions on a schedule, and you can add security, which as Elliott said, is quite important. So there is a lot of things that you can do.

So next time you're in a situation that you desperately needed a back-end engineer, think about it. Maybe you can actually be your own savior and do it with cloud function.

0:10:45.5 Zamzam: **I just wanna take this moment and say that I want to dedicate this talk to the brave women of my country Iran, who are right now fighting for their freedom.**

Merci. Thank you.

0:11:12.4 Greg: Thank you, Zamzam... Once again, a round of applause please.

[applause]

0:11:26.0 Zamzam: Thank you.

0:11:30.5 Simone: So I'd say, well, thank you for speaking about that first of all, and actually, I didn't expect that. But I think it's very a nice touch, and it's a topic that should matter to all of us. So, well...

0:11:44.7 Zamzam: Thank you.

0:11:46.6 Simone: So how did you get to learn TypeScript and kind of backend development, was it like a hard step to get into that?

0:11:56.6 Zamzam: It was definitely hard to accept that I have to do it, because [laughter] I really didn't want to, but then there was no one else, and we had to finish this project. So I ended up doing it. But when I actually got to do it, it was much easier than I expected it to be. So...

0:12:15.4 Greg: So have you found other services like Firebase that gives the same kind of services?

0:12:22.2 Zamzam: Yeah, definitely. So AWS for instance, has something like a lambda function, which is almost the same, which is... But it runs on AWS, whereas Cloud Function is Google based. I guess there are more, but I know these two.

0:12:37.7 Greg: And why did you choose Firebase over...

0:12:40.5 Zamzam: The thing was at that point when I started this, our company was already using Firebase and Google Firestore. So it was sort of built in into our other tech stack that we had. So I use Firebase.

0:12:55.7 Greg: Okay, makes sense.

0:12:57.3 Simone: And what do you use Cloud Functions for in your project?

0:13:02.9 Zamzam: Yeah. So the part that... The time that I used Cloud Function is that we wanted to make a notification service, but we wanted to have some sort of business rules around it. And the way I used it was that we were actually using Firestore plus Cloud Function. As I said, there are some triggers in Firestore that can activate a cloud function. So whenever something was written on a Firestore, we would start a cloud function, which would send notifications to user.

0:13:32.9 Greg: So we have questions from the audience. Do you know the costs of using those Cloud Functions?

0:13:38.3 Zamzam: Yeah, so Cloud Functions are not for free like other Firebase features. But they have a plan, it's called Pay as You Go or Blaze Plan, which is like, you pay as much as you use. So it will give you an estimation of like based on the things, and like how much you would end up paying, but it's not like a fixed amount. So it's like you pay as you use, as much as you use their resources.

0:14:06.6 Greg: So for instance, the project you're working on, how much is it?

0:14:10.7 Zamzam: I actually don't know, [chuckle] that's not my part, but it was worth input, it was worth it. So, but I don't know exactly the number. Yeah.

0:14:21.4 Simone: Do you see any potential risk? Like a leak of information using those services for some reason?

0:14:31.8 Zamzam: So they have a lot of things for security, as I said. So you can add security code to like how, or who, or like who has access to use your cloud function and also Firestore. And they are saying it's pretty secure. And in our experience it was pretty secure. We all, of course, we had our own sort of security level on top of it for authentication and everything, but it is pretty secure and as Elliott said, so like the code is not on the client anymore, so it's somewhere on the server. So if someone get access to your code, they don't get access to everything because a lot of it could be on the server.

0:15:15.9 Simone: Alright. Yeah. So thank you very much.

0:15:18.8 Greg: Thank you Zamzam.

0:15:21.0 Zamzam: Thank you.

[applause]
