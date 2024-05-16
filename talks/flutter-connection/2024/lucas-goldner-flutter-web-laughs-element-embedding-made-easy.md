---
slug: >-
  /talks/flutter-connection/2024/lucas-goldner-flutter-web-laughs-element-embedding-made-easy
date: '2024-04-24'
title: 'Flutter Web Laughs: Element Embedding Made Easy'
author:
  - Lucas Goldner
video: Hhq5PRD6c3I
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/Hhq5PRD6c3I.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: '2024'
allow_ads: false
---
### Lukas
Welcome and thanks for joining my talk today. My name is Lukas Goldner, and I'm going to talk about Flutter element embedding today. So first, let me introduce myself.

As I said, I'm called Lukas Goldner. That's my Twitter handle. I'm currently working as a Flutter engineer at a Japanese company called uTrust, German-Brazilian, 23 years old.

And I talk those languages. So if you want to talk in any of those, let's have a chat later. But enough about me.

Let's have a look at Flutter element embedding. So how many of you have heard about element embedding? Please raise a hand.

OK, not so many as I've expected, because unfortunately, this feature came out during a time where the introduction of Impeller was a big topic, and FFIgen came, and as well as Dart patterns and records and pattern matching. So that's why I think this feature got a bit left in the background, even though it's such a great feature. So that is why I'm going to present it today.

So element embedding, what does it do? So basically, element embedding allows you to take any Flutter app that supports web build and put it into your website directly, so no iframes or something like that. And some potential use cases for that are, for example, taking a vertical slice of your app and putting it on your landing page so users can try it out the app directly on the home page.

Another use case could be like a documentation page where you embed multiple Flutter screens, and then depending on the values on the website, you can re-render the layout directly and see the results. So I think that's also a nice feature there. And the best thing about this, it also allows you to take the app state and the website state and share it with each other so they can modify it from one side and through each other.

So this opens up a lot of potential. And the feature came out with 3.7 like one year ago, so hopefully most of you have migrated so you can use this awesome feature. So now we will have a look at some demos.

Rauf?

### Rauf
Hey, Lukas. How's it going? So I've released a new app. Can you check out the home page real quick, please?

### Lukas
I'm in a presentation.

### Rauf
Come on, please.

### Lukas
OK, I guess.

### Rauf
OK, thanks a lot.

### Lukas
OK, so Rauf just called and sent me this web page, so let's have a look. RedCounter, so this looks very interesting. Haven't seen an app like that before.

It has so many nice features. But I think we can take this a step further. So as I've said, we can take any app that supports WebBuild and put it into the website.

So let's do that. So the first thing that we're going to do is build our web version of the website. Then we will receive an output you probably can't see, but the important files here are the flutter.js and the main.js as well as the assets, of course. So the first thing we're going to do in our website is embed the flutter.js in a script text because that flutter.js handles the logic to load our actual app then. So when the first script is loaded, you can now use the second script and use the load event of the website to trigger, for example, loading the flutter app. And then we need to pass in the path to the main.js because that includes our app logic. And then we can select under the host element the element we want to embed the app into. So when that is done, it's not so much. We then create a diff, for example, with the same ID, of course, otherwise you won't see anything.

And yeah, this is it. So let's have a look again. Yeah, pretty nice, right?

You can see how it updates the counter. So that's the actual app now embedded in our website, but we can take it even a step further. So as I said, we can modify the app state using the website and in reverse.

So we're going to do that. And in order to do that, we need the Dart site to intact with the JavaScript code. So for that, we're going to use jsinterop.

The first thing we're going to do here is add the dependency, js. And the next thing really depends on your app. It could be pretty quick.

It could be also pretty slow, depending on your complexity and on your use case. In this case, we just have a simple counter app. So let's go to the important part.

In this case, we just have our home state app that we want to export to the website. So in order to do that, we use the js.export decorators and export firstly our widget, as well as all of the functions that we want to get, as well as, in this case, our account. So we can then access it on the front end.

When that is done, we also, in our init state, have the option to set properties using the set property that comes from the JS library. In this case, we bind it to an identifier, in this case, underscore app state, and export the current widget into there, the state of the widget. And there's also a call method function that allows you to call method on the front end, of course, using the same identifier.

And there's an empty array behind of that where you can pass like values inside and then read it from the front end. So this allows you to modify the website behavior, depending on the arguments, for example. And yeah, this is something you can do.

And one more thing that I want to explain before we go back to the front end is why are we using a stream controller for a simple counter app? The reason for that is we need to tell basically from the Flutter app to the website how to update it. So we have the stream controller in the Flutter app.

And every time an event, in this case, our increment function triggers, it sends an event to the website. And we have also this add handler function, which takes in a function, and this will be given from the front end. So every time we receive an event there, this function will be called.

But it will make more sense when we see the front end now. So the first thing is these underscore state set, which was the function that we declared. In this case, it's just logging something, but as I said, you can pass in some values and read them out in the front end then.

Inside of this, you have to be careful though with the values because it's not type safe. So depending on what you're doing, it could break maybe. So be careful with that.

After that, I'm getting my app state now from the window object of the browser with the identifier that I declared. So now we have the app state. I also added a value field on the website, which I'm getting here.

And created an update state function, which sets the value of the value field with the count of the app. So they're synchronous. And also this add handler function that I explained before, we are passing this update function into there.

So every time the stream controller gets an event, it triggers the update function again. And in the end, we have the increment button, which just is binded to the increment function. Then we set our IDs.

And when all of that is done, hopefully correctly, we get this. So now when I press the button inside of our app, we see the value field updates, which is awesome. Then we also have the button on the website, which when we press that, actually doesn't update this value field here directly.

It updates firstly the app. And the app has the stream controller. So it updates again the value field.

So we have got a nice cycle over there. And yeah, this was basically it, what you can do with Flutter element embedding. Regarding other frameworks, because most of us don't use only plain HTML websites, like I just described.

For Angular, there's a really nice documentation that you can check out an example and some repo, you will find it. But React is a different thing. I don't know why.

I tried all of the steps and somehow it didn't work. But there was a nice guide some user on GitHub created, where you have to edit the output of your Flutter app. So it matches for React.

I guess it depends on, it is because React handles what files you can access in this public folder, and you have to set the correct paths then. And so you need to do some adjustments, but this talk would be too long if I go through all of them. So I've created a medium article, you can check out in the repository.

And I've gone through all of the steps there and also created a script myself that you can just copy paste for yourself and run this so you don't have to go through all of these steps. So feel free to do that. And earlier someone asked me, hey, I don't want to build my website with like Flutter, but using Jasper, it's a library that allows you to create websites with Dart in a Flutter like way.

So you can use that. I hope you heard it. So you can try that out.

It's really nice library. And it also supports Flutter like element embedding. So this is also pretty nice.

And this was basically it, but actually one more thing. So those slides were made with Flutter, right? If we have a look, it's now running inside of a website.

So this entire Flutter slides app was embedded into a website as purpose of a demo. So you see how flawlessly it works. And the best part about this, it's not a simple website.

It's actually a React website. So. Yeah.

Yeah. You see it works. You just need some adjustments and yeah.

Thanks for listening. And this was it. Yeah, you just clap.

### Romain
Thanks a lot. Please come with me.

### Simone
All right. Since Alois had live demo, Lucas coded a live thing while Alois was talking to have a live demo as well. So no, I'm joking.

So do you, just in loading the questions, do you have any, do you know of any website already doing or using this in production?

### Lukas
Okay.

### Simone
I mean, not solution particularly, but this kind of an embedding and back and forth from JavaScript and Flutter.

### Lukas
I haven't encountered a website like this. If you have any example, please let me know. I want to look at them as well.

I used it in my own, I had a timer. I used it in my own website, like for documentation purposes, I embedded the actual app inside of the website. So you can test out directly as I send and see, but I don't know.

I can't think of any website right now.

### Romain
Another question that we have is, do you have in mind any use case where you wouldn't recommend it? Maybe because of performance or security issues?

### Lukas
Yeah, so it takes not, okay, it depends on your app, of course, how big it is. Then it could like take a little bit of time to load it. So if that's a requirement that you have, then you probably shouldn't use it.

Depends of course on your requirements. For example, with the React app, since I needed to update the output of the Flutter app, I couldn't use the minimization of Flutter when it builds the web app. So that's a case where it would be even slower and the client has to download a larger bundle then.

It depends.

### Simone
Would you recommend a React native app with a web view that contains React, that contains Flutter?

### Lukas
I mean, I had, so I had this, I built the website in React and I had, and it embedded my Flutter app and inside of the Flutter app, there was this red counter page demo, which was a completely separate site. And inside of that, I also embedded a Flutter app. So you can go crazy here.

### Romain
Flutterception. You told about the communication between JavaScript and Dart. Do you know about some packages like Python that we could have for meta channels to help us serialize the data and have a better communication or?

### Lukas
I haven't tried it out with Python. I have no idea if it supports that. It would be great though, but for now, I haven't seen anything like this aspect.

Would be nice though for type safety, of course.

### Simone
Well, what about the size of the final app? I mean, what's the final bundle that you download from the web?

### Lukas
Can we look at that in the browser? I don't know the exact size. We can check later whoever asked that.

All right.

### Simone
Awesome. So I think it's all for these questions.

### Romain
Thank you very much.