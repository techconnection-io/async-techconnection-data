---
slug: >-
  /talks/flutter-connection/2024/leigha-reid-how-flutterflow-generates-flutter-code
date: '2024-04-24'
title: How FlutterFlow generates Flutter code
author:
  - Leigha Reid
video: qf8OKwL-aig
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/qf8OKwL-aig.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: '2024'
allow_ads: false
---
[Leigha]
Thanks so much for coming, and I'm so excited to talk to you today about Flutter Flow. So Paris is one of my favorite cities to visit, and I already have seen a lot of familiar faces here, so I look forward to connecting with you all throughout the day. I'm Leah, and I've been involved in the Flutter community for a couple years now.

I was previously one of the product managers for Flutter over at Google, and now I'm leading up product and developer relations at Flutter Flow. So I joined the Flutter Flow team about three months ago, and I was really excited about Flutter Flow's company mission, which is to help the world build great products. And I was excited about this mission because to me this means democratizing access to building apps, giving everyone the ability to bring their ideas to life.

And when I think about our product vision for the Flutter Flow platform, I think it's important to consider all the different ways that someone can build an app. So we kind of have different levels of abstraction. At the lowest level, you could be going and writing machine code, or maybe you're talking to graphics APIs, like writing shaders or hitting the metal API on Apple's platforms.

And then we have higher abstraction tools, going all the way to design tools like Figma. And most low-code tools are kind of high on that abstraction level. You don't have to worry about things like state management or rebuilding widgets or pages because the platform takes care of all of that for you.

But of course that has lots of tradeoffs, like maybe it's hard to figure out what's going on, everything's sort of a black box, so you lose control, and maybe you're sacrificing on your app's quality or certain features that you want to build into your application. So I'm considering Flutter Flow to be in its own category. I'm going to stop everyone from calling Flutter Flow a low-code tool, and instead we're going to start calling it a visual development environment.

And the reason why I want to make this distinction is because I view it as lower abstraction compared to other low-code tools. So instead of kind of hiding everything that's going on under the hood, you're actually just having a slightly higher abstraction over the core Flutter framework. So taking care of common workflows for you, but still giving you more granular control to do things like control your data flow, fine-tune performance, or even drop down to the code layer if you want to do something more custom.

So when you're working in the Flutter Flow platform, you're working in this user interface that's over here on the left-hand side, where you're composing your pages, your widgets, your styling them to your needs. And as you're clicking around in this user interface, Flutter Flow is tracking all of this in an intermediary format of your project or your app. And that is what's used to actually generate the Flutter code that you have access to.

Now for developers, our goal is really for Flutter Flow to make you faster. We want to make you more efficient so that you're focusing on the harder things in terms of development, and we'll take care of the easier things for you. And it's important to us that when you're using Flutter Flow, we're not asking you to sacrifice on your app quality or certain features.

So we want to make sure it's flexible enough and that you can drop down to the code layer where necessary. And really, our goal here is to export a repository of Flutter code that looks like something you would write yourself. So our goal is really to make sure that the generated code is going to follow Dart and Flutter best practices as much as possible.

And I put this little asterisk here because I know that best practices is something that is often debated. So really, we're focusing on best practices that we can all agree on, you know, things that we know have a really sizable impact on performance or code usability and readability. And one of the things that also makes Flutter Flow different from other low-code tools is that you can see the code as you're going, and you can always export the code, and you own it.

So this is your intellectual property. If you feel like Flutter Flow is slowing you down, you can export the code and just continue writing it as you would any other Flutter app. Okay.

So that was kind of an overview of Flutter Flow. But now I want to talk a little bit more about the anatomy of a Flutter project when it comes out of Flutter Flow. So first, let's talk about the anatomy of a Flutter app itself.

And if you've used Flutter before, you know that Flutter is mostly composed of widgets. So we have widgets all the way down. We start with a widget that represents our entire app, and then we might have a widget that represents a certain page.

Within that page, we can have a widget that represents a layout, and then we might have more atomic widgets, like buttons or text that are composed within these layouts. And to style these different widgets, we use style constants or the theme object to have a consistent design. Besides using widgets that are built into the framework, like your column, your button, your text, you might also create your own widget classes, and these can be things that are more higher-level design system components, like dialogues that meet your own branding, or it could be something more custom, like maybe you want to go even lower level to use custom paint or even drop down to, like, the native layer to do something really crazy. So when you're working in Flutter Flow, we have really similar classes that are exposed. Instead of creating a widget called my app, you create an app by creating a new project in Flutter Flow.

And when you want to create pages, you go and create a page. And then we have built-in widgets, and these are the same things that you would have access to in the material library or the Flutter framework, like buttons and text and layout widgets. And we also offer the ability to create custom widgets or components, and I'll talk more about that in a minute.

And just like when you're working in Flutter writing code by hand, you can create a design system or a theme class that has different colors and textiles and things like that. Okay. So I wanted to do a lot of live demos, but I got scared last night when folks were talking about the Wi-Fi being a little unstable.

So lots of screenshots to come. But when you log into the Flutter Flow platform, you see this builder interface, and on the left-hand side, I've already added a page. So this is like a sample e-commerce app, and this is my product detail page.

It tells me all the information about my product, and it allows my user to add that product to their cart. So on the left-hand side, you can see the page selector up at the top. That's where I select what page I'm currently viewing.

On the bottom, I can see the widget tree, so these are the widgets that are included in the build method of that page. And on the right-hand side, I can configure different widget properties. So right now, I'm selecting just my page class itself.

So these are properties that are mostly tied to the scaffold of the page. Now, I can go ahead and add different widgets to the widget tree of the page. You can see this modal that's opened up over here, and this is where you see those built-in widgets that I was talking about before.

Layout widgets, atomic widgets, like form elements, buttons, text, all that kind of good stuff. And I've already set up a design system here. As you can see, there's a light mode and dark mode, which I didn't really change because I was in a rush.

But those are all my text styles and my color styles, and those can be used in the properties of the individual widgets, either on my page level or in individual widgets on the widget tree. So now let's take a look at the generated code. And like I said, one of the things I really love about Flutter Flow is you always have access to the code.

So there's this part in the Flutter Flow platform where I can hop over and see the code as I'm building. And one thing you'll note when I go to my product detail page, and I have my page open on the right-hand side, which makes it really nice to, like, click on a button and see specifically the code for that button and so on. But you'll notice the widget and the model toggle at the top.

And this is where I'm able to have separation of UI and the data model. So when Flutter Flow generates the code for you for things like pages and components, it generates two classes, one to hold the data model and one to hold the UI layer. So first I'm going to talk about the UI layer.

So taking a closer look at my page's widget code, you can see that pages in Flutter Flow are just widgets, right, just like in Flutter, only we make them into this different object because we want to take care of a lot of the annoying stuff for you. Like we know pages are going to have a scaffold and we know you're probably going to want to do routing, so we set up all the routing for your pages for you using go router. And one thing I hear when I talk to users about their concerns when using Flutter Flow is that Flutter Flow generates a lot of code.

And I do agree with you. When I look at the code generated by Flutter Flow, at first it's a bit overwhelming. You often see, like, a pretty long widget tree.

But as you go in and you start digging deeper, a lot of what I've realized is that Flutter Flow is taking care of kind of like the fine tuning of your app for you. So this is one example where we have a setting that allows you to hide keyboard on tap for certain pages, and this is enabled by default. And what you'll see is this little bit of code for the gesture detector returned in the build method for every page.

Basically all this says is if the keyboard is open and someone taps the page, dismiss the keyboard. And it makes your app feel more natural. So aside from that, we, of course, have our scaffold, and then we have all the widgets that we've added to our widget tree.

And most of these widgets are going to be just things that are built into the Flutter platform itself. So for example, app bar is just the app bar widget from the material library. But you'll also notice some of these, like, Flutter Flow or FF custom classes that we've included in the generated code.

And again, we've done this to try to take care of the stuff that we think you're going to want to do but is sometimes annoying to do in code or maybe not built directly into the Flutter framework. So one example is customizing material components. We know that sometimes this is a little bit difficult to do.

So we've created our own classes for a lot of these common UI elements so that they better match your own design system. And back to that theming that I was mentioning before, I've already set up my theme in Flutter Flow. I've set up my textiles and my colors.

And that creates a Flutter Flow theme object. So this is a class that we've, again, defined so that we handle things like light mode and dark mode for you, and you don't even have to worry about it. But in the generated code, you'll see our Flutter Flow theme object being called in the same way that the material theme class would be used.

All right. So that was pages and a little bit of how we generate code in general. Now let's talk about creating components.

So when I first created this page, I have these three different kind of like option buttons on my page to do things like select my size, my color, the quantity of the item that I want to add to cart. And at first I just added these to my page's widget tree. But there's lots of things that I'm repeating here.

Like the styling, the sizing of the container, and I don't want to repeat myself. So instead of having these three, you know, highlighted bits as their own widgets on the widget tree, I can click that button all the way over to the right-hand side to create a component from the widget tree. And when I create a component, this just creates a new class in the generated code.

So it creates a new widget class, which I'll show in a second. Now on the left-hand side, you can see that instead of having all that code that I had before, I just have three different widgets. And those are instances of this new product option class that I've created.

And when I create this class, which you can see in the top right-hand corner, I can pass in things like parameters. So in my case, I just created an option type enum variable, and I'm passing that in as a parameter. And then when I add that widget to my widget tree, I can configure what the parameter needs to be when it's being passed in.

OK, so that's what it looked like in Flutter Flow. Now hopping over to the generated code, we can see that these components are also just widgets, right? Everything is a widget.

And these are more granular things, like the button we just showed. So we don't need a scaffold, and we won't set up routing for you. Instead, this just is a stateful widget.

And earlier, I mentioned that sometimes you want to create custom widgets. And those custom widgets in Flutter might be classes, like we just showed, that are just a composition of classes coming from the framework. Or they might be something where you want to go even lower and access custom paint, or maybe use some widgets from a different library.

And in that case, you can drop down to the code layer in Flutter Flow. And we call these just custom widgets. So you define the code for what you want your custom widget to be.

You can pass in any parameters. And you can also specify a PubSpec dependency. All right, so that was an overview on the widget layer.

But now let's talk about that data model layer. And of course, if we're talking about data model, we probably need to talk about state management. So in Flutter Flow, we have three different types of state management variables, or state variables, rather.

We have our app state variable. And in my example of an e-commerce app, I might create a cart app state variable. Because this needs to be persisted across my different pages.

I might need to interact with it from the product detail page to add an item to my cart. And then I might have a checkout page that also needs to access this data. Then we have the page state variable.

And this is just shared within the page itself. So an example of this might be the rating of the product that I'm looking at on the product detail page. And then I have my component state.

So this is a state variable that's just confined to the component. So one example of this might be in that product option component I created. Maybe I want a state variable that tells me if it's selected.

So I can, like, add a border or show some selected state. Okay. So how do we do this in Flutter Flow?

Here I'm on my page that I showed you before, my product detail page. And I've created a state variable, which is what you can see over on the right-hand side where it says local page state variable. I've created the rating state variable to store the rating of my product.

And now I can use that variable in the widget properties. So for example, setting the text string value of the text widget that's on this page. So now heading over to the generated code, before I showed you what the widget layer looked like for the page, now I want to show you what that data model layer looks like.

So you'll see a separate class for handling the model. And in this class, first I'm showing the state variables that I've created. Now I just showed you rating, but I've also created some other state variables that are stored at my page for what the selected color of the item is, what the selected quantity is, and what the selected size.

And what you, I didn't point it out before, but that class that I just showed actually extends a base Flutter flow model class. And this basically handles the initialization of state and some disposal methods for you. And under the hood, we're using provider to make the model available to other parts of the widget tree.

What you'll also notice if we go back to that product detail page model class is that aside from declaring my state variables that are stored at the page level, I'm also going to instantiate the model for any components that are used in the page itself. So the reason why Flutter flow does this is because there are often lots of business cases where you want the page to have access to state variables in its children. So in this example, each one of my three components has a component state called is selected, like we mentioned before, which tells me if that button is in the selected state.

So if I'm working on my page and I want to set a widget property, I can use that variable is selected from any of those widgets or components, rather, to set the widget property. And I won't go into too much detail of different use cases for this right now, but this comes in really handy if you're creating a page that's like a form, for example, where you really need to know what the selected value of every form is. Okay.

So that was a little bit about the page model. Now let's talk about a specific use case where I want to update the page state from a component. So in my case, I'm storing the selected size, selected quantity, selected color of the item as state variables, like I showed before.

And when a user is interacting with one of these components, I need to use their interaction to update that state variable. For example, change the size of the selected item. So the way I'm going to do this in Flutter Flow is I can specify an action as a parameter for my component.

And an action in Flutter Flow is basically a function. So all I'm saying is now my size option or product option component or widget class is now going to have the option to take in a callback function as a parameter. So I set that at the component level.

I define a parameter. And then when I'm instantiating that class, I can pass in the callback function to update my page state. So if I head back to the generated code, I can see that now I'm looking at my product option widget.

That's that component that I created. That's reusable for my selecting size, color, and quantity. And now there's another parameter that's added as an input.

And it's a function. And when I was showing it on the last slide, I didn't point it out. But actually the function that I was passing in has its own parameters.

Option type and selected size. So this is a callback that can now be called by my component to update that state variable. And to actually define what that function is to pass it into my class, I can use, again, what's called an action in Flutter Flow.

So I've created what's called a page action block, which is essentially just a function that is scoped to the page level. And here I've configured the logic of this function, which in this case is just using a condition to check what type of button is it. Is it the one for selecting size?

Is it the one for selecting color? And it updates the state variable according to, you know, what type of option it was. Okay.

So that was me configuring my function in Flutter Flow. Now if I look at the generated code, this function has been added to my pages model because I scoped it to be at the page level. And this is pretty simple.

You know, it's basically just a function that has a condition and then sets the state. So now if I want to actually execute that callback in my component itself, I open up the component in Flutter Flow and I specify when that function should be called. So the component has the function because it was a parameter and now the component needs to call that function.

And in this case, I'm using the size as an option. So when someone changes the size dropdown, as soon as they change that dropdown option, the callback will be executed. And just to kind of show you what this looks like under the hood, if I open up my data model for the component that's generated, I can see that state fields for different widgets that are used in that component are also declared in this model.

So for example, a form field controller was automatically added because I used the dropdown widget inside of my component. And then we simply see the callback executed when the dropdown is selected. Cool.

So that was page and component states. But there's one other state variable that's at state. And this is when I want to share a variable across different pages.

Like cart, which I mentioned before. So the way I would do this in Flutter Flow is I want to create a cart state variable, which I can show here in that app state image down below. But I actually want this to be a custom data type, right?

Because my cart has lots of different attributes, like the cart ID or the items that are in that cart. So what I've done first is I've created a cart data type. And that's essentially just a struct, right?

And that's what I'm showing right over here in this left-hand corner. So I've created my cart struct. And I've created an app state variable that is of type cart struct.

And in the generated code, I can see this come to life. So the way Flutter Flow handles app state is we have one Flutter Flow app state class, FFAppState, which extends change notifier. Essentially it exposes some getters and setters for the different app state variables.

And like I mentioned before, we're using this custom data type, which you can see over here. I won't show the definition, but this is its own class that's stored in your code base as well. And then when I actually want to use this app state variable, for example, in some cart checkout page, that cart's widget will include context.watch to watch the Flutter Flow app state class. Now, I do want to say that we think there's room for improvement here. Right now, this is kind of one giant app state class. And we're working on breaking it up into smaller modules and having more granular watching so you're not watching the entire class.

But it's still a pretty good start, I think. And one cool thing I wanted to point out is that in Flutter Flow, what you can do is something called dynamically generate children. So on the right-hand side, I've actually created a list view that just dynamically generates one child for each item in my cart.

And then it uses my cart item component to show what the item should look like. And in the generated code, all this looks like is a list view builder where I'm iterating through each item in my cart. All right.

So that was state management. And now I want to talk very briefly about connecting to the back end. So you might have lots of ways of managing your back end.

Maybe you have different databases. Maybe you're using Firestore or SQL database. And we offer pretty good options to connect to those.

But we also have this ability to just connect to any API. So in Flutter Flow, I can create an API call. One nice thing is that you can upload an API spec, like an open API file, to just automatically handle this for you.

But in my example, I've created an API that just calls this URL to get the ratings of my product. And in the generated code, we actually have a couple of different classes that we create on our own to use to configure this API. So the first one is the API call options class.

And this just configures the details of an API call. And it uses this equitable package to easily cache the options. So we're not unnecessarily hitting your API.

Then we have this API call response class, which, of course, makes the API call response easily consumable by the rest of your application. And then we have an API manager, which just manages the request creation, execution, response handling. And under the hood, it's mostly using the HTTP package.

So those were the classes that are just generated by Flutter Flow to use in all API calls. But when you create an API call the way I did before, it will also create a class specific to that call. So in my case, I created an API to get my product ratings.

So Flutter Flow has generated this get rating call class. In Flutter Flow, when I want to call that API, I can, again, go back to actions, which are essentially just functions, right? So up at the top, you can see the trigger.

And I've set this to run when my page is loaded, specifically my product detail page. So when my product detail page first loads, then it's going to make this back-end call, where I'm simply saying make the back-end call, use the get rating call that I've configured and pass in any variables. In my case, I already created a query parameter variable called product ID.

One nice thing is this kind of format makes it really easy to parse the response into a custom data type, which would be configured over on the right-hand side. And I can set different paths for how to respond in the case of a success or an error. And you can make this more granular, like responding to certain status codes or messages and showing something like a snack bar or maybe just, like, setting the state to some specific value.

In my case, I was just moving quickly, so I said, okay, if this worked, then just update my page state variable so that my rating state variable is refreshed with the results of the API call. Cool. So over in the generated code, I'm going back to my product details page widget code, so the UI layer.

And I can see that this bit of code has been added. So in init state, when the page has actually loaded, then make a call using the class for my API configuration. And if you did something like handle errors or transform the results of the API call, all of that would show up here.

Cool. So I didn't have a ton of time today, so I was moving very quickly, and there's lots of stuff we didn't cover, like connecting to a database, configuring authentication, animations, navigation, localization, so much stuff to talk about. So I would love if you give Flutter Flow a try, and I'm very eager to get all of your feedback.

And I did want to say that there's lots of things we're improving on. I recently wrote up a blog about our vision and roadmap, so feel free to take a look. But a big part of our roadmap is improving the architecture of apps generated with Flutter Flow.

This is things like breaking up our app state into different modules, being more specific about only watching the variables that you need, making components more powerful in general so that you can create components wherever possible. And also just making it easier to debug, because I know that's just something that's in general difficult to do in low-code tools. Anyway, that's it.

So I'm looking forward to hearing some questions.

[Guillaume]
Thank you very much, Leigha. If you care to join us to the Q&A table. With the X?

Yeah, you can sit on that one.

[Leigha]
Sounds good.

[Guillaume]
So people can see you. Thank you very much.

[Leigha]
Thank you.

[Guillaume]
For this awesome glimpse at what's under the hood of Flutter Flow and how things are working. We have, like, so many questions. Yeah.

People are really interested.

[Simone]
I think we have just a big sum, and we'll do screenshots to forward so you can be able to answer. Sounds great.

[Guillaume]
Exactly. So, yeah. The first one is can you take a built-in component or a page of your Flutter Flow app, export it, and, yeah, embed it inside a Flutter app classic?

[Leigha]
Yeah, you can. There's nothing stopping you from doing that. And, in fact, we're trying to make that even easier.

We're trying to make it into a kind of happy path where you could export your Flutter Flow project as, like, a package that you would use and consume in any apps or that you could maybe use in other Flutter Flow projects itself. So possible right now. I haven't personally done that myself.

So I'd be curious to hear what the issues are that you run into with going through that workflow. But it's definitely a path we're working on making even easier.

[Guillaume]
So please try it and give some feedback to Leah.

[Leigha]
Yes.

[Guillaume]
Yeah. So Guillaume is asking can Flutter Flow detect which is the most optimized widget that you should be using? For example, using a single child scroll view or a custom scroll view or something else?

How is it possible to optimize? Is it optimizing?

[Leigha]
We've definitely done our best to optimize the widgets that we're offering. So we're really focused more on kind of, like, the business aspect. What are the common types of UI that you want to create in an app?

And then we'll research, you know, Flutter and Dart best practices to make sure that our default configurations are putting your app in the best spot possible. But I think a lot of that also has to do with the settings that you're using inside of Flutter Flow and what widgets you're adding or any custom code. So in general, we do our best to make sure that, like, the default option is as optimized as possible.

But a lot of it's up to you to kind of configure.

[Simone]
And what do you think is the maximum team size for collaborating on a Flutter Flow project?

[Leigha]
That's a great question. So right now we're really focusing a lot of our attention on branching. And I think branching is so key to working on a project at scale.

Right now there are a couple of known issues with branching. So, like, I wouldn't recommend Flutter Flow for a huge team. But I would say check back in a couple of weeks or months because we have lots of exciting branching stuff coming out soon.

[Simone]
Weeks even.

[Leigha]
Yes. Awesome. Stuff is coming out.

Today is Wednesday, right? Tomorrow more branching stuff is coming out. So hours.

[Simone]
Hours. Yeah. Awesome.

[Guillaume]
Do you manage automatic golden tests?

[Leigha]
We don't right now. But that's actually something that we've talked about. Because we have this cool opportunity where we have a preview of what you think your project should work or should look like.

So I do think it's something that we'll do later down the line. But it's not something we're doing right now.

[Simone]
And more about, like, an everyday question. Can you actually use Flutter Flow while you are offline?

[Leigha]
So right now, no. And I know this is kind of frustrating, especially because we have a desktop app. And even myself, I open up the desktop app, and I was like, great, I don't have Wi-Fi.

And was kind of disappointed when I realized it didn't work. Again, I think it's something we'd love to do longer term. But it's just not set up to work right now.

[Guillaume]
All right. Are tests also automatically generated?

[Leigha]
Tests are not automatically generated. But we do have testing capabilities where you're able to set up integration tests. Which is actually quite nice.

It's kind of easier to do in a user interface, I think. You can also set up unit tests for things like custom functions that you create where you set up what you think the expected value should be. So we have some testing capabilities.

They're not automatically set up. And I think there's lots of room for improvement. Like golden tests or maybe anticipating what types of tests you should create.

[Guillaume]
All right. One last one. Because I think this one is very interesting.

It's from someone that has actually used it, I think. Has FlutterFlow been able to reduce the amount of duplicated generated code?

[Leigha]
So I think a lot of the duplication actually comes from the structure of your app. I gave a really good example where when I first created that page, I was just copying and pasting some widgets. FlutterFlow is not going to detect automatically, hey, you copied this.

I need to create a class. You have to be the one to create a component which makes it into a reusable class. So it's similar to writing code.

If you copy and paste it, that code is going to be duplicated. But if you create a reusable class and use that in multiple places, that's not duplicated. That just creates a class in your code base.

[Simone]
Awesome. All right.

[Guillaume]
There are so many more questions, but we don't have time, so we'll definitely share them to you so that you can give the community some answers.

[Leigha]
We'll do. And I'll be around, so come find me and we can talk about FlutterFlow.

[Guillaume]
Thank you very much, Lea.

[Leigha]
Thank you.