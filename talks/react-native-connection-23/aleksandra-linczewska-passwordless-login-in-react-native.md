---
slug: >-
  /talks/react-native-connection-23/aleksandra-linczewska-passwordless-login-in-react-native
date: 2023-06-01T00:00:00.000Z
title: Passwordless Login in React Native
author: Aleksandra Linczewska
video: CocLa_PCHsg
thumbnail: https:/async-assets.s3.eu-west-3.amazonaws.com/thumbnails/CocLa_PCHsg.jpg
slides: >-
  https:/async-assets.s3.eu-west-3.amazonaws.com/slides/talks/react-native-connection-23/aleksandra-linczewska-passwordless-login-in-react-native/slides.pdf
tags: []
year: 2023
conference: react-native-connection
edition: 2023
allow_ads: false
---

A few words about myself.

So this is the first time I'm giving a talk to real people. So I hope it goes well, and I hope you like it.

My full name is Alexandra.

I often go by my shorthand Polish name, Ola.

I've been a software developer for the last 11 years and I've spent the last year and a half, two years at Callstack, which is a really great company. Maybe you've heard about the conference we're organizing in September, React Native EU.

Maybe we'll see you all there.

I have a pretty big household. I have two kids, lots of animals, and I'm always writing at least one book all the time.

And two of them got actually published.

One of them is on theory of literature and the other one is on state management in React Native because apparently I lead a double life.

Thank you.

You can find me on Twitter, on Bluesky, on GitHub.

Let's dive right in.

I've divided this talk into three parts:

1. First we'll talk about the question why you should even care about passwords.
2. And we'll look a little bit at what are the options right now
3. and the solution, which are the pass keys.

So first of all, why should you care about passwords?

Here are three really good reasons.

Hackers have published as many as 555 million stolen passwords on the dark web since 2017.

And that's a statistic from three years ago.

So you can imagine the number is really much bigger now. 80% of hacking incidents are caused by stolen and reused login information. And we are all guilty of it.

Let's be honest. We all reuse our passwords everywhere.

And the third statistic, every 39 seconds, there are hacking attacks using scripts that try to guess usernames and passwords.

So how about your company and the app that you're working on?

How sure are you that your app is not going to get breached?

Maybe you're thinking, OK, but the app problem working on that's just like some small thing, maybe I don't really have to care about it, I don't work for a bank, you know, whatever. But you have to remember that your users do reuse passwords everywhere. So your small app gets breached. The app is not really hurt much, right? It still works. But the passwords of the users are out there on the dark web and the hackers are really good at guessing passwords even if your users are using maybe like password one and password two in their bank or for their email account, hackers will just guess all of that stuff. So what is the current status? What are the options available to us right now? Well, the first option, of course, are passwords.

The problem with passwords is that they have to be unique but also memorable. I remember I thought I was super smart when I figured I'm going to use the same core password and then the second part of my password for every website is the name of that website.

I thought I was super smart.

I was listening to a security podcast where a hacker was explaining that he laughs at the face of such smart passwords.

So then you have email magic links. Really great security wise.

Unfortunately, we live in a world where there's a lot of phishing scams, emails go to the spam folder, and users have learned not to trust their emails really that much.

What else is there?

We have multi-factor authentication.

Really great for security, right?

You have your authenticator apps, your tokens, soft tokens, hard tokens, everything you want. And they are usually used in big corporations. And they are usually also pretty difficult to set up.

And you don't want your user to get into your app and then see that they need to go through five or four different steps just to sign up and use the app, right?

And then we have passkeys, which are secure, unique, and easy for the end user.

So let's look a little bit more at those passkeys.

When I started planning this talk, Apple have published their passkey API.

Since then, we have also Android Credential Manager.

So that changed the shape of this talk.

And a fancy description of passkeys is that they give you a simple and secure way to sign in without passwords by relying on biometrics identify when you sign in to supporting websites and apps. That sounds very fancy.

Let's take a look at what the user flow actually looks like. So the user gets into your app, they want to sign up or sign in, they put in a username. If they don't already have an account, they are presented with a question if they want to create a new account and then they are are presented with the option to save a passkey.

At this moment, you have an overlay, which tells you your username, and then you click Next.

The next part is not screen shot here, because the next part is just that you use your biometrics on your phone.

And that's it, as much as we talk about the user-facing flow.

Now, let's talk about the code.

So user-facing part is great for the user. They just put in a username, they put their finger on their phone or maybe they scan their face if they use iPhones.

Unfortunately, for the developer, it's going to be a little bit more complicated.

So when you use like a regular authentication flow, you get your username, your password, you send it to your server, the server does all the magic stuff and then tells you, okay, the user is logged in.

In the case of fast keys, there's a little more back and forth.

So we start by contacting the server, which needs to be correctly configured with this very great standard called Fido, and I will talk a little bit more about that later.

The server responds with a challenge that's a base 64 encoded string.

So we get our answer from the server, and then we do the whole pass key magic.

In this code example I'm using an open source library called React Native KeePass and that's pretty much this one line of code you're calling `passkey.register`.

At this moment in the app your user will be presented with the overlay and they will be able to log in with either biometrics or with their face.

We are returned from the -- we receive data that we have to pass back to our server, to another route, and to confirm that the user is logged in.

So you can see that the number of steps is bigger than for the normal authentication flow.

Where can we find pass keys?

So there are drop-in solutions, especially for websites.

For the websites, there's a whole choice of stuff.

As for the mobile scene, we have Auth0 and they are working on the feature to have passkeys on mobile.

They already have a video presenting that you can enable passkeys in your app, but it's not available.

Maybe it's available in some higher paying tiers.

I'm not paying them, so I don't know.

You can use open source solutions.

So far I found one, react-native-passkey. And this is a React Native library that uses Apple PassKey and Android Credential Manager.

Or you can work out your own solution.

As I've said, we have those two native solutions that are very well documented.

So if you have the courage and the time to do something new and better maybe than the existing library, then I think that would be great.

A couple of things to keep in mind.

I mentioned FIDO before. FIDO is an association. It's like a complicated name. FIDO Alliance is an open source industry association. They set the standards for what your -- for how secure your backend server needs to be in order to work with Passkeys. They have a great website where they explain all of this in detail.

And there are a lot of libraries that you can use for your backend to make them FIDO compliant.

For example, for Node.js backends, there's FIDO2lib that you can use that also has great documentation that will help you out to get your backend in shape.

The second point is setup.

There are, unfortunately, additional steps for the setup.

If you want passkeys to work with your app, you will need to set up associated domains.

So that's just one more thing that the developer needs to do.

So these are the bad parts.

Now the good part is that you can use the same passkey across different devices.

That's like a game changer because your user can take either, you know, a phone from whatever phone they want to take and they can log in to your app with their username and their biometrics.

So that's great.

They also can log in into websites.

I've seen flows where if you're on a computer that doesn't support fingerprinting, you're presented with a QR code, you scan the QR code and you still log in using your phone.

So let's take a quick look at links to demos.

Because there are a lot of web demos out there that you can check out, you can see what the flow really looks like.

Shopify includes passkeys in shop pay, so they have published a bunch of articles on the topic.

And the open source library I've mentioned before, React native passkeys has an example app that you also can take a look at.

And so I really hope I got you excited about passkeys because I really believe they are the future, even if you're working on a small app or a bigger app.

We can imagine if you're working on a bigger app, you probably have DevOps engineers who will make sure that your database is really safe and that all the passwords are coded and encrypted and stuff like that.

If you work on a small app, you probably don't have those resources.

So pass keys are really a great way to make sure that all your users are safe.

And that's it for me.

Thank you.

[APPLAUSE]

Thank you very much.

Thank you.
