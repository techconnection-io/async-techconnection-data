---
slug: >-
  /talks/frenchkit/swift-connection-2024/etienne-vautherin-how-apple-intelligence-infuses-and-distills-its-models-into-the-app
date: '2024-09-23'
title: How Apple Intelligence infuses and distills its models into the app
author:
  - Etienne Vautherin
video: xCIMaF1sqDY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/xCIMaF1sqDY.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Etienne
So, I'm Etienne and my activity is to build baby apps with software developers. What are baby apps? Yes, baby apps are apps that are made for practice technologies, for proof of concept, for minimum viable product.

The idea is that we are at the beginning of the app and we just want to have some training, workshop, things like that, or to test very specific topics on the application. I've done this kind of work for many years with large companies and now, today, I will do these baby apps on my own activity. So, this is something that could be funny, but in fact, this is a very serious activity.

For people in France, I'm working with organisms that do certifications and that are not funny. So, we have spoken of the past, of the present, and now we go to the future. And the future for mobile applications is this kind of interaction with the app.

The idea, as presented by Apple, is to have this kind of conversation between the user and your application. So, this is what Apple has shown during the keynote and the other event for announcing Apple Intelligent. So, today, we have the series of shortcuts, which in fact, give something relatively simple because the user designates the application he wants to talk to and the sentence is built around something which is always known.

With Apple Intelligent, in fact, the user can compose functionality or functionality of the application and elements without any app reference. So, that means that, in fact, the developer needs to expose this functionality and element that the user will compose later. So, how does it work?

In fact, it begins with what Apple calls domains. Domains are the color, you see. Apple defines 13 colors for covering current domains, beginning with photos and mail, but they have announced 30 domains.

In this domain, you define schemas. Schemas are the shape of the thing you want to expose to Apple Intelligent. So, you see, it's very conceptual, its color, its shape, but we don't have a very precise definition.

The precise definitions come with some code and, in fact, the application defines the custom implementation of a global concept, a concept which is common to all applications, you see, but each of your applications can define something more precise in this domain and in this schema. Here we have the example of an application which defines an open baby intent. That means that we want to display something and the thing that we want to display is generally defined by the target field of the intent.

Here we have this and you see that we have the main function of the intent is the perform method and, in this case, as we will display something, this method is run on the main actor. The baby entity is something that is a custom object or structure which is defined by the application itself the same way with the struct baby entity. The both are using a macro, so macro just say it's an intent, it's an entity, and this intent uses the schema .photo.openasset. The .photo means it's on the photo domain, openasset is the intent to open the asset. For entity, the same thing, photo domains and the asset that we define is the baby entity. That means that all applications have the same structure for defining things that are similar, but the implementation that you are doing is your implementation. So we have this application which defines an intent and an entity inside the photo domain.

This one defines also an intent and an entity, but this time it's on the male domain. So we have the schema of the intent is send a draft and the schema of the entity is a male draft. So at this time this is very simple.

These schemas are defined by your application and when your application is installed on the user device, these definitions are going to what is called the app intent toolbox. It's something that is a kind of store, it's not really a store, but it's a place where Apple Intelligence references all the schemas that have been defined. This is the only technical slide that Apple gives us to explain Apple's architecture.

You see that in fact we are only working with the arrows. You see the applications are on the top, not the full top because the full top is for the user. You have the applications and we are working between the app and these two blue boxes here, the app intent toolbox and what is called the semantic index.

The semantic index is in fact what we will use a lot in the next slides. But we have a problem, not really. Now how does it work to create the intent that the user wants to do with the sentence, the prompt he gives to Apple Intelligence?

We have a first step which is to transform the natural language to a conceptual intent. The domains are trained, are pre-trained and something that I have not explained is that Apple Intelligence has not a full pre-training for all a universal way to converse with the user. The domains are a way to have smaller models for the topics the user is using because we need to run on a smartphone so we cannot do what a chat GPT or something like that is doing.

So we use the domain to transform the sentence in a conceptual intent, the intent that fits with this sentence. Then Apple Intelligence compares this conceptual intent with all the intents he has in the tip toolbox and if he finds something that matches very well, it generates this intent. In fact, it instantiates the intent that has been defined by the Swift code we have seen previously and it runs it calling the perform method.

Now we will see what it means for an application. The applications, for example, your application could be with this kind of architecture which is very common. You have the model, you have the view and the view model MVVM.

So Apple Intelligence will go with this kind of application and now we need to make the action that is defined. Today an action in the MVVM is frequently done this way with the unidirectional data flow which makes that when the user clicks a button you run an action which modifies the model and the modification, the update of the model will create a new state and the new state will update the view. To do that we need to have a reference to the model because we are modifying something in the model with this current way of doing the data flow.

So this is a way to get a reference to the model. This way is perhaps a little complicated for applications which could be simpler. I just instantiate a model when the view is instantiated but we are going this way because when you want to have the intent to run the same application you will need to have the model which is accessible from the intent.

So you have the view, you have the app intent and the both could use a common action. You could define two different actions but it's better when you're doing the same thing to have the same code doing the same thing. And the idea of the intent is frequently to be run in the background.

When you have the example of when mom's flight landing, you don't want to have the switch between applications. So each application which gets some data will run silently in the background and pass the result to the next application and the last application will display the result to the user. So very frequently in fact you run the app intent in the background with no UI.

So as your reference to the model was defined as, I don't remember the name, an environment in SwiftUI, you have to get another way to reference the model and this other way is an app dependency which is defined by the app intent framework and the app intendency is a way to get something. It's a kind of singleton which is Swift 6 compatible in fact. So we are using this kind of thing and you see that now in the init of the app we are using the same environment code when you call the scene, the body of the app.

But if we never call the scene you need to have a reference to the model and the reference to the model is defined in the init with instantiation of the model and I have not a mistake in this but it's not very a big problem. And when you need to perform the intent you have the dependency which defines, in fact, who tells app intent to get the matching definition in the app dependency manager. So now we have the way the intents are executed but we need to have the semantic index definitions and now we have really the problem because the semantic index will contain user-specific data, not really the data but it will explain what the user means with this word and for a user a word may tell something, for another user the same word could tell another thing.

So we have to install Apple Intelligence on a user device because it will use the data of the device and we have the problem because in Europe we cannot run Apple Intelligence before next year. Hopefully today in Paris we can access the Sequoia toy shop and the Sequoia toy shop could give us some very cool baby tools like the writing tools. So if you want to test writing tools with your machine you can use it on sequoia-version.one but you can do it. However, the writing tools are on the upper map of the whole Apple Intelligence so it's mainly for baby users. If you are a baby developer you need to go back to the Sequoia toy shop and to get these lovely tools. We have two lovely tools.

These tools are similar to adult items but they are not yet fully functional. So for example the label on the rag box says that it's a little rag cuddly toy that receives all personal secret meanings. So we have this lovely toy to do that and this is a serious tool in fact.

When you modify the model or when you use the model in the general way you use a unit of data and this unit of data is defined by a NAP entity. A NAP entity has two major functions. It's one to be retrieved when you need this information so you have an ID and you have a query which are associated to the entity and the overall role of this entity is when you want to use the semantic index is to update the semantic index and this is done with the indexed entity.

The indexed entity is an entity which has an attribute set and this attribute set is in fact a technology which comes from a core spotlight and which defines some attributes like a name, a location, a tag, every information you want to add to describe what data is contained in the entity. An important thing is that the entity in general is a protocol so it could be a very simple thing to add this protocol to data in your model. In fact it's a very bad way and we could discuss that later.

So here is a full flow now that we have a way to populate the semantic index. When the user make a prompt you have the intent generation that we have seen before. This intent generation generates the intent.

The intent runs the action which could modify or not the model but if the model is modified you update the index with the new value of the entity and so the semantic index is synchronized with the meaning of what is done by the user and to synchronize the meaning we have this way but we have also a special domain which is in AppSearch. In AppSearch the blank, the white train here is something which calls the UI of the app to make the search. So this is an example with the UI of mail.

When you search a mail you type what you are searching and in the first time the semantic search suggests you a number of options that he thinks could be relevant for that and if you choose one it replaces your first request with one of these choices. And when you have the final choice which is search the user will click on the this example the mail which match with the initial request he made. So this way you have you could associate a meaning to a mail you see and it's a very powerful way to populate the semantic index with real entities and say when the user speaks about Apple renewal invoice this is this mail and we could imagine that in the prompt when is mom's flight landing the mom's flight is something that has been defined this way by the user in a previous search and so now we can define the parameter that is sent to a flight tracker.

The flight tracker needs to understand what is the content of the mail. So the content of the mail has to be translated with what is called a transfer representation. A transfer representation is a list of ways to translate.

So you begin with the richer translation and you finish with the less with a simple transition meaning that you transfer more or less meaning in that thing. So we imagine that the flight tracker has a way to get a full text and to extract from this full text the information of the flight, perform the information of the flight, create an entity result, describe this result and display this as an answer to the user. We are going late so i will go faster for this part but here is a way you are explaining to the semantic index that the user has selected this suggestion and this result from the items that are displayed.

The first one is just to explain when an item is used frequently and it becomes a default item, a default entity when you don't precise what entity in the whole model you want to use. So this is a second tool which is a find in fact which will help us to define this kind of thing. I will go more rapidly.

In fact when you define two special queries, one is the enumerable query and the other is the entity property query, you have a way to search inside the entities in an implicit way in fact. So if we imagine this kind of thing, the problem is that you see the intent is defined as a train. You have only one engine and you could have several coaches but you cannot have another explicit intent defined in the way you speak to Apple Intelligent.

So with the implicit find you can have an implicit find intent which is called in the ping application and that will populate the second parameter in the sentence like add a pokemon waiting more than 10 to the last slide. The last slide is the blue parameter and a pokemon waiting more than 10 is the ping coach. So this is really my last slide but this is just the beginning and we have many things which are moving.

For example we received a new beta version on yesterday during the party so things are moving very rapidly and what I propose is just to have a special talk with each of you if they want so you could book and register using this code to discuss with me during 30 minutes or more. Okay so this is a quick presentation of Apple Intelligent. You see that there are many many other things to describe.

In fact it's a topic which needs a full day I think but I've tried to make the essential here.

### Zino
Thank you Etienne. So as developers we're used to having full control over our code and with machine learning in general but with Apple Intelligent in particular right we have to delegate a lot of things to systems that work magically behind the scenes and that may or may not be available that may or may not work. Do you recommend developers to get into that habit of letting the machine work because it's hard for developers not to How do you square that?

### Etienne
I think that we are already letting the control to the machine with SwiftUI. You only define how to display something but you are not in an imperative way. You don't say display this thing, display this thing.

In the same scheme here you define what is a kind of entity, you expose what is in this entity, you expose what the application could do and you let the user compose these things and Apple Intelligent calls you through an intent. I think it's natural. You cannot do things in an imperative way but the perform method is imperative because you are modifying, updating the model and you are doing things that need to be explained explicitly with a sequence of instructions.

But all the definitions are declarative in fact. So you just let the system to choose what you want to extract at one time.

### Audrey
Thank you. So there is a question which has been pushed by the audience and let's suppose you have two mail apps and both support the right mail intent. How will the system choose the right app?

### Etienne
I think that you have two instances, two entities which are available for, in this case, for the mom's flight. You could have one big mail application which defines one and another which defines one. You cannot have two mails which are the same, you see.

I think that the user in fact will choose one or another and perhaps will use more frequently one than another. And it's the way we update the search index. You see that one application is more frequently used or has been used more recently than the other and App Engine will choose this one between the both.

And if you remove one app, the other could take the wheel at this time.

### Zino
Thank you very much.