---
slug: >-
  /talks/react-connection/2024/flora-soussand-robin-carrez-a11yinyerface-the-platform-that-puts-us-in-our-users-shoes
date: '2024-04-22'
title: 'A11YInYerFace: The Platform That Puts Us in Our Users'' Shoes'
author:
  - Flora Soussand
  - Robin Carrez
video: b4nZ5v-XQbI
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/b4nZ5v-XQbI.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
### Flora
We both work at Teodo, which is a firm that aims at answering complex situations and answering them with smart solutions. We are both part of a team that gathers every week to discuss accessibility subjects. And one of the issues we try to tackle is to try and understand how we can help developers understand what an accessibility issue is.

So as I was saying, we're trying to tackle accessibility issues, and today the issue that we wanted to tackle is to help developers understand what an accessibility issue is. And especially today, we're going to discuss this issue by following the stories of four different people. Claudia, Chris, Pavel, and Simon each have their own history and their own problems, and they each present with one disability, and so what we're going to do today is to understand what they're going through when navigating the web.

But this is not just four people that we are talking about. Actually, we're talking about quite a large part of the population. The World Health Organization considers that at least 16% of the population presents one disability.

16%. It's 15 people in this very room, so we consider this number is quite huge and should not be negligated when developing an app, especially since it is increasing due to aging in population. But it should also be noted that accessibility is not just about permanent disabilities.

What first comes to mind when thinking about accessibility is probably wheelchairs or walking sticks. But it should be noted that accessibility can also be about situations. I will use two examples to illustrate what I'm saying.

First example would be you after this talk wanting to enjoy sun and wanting to take a coffee outside on the T-Rex, but you need coffee outside and you also need to read your emails because there's a really important email that you need to go through. But there's so much sun that you can have troubles actually reading your emails. So you will need the website to navigate on to be well-thought for you and, for example, you will need the contrast to be well-managed in order to actually be able to read your emails.

So the second example I will use will be you this winter. You went skiing and unfortunately you broke an arm. A few weeks later, you go to the doctor and you need to take an appointment to check on your arm, but to get this appointment, you will need the app to be well-thought for you because with only one arm, navigating is not so easy.

So once again, you will need accessibility to have been thought for you.

### Romain
So, with this in mind, we wanted to help everyone understand how some users could see our applications. To do so, we created a small application called Ally in your face. So what is it?

It's a small marketplace where you have a goal, the goal is to pick the right ingredients to make an apple pie. So, on this app, you will see some disability simulations and what you should not do on your applications. We build these tools using React, Material, UI as component library, and Jotai as a store manager.

So, let's go back to our four personas. First, Claudia. Claudia is a 54-year-old social worker and she is colour-blind.

Colour-blind touches four per cent of the world's population, and there are multiple kinds of colour-blindness, some don't see green, some don't see blue, et cetera. So, this is our application. Yes, everything looks a lot greenish.

It can be difficult to pick the apple between all these images. And why? Because only images give the information of what each item is.

To help Claudia, we should make sure that it's not only an image that gives this information, maybe add some text under the image, and we should make sure that the contrasts are great on our application, so she can use the app as everyone else will do. Now, let's check on Chris. Chris is 53 years old and suffers from Parkinson's.

Parkinson's is one person in a million, in a thousand, sorry, but it's not the only mobility disease that exists. For example, arthritis is more and more common due to people ageing, and it can make it difficult for users to use our application. So, Chris wants to pick some fruit for his cake.

But, here, you have to imagine it. You have your mouse, and every time you move it, you are checking, so it makes it really difficult to click on a small icon like this. To help Chris, we should make sure that our icons are bigger, and help him, when he uses the zoom option, make sure that every element grows bigger too.

### Flora
Okay. Now, we're going to focus on Pavel. Pavel is 24 years old.

He studies chemistry. But he also presents with attention deficits, like 4% of the population. What Pavel experiences is that he might have trouble focusing on things, and really sticking to one information.

It might be similar to what anyone experiences when they're really tired, or when they have a headache. So, what does the experience look like for Pavel? Here, we tried and simulate what Pavel goes through.

He wants to select an egg, but it gets quite complicated for him, because he starts to go elsewhere, and he has some troubles actually focusing on the egg here. So, once again, you need to help Pavel by keeping clear designs, giving him just the information he needs. Last person that we're going to focus on today will be Simone.

Simone is 41, and she's an office manager. But she also presents with dyslexia. It's not so easy to estimate how many people in the population have dyslexia, but some studies, like one by Yale, considers it's up to 20% of the population.

So, this is quite a huge part of the population that we want to help here, and what do they see exactly? Here, we see that for Simone, the letters are mixing, and she has some troubles actually reading the contents. She wants to validate her card to make sure that she has everything she needs to make her Apple Pay, but it can get quite complicated for her.

So, here, if you want to help Simone, you have to keep a clear design, and why not adding some images to help her?

### Romain
So, now, we've seen it on a design website that helps you understand your users, but what would be best is if we can try it on our own applications that we are working on. To do so, you have multiple plugins that exist. For example, we will talk about Web Disability Simulator.

This plugin allows you to simulate some sight diseases, like color blindness, and also mobility diseases. So, what does it look like? Here, this is one of the first slides that we showed on our presentation, and we will simulate, like we said earlier, if we have a lot of sun on our screen.

Okay, yeah. As you can see, we lose a lot of information. Here, it just colors, but if we add some text on this, we can't read it anymore.

So, now that we have seen how we can check in on our applications, how can I improve my website, really? To do so, you have some tools that exist, too. For example, Axe or Wave that can give you an activity score, and we decided to focus on Lighthouse.

Why Lighthouse? Because I think most of you know what it is. It's already integrated in all Chromium browsers' dev tools, so it's really easy to use.

Here, we tried it on the right connection home page. As you can see, it has a pretty high score in accessibility, but what is really interesting is that we have some guidelines on how to improve our application. For example, on this web page, we should have a better contrast on the tickets button, because here, white on a blue button, it's not really great to check what is it.

So, now, we hope that we helped you understand why accessibility matters, and how you can try it and improve it on your applications. Also, if you want to use your application to show it to your friends or co-workers, to show how you can have some problems using a website, feel free to do it. Thanks for everyone.

### Christophe
Thank you. Please come in. So, we'll try to pick two good questions, and then you can feast.

I think, and then we feast, is the production company behind Hot Ones, isn't it? I think it is. Everybody knows.

It's, like, weird. You know the production company behind Hot Ones better than you know accessibility problems. It's, like, weird.

Got some good questions coming in?

### Romain L.
Yeah, I have one by myself. How do you engage developers to work on accessibility issues?

### Romain
This is kind of the problem right now. It's very difficult. It's part of why we created this application, to show them why it's really important.

And right now, we are trying to understand why they are not doing it, and to give them tools and help them to make it one of their priorities when they are working on their applications. But right now, it's really, really difficult to do so. And we have no solutions yet, honestly.

Just talking to them and explaining why it's important, and trying to understand why they don't think about it. We are just at the first step of what we want to do. That is, everyone thinks of accessibility all the time, and develops websites directly, respecting the guidelines that we can see on a lot of governmental documentation, for example, on how you should do accessibility on your websites.

### Christophe
It actually doesn't take more work. Sometimes it takes less work, actually, because it forces you to make decisions that happen to be easier to implement. There's a side question to this.

What would you say are some of the biggest benefits besides legal compliance, right? But the actual benefits, even sometimes to developers themselves, to bringing accessibility as a core part of the process?

### Flora
To me, it's a question of design. When thinking about accessibility, sometimes you might end up by making anyone's experiences better, because when you try to think about accessibility, what you think of, really, is your users and what they're going to do. I think that if you put some energy on accessibility, you just put some energy in the user journey in global.

### Christophe
Better design, basically. And it's like in real life, right? Accessibility for one target group usually benefits a lot more than that.

Just like in real life with curbs and audio feedback for blind people or whatever. It's for wheelchairs, and then it's for strollers, and then it's for people with crutches and whatever. It just helps a lot more.

The blast radius is a lot better than we usually think. Thank you very much. Please, please, please go talk to them about accessibility.

It's a lot easier than you think. And it's not a feature, it's a process. Thank you very much, Flora and Robin.