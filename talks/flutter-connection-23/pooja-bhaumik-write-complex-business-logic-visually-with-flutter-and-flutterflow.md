---
slug: >-
  /talks/flutter-connection-23/pooja-bhaumik-write-complex-business-logic-visually-with-flutter-and-flutterflow
date: 2023-06-02T00:00:00.000Z
title: Write Complex Business Logic Visually With Flutter & FlutterFlow
author:
  - Pooja Bhaumik
video: ciO85zG8r2A
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/ciO85zG8r2A.jpg
slides: null
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

POOJA BHAUMIK: Bonjour.

So hello.

I'm Pooja Bhaumik.

I'm a Google Developer Expert on Flutter and a Developer Advocate at Flutter Flow.

And how many people are here French?

Like, I mean, just raise your hand if you're French.

That's a lot of people.

So I've heard that French people can get mad if you butcher the language.

But can I try?

All right.

So I forgot.

Wait.

What was it?

OK, it was something like, "C'est un plaisir d'être à Paris"

So I'm pleased to be here in Paris, coming all the way from India.

And I'm going to be talking about Flutter Flow.

And have you heard of Flutter Flow, or have you heard about Flutter Flow from Flutter Forward this year?

Anyone who has heard of Flutter Flow?

Awesome, awesome.

OK.

So a little about Flutter Flow is that it's a UI visual builder that lets you build Flutter applications in a low-code way.

Now, the thing with Flutter Flow is that people kind of assume that, OK, you can build UI with Flutter Flow easily, which mostly all local platforms let you do.

But FlutterFlow is slightly different.

Like, of course, you can build UI.

I mean, this is already built.

You can build UI fast with Flutter Flow.

But what I want to cover is that how we can build complex logic in Flutter Flow in a local way and also use Firebase and Flutter code inside the Flutter Flow platform and build applications even faster than Flutter can.

Right?

So I just want to make sure that I'll let you know that at the end of it, we do get a Flutter application.

So you're not moving away from Flutter at all.

So at the end of the day, you get back Flutter code.

But why do we want to build with Flutter Flow?

I mean, there are a lot of reasons.

But it's boring.

I mean, isn't it better if I just show it to you?

So we're going to build something today live.

OK.

All right.

So we are building-- get ready for it--

Kahoot!

And this will be with Flutter, Firebase, and inside a Flutter Flow application.

So before we actually move on to the building part,

I want to make sure that you understand how the Firebase collections are structured here so that you understand when I'm building it in-- or querying it in Flutter Flow.

So let's hope-- yeah.

So in this case, we have a Kahoot Quiz Firebase Firestore database.

I do have certain stuff already created, which is I will be showing it in the Flutter Flow platform.

If you see it here, this is the Flutter Flow platform.

And hopefully, this is visible for you.

So here, if you see, you can actually see or create your schema and easily see what the games collection is, which is the main collection here, which we are saving a game info.

In this case, game info could be the game status and preparing, waiting, playing.

That could be the status.

And also the game code, which is the room code for you to enter into the game.

So it's kind of a unique identifier.

Then we have the question list, which I have prepared, which is all the trivia questions.

And then we have the current question, which is what is the current question that is currently being played or viewed to the audience?

And we have the last ask time, which is, OK,

When did this question start that time?

So that we can actually see how much time it took you to actually answer the question.

And depending on that, we will actually calculate your score.

And also the answers count, which is like all the people will be answering the question.

So we will increment the answers count.

And inside it, we have the players sub-collection, which has the player ID, which is nothing but the user

ID in a way, the nickname, the score, and a score list, because we're storing a list of scores for each question.

So each index corresponds to the question index, and then the cumulative score, which is the final score.

This is how the schema looks.

So I'm getting--

I hope you understand it when I actually start building the Flutter application.

So I obviously have done the UI part of it, because I think you're not impressed by the fact that it can build UI fast.

But what we're going to do is we are going to first build-- query the Firebase collection.

So in this case, we have this page where we have-- we will probably have a list of games, right?

So in this case, we kind of have-- if you see, there is a list view, which we are familiar with.

Inside it, we have the row and column.

Again, you're familiar with this same concept in Flutter.

And we have the text and text.

So each item in the list view is prepared.

So it's kind of ready.

But now we have to get this list from the Firebase collection.

So in this case, we have the list view.

And on the right side, if you see, there's something called a back-end query.

This is where you can actually do any kind of data queries, like Firebase queries, Superbase queries, get the document API calls, et cetera, so any back-end data query.

In this case, I will do a query collection.

The collection is the games.

And I just need the list of documents.

I don't need any limit, no filters, no ordering.

And make sure the single time query is checked off, because I want the real time data.

So I confirm it.

And now it says that all my list items are going to be populated with that query collection response.

All right, so it did create something in the UI.

But if you see, there is still some static data.

So in this case, it's a static 3456, but I need to change it to the actual Firebase data for each item.

So in this case, I can here set this variable from a source.

Now, this source could be anything.

It could be an app state, page state.

It could be date time.

It could be a custom function, random data, sample data.

But what I need is the games document that is now created for you from Firebase, which is each document of game.

So I do game info, and inside it,

I make sure that this is the game code.

I confirm that.

And here, instead of waiting, this would be game's document, game info, game status, confirm that.

Now, if you see, there is a Join Game button.

And basically, I need to make sure that they are only enabled-- the button is only enabled when the game is not preparing in the preparing game stage.

So here, if you see, there's a lot of properties like the width, height, et cetera, et cetera.

But there is also a button disable option.

So in this case, I'm going to click on this.

And I'm going to make sure that the single condition-- so you can set a single condition, a multiple condition, or whatever it is.

And the first value is games document, game info.

In this case, the game status.

Confirm and make sure if the value is preparing-- so I'm going to hard code the value to preparing-- it will be disabled.

So I want to run this, but currently I have one error here.

So if I click on it, it will tell me exactly where the error is.

And it will take me to that place.

So that way you know when your error occurs, where the exact error has happened.

So in this case, it says that when you click on Join Game, it actually opens a bottom sheet.

And here, this is basically the Action Flow Editor where you can define your entire action flow.

So here I'm actually opening a bottom sheet and giving it an Enter Name component, which is a UI component here or the UI widget here.

And I'm sending some parameters here, which is the room code, which would be, again, games document, game info, game code, confirm, and games reference, the document reference, which is also going to come from games document and the reference.

So now I have passed it to the component.

The error is gone.

So now I can build this on browser.

And by the way, this is built in Flutter, the entire thing, on browser, Flutter web, actually.

So let's see if-- is the internet not working?

Yes, OK.

All right.

So this will take some 30, 40 seconds, like any Flutter application, to actually render the build mode.

So I'm going to wait for that.

And let's see what the next thing is.

So once we have done the querying the Firebase collection, I will show it to you once it runs.

But the next thing is actually an authentication.

So when you do join the game-- so if you see, this is the bottom sheet that's going to happen when you join the game.

And when you do join room, I want to make sure that the user is authenticated into the app.

But I don't want any email ID, password, or anything else.

I just need an anonymous authentication.

So in this case, I can do that by-- let me see.

So I can do that by, again, going to the ActionFlow Editor.

And as you can see, you can either create an action or a conditional action.

In this case, I just need a single action.

But here, there are various actions that you can do.

Here, you can do a Firebase query, API calls, navigation, uploading data, et cetera.

But what I really want is auth, so login.

And auth provider could be email, Google, blah, blah, blah.

But I want anonymous.

And it should be for the collection users.

Remind you that users collection are automatically created for you if you enable authentication in FlutterFlow project.

So this collection will automatically be created for you.

So you do the auth.

And that's it.

The auth login is done.

But let me see if this is--

I don't know if this is the internet or not.

But hopefully this will run.

So we did authentication.

But once we have done the authentication, what now?

Like, if you see the Firebase collection, each has something called a players.

And each have a player ID, right?

And a nickname.

And that is coming from the bottom sheet, if you remember the bottom sheet.

So here, what we are going to do is that we are going to do a create document kind of thing.

So what you can do here is you add another action after login.

So in this case, it will be create document.

And again, which collection do you want to create it to?

It will be the players, which is the subcollection.

And it needs a game reference because it's a subcollection to a game document, right?

So it needs a game reference, which is, again, coming from the parameters that we had set.

We had actually sent it to the component.

So we have the game's reference, which is cool.

And it says, OK, what do you want to set it to?

So the player ID could be-- let's see.

We have the authenticated user object also created for you once you did the login.

When the login-- if you see it here, there won't be an authenticated user object created before this step. But after this step, it created authenticated user object. And now you can get the user reference from it. You can also do the nickname, which is a widget state. Also, you can get it from a variable from the widget state here. Which is nickname.

Now let's see if this is running so I can show that to you.

All right.

So it takes some time.

We know.

All right.

So we do have the page now basically populated from the Firebase Games collection, if you can see this preparing, preparing.

If I change, suppose, this to waiting, this is a real-time one.

So if you see, this is now waiting.

And now you can join the game.

Right?

So that is working great.

If I do join game here, there will be a bottom sheet.

And when you click on it, it will do the join room.

But since I ran this before I did those code changes, probably I need to do an instant reload.

So here if you see this, I did that.

But there was one step that is still left.

Here is where we have an app state which is taking in your authenticated state, it takes the current user reference and the current game that you have chosen, that reference in your local state so we can keep it on for the entire state.

So in this case, we need to set it once the login is successful.

So I'm going to again create another one here and make sure that we do app state update.

And it's going to ask you what do you want to update?

I want to do the current game reference.

Okay.

One thing.

I'll do the current game first so that I don't confuse you.

But here is the game reference.

Great.

But if you see, in this document call, we can also return the response and just play with it.

So in this case, I can do a logged in user.

So this is a variable that basically is returned back from Firebase that I can maybe use it for further computation.

So what I need it for is that when I actually

So, this is where I get it. I got it from this back-end call response.

So, this is kind of ready.

So, if I now instant reload here.

There is probably an internet issue why this is late.

But so, we do need to set the player reference to the player.

So, I'm going to set the player reference to the player.

And then I'm going to set the player

We do have the first three steps probably ready.

So in this case, I can do a join game.

I can do the name.

Join room.

And this will put me inside.

So this is a previous game that I played.

And this is going to have me on the list of the people.

And yeah.

So I can log out as well.

Now, we did this.

We did also creating documents in Firebase and updating the app state.

But we also want to do something with UI here.

So in this case, when you did the-- when you joined the game, you saw a list of users.

That's one UI component.

The reason why it also had some UI issue at the end is because if you see, if you probably game room page, if you see here, there is one component here, which is for the waiting stage.

And there is another component here, which is hidden here, which is for the playing stage, the game stage.

I want to render my UI according to the game status.

So in this case, we probably would have done some if-else condition in code.

But in the end, it is probably going to be that.

But here, what you're going to do is that you're going to enable a condition visibility.

And you're going to set a single condition where the first value is going to be, again, game info.

And this is going to be game status.

And this is going to be for the value, specific value of waiting.

All right.

And I don't want to really do this again, write this again for the second state.

So I'm just going to copy this variable.

And in the playing state, I'm going to, again, enable the condition visibility and just paste the variable and change the specific value to playing.

So now in this case, if you join the game, but before that, instant reload.

Because this will not work otherwise.

And then I will panic.

So let's reload this.

And join game.

I'm gonna make something weird.

And if you see, the error went away.

Because now it's only going to be the waiting stage.

But I can show you the playing state as well.

So, if I change this to playing, and if you see here, it's basically showing something.

Did I miss out something?

I don't know.

So, basically, here the UI was supposed to come, but it did not come.

But it's -- this game is about to start thing.

So I don't know if I have the spelling wrong or not.

I don't see that there's a spelling wrong.

But you get it; right?

So I will not waste time to fix debugging this on stage.

Because we have one last thing that I want to basically talk about before we actually play the game is that what if we have a very long, conditional, complex custom business logic action? Now, this is my favorite part here. Because you all are Flutter developers and there are a lot of times that you realize that you do not want to lock in your cell

-- lock yourself to a platform because it does not let you do custom work. It does not let you code or add custom code kind of a thing. So you're kind of lost. But here you you won't be lost because you can use your Flutter code,

Flutter packages, Dart code, et cetera, all in the Flutter Flow platform.

So instead of actually doing this by self,

I'm going to be showing you-- basically, here I have the actual project.

So here, if you see, this is the actual-- you know, the player one where you can actually give the answers.

And this has a lot of complex logic where first we are going to make sure that the answer that you have selected is correct or not.

Then we are going to-- if it's true, then we also update the scores.

And we also update the answers count.

And when we do update the score, we are also calculating the score according to the time that you have taken to answer the score.

Because if you've taken 15 seconds to answer the score, your score is going to be lesser than someone who has taken one second to answer the score.

Now, that's too much of logic in a way.

And can Flutter Flow do it or not is a question.

But here, I'm going to open this.

And this is basically the logic for that button.

And one thing that I really, truly love is that I can understand by just looking at it what exactly is the flow of logic going through.

I have to click on it to actually read it.

But you can also add documentation to each of your steps.

So when the Flutter code is generated at the end of the day, you will have some documentation for each step that you have done.

So now let me just go through the steps here.

First, we basically check if the index in the list of options, in the four options, is that the correct index or not.

Because my correct index is stored in each question in Firebase, right?

So I first check that.

If it's true, I update the answers count.

But I also have to basically check if-- you know, that is this answer already given?

Is it a fresh answer or not?

If it's already answered before, I will not be updating the answers count unnecessarily.

Like, if you're just constantly clicking on the button,

I'm not going to keep on updating the answers count.

So I basically do a check on the score list that is this index already there?

If it's not there, it's a fresh answer.

But that's too much of work to actually do it in Flutter Flow with the UI.

So I thought, let me just write some code for it.

So here is all the custom code.

So you have custom functions, custom widgets, custom actions.

So custom functions is basically a simple input-output Flutter code.

Then you have the custom actions, which is custom functions on steroids, kind of like.

You can do so much more with actions.

And you can also add it to each button user interaction kind of thing.

Custom widget, you get it.

So here I wrote a custom function for, suppose, getting the incrementing the answers count.

I don't know if you can probably-- you can't see it.

But then if the current score already has this key, the index key, then we increment it by zero.

Otherwise, we increment it by one kind of a thing.

You also have the other code, like, OK, how do we add the item to the score list?

You can probably do that in FlutterFlow as well, but I was more into writing this myself.

And this can be used in the UI in FlutterFlow when you actually are creating the custom action here.

So here, the answers count.

It says that increment the answers count by a certain value.

Now, in this case, I could have done a 1, or like a static value 1.

Or I can, in this case, basically go to custom function and increment answers count.

And I supply the parameters, which is the score list and the current question.

So in this case, I am using a Flutter code inside the Action Flow Editor.

So basically, you could do any kind of Flutter code.

And if Flutter Flow does not have that feature available, if Flutter has that feature available, it is possible probably in Flutter code because you can write the same code here and somehow import it into your UI and your user interaction kind of a thing.

So yeah, and then I update the score list.

And at the end, I create a cumulative score.

The best thing about this custom code is that I can test the function and write test cases right in the platform.

So in this case, if this is a list of five and six, and I am checking if the current question index two can be added or not, is this a fresh score or not,

I can just run it here itself and run my test case here.

So you can add all the test cases here itself and make sure that everything works fine before you start using it.

And if you are feeling like you don't want to actually write the code, we also have OpenAI itself.

So you can just explain the thing that you want, and you get the code.

Just make sure that your arguments are perfect here in case what you exactly want from OpenAI.

So that's the entire thing for basically--

I mean, I have showed only a part of it.

But basically, we did query collection.

We did adding documents.

We did updating app state.

We also did custom code in FlutterFlow as well.

And if you can understand that there is a lot of custom things that we can do with FlutterFlow.

But for now, in the interest of time,

I will go and play the game.

So I obviously had the backup ready.

I mean, I'm not going to be deploying it on stage.

Come on.

So I already have this ready.

Just log into this.

And before you do that, let me make sure that you don't get to the wrong game.

So this would be preparing.

And yeah, so get to the kahoot-quiz.flutterflow.app, something like that.

And once you're ready, I will move to the host tab where we will be showing the Kahoot questions.

And you're going to be actually playing with us, because we have a lot of stickers and t-shirts.

Probably not a lot.

I've hidden it for--

So we have a tea badge, if you like tea.

So basically, it's a widget.

So if you see it on Flutter platform, it's actually a widget, but we changed it to tea.

And we also have coffee widget.

And we have some stickers.

But it's only for the winners of the Kahoot.

So there are going to be 10 winners from the Kahoot quiz, which will be on screen.

And they are going to get these stuff.

So play seriously.

If you're done with this, I will get to the host app.

So can I move to the host app?

[INAUDIBLE]

Yeah, so we have more goodies.

But yeah, so I only have 10 winners on stage.

After that, you guys figure out how you're going to distribute among yourselves.

So I'm not going to be part of that.

So if you're done, I'm going to move to the host app, which is somewhere here.

All right.

So in this case, this is my-- so there are two apps that we built in Front of Flow.

One is the player app that you're actually playing with.

And one is this host app, which is going to have the questions and also the images.

Your app will not have any images.

So you will have to see the screen to actually see if there is an image on the question.

And yeah, just answer like you feel.

So I think this is the one that I created for you.

So I'm going to be joining my game.

And this is the game code 4058.

And I'm going to allow players in.

So now things are going to start popping up.

So I'm trying to find my phone.

But yeah.

Oh, so I was supposed to tell you this, that please have your names a little original if

I have to call you out.

But yeah, sure.

Okay.

Baptist.

Sure.

Cool.

And I mean, they're mostly real names, so I'm guessing that's pretty cool.

T. I don't know who T is, but I'm not going to be fighting for you if you win it.

So if you're ready, we will begin.

But 4058.

Creative.

Creative.

So much.

[LAUGHS]

Have your real names if you really want to be on stage to get the goodies and all.

But yeah, I'm not going to be fighting on who gets it.

So shall I begin?

Anyone left?

Awesome.

Start game.

This changes the game status to playing.

Woo-hoo!

What was the Flutter web project originally called?

All right.

What is this piece of technology?

Are you guys too young for this?

The function that is a starting point for any Dart program.

How do you say hello in French?

I shouldn't have done this.

[LAUGHTER]

What does IT stand for?

There are some trick answers here.

Are you really discussing all this?

I'm ashamed.

[LAUGHTER]

Flutter's 1.0 launch event was called this.

The new rendering engine that Flutter is experimenting with is called -- constraints go down, sizes is go up, complete the sentence.

What is the framework language used to write the Flutter Flow builder?

I heard that.

[LAUGHTER]

If you wanted to, what type of custom code does FlutterFlow allow you to add to your project?

Which of the cities are not in France?

I don't know.

What is the name of this plushie?

If you don't know this, please get out.

Scaffold is a dash widget.

It's dash.

No, no, that was not the answer.

I mean, anyway, it doesn't matter.

Dart is a dash programming language.

Dash works for everything.

Did you enjoy Pooja's talk?

You know the answer for that.

You know you could lose if you don't answer it right.

All right, are you ready for the results?

Oh, 99 answers.

Are we really 99 people here?

Can one person join?

All right.

Woo!

[...]

So thank you so much, Pooja, for this amazing talk.
