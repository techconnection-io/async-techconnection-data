---
slug: >-
  /talks/frenchkit/swift-connection-2023/simon-b-stovring-achieving-loose-coupling-with-pure-dependency-injection-and-the-composition-root
date: '2023-09-21'
title: >-
  Achieving Loose Coupling with Pure Dependency Injection and the Composition
  Root
author: Simon B. Støvring.
video: bmIW1skJQFo
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/bmIW1skJQFo.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/44bef41cfc2041b68ec6ff3e6aa2a08a/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---
I'm here to talk about loose coupling, dependency injection and the composition route.
And I'm also here to inspire you to think about how you compose your Swift apps.
All right.
I'm here to talk about loose coupling, dependency injection and the composition route pattern.
And I'm also here to make an attempt to inspire you to think about how you compose your Swift apps.
So I've been building iOS apps since the iPhone 3GS came out.
So that's around 14 years, give or take.
And during long nights or late nights and long weekends, I work on some of my own apps.
Amongst others, RuneStone, a text editor for iPhone and iPad, and Scriptable, an automation tool for writing and running JavaScript on your iPhone and iPad.
During the day, I work at a company called Shape.
We are a bureau based in beautiful Copenhagen, Denmark.
And we have a focus on native development for both iOS and Android.
And the topics I'll cover today are some that I've dived deep into over the past year or so, working at Shape to improve our codebases.
So the title of the talk is quite a mouthful.
Achieving loose coupling with pure dependency injection and the composition route.
But we'll go over these topics one by one to see kind of what they mean and how they relate to each other.
And we'll start by reminding ourselves what loose coupling means and how it relates to dependency injection.
So loose coupling ensures that our codebase is flexible enough that it can adapt to changing requirements and accommodate new features with the minimum changes needed.
And loose coupling also ensures that our codebase is maintainable because our components have well defined boundaries, which means that we can fix bugs and introduce new features in a limited scope of our application without the risk of unintended side effects in other parts of the system.
Furthermore, these well defined boundaries also means that we can work on components in parallel across the team.
So how can we make our code loosely coupled?
Well, to answer that question, I'd like to introduce an example app that I've built.
It's called Coffee Shops.
So I like to work from coffee shops.
So I've made this app to track and rate the coffee shops that I've visited.
And we'll use it as an example app throughout the rest of this presentation.
And I'll just show you the app so you know what we're talking about.
So this is the onboarding flow in the app.
The user can either create an account or they can sign in.
And I'll proceed by signing in.
And fortunately, iOS is smart enough to hide my password and the keyboard while I type it.
So there we go.
Now I'm signed in and you'll see that we see the nearby coffee shops on a map.
And we can pan around this map.
We can zoom in and out to reveal more nearby coffee shops.
And yesterday, actually just this morning, I visited a coffee shop called Comets.
And it's a great coffee shop.
It's just around the corner.
So if you're thirsty for a cup of coffee, I recommend going there.
Because they're a great coffee shop.
It's actually part a coffee shop and part a vinyl shop, which is great for a vinyl lover like me.
So I'll proceed by rating this and I'll give it five stars because I really like the place.
And I'll also make a note to remind myself what makes this place special.
So next time I'm in Paris, maybe for Swift Connection next year, I know why I liked it.
All right.
We'll close these details of the coffee shop.
And we'll return to the map where you can see that the marker has now changed color.
It's a blue color now, meaning that this is a highly rated coffee shop.
And the coffee shop next to it that's a yellow marker is, well, rated lower.
So next up, let's head to the profile where we can see our membership status and we can log out.
We can also see the coffee shops, a list of all the coffee shops that we previously visited.
That's the app.
And let's return to the map and see how we can implement a map like this.
So we have a Swift UI view here called coffee shops map view.
And we need to display some markers on this map view, particularly our coffee shops.
So we also have a database called Swift data coffee shops database.
And we reference this in our view.
So we create an instance of it.
But you'll notice that now we have tight coupling.
Our view is tightly coupled with our data source.
And this tight coupling happens because we initialize an instance of our database within our view.
And when� oh, sorry.
And this makes it difficult to swap out this data source.
Maybe because we need to� maybe we need to swap it out for stopping our data with hard coded data.
Or maybe we need to swap it out for a unit test.
Or maybe the data source has just changed and we need to provide a new one.
And in the context of dependency injection, we call this the control freak anti-pattern where the consumer of the dependency, in this case the map view, creates an instance of the dependency, in this case our database.
So let's get rid of this tight coupling.
And we know from the dependency inversion principles that high level modules or components, in this case our map view, should not depend on low level components, in this case our database.
Instead, they should both depend on an abstraction.
Put differently, we should program to an abstraction, not an implementation.
So let's just real quick see how we can apply this.
We'll start by introducing this abstraction.
In this case a protocol called coffee shops repository that specifies that we need a list of coffee shops.
Then we'll make our database conform to this protocol and we'll replace the instance in our view, in the instance of our database in our view, with a reference to the protocol.
And now we're programming against an abstraction rather than an implementation.
So now we have a loose coupling in our code base.
And you'll see that we achieved this by using dependency injection.
Because now we no longer have a concrete instance of our database, but we depend on a repository.
So someone needs to provide that to us at some point.
And with that we've just convinced ourselves that dependency injection is a technique that enables loose coupling.
So let's turn our attention to dependency injection, just for a minute or two.
At a high level we have three different types of initialization injection.
So when we have a consumer like our map view, we can inject dependencies in three different ways.
We can either inject them through the initializer, like we just saw, or we can provide a dependency to its consumer through a method.
So whenever we're invoking a method on the consumer, we can provide the dependency.
Or we can use property injection, where we just set the dependency on the consumer.
An example of this is the delegate pattern that's quite common in UIKit.
And as developers, we don't really think about these three patterns as dependency injection.
Maybe some of you don't.
Maybe some of you do, maybe some of you don't.
But we use them multiple times every day as developers, right?
But these three patterns are key to dependency injection, because these are what lets us swap out a dependency with another dependency without touching the consumer.
Or the implementation of the consumer, rather.
But the remaining part of this talk will focus solely on initialization injection.
And that's because initialization injection is ideal for dependency injection.
Because initialization injection is fail safe by design, because the compiler will enforce the relationship between the consumer and its dependency.
And that's because the consumer specifies through its initializer that it cannot exist without an instance of the dependency.
That's contrary to property injection, for example.
And also with initialization injection, this is quite good.
When we type a line like this in Xcode, Xcode will tell us the dependencies that our authenticator has.
So here it's quite clear to see that in order to create an authenticator, we need to provide a credential store, something conforming to the credential storing protocol.
Right.
So let's consider for a moment what happens when we start to use initialization injection in our code base.
So I pulled up our profile view here.
And this profile view needs an authenticator that we just saw.
And that authenticator needs something conforming to credential storing.
We will use the authenticator to log out, for example.
So we could have a method on our authenticator called sign out or log out or whatever we want to call it.
And when invoking that, we'll probably clear the credentials in our credential store.
All right.
So we'll add that to our profile view.
We have a profile view here.
A plain Swift UI view that depends on something conforming to the authenticating protocol, which I forgot to note here, but our authenticator conforms to the authenticating protocol.
Anyways.
Our profile view also has a dependency on something called the visited coffee shop's repository.
That's another protocol that can hand us or provide us with the coffee shops that we have visited.
So if we squint a bit, we'll see a pattern here.
This is really an object graph.
Profile view depends on something that conforms to authenticating, which in turn depends on something conforming to credential storing.
And then a similar story for our visited coffee shop's repository.
But this is only part of our app.
We can zoom out and we'll see an even larger part of our app.
Or rather, an even larger part of our object graph that will occur as soon as we start adopting initialization injection in our code base.
And even this is only part of our object graph, but it couldn't really fit anymore into the slide.
Now, just a reminder that the edges leading out of the vertices here or between vertices here doesn't mean that the source vertex creates the destination vertex.
Rather, this implies a relationship, a dependency between the two.
So again, profile view depends on authenticating, but doesn't necessarily create an instance of it.
We'll get back to that.
But when we have an object graph like this, this doesn't have to live� this object graph doesn't have to live in our app target.
We could distribute these� the implementations of these objects to Swift packages.
In fact, Christoph covered part of this yesterday.
And now we'll just kind of reiterate it.
Me, for example, I'm inspired by an approach presented by Airbnb, which by the way happens to be very similar to the one presented by Christoph, where they move all of their code into feature packages.
So each feature lives in an isolated package, and these packages might in turn depend on some library packages or whatever you want to call them, some shared code.
But the feature packages never depend on each other.
So I tend to use an approach similar to Airbnb's and similar to Christoph's.
And because we have loose coupling in our code base, because we have these abstractions in place and because we use initialize injection, it becomes quite trivial to move our code into these packages.
So I'll take all the components that are related to the onboarding of my app, or the onboarding feature in my app, and I'll put it into the onboarding feature package.
I'll take everything related to the profile and put it in the profile feature package.
I'll take everything related to the map, put it in the map feature package.
And I'll take everything related to the details and put it in the details feature package.
These are my feature packages.
Now something remains here, and that's everything related to authentication.
But I'll put that in an authentication package.
All right.
So now we have all our Swift code, we have all our application logic or business logic, and we have all our UI living in these packages.
Specifically our UI lives in the feature packages, whereas our authentication package contains some business logic.
All right.
But remember, we still have an object graph.
We didn't get rid of the object graph.
It's just distributed across Swift packages, or rather across the targets within those
Swift packages.
So now that we have an object graph, and we have that object graph distributed across
Swift packages, the question we need to ask ourselves is how do we compose the object graph?
And that brings us to the last topic here, the composition route.
The composition route was originally presented by Steven Van Derschen and Mark Seaman in a book called dependency injection principles, practices, and patterns.
And this book answers the question, how do we compose the object graph?
It answers many other questions as well, but that's one of them.
And it answers this question by introducing the composition route.
And the composition route is defined as a single logical location in an application where modules are composed together.
Now, modules in this case is our Swift pages, rather the targets in Swift pages, which in turn contains our components.
And the thing that we want to compose together is really that we want to compose our object graph, right?
And the single logical location in this case is really something that we need to define as developers.
We need to figure out where can the composition of this object graph be logically organized.
And that's really what we're here to answer.
So we'll do that throughout the remaining part of this presentation.
To figure out where is this single logical location.
That's our task at hand.
But before we dive into that, I'd like to just mention a couple of other attributes that the composition route has.
Namely, it needs to live as close to the application's entry point as possible.
That's something specified in the dependency injection principles, practices, and patterns book.
And what this really means is that once you start deferring the initialization of your dependencies, remember, the consumer doesn't create the dependency itself, rather it defers the initialization.
And once you start doing that, at some point you need to initialize your dependencies, right?
But if you defer it for as long as possible, you quite naturally end up at the application's entry point.
So the entry point is really the very first thing to happen when your app gets launched.
I also want to stress that the composition route can span several types.
And I want to stress this because it's a mistake that I made when I started adopting the composition route in my projects.
I thought that the composition route was a struct or a class or something, some specific type that lived in a single place in my application.
But that's not the case.
The composition route is a layer in my application that can span several types, and these types will have several properties, several functions.
And this layer, the composition route layer, is made up of something called composers.
And the composer is a property or a function that creates and returns a part of our object graph.
So it can be a teeny tiny part or it can be a very large part.
And we have multiple composers, and these composers call each other, we can start building an entire object graph.
And we'll see how we do that.
Yeah.
So here we have another visualization of our app.
And it might be a bit difficult to see, so you'll have to take my word for it.
But this is basically the same object graph that we saw earlier, except they're now loosely coupled, living in separate Swift packages.
But we once again see that the profile view depends on something that conforms to authenticating, which in turn depends on something conforming to credential storing and so on.
But this is a common way to visualize the composition route.
So I want to show it to you.
And when you have an object graph like this, and when you lay it out like this, you have your composition route in the middle.
And you'll notice that we've added a bunch of edges to the components in our object graph here.
And these edges doesn't necessarily or particularly specify a dependency.
But rather the blue edges here means that our composition route creates these objects.
And then you might say, well, Simon, duh, you have edges pointing to every object in this graph.
And that's correct.
That's because our composition route is responsible for creating every single object in this graph.
And that's because what that means is that our composition route depends on everything in our app.
It's allowed to depend on all the Swift packages, all the targets and so on.
But it's the only place in our app that's allowed to depend on everything.
Because the entire responsibility of the composition route is to compose everything together.
So, as I mentioned earlier, this composition route consists of consumers.
And now we'll see our first consumer.
Sorry, composer.
It consists of composers.
And we'll see our first composer.
And this composer is a property.
This property is called profile view.
And it returns some view.
In this case, it returns a profile view.
In other words, it creates a profile view.
And in order to create a profile view, we also need to create the dependencies of that profile view.
And that's an authenticator.
And to create an authenticator, we also need to create its dependencies.
In this case, a credential store.
And also our profile view has a dependency on that visited coffee shop's repository.
So we've created a Swift data visited coffee shop's repository here that conforms to our protocol.
All right.
Remember just a second ago we threw everything into separate Swift packages.
And we saw that using one visualization.
I'll just show how it looks when we have this visualization.
So I'll throw all of these components into the same Swift packages.
And then let's see what happens.
So we introduce our onboarding feature, profile feature, map feature, details feature, and authentication.
And all that remains is now our composition root in this graph.
And our composition root depends on these Swift packages.
Or rather, the targets within those.
So if we have all our UI and all our business logic living in Swift packages, where does that put our app target?
Well, our app target is the composition root.
That's our composition root layer that contains composers.
So you might not be totally convinced yet.
I wouldn't blame you.
But we'll see how it works in a Swift project just in a second.
But just trust me.
We've just learned that a composition root lives in our app target to create the object graph using composers.
Now let's head into Xcode.
And we'll start by opening our coffee shop's app.
And then I'll just convince you that everything lives in Swift packages.
I'm not unfolding them.
So you'll just take my word for it, right?
I'm a trustworthy guy.
Please.
Why do you laugh?
Okay.
I'm a trustworthy guy.
Okay.
Let's open our app target.
And you'll see it contains surprisingly little code.
Or it contains two source files, two Swift source files.
And they in turn contain very little code.
And that I want to convince you of.
You won't have to take my word for it.
The second thing you might notice is that we have a ton of imports here.
And usually this is a code smell.
But remember, our composition root layer is allowed to depend on everything.
But it's the only place that's allowed to it.
So it's not really a code smell here.
Let's scroll down a bit.
And then we'll meet some of our first real composers.
And I'd like to turn your attention to the coffee shop's app struct here that conforms to the app protocol.
And the first thing I want to highlight here is that this struct is annotated with at main.
And what this means is that this is the� this struct is the main entry point to our application.
And it contains the first code to be executed when iOS hands off control to our app.
And remember, the composition root was supposed to live as close as possible to the application's entry point.
And, I mean, it seems to me that we just found that.
This is what the app is.
We can't get any closer than this.
The next thing I want to highlight here is that we now see our two first composers.
And they're implemented as properties.
So these are composers that create as tiny as possible� as tiny as possible a part of the composition of the object graph as possible.
Namely, they only create one component.
But a single component is still kind of a graph.
And here we create our credential store.
Keychain credential store, which conforms to the credential storing protocol.
And we also create an instance of Swift data DB, which is just a type that can set up our
Swift data stack.
And these are created in the app and stored on the app, meaning that these two dependencies, which we can now inject into our consumers, are using the singleton lifetime.
Now, this is not the same as the singleton pattern.
The singleton lifetime is specific to dependency injection.
And what that means is that we have a single instance of a dependency throughout our entire app's life� throughout our app's entire life cycle.
And we can then inject that into all the consumers that need it.
And we might do that in order to share some state between our consumers.
Then we have another composer here.
And it creates a scene, not just a scene, but one and only scene.
And that contains an onboarding view.
And our onboarding view, in order to compose that, we need an authenticator.
And we also need to provide a view builder.
And here we are calling two other composers.
So authenticator map view and profile view are properties on this coffee shop's app.
And they live in an extension that we'll see in a second.
But this is actually quite key to the composition route pattern.
A composer is allowed to call other composers.
So to create one part of the object graph, we might call a composer that can return a sub part of the object graph, a sub graph.
So let's go back to Xcode and scroll down a bit to see how some of these composers are implemented.
I'd like to turn your attention to the map view composer here.
Well, the map view composer is called map view.
And it returns some view, a SwiftUI view.
And that view is a map view.
Unsurprisingly.
And it has a bunch of dependencies.
There are a lot of things going on here.
But the particular code is not that important.
I'll take you through the highlights.
And the first thing I'd like to turn your attention to is this visited coffee shop's repository variable.
Which is assigned to self.visitedcoffeeshop'srepository.
Self.visitedcoffeeshop'srepository.
I'm starting to regret that variable name.
It's really difficult to say.
That's another composer that returns a part of the object graph.
And then we store that in a variable named visited coffee shop's repository.
And we use that variable in multiple parts of our composer.
So this is an example of the scoped lifetime.
Which is a bit similar to the singleton lifetime.
But which means that we use a single dependency or a single instance of a dependency in a sub part of our object graph.
Possibly again to share state.
But we might have multiple instances of this visited coffee shop's repository and use it in different parts of the object graph.
And when we share it in a part of the object graph, we have the scoped lifetime.
And then we'll just see our third and last lifetime.
And that's the transient lifetime.
And we see several examples of this here.
But I've highlighted one of them.
The transient lifetime is when we create a dependency and just pass it to the consumer right away.
So every time a consumer needs a dependency, a particular type of dependency, we just create it and provide it.
That's the transient lifetime.
And this means that the dependency is� the lifetime of the dependency is tied heavily to the lifetime of the consumer.
The third and last thing I want to highlight in this part of the code is this training closure.
Which is really a view builder.
And in this view builder, we return an instance of app details view.
That's a Swift UI view.
And this is where our composition can tie two feature packages together.
So remember we took the map and put it into one feature page.
And then we took the coffee shop details and put it into another.
So our map doesn't know anything about the coffee shop details.
It's the responsibility of our composition root to tie these two together.
And it can do so through this view builder.
There are other mechanisms, but we're using view builders here.
All right.
We'll just have a quick look at the implementation of this app details view.
Nothing in particular I want to highlight here.
I just want to show you this is a regular Swift UI view.
It has some dependencies.
It has a body.
It returns a details view.
And that lives in our details feature package.
What I'd like to convince you of here is that our composition root can actually span several types and it can span several Swift files.
All right.
Then we'll scroll down and see our two last composers.
We have the authenticator and we have the visited coffee shop repository.
These are teeny tiny composers.
And I like to keep them tiny.
Because if I use this composer in multiple parts of our object graph, maybe to create transient lifetimes, maybe where I have multiple parts of my app that needs a visited coffee shop repository and I want to create it every time I want to inject it.
Then I can just if at some point I want to change what a visited coffee shop repository is, so in this case it's a Swift data coffee shop repository, but say that I migrated back to core data, why would I want to do that?
I don't know.
Maybe I came with some new technology that I want to adopt instead.
Or maybe I want to inject stop data.
Then I'll just find the composer that creates this repository, return another instance, and now I've changed it throughout my entire app.
Because they all use this composer to create instances.
That's really our composition root layer.
But I'd like to show you how all of this works in our Swift packages as well.
So I'll move into the map feature package and I'll select my map view.
And I'll start the Swift UI preview because we're going to need that in a second.
And then I want to highlight the dependencies, at least one of the dependencies of this map view.
You might see that it depends on something called a coffee shop map, coffee shop marker service, that's just what provides the markers to be displayed on the map, fairly unimportant.
But then it depends on this view builder that we saw just a second ago.
And the thing that I want to stress here is that a dependency can be of any type, doesn't have to be a struct, protocol, class, whatever.
It can also be a closure, as in this case.
And this is what allows us to tie these two Swift packages together.
And if we scroll down, we'll see our Swift UI preview for this map view.
The one thing we also see on the� we will see the implementation of the preview and we see it running on the right-hand side here.
And you'll notice it's a quite rich preview.
We have some stopped coffee shops and we even have a stopped implementation of this coffee shop details.
Remember, the particular details lives in another Swift package, another feature package, and feature packages are not allowed to depend on each other.
So I have to stop the details here.
I have to return some mock data, right?
And you'll see that my Swift UI preview is quite simple.
I just inject this stopped instance.
I inject something called a preview coffee shop marker service that just returns hard coded data.
And then I return my stopped details view.
And with this I allow myself to consider my Swift UI preview as a composition route.
Because it's convention that Swift UI previews lives in the same file as the view� as the implementation of the view we are previewing.
So we cannot really move this out into a central composition route layer.
So we just regard this as a teeny tiny composition route that creates a preview.
And then I would just like to show the implementation of this preview coffee shop marker service.
So I like to have a folder named previews.
A bit similar to� I like to have a folder named previews where I store the stopped services of repositories that I use in my Swift UI previews.
And this is a bit similar to the preview content folder that Xcode creates for you where you can put in your mock assets.
And I just show that this is just an instance that returns hard coded data that we use in the Swift UI preview.
A question that I often get is how does this work in unit tests?
How does the composition work when we write unit tests?
So I like to turn our attention to a sample unit test that I've pulled up here.
The code is not that important.
But this is a unit test that tests that when we rate a coffee shop in the map, that the color of the marker then changes.
Or reflects the rating.
It's probably a shitty unit test, but let that be.
The important part here is that we create a type with quite a mouthful of a name.
Persistence annotating coffee shop marker service.
Not that important.
What's really important here is that it has two dependencies.
And what's even more important is that we create those dependencies on the lines before, just above, and we inject it into the service that we're actually testing here.
So you might say, well, Simon, there's not really anything new here.
And you're right.
The composition route, introducing a composition route in your app target has no effect on your unit tests.
We allow ourselves to regard this as a teeny tiny composition route.
Each unit test is just a composition route that composes a very tiny object graph.
So with this, we've seen that we can compose an app.
We've seen that, sorry, using dependency injection and loose coupling and using the composition route, we can compose an app and we can have that composition route living in the app target.
We've also seen that introducing a composition route means nothing for Swift UI previews and nothing for unit tests.
The last thing I want to mention is dev apps.
That's something we've recently started adopting at shape to iterate on features.
Christoph talked about this yesterday as well, but called them preview apps, I believe.
And these are separate app targets that launch directly into a specific feature in our app.
And in our app, we have four of those.
The onboarding dev app, the map dev app, the details dev app, and the profile dev app.
So if I want to work on the profile, I'll just launch the profile dev app and I'll start working on it.
And these dev apps typically rely on stop data and mock behavior.
But what's important in this context is that they become straightforward to create when you have loose coupling, initialize injection, and you adopt a composition route.
Because each of these dev apps live in their own app target, and that app target is really just a composition route layer, similar to the app that we just saw, except they're much smaller because they only contain a single feature, right?
If you want to have a look at this example project and if you want to see the dev apps or any of the other things we've discussed, please go to , github.com,  slash shape HQ slash coffee shop example, where you can find the entire code for this.
And here we've seen how pure dependency injection and the composition route enables us to build loosely coupled Swift apps.
And if you think that's interesting, I recommend that you read this book, dependency injection, principles, practices, and patterns, by Steven Van Gersen and Mark Seaman.
That's where I've learned most of this and then I've just tried to adapt it to a Swift-based app.
And if you think moving code into Swift packages and dev apps is interesting, then, well, go back and watch Christoph's talk again or read this article from Michael Bagan at Airbnb called designing for productivity in a large scale iOS application.
That's where I found my inspiration.
And if merge is more your thing, then come find me after this talk, I have some pins and stickers that I'd love to hand out.
And then I encourage you to think about how you can use pure dependency injection and the composition route to build loosely coupled apps.
And that's all for me.
Thanks.
Thank you.
Thank you very much.
Thank you.
We had some questions, but let's start with something that kind of made a questioning.
In your app target, if you have to inject lots of things, how do you manage the maintenance?
So does it get too big?
It doesn't grow too big?
That's a good question.
Your app target will grow the bigger your app is, because you create all your objects up there.
And then it's really up to you to figure out how do you logically organize this, how does this fit into your head, splitting it into components that make sense in different Swift files.
Yeah, I've taken a few different approaches for that in different apps based on how it kind of makes sense in those.
But I think in terms of maintenance, what I really like is that it makes it easy for me to swap out a dependency.
Because I can always, like, it's just easy to locate the exact point where I'm actually creating this object and just return a new instance, as I showed.
So I think, yeah, there's something to be done in terms of maintenance and in terms of logically organizing your code.
But you quickly harvest the fruits.
So I want to stress that when you introduce a new dependency in one of your feature packages, and you inject that through the initializer, that will surface all the way up to your composition root as a compile error.
And that's really good here, because it makes it easy for you to locate the place where you need to inject that dependency.
And this is in sharp contrast to using property injection, where you usually have to deal with optionals.
Which in terms means if you introduce a dependency, you don't get a compile error.
And sometimes in your project, you might have something that is already a bit of a dependency injection already installed.
For example, if you use SwiftUI, you have the environment.
Do you have an opinion on using that?
How does it mix much or not at all with doing dependency injections that way?
Yeah, I mean, totally use the environment property, if that's your thing.
It's definitely not mine.
Because I don't like doing my dependency injection like that for several reasons.
And I just want to highlight some of them.
One, it only really works with SwiftUI views, as far as I know.
I could be wrong.
And second, when you introduce an environment key, you're also forced to provide a default value for that environment or for that dependency.
And in my experience, I don't think that's a good thing.
Because if you have a default value, then you start hiding your dependencies.
Because what if that default value is unsafe to use?
For example, in a unit test.
What if that default value creates a network request?
That's a problem.
And secondly, and maybe even one of the most important things to me, is that your dependencies are hidden.
So you don't really see them when you call the constructor.
You're not required to inject them.
You need to know about the internals within the SwiftUI view to know what you need to inject using the environment view modifier.
Yeah?
Just another...
Basically, the same question, but different flavor.
It's like, there's a few libraries out there that does...
That help you set up dependency injection.
Is there a point to use pure Swift or one of those libraries?
Or is it just a preference that is just personal?
Yeah.
Sure.
I will actually make the same point as they do in the book that I just mentioned.
Because I think they're right.
When you start using a framework and you do that in all your modules, in all your Swift packages, then you somehow tie your code heavily to that framework.
Which I believe makes your code less maintainable.
Because you drag in that dependency.
Whereas when you use initialize injection, you harvest a lot of fruits, like the compile time errors we just saw, with very basic mechanisms.
So I'd say if you want to use one of these frameworks, use it in your composition layer only and rely on initialize injection in everything else.
So when we were discussing about your talk, you were saying...
Okay, I expect people to ask me about routing and navigation.
So actually people are asking about that.
Okay.
So I guess the question is how do you handle routing and navigation?
The cheeky answer, but also the real answer is that the composition doesn't really care.
If you need to do some navigation from one feature to another, then inject something that can handle that navigation.
I mean, we saw an example of how we did it here.
It was just using view builders and then the map decided to present it modally.
But it didn't know which view to present.
But you could inject whatever you want to call it, whatever pattern you're using, a coordinator, a presenter, whatever works for you.
The composition doesn't really care about that.
You could also use some...
But then it starts getting a little more elaborate for a short answer, but you could use some callbacks out to the composition route where you then have a coordinator living.
But I don't know if I would go that route.
Awesome.
Let me see.
That's an interesting question.
How do you deal with Apple pushing tight coupling, like the add fetch request?
How do I deal with it?
I sleep bad at night, first and foremost.
I think Apple...
Some of the things they're doing with Swift data...
You mentioned the...
What did you mention?
The fetch request.
The fetch request, right.
That's not really my cup of tea.
Because it does introduce tight coupling between the view layer and the data layer.
Now I know there are some things you can do in Swift data to create a model container that only lives in memory.
And you can use that in your unit tests.
And that's all fine and dandy.
But you still have a tight coupling to Swift data.
Replacing Swift data is not easy.
So I like to do whatever I can to get rid of that.
So in this example project, I've actually gotten rid of it and implemented some wrappers around Swift data.
Those of you who have used Core Data before probably know the fetched results controller that you can use in your view models to fetch data.
And I've implemented something similar to that in this app.
So I'd love to discuss this.
But that's actually a pretty good example to show how I deal with this.
And how is...
So how can you phrase that?
So specific about Swift data.
Let's say it's something that can be structural to your app.
So would it make sense to always make abstractions around it?
Or would you actually...
Like, in some cases, say...
It's so coupled to my app that I won't fight it.
Yeah.
Absolutely.
It absolutely doesn't make sense to create abstractions all the time.
I'd say if something is your...
Is in your domain layer of your application, then go ahead and use it.
This app is tightly coupled to showing coffee shops.
It's not like I've made the most generic app in the whole world.
But also when we kind of discuss what to couple and what not to couple, we usually think in terms of volatile and stable dependencies.
Volatile being those making network requests, those being non-deterministic and so on.
And those are the ones we want to hide behind an abstraction.
Just a practical question is...
When you're telling...
You have your feature packages.
And you want to have your app handle the composition root.
I've seen sometimes in application people doing a smaller composition root inside the package and then having the application just dispatching this and saying...
Okay.
So this feature, I'm going to call that.
And it's going to handle everything else.
Is there a downside to having that?
That's a good question.
I'm not really sure about that.
I'm not sure how that actually works.
Intuitively, I'm not so fond of it.
Because it means that my...
Or maybe I'm misunderstanding.
But it sounds a bit like my Swift package becomes a little less loosely coupled to the entire app.
And I don't like the thought of that.
But maybe you can get around it somehow.
But the picture is not really clear to me, honestly.
All right.
Thank you very much.
Thanks.
Awesome.
Awesome.