---
slug: >-
  /talks/flutter-connection/flutter-connection-2024/alois-deniel-server-driven-ui-with-flutter
date: '2024-04-24'
title: Server-Driven UI with Flutter
author:
  - Aloïs Deniel
video: O15L2zduOKM
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/O15L2zduOKM.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: flutter-connection-2024
allow_ads: false
---
[Aloïs]
So, yeah, my talk today is about server-driven UI with Flutter. Before diving into the topic, I want to present myself. So I'm French.

I'm based in Brittany, in the west of France. I'm also a Flutter GD. I've been Flutter G for a couple of years now, mainly because of my open source contributions.

I have far too many repositories now. So you can go check them out directly on GitHub. I work for ClickUp, which is a productivity app.

We are working on the mobile app with a bunch of crazy people, amazing team. And I'm a father, so I have far less spare time now. That's why I'm a bit less active now on the social medias.

But I'm trying to catch up now that she's aging a bit. Okay, so why am I talking about server-driven development? The root of all this thinking was at ClickUp, we have a need to build really dynamic dashboards like this one.

We want to have really customizable cards that each user could add up to its own experience. We want also to provide different cards. We want to update them really frequently.

As you may know, it's a pretty difficult task on mobile. You have to release and all that stuff. It's a really heavy process to push a new release on the store.

You have to pass a few tests. It can take up to several days until your update is finally there in the end of users. For small minor updates, like a few refinements of the UI, like that, it might feel a bit weird to having to wait so much time just for that.

So that's why I was studying server-driven UI at that time. It was a couple of months ago. And I found a few solutions.

But before presenting how we could do that with Flutter, I want to come back to the early 2000s, because at that time, all of the websites you were navigating were, in fact, server-driven. Everything was a single HTML document that was built on the server and simply sent to your browser and rendered just as it is, just a tree of UI components. Then we saw many other solutions, more evolved framework, come like React, mainly the most popular one, but many others.

And it changed the paradigm quite a bit. And from that time, we would optimize a bit things by sending just raw data through APIs from the server. So we would send JSON data, and we would let the browser have the responsibility to build the HTML tree and to render it.

So we wouldn't have many logic for the UI on the server, just sending the raw data. We need to build the UI on the client side. And this was really handy for mobile apps as well.

We could just reuse this data and use a different technology to render the view in a different way. So with widgets in the case of Flutter. So my conclusion is that server-driven UI is really easy on the web, because it was designed to be in the beginning.

So it's really easy to, still today, to render server-side UI by sending a bunch of HTML over the network and just render it through the built-in browser APIs. And we still have a few solutions in the web, like HTMX, which is quite popular nowadays, and it's exactly that, going back to the roots of what server-driven development was. The question is, is server-driven development really interesting for mobile?

Because the way mobile frameworks were designed was client-side, mainly for performance reasons. Because when you are on a mobile app, you generally have limited connections, so you need offline apps. You also have limited resources, mainly with lower-end devices.

So does it really make sense to have server-side rendering on mobile as well? I think yes, because of obviously the reason why I started studying this whole thing. So you avoid the whole process of publishing to the store, which is quite painful.

Also it allows you to build really adaptive UIs for users. If you want a different screen for each one of your users, and you need to anticipate with the built-in package, your built-in release, it can be really difficult. Last reason maybe, it's more difficult to exploit an API that sends UI than an API that just sends raw JSON data.

So that might also help in that way. Many popular apps are using server-side rendering. You might have seen Airbnb dynamic UIs.

Also Google Gemini recently, all the dynamic UIs for the cards are using server-side rendering as well. But there are many, many, many. Now the question is, how could we achieve exactly that with Flutter?

Because the issue with Flutter and all of the mobile framework basically is that it hasn't been designed to send UI over the network. So we need a built-in, we need a document representation for a UI in Flutter. Fortunately, Flutter is just a widget tree.

So if we find a way to serialize a widget tree in bytes, we could send this to the mobile apps and it would be easy to deserialize it and just push the widget tree in our widget tree. And this exists. It's in fact RFW for Remote Flutter Widgets.

It's a package which is available on pub. It's an official package built by the Flutter team, which is interesting. And its main purpose is exactly that.

It's to replace this intermediate representation that we can send to a mobile app. And it contains three main parts. So the main one is a specific language named RFWTXT, which is a different language than Dart, but also really different from JSON.

So it's a specific language to describe widget tree. It's also a way to serialize it into a binary format that we can send. It's a lot more efficient than JSON, for example, because it's not text-based, it's binary.

And finally, it's a way to deserialize these bytes and to rebuild a widget tree out of these bytes. So we have now our solution. We could send widgets to Flutter.

How does it work? It's pretty simple. You have a parse library file function, which allows you to generate an instance of a remote widget library that we could then encode with the encode library blob.

And we can send these bytes over the network. So this is RFWTXT language. And as you can see, it looks like Dart, but it's still different.

For example, the text direction is a string. The color is directly an int value. So we can see similarities, but it's not exactly the same as Dart.

On the app side, it's pretty simple. You load the bytes with the dedicated method, and you use a remote widget to inject your remote widget, and it's rendered as a regular widget in Flutter. It's a lot more.

I won't enter into every detail about RFW. But it's also a way to do templating, for example, so you can bind data to your widget to build it differently without requesting a new widget over the network. So it could be useful in that way.

You can also bind custom widgets into your remote widget and use special binding to send custom widgets over the network, this kind of stuff. So you can check it out on the official documentation if you want more details about this. I'll do a quick demo.

So it's a pretty simple one. Basically, just what I have shown a couple of seconds ago. So I declare...

Sorry. This is the server side. So I declare my custom widget here.

The interesting part is that I'm extracting a query parameter out of the URL, so the name, and I build my custom widget with this custom parameter here. And then I'm parsing the library and coding it and sending it over the network. On the Flutter side, same stuff.

Just creating a runtime by creating a request and getting the content from the API URL and decoding it, rendering it with the remote widget. That's it. And boom.

We have our widget, which was declared on the server. So pretty cool. And if I change the URL, for example, here...

If I put Paris here, and I'm restarting the app, then my widget is updated. Everything has been done on the backend here. Including the styling and so on.

So really cool stuff. But I found that it's not the best solution. Because of...

Mainly because of this language, which is really specific. And also it's a raw string, which makes it not really maintainable in my own point of view. And also it's quite similar to Dart, but also very different.

So you have to learn pretty much a new language, a new way to build your UI. And to me, it's not realistic to use it in production until we have proper tools to create these widgets. Like linters or formatters and all the IDE tooling we need for production-ready stuff.

But there's a way. I'm sure we could do it differently and use real widgets on the server. And that's what Swap is.

It's my own repository. I tried experimenting with it to fill the gap and just make RFW more usable. So the main purpose of Swap is to be able to write Flutter widgets the same way on the server that we would on the Flutter side.

So you use the exact same APIs to build your widgets and you can send them through the network. They are serialized in the RFW binary format and deserialized with the Flutter RFW package on the Flutter side. And it's just like Flutter.

So you would be able to copy this code and paste it into your Flutter app when you're ready and it would be rendered the exact same way in your release. It also adds a few more widgets to add interactivity to your remote widget. For example, if you want to tap on a button to regenerate a new dynamic widget out of this tab, you would be able to do this with Swap.

I will show you this in a quick demo as well. So I'm going to switch to my dedicated demo. So same, we have a server app.

I will start with that. We are just calling the widget method, which converts it to a handler for the server and we are sending a widget, a regular widget. This widget is just like any widget in the Flutter environment.

So it's just a status widget. We can get a parameter and we can, by using an inherited widget, and then we are switching from one page or another. And everything is just regular Flutter widgets.

We use safe area, column, container. And I mean, it's the same thing. And from the client side, it's pretty simple as well.

If I go here, I will switch back to my Swap app instead of the previous one. We load it. So I put a button.

Yes. And that's the widget that is actually declared on the server and deployed on globe.dev for your intention. And if I go to the Flutter code, it's pretty simple.

So it's a simple swap scope, which declares a scope for a swappable area in your app. And then you put a slot with a dedicated identifier so that it can be swapped at runtime. And then you can simply call swap get with your identifier and give it a URL where the remote widget is loaded from.

And it will replace your slot with your remote widget. So that's it. It's just a bunch of wrappers around the value to make life easier.

But it's just a thin wrapper on top of it. Yeah. If I go back to my server side here, you can see that these swap widgets are also available on the server side.

So here I have a swap widget, which will trigger a new swap on the Flutter side. But when the child is tapped. So when I will tap on next, it will say to my mobile app, OK, you need to load this path and replace the widget with identifier page with the result of the HTTP call.

So here I'm loading a new remote widget and replacing it at runtime, which is pretty cool. So you don't have any code in the Flutter app for all of that. And finally, a final page.

So yeah, that's it. And this way you can update your app really frequently from your server without any update on your client side. Small disclaimer.

It's still really early stage. It's not used in production yet. It's just some prototypes I'm building for ClickUp or maybe other use cases.

But it's still early stage. And really, if you want to participate into the development of this package, don't hesitate to contact me on the GitHub repository. I would be happy to have help on this.

Now, OK, we are able to send widgets from the server. Wouldn't it be easier to send the full app like this? Yeah, it's theoretically it's possible, but I don't think it's a good idea.

First, you will have a performance impact because every widget will have to be deserialized. And even if it's binary format, it still has a cost. Same for simply sending the request.

It takes time and depends on your connections, connectivity, and so on. So yeah, just use it where you need it. Also, it's more limited in terms of interactions.

You want to be able to create beautiful animations, nice transitions. You can kind of prepare pre-built transitions, but you can do really customized transition animations and gestures with this kind of mechanisms because it needs to have the real-time updates from the user to do it. You will have just really basic offline support.

You wouldn't be able to navigate an app offline if it would be fully built this way for obvious reasons. And finally, same remark as for Shorebird, be careful with store policies. It's not really well seen from Google and Apple to have dynamic content sent this way because they want the best experience for their users.

So yeah, be careful also with the rules from the stores. So in conclusion, I would say use it wisely if you have specific use cases, just like what we have at ClickUp with the dynamic dashboards, then yeah, don't hesitate to use this kind of technologies. It's a great piece of technology that allows a lot of stuff.

And it's really fun to use, too. Thank you for following this talk, and don't hesitate to reach out on X or GitHub or on my blog and whatever.

[Guillaume]
Thank you very much, Alois.

[Simone]
Can we have a bigger applause for this person doing live coding with slides made on Figma? It's impressive. I was impressed, honestly.

[Guillaume]
And that's the first live coding of the day, right?

[Simone]
Yes. So yeah.

[Aloïs]
It's not really live coding.

[Guillaume]
Kudos to you. I'm not showing the code.

[Aloïs]
I mean, it's...

[Guillaume]
It's a live demo. Yeah. I mean...

I have my own personal question, actually, to start. What happens if I want to use a hero animation between a locally built widget and a server UI rendered one? Does it work out of the box, or does it...

[Aloïs]
Currently, you don't have any material widget in Swap, but it's perfectly doable. You could, yes, send a hero widget, and it would be used in the exact same way. It's just a way to serialize it and deserialize it on the other side.

So yeah, it would work perfectly fine if you define this custom widget, this custom hero widget, which is not part of Swap currently.

[Guillaume]
So I'm guessing, because there are many questions about animation, I'm guessing if your widget or component is rendered on the server side, how does your application would be able to manage the transition between those two components?

[Aloïs]
Yeah.

[Guillaume]
Well, it's not on your application at the time your animation is supposed to start, when you navigate from one page to another. It's not even there. So...

[Aloïs]
Yeah. You can define a custom event for navigation. For example, you could say...

You can define your own navigation page to say, navigate to this page and load this remote widget, for example. If you tap a button in the remote widget, it would trigger this whole thing and create a new page, load the remote widget.

[Guillaume]
Okay, so as long as you preload it, then it should work.

[Aloïs]
You have to anticipate at least the basic mechanism for navigation, yeah.

[Guillaume]
All right. Thanks.

[Simone]
I mean, you said that it's just a light wrapper around RWF. Is there anyway a small performance impact or zero at all?

[Aloïs]
No. I think it's even more performant than RFW, because there's a parser for the custom language that needs to process this text, this raw text to build the instances, whereas with Swap, it's directly Dart instances. So I think...

I guess it's more performant, in fact.

[Guillaume]
So another question is, does Swap have support for versioning to avoid pushing outdated code to your app?

[Aloïs]
It's up to you. You can do it with your APIs. It's just a way to receive code.

You can invoke code to your APIs and receive data. So you can define your own headers, for example, for your calls and manage it on your server. So it's doable.

It's doable. It's not built in. There's no way to do it in a standard way, but yeah.

[Guillaume]
It's up to you. The way you define your API and versioning is always a pleasure when working with API.

[Aloïs]
Does it work with the web? That's a good question. It does not work with the web, but I have a prototype for serializing W instances with Node.

So it's doable. If I have time in the future, I could eventually develop a TypeScript library for that. But yeah.

It's doable. It's doable.

[Simone]
I think it... Well, anyway, it's very interesting stuff. It's more...

Well, does it work on Flutter web?

[Aloïs]
Oh, on Flutter web? Yeah. Yeah.

Yeah. It should work. I haven't tried, to be honest, but I'm sure it will work.

[Guillaume]
As everything with Flutter.

[Aloïs]
Yeah. It just works.

[Guillaume]
Does Swap or RFW support a caching system that avoids long reload when...

[Aloïs]
I have a basic caching mechanism in Swap. Not in RFW, because RFW is really basic. It's just the protocol, the serialization, and the language.

But yeah. I have a basic store that won't send a request that has already been sent, and you can customize just a bit, adding a custom store for that if you want to store it in file, in a database, or whatever. But yeah.

[Guillaume]
Okay. So yeah. Yeah.

That's... The question is easy, but the answer might not be. What's the difference with Shorebird?

[Aloïs]
Yeah. That's a good question. I'm not a Shorebird expert myself, but I see Shorebird more like a way to push an update to every user at the same time, whereas here, it's more like if you want to send a specific version of a widget to every user, customized experience, it's more adapted this way, in my opinion, than pushing patches and doing crazy stuff to push the patch to specific users.

It feels like easier this way if you just need a custom page for several users, for example, and you want a really dynamic page for all of your users, something that changes every day, and it won't affect the rest of your app.

[Guillaume]
I would add that on the technical side for that question, Shorebird is actually uploading a new patch that would change your application locally on the device, while yours would be just at runtime injecting some components. So yeah. It's technically different, and I guess the use cases are also different then.

[Simone]
Yeah. It doesn't also involve to have a specific version of the Flutter SDK.

[Aloïs]
No.

[Simone]
Yeah. It just works.

[Aloïs]
Yeah. That's a good point. Yeah.

Yeah. You don't need any, you have to have the same FW protocol, so you need to declare the same widgets on both sides, but yeah. You can update it at any time, so it's easier to manage, yeah.

[Guillaume]
So another question is what happens when you need to import packages? So we've discussed this last week, but there's actually one question about that. So if you're using a specific package for the widget you're injecting, should it be serialized along what you're passing through the network, or should it be installed on the front application already?

[Aloïs]
That's a good question. You have to anticipate for custom widgets, you have to declare them as serializable widgets, so you have to create a custom encoder on the server side and decoder on the Flutter side. But as soon as you have all of your widgets declared this way, you can compose them the way you want.

But yeah, you need to have them in the release.

[Guillaume]
Yeah. So you probably are not able yet actually to serialize the entire package, and it's probably not recommended because of the size of the bundle.

[Aloïs]
Oh, yeah. You mean creating like a swap package with all of these lines?

[Simone]
Yeah. Or even bundling a package. Yeah.

[Aloïs]
I don't think it would be a great experience.

[Guillaume]
So please don't do that.

[Simone]
I think you are the speaker with most questions. It's very, I mean... Yeah, there are so many.

[Guillaume]
So one last one, maybe, yeah, what strategy would you recommend for offline behavior when using Rmw?

[Aloïs]
It depends a lot of your use case. If it's like a dashboard, you could perfectly cache the whole dashboard and show it offline. It makes sense.

But if you, like in the demo, if you have navigation buttons and so on, I wouldn't cache it. I would simply say that the widget isn't available offline and just disable it. But yeah, it's really dependent on the use case, in my opinion.

[Guillaume]
Okay. So no standard strategy, just take a look at your use case. Thank you very much, Alois.

You're welcome. Yeah. Thank you.