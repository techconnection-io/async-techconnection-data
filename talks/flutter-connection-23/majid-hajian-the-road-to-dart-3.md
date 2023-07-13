---
slug: "/talks/flutter-connection-23/majid-hajian-the-road-to-dart-3"
date: 2023-06-02
title: "The Road to Dart 3"
author: "Majid Hajian"
video: 8ic_lYBzpvU
thumbnail: thumbnails/majid.png
slides:
tags: []
year: 2023
conference: flutter-connection
edition: june-2023
allow_ads: false
---

OK, OK, OK.

Everyone ready?

We're going to run from now until 15 minutes.

And I know this is the worst time for giving a talk after lunch, because all the blood from here goes there.

And suddenly, the eyes goes down.

So and the funny thing is that I don't see any of you for some reason because of this.

But anyway, I have a plan.

So I have two special socks right now, which you can't really find it easily.

One is Flutter, another one is Firebase.

We're going to play a game.

And I will start my talk afterwards.

All right?

So I will hand over this sock from that row,

And this one from end that row.

OK?

So from now until end of the talk, it could be any minute.

You need to focus.

OK?

I know it's a lot of blood.

But whoever gets this t-shirt-- sorry, this socks-- when I say thank you very much at the end,

Let's keep in touch.

Thank you very much.

End of the match.

You should stand, whoever has this, and say, bingo.

That person gets the socks.

All right?

Ready?

All right.

Sorry.

Just hand it to that person.

Very sorry.

[LAUGHTER]

You ready?

All right, we're going to go to the road to Dark Tree.

I'm going to stop my timer.

I'm not going to say when I'm going to finish.

You will figure it out.

Disclaimer, we're going to talk about Dark Tree, but I don't expect you to understand everything.

OK?

You have time after the talk.

You can go through the slides.

You can go through the documentation.

You will understand more.

The purpose of the talk is, though, to show you the road to get you to the dark tree, and you see what you can do.

I exercised a lot, actually.

My name is Majid.

I am head of DevRel at the universities, and a GDE for Flutter and Dart, and a community leader for Flutter.

When I start writing code in Flutter, a typical scenario that I usually face-- well, you get some JSON.

Here's the JSON.

And well, sometimes you want to get some of these values, maybe three of them.

What you do in Dart-- well, you can actually return a list of dynamics, because the type are different, right?

And well, you get access to these indexes based-- to these variables based on the index, right?

OK.

What you do typically is you create a class, because this is not really type safe, right?

You get a list of dynamic or objects.

So not really type safe.

So you can create a class.

Nice.

Well, in a set of lists, you can return this class.

Who is doing this?

How do you get-- those who don't raise hand, how do you get access to this data?

I'm curious.

OK, it sounds good.

Well, in this case, you get a type safe.

You have a Dart object, a speaker.

Sounds good.

You sure do this, right?

Are you Flutter developer?

Am I in the wrong-- all right.

But in Dart 3 right now, there is a better way-- or not better way.

There's another option that you can do, and that's records.

Records are here to help you to define-- well, type, as you see, values here.

So I have this record on the top.

As you see, the records are defined by parentheses,

And the members are separated by comma.

Simple enough.

OK?

You can have positional and name parameters.

Let me tell you.

Tell me, please, you know what is positional and name parameters.

OK.

So then in this case, I can actually return tree values with records.

This is a type of record that I can return.

I can say now, instead of that speaker Dart object,

I want to return this record, which

I define each field of this record to have a type.

And well, then I get access to these valuables.

The problem is that-- or there is no problem here.

That's the way it works.

The records are immutable.

And you just have getter, and you get access to those, well, fields by dollar.

This is not really the way that you like to see the code, right?

You probably need a better way.

In fact, that's where patterns come.

Patterns usually-- don't worry.

You still have time.

Just pass it over.

Patterns are typically either destructuring values or matching values.

This is a destructuring recourse, as you can see.

So then I can get access to each of these fields.

As you can see, I can destructure them.

All right?

Sounds good.

This is pattern.

But what else I can do?

Can I name them?

We said that, yes, it is possible.

We can have name and positional parameters.

That's fantastic.

So there you go.

I can go and have these curly braces, very familiar.

I'm just going to go and return my name records.

Fantastic.

Then I get very familiar syntax.

Good.

There is a shorter way of accessing these values, where you can use this column and the name, which

In this case, it's going to assign the name or the key to a variable name as same as name, or age, or active.

So that's shorter.

OK, fine.

But what if I want to change the variable name?

Like, I don't want name.

I just want name one, for example.

What should I do?

So that also is another option that you can do.

You can just change the syntax slightly, say the key's name, fantastic, but then say what is your variable name.

In this case, name one.

If you have records that you want to ignore some of the positional, especially fields, you can simply use underscore.

Simple enough so far, right?

Is it simple?

Is it?

Really?

But can we just destructure records?

No.

You can also do it for lists and collections.

And as you can see here, I have another JSON right now.

So the speaker has a key and a list which gives me name and age.

I'm not that age, by the way.

I'm younger.

Well, you can now destructure it again, which is very nice.

And I deliberately wrote this syntax because I just wanted to show you how easy you can see where you can match and destructure the values.

Here is the case.

I can just put name in this case as my variable and age for the least here.

OK.

What else I can do?

In the previous example, I have a question here.

Well, usually you don't get this JSON like that, right?

You get it over network, like by a network request.

What do you do to make sure that these variables having the same-- let's say if for this case, age is not integer.

What do you do as a developer?

[INAUDIBLE]

Guard?

[INAUDIBLE]

War?

[INAUDIBLE]

Yes, scream at the back of people and put a lot of if statement.

If it's not null, if it's blah, blah, blah, blah.

Well, now in Dart 3, we have another option which is added to the if statement, and that is case.

Where in this case, you can actually mix it with this structuring.

And what it does, when you say you're expecting name as a string and edge as integer, it is going to check all of the checks that you need to do.

And if it's passed, then you get to that if statement block.

Isn't it nice?

Of course.

You can also turn it to a switch, exact same thing.

In this example, it doesn't really make sense to have a switch, maybe if it's easier.

But just an example.

All right.

But what if you want to guard your case in this case, or case in switch.

You have another guard keyboard, which is when, where you can also add another logical operation, let's say, here.

So for example, here in this case,

I want to say if everything is fine with the destructuring,

OK, and when the custom edge is equal to whatever of the edge.

Everyone understands?

Even if you don't, I don't think you say.

Yes.

Where is the socks, by the way?

There you go.

There are two socks.

There you go.

So you can shorten the when that I showed you, and even have these type of syntax.

I'm not really sure if I really like this or not, but this is the way that you can also put it to your-- well, here is the case.

You're destructuring.

Very nice.

But a typical example in Flutter-- who is getting team data like this in Flutter?

Or at least when you started learning Flutter years ago, you do that.

Let me see who is-- many of you are new to Flutter.

That is good.

So in fact, there is another way right now that you can simplify what you've done.

And that is expression in the switch, where you can omit the case and say, just check the type of the mode in this case, if it's light, and return the value that you are requiring.

That is very nice, because then now you can mix and match it with other features, like record and pattern and destructuring all together.

Imagine now you want to get a get setting just two values.

In typical scenario, you would do a class probably that has only two fields and, well, a lot of code.

But now with records and pattern and destructuring and expression, you can just squeeze it to this line of code.

All right.

Another example, who is doing feature builder?

Are you really Flutter developer?

That's a good one.

Yes, feature builder, or any type of these kind of widget that gives you a builder that you can have a switch to decide what to show when.

This is exactly a typical scenario for using now-- sorry, destructuring and using when and using expression and returning the switch value to your builder.

You can even do this simpler with this syntax.

You can use now even destructuring into a single snapshot and get the data and even omit the exclamation mark.

Okay?

That's a real example.

Another thing that I want to do, are you handling exception?

No.

Crashlytics will do that.

Well, if you handle your errors and exceptions, then you probably have seen this kind of implementation.

You're going to have a class maybe implementing an exception from exception and you're going to go and maybe create any type of exception you get from backend.

Email, password, not found, whatever.

Then typically you're going to transcribe or describe these kind of exceptions, right?

You want to say if it's for some reason user not found exceptions, I'm just going to say to user, hey, blah, blah, right?

Well, this is a typical scenario.

You can turn this right now to expression and destructuring and make it a bit simpler, which is very nice.

But what is missing here is, as you can see in my describe,

I deliberately omitted user not found exception.

And I can continue doing my code.

There's no problem with that.

It's very easy to kind of miss these kind of subclass classes, let's say.

So what should you do then?

Dart 3 then gives you sealed class.

There are many features to sealed class, but what is very interesting to me as a Flutter developer or Dart developer is to use it for these kind of scenarios where I want to get all of the subclasses into my switch, for example.

In this case, my compiler or the compiler is telling me, hey, you're missing one of the subclasses here.

You need to add it here, otherwise you cannot move on.

We're getting to the end.

Where is the socks?

Good.

I still have two minutes.

So, well, these are the typical scenarios for mobile and Flutter development, if you have done any.

Apparently, many of you have done that.

So very good.

And I'm just joking.

This is a typical scenario in many Flutter applications and Dart applications.

I just try to tell it in a way that I also use it.

And if you want to learn more about these features, there are a lot more.

I didn't want to confuse you.

So I just wanted to bring whatever is typical scenario of a Flutter development and give you a sense how Dart 3 can help you, show you this road.

There is one fact to my slides.

I showed you two pictures.

Can you tell me what is this fun fact?

I give another slice to person that says this fun fact.

No.

They are AI generated, by the way.

Thank you very much.

[APPLAUSE]

I hope you enjoyed the talk.

So it was mostly inspirational.

And congratulations to those who win the socks.

If you need more socks, please visit Invertase booth.

I'll be there and meet you.

Thank you.

Thank you, Majid.
