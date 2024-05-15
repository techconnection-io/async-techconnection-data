---
slug: >-
  /talks/flutter-connection/flutter-connection-2024/elaine-dias-batista-getting-started-with-genai-in-flutter-apps
date: "2024-04-24"
title: Getting Started with GenAI in Flutter Apps
author: Elaine Dias Batista
video: CujkphnSHOQ
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/CujkphnSHOQ.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: 2024
allow_ads: false
---

[Elaine]
So, yes, yes, I'm that person talking about AI on a tech conference. Hopefully you enjoy it. So let's get you started with Gen AI on Flutter apps.

So this is me. I'm Elaine. I work at Sfeir here in Paris. I'm a Flutter GDE. Right now my current role is Android development. And I am actually a former Google Assistant GDE.

Right now we are in the process of basically everything that was Google Assistant is going little by little, it's transitioning towards Gemini. So yes, so the Google Assistant GDE title is no longer, I think, for me. But we'll see what is coming up next.

Here are my socials on Twitter and on LinkedIn, if you'd like to follow me, catch up with me, don't hesitate. So let's get started with Gen AI for Flutter apps. And we are going to I'm going to be walking with you through four steps from easier to harder or more expert stuff.

And the very first step is actually a very naive one. I think everyone here in the room has already started, actually, with Gen AI. You start with Gen AI, actually, by having fun.

Right here I put a screenshot of the Gemini Android app and the ChatGPT Android app. And everyone can do this. Everyone can either download those apps or go to the web client, start asking funny questions, create stories, do funny prompts, asking random stuff.

So this is actually how you get started with it, is actually playing with it and seeing how it works. So behind those interactions, there are some key concepts that you have to know. So as I said, those are the clients, Android clients for ChatGPT and Gemini.

And what's going on is that when you're giving when you're typing a text and sending it to the client, you're actually entering what we call a prompt. A prompt is basically a comment, what you're asking the agent to do. And when you send it, what's going on behind the scenes is actually you're sending it to a server, either a Google server or OpenAI server, and it is on the server where inference takes place.

This inference, basically, if you start reading about GNI, you're going to be hearing that a lot. It's basically the predictions, how the models are predicting the next word of the generation. And so, yeah, so the server makes this prediction and gives back the response to the user and shows it on the screen.

And in order to do those predictions, we are actually those predictions are being run on models and those models for generative AI, they are called LLMs. Everything that you need to know is that they're very, very, very big models that have been trained with a lot of public data. So they're pretty huge. And on the clients that we use as an average user, not a paying customer, on ChatGPT clients, the model they're using is GPT 3.5, and on the Gemini clients is Gemini 1.0 Pro. So that was the first step, actually playing with it. So I call people who have actually started with GNI the commoners because basically everyone can do that. My mom can do that, my grandma can do that, children can do that.

So I guess I said I was guessing that everyone has already started playing with either Gemini or ChatGPT. So how many commoners who have actually don't be shy to show your hands who have actually played with some prompts, have used the ChatGPT on the web, so yes, and I actually cannot see you that much. Yeah, so basically everyone.

So congratulations. Step one is done for you. So let's take the second step.

Let's go further. And the second step is actually saying, okay, so I started asking funny questions, I started playing with this tool. So can I do more interesting stuff?

And as I said, I was talking about this concept of prompt, which is the comment that you give to the tool. And you can actually tinker with it a little bit to have more interesting answers. So for example, you can say, okay, act like a software programmer, act like a kindergarten teacher in order to model the way that to better how to say to better target your audience or have better answers, more suited to your audience through that.

The second example, the second screenshot you see on the middle, it is actually giving examples. So, okay, this is what I have began to write a list that is describing something for my app. Can you write more data like this?

And it is generating more examples that I can use, for example, for tests, for mocking data. So this is interesting. And on the right-hand side of the slide, you can see that maybe you are already using the APIs that those providers provide by actually using tools that you use every day that have integrated those kind of features, such as GitHub Copilot, Notion, Google Docs, and so on.

And so basically you're integrating those generative AI features in your workflow by actually using it to help you write faster code or write better emails and so on. The key concepts behind those concepts, the things that I just said, it's prompt engineering. Basically writing better prompts means mastering something that we call prompting engineering.

The input can be either a question, a task, something that is representing an entity, or something that is going to be completed. And you can add context, constraints, and you can give examples. On my screenshot right there in the middle, you said that I gave one example.

Again, on the literature about gen AI, sometimes you can see things that people are saying, okay, zero-shot prompt, one-shot prompt, or a few-shot prompt, sorry. Zero-shot is when you give zero examples, one-shot is when you give one example, and few-shot prompt is when you give, well, two, three examples. So right here, I did a one-shot prompt.

And then for the tools integration, just as a GitHub copilot, Notion, Google Docs, basically you're indirectly using the APIs. And other concepts that you may encounter when you're at this stage, at this step, is that you are writing a lot with, you are interacting a lot with agents. So you're maybe, I don't know, five, ten minutes after you started the conversation on the same screen, basically, sometimes it loses the context.

It starts forgetting what you said in the beginning. So this is what you call a context window. And those are some limitations of the models that we're going to see further.

So these people, I call them the workflowers. So who here has used a GitHub copilot, helpers on Google Drive, or something like that? So I think maybe 50%, something like that.

And I think it's falling. Okay. Should I...

No? Okay. I think I just...

I'm not... Maybe I... I can...

Okay. So, yeah, so maybe 50% of the room have already used or already has been doing this more advanced usage. So really interesting.

So let's go further, because, of course, we want to integrate it in our app. How do we do that? We use APIs, we use SDKs.

So for the purpose of this talk, I'm going to be talking about two of those. So always the same, Gemini and OpenAI. For Flutter, there is official package provided by Google, which is implementing the Gemini APIs.

For OpenAI, there isn't an official package. So I just put here for the reference the one that is the most popular. So when you're actually interacting with the APIs, you have to choose the models which you are going to be using for your app.

Here are the models for Gemini. I'm not going to go through all the details. The very first one is the most capable one.

And it is on preview right now. You cannot use it through the APIs. I should just take this off, because it's falling.

Or maybe just leave it here. And this one, it is the thing that really Google brags about. It is the one million number right there, because remember when I said that at some point the AI starts forgetting what you're saying, this is due to the context window and is directly correlated to the input token limit that we see right here.

I didn't check Lama 3, who just came out, but this one is the one that provides the biggest context window, the biggest input token limit. So basically it is the one that is going to be able to remember the most tokens. The capabilities, so code generation, text generation, problem solving, and so on.

But the most popular ones that we are seeing today are either Gemini Pro, which is generating text via text, so you do a text comment and it generates text, and Gemini ProVision, which takes text and image and generates text. And then there are other models that are less known, like the embeddings one. Embeddings, very important notion as well, is basically you transform strings, which are transformed characters and words, into vectors, so you can compare them and do similarity and search.

And then you have the AQA model, which is specialized in Q&A, basically. Very quick look at the Gemini API, I'm not going to get into detail, but right here we see the main function that we have, which is generate content. Does this work?

The pointer? I shouldn't be doing this. I think I'm maybe breaking everything.

Yes, here. Oh, can you see it? Yes.

So generate content, which is basically taking your prompt, the prompt that you have given with your text, and then you can see that there are other parameters that you can adjust, such as safety settings, so the model, it is going to be like censored, there's not going to be saying bad stuff, harassing stuff and so on, hate speech, and then you can see there's another parameter right here, which is a generation config, and has some things which you can tailor to do your request.

So basically there's not so much going on there, because you can see what's going on is that you're making a request, you're making an HTTP call, that's pretty much it. And OpenAI, what about OpenAI, the OpenAI models? So, of course, GPT-4, GPT-3.5, which is the one that regular people have access to, through a chat GPT. Biggest difference is that OpenAI provides Dolly, which is generating image through text. And then another difference is that OpenAI puts their text to speech and speech recognition models, with the other ones that are considered generative AI, those ones, they do exist for Google, but they are not considered GMAI models, they are elsewhere in the Google ecosystem, but that's fine, they also have text embedding. And another difference is that for moderation, so basically for censoring hate speech and so on, you have to use another model, so you have to make two calls, you have to make a text moderation, if you want to censor those data, and then other regular text generation models right there.

And same thing for the API, so here I show you the parameters that you can send, and then for the completion, for the completion API, sorry, and then the moderation. What you can get for the moderation. So what have you seen here, what are the key concepts that we have just seen?

We saw the concept of multimodality, which is basically using not only text, because a lot, a lot of people only talk about LLMs and text generation and so on, but we have more and more image generation, and we can also put image as an input. So this is what we called multimodality. So yeah, so we also learned that each model has its purpose, or several purposes, but they can be specialized.

And you saw the concept of token. Token is a very, very important concept. Basically, a token corresponds roughly to four characters, so it is important to know that.

All of those APIs, well, Gemini API is still free until May 1st, I think, so if you want to play with the Gemini API for free, you have one week to do so. Afterwards, it's going to be a paid service, OpenAI is already paid, and the way they charge you is by, of course, API requests, such as every paying API do, but also the token utilization, so you should really control the token utilization. This is why I put here that you can actually limit your requests.

You can, if you take a look, you can send max tokens here, for example, for OpenAI. And another interesting configuration that it can do is the temperature. The temperature basically means that, sorry, it's a configuration that varies from zero to one, one being, you're actually saying to the model, so be very creative and be very random, so it's going to be really good for creating stories and stuff like that, but not very good for actually answering to factual questions, and if you put zero, it's going to be less creative, it will choose the most likely token that is going to be the next word. One thing that is important to notice, to note here, is that when you put zero, it doesn't mean that your AI is not going to hallucinate. Hallucinations is a really big problem that there is going on with generative AI, when your AI is basically saying something that really doesn't make sense.

This is called hallucination, and there are technical solutions for that that we are going to see. So those who have here played with the APIs, OpenAI API, Gemini API, no? Oh, yeah, yeah, yeah, maybe five per cent, maybe?

Okay, cool. So I don't know when you used the APIs, if you took a look at the warning that Google put here, so people basically who have played with the APIs, I call them the prototypers, so we have maybe five or ten per cent of the room who have done so. Google encourages you to use it, to play with it, to see what's possible, to, well, basically already put it in an app, get it up and running, see what you can do, have ideas, but it is not recommended to do a direct call to Gemini on a client, so this should be done on the server side, because as you can see, the models are very, very big, and billing can get very, very high if you don't protect your API keys, and I guess most of you know about security on mobile, it is very, very easy to get it, it is actually impossible to hide a client API key on a mobile device, so this should be done on the server side.

Nevertheless, there have been a lot of people who have tried out the Gemini API, and I wanted to show some of them to you so you can have some ideas what was done on the Flutter community, and the very first one was done by Manguidas, who is a Flutter GD, he did a scavenger hunt, and on his app, he is basically generating items, either located at home or outside, and he's giving a prompt and saying, OK, give me a JSON file that is containing items with this model right here, and then he's calling the generate API end point, and then using it to generate the things that you have to find, and then what is really cool is that you take a picture of the object that you find, and then you send another API call to validate, and so you're saying, you're asking the Gemini if this is a valid image or not, and then you get your points or not, and he's actually using Vertex AI, it ends on the same Vertex AI, it's basically a workaround to use Gemini APIs in Europe. Another one is done by Daria Orlova, she has an app that is giving information about cruelty-free brands, and then she integrated prompts to basically give a cruelty-free status analysis of some brand with some criteria, so really interesting as well, and this one right here is giving this prompt and an image, which is actually the photo of the product.

Really interesting stuff as well. This one is giving an image, which is the photo of ingredients, and then they're saying, OK, you are a very experienced diet planner, and please give me a recipe with the ingredients that you find on this photo. So really cool stuff as well, and the last one, I think, is storage generation, so pretty cute as well for children and other kinds as well.

So it takes a photo from your phone that you have already taken, some parameters, and then the first part, basically, it gets information from the photo, so a teddy bear, a little car, something like that, some toy, and then it creates a story with the things that it has found on the photo and the parameters that you have set. So pretty cute as well. All of these examples are available on GitHub, you should check them out.

So, as I said, it is not recommended to call the Gemini API or the OpenAI API directly, so there is actually, of course, maybe you're seeing where this is going, I'm going to be talking about the cloud just afterwards, but there's an in-between solution, which is very suited, I think, and very good for mobile developers as well, it's actually Firebase, because Firebase, it is basically a service that you can use where you're not directly calling Gemini, you're going through Firebase, and Firebase is managing those calls, so Firebase provides two extensions, one for JetBot and one for multi-modal tasks. If I'm not mistaken, you have to, well, Gemini API is free to use until May 1st, until next week, but in order to use those Firebase extensions, you have to get into the Blaze plan, and it is actually, I think it is costing money right now, so not so much popularity right there, but Ranuka did a worksheet generator by using the Firebase extensions, which is really cool, and as you can see, the code is a little bit different, of course, because you're not calling the Gemini API directly, and you're basically calling, interacting with the Firebase API, so pretty cool stuff. And I call them the Sparker, because the mascot for Firebase are Sparky, it's called Sparky, and I don't know if anyone here has played with the Firebase extension that is doing Gemini calls.

Zero? Oh, one, one person, oh, cool, and so, yes, so let's go to the fourth step, the real deal. And you have two options to go further and really get, like, expert solutions on your application.

The very first one I'm just showing you here what cloud services have to offer you regarding AI services. You have Azure, Amazon, and Google Cloud, a bunch of stuff. If you're interested in going further, please do.

They're really, really being developed a lot. They change all the time. They get better and better.

So this is where the real AI code should be, Gen AI code should be running on. So those are the cloud riders. I don't know if there are any cloud GCP, Amazon, or Azure, yay, okay, cool, people here, yes, some of you are.

So there's another option, because either you go to the cloud or you don't go to the cloud, you stay on the device. It's actually going local, running those models locally. I'm going to confess something right here.

I don't have a lot of time left. I was expecting to find maybe, okay, Gemini Nano, TensorFlow, stuff that you heard about. There's so much stuff going on.

People finding solutions to run locally. I'm going to go really fast through them, because it's not that important. It's just so you know that there's a lot going on on that space.

So I'm just going to go through the slides and mention them to you. If you're interested in local solutions, please investigate more, because it's a really, really nice ecosystem that's really dynamic and it's really being really developed. The first one, actually, this one was on my mind as well, MediaPipe.

MediaPipe is Google solutions. You have Google solutions to run machine learning and AI solutions on the device. And you have image generation and LLM inference.

They are only available for Android, iOS, web, the basic SDKs. But Sasha Alexander Denisov did a package that is using MediaPipe, and I have actually tried it. So it is using Gemma.

Gemma, which is the open source model from Google. And it is through MediaPipe you can run locally. You can run the Gemma model locally.

Keras NLP, TensorFlow Lite, a lot of resources there as well to run LLMs on Android. LangChain. LangChain is huge on the GNI world.

It is a framework basically to give better predictions by adding documents, for example, by allowing the user to switch models. And there's some developers that are really, really active. There is a Flutter package that is implementing LangChain.

And there are a lot of people. Examples of people who are using LangChain. I'm not going to get into detail.

You can take a look at the slides afterwards. But so much stuff going on. Llama and Ollama.

Llama C++ is an inference engine. So basically for running LLMs on the device. A bunch of packages as well.

And I give you some examples here. So basically you have MediaPipe, Keras, TensorFlow, LangChain, Llama and others. And it is a really, really dynamic world there.

So to end, so this is a summary of what we have seen today. All the four steps with the two options. So basically discovering, getting better at prompting, calling the APIs locally through the official SDKs and APIs.

Go using Firebase extensions. Why not? Going to the cloud if you want to.

So this is another world completely. Or staying on device and maybe using one or several. This is not extensive at all.

Those are the ones that I have found. But and behind all of those, you have to, it's really, you have to get into the definitions and the theory that is behind all of those stuff. But it's really, really exciting.

And I'm really looking forward to exploring that more. So that's it for me. Thank you.

[Romain]
Thanks.

[Simone]
We won't have much time because for obvious reasons, we are running a bit late. So we're going to be quite fast. But I assume there are lots of super interesting questions.

So if you stick at the bar, I think there are lots of people wanting to talk with you. I have some questions myself, by the way, which are basically, so we saw so many, so much stuff that could run on a physical device. Is there a recommended device on iOS or Android by Google to run Gemma?

[Elaine]
I haven't actually talked about Gemini Nano. Gemini Nano is under preview right now. It is the way to run Gemini officially on Android.

It's tightly, it is tightly coupled with the system with Android. And as far as I know today, it's only available for a Pixel 8 Pro and Galaxy S24 devices because it is running, it's actually a physical problem. It's running on TPUs or, yes.

[Simone]
And just linking a question that just arrived. This is for LLM and still for locally, do you have any like a prompt to image solution that they could run on an Android device?

[Elaine]
I only saw text-to-text.

[Simone]
Okay.

[Elaine]
I only saw text-to-text. Yeah, for now. But maybe there exists.

[Romain]
Yeah, it will. So much stuff. Yes.

Do you know if there are some legal restrictions for these tools usage, either from the country the app is targeted for, for example, or from Apple or Google? Are there some restrictions?

[Elaine]
Right now, unfortunately, we cannot use Gemini APIs in Europe. I hope it is only, yes, a legal issue that they have to figure out. But it should be available to everyone.

So I'm not aware. Maybe there are some restrictions. But the only restriction that I know is this one.

[Romain]
Is it based on where the user is with its phone or? Yes.

[Elaine]
It detects if you are in Europe, you have an European IP and you're using some application that is implemented in the Gemini API, it will say invalid region, something like that.

[Romain]
Okay. So it's based on the IP?

[Elaine]
Yes.

[Romain]
So if we use some tools to change the IPs?

[Elaine]
Yes. In order to create the, as a developer, in order to create the key, the API key, you have to use the same tool. Okay.

[Simone]
I think we have time for our last question. When do you think you'll see a Gen AI capable enough to answer with, I guess, a flutter to visualize answers? Like having a Gen AI that is able to produce and run, of course.

Yeah. Because in a way- It depends on the app.

[Elaine]
If it's an app, there's only a show in the button, it's available today.

[Simone]
Yeah, exactly. Because in a way, with OpenAI, to put more context. So with OpenAI, we already have an interpreter, which is based on Python.

Do you know any initiative of having an interpreter based on Dart or?

[Elaine]
I don't know. No, I don't know. But maybe one day.

But I don't think it's going to be perfect. I don't know. Well, this is a very, very long discussion that we can have.

But yes, for real apps, I think that those tools, they can help us. Yeah, sure. They're never going to be completely- They are not going to replace us completely.

[Simone]
I mean, so far.

[Elaine]
We'll see.

[Simone]
All right. Thank you very much, indeed.

[Elaine]
Thank you.
