---
slug: >-
  /talks/flutter-connection-23/remi-rousselet-make-your-codebase-more-maintainable-using-custom_lint-by-creating-custom-refactorings-and-lint-rules
date: 2023-06-02T00:00:00.000Z
title: >-
  Make Your Codebase More Maintainable Using custom_lint by Creating Custom
  Refactorings and Lint Rules
author: Rémi Rousselet
video: xZQJftO1C-4
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/xZQJftO1C-4.jpg
slides: null
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

All right.

So today I'm going to talk about custom lint, which is a tool I developed at Invertase.

It's a tool for helping you to write lint rules and fixes and refactorings.

You're probably familiar with those because you likely use those daily in your daily jobs.

But the thing is here, you're able to make your own link rules so you can empower your developer experience quite a bit.

And so you probably already know the value of link rules and things like those, so instead of just explaining why you probably should use it, I'll instead consider showcasing you how writing linked rules is not that hard, and we're likely going to do a live talk together today.

So we're going to make a simple linked rule together.

Wow.

Oh, I forgot to delete stuff.

Give me a second.

Yay.

Spoilers.

All right.

So what we're going to do today is we're going to make a simple intro which is useful for a common pattern like for code generators.

Typically code generators are like a class or function which is annotated by something.

So here I'm using RiverPud.

And then when using code generators, you often have to subclass a specific generated class which is usually based on the annotated function or class.

So here the class is example, so I have to subclass underscore dollar example.

The thing is, if somehow I have to rename this, I also have to rename this, which is a bit tedious.

And I can maybe make mistakes.

Like if I have two classes, maybe I can have two classes with the same name almost like example two but I forgot to have example two here.

So it's a bit tedious.

So we're going to make a lynch rule which will highlight whether we forgot to specify an extent or whether we made a typo and with a quick fix for it.

So let's get started.

So what we have here is a simple application here which is doing nothing but using a real pub, it's using the code generator, which is here.

It also has build and install because of code generation.

Then we have custom lint installed as dependency.

And then we have our custom lint package installed.

I'm using a path dependency because our package is not published on pub yet.

So what we actually care about is our custom package here, which is right there.

It currently has no source code, just the pathspec.yaml.

So here I have a few dependencies.

I have the dependency on the analyzer package, which is used for analyzing Dart code and reading the content of a Dart file. a plugin, which is what customint is built on, and we are going to use it here for exposing utilities to modify Dart files.

And last but not least, customint builder, which is a dependency that all packages which emit lints must depend on.

All right.

So that's for what we have currently.

So let's just get started.

So when we want to make a package with define lint, the first thing we have to do is we have to create at the root of the lib folder a file which corresponds to the package name.

Custom lint.

Let's call it package.r.

Right?

And then in here we have to define a function which is called create plugin.

Here let me import something.

Right?

Basically it has to return an instance of a plugin-based object, which is a custom class you'll make which will represent your plugin, and then we have to overwrite the getLinFull method to override a list of LinFulls implemented by our product.

Currently we don't have any, so it's an empty list, but we're going to make one right now.

So to make a LinFull, we make another class. here is a class which extends Dart Lintful. We could technically extend just Lintful if you don't care about Dart, but here we want to analyze Dart code, so we extend Dart Lintful.

Then we have to add our new class in the list of Lintfuls we just defined. Okay. So in this class here, what we have so far is this bit here is a static constant associated with a lint rule which defines narrow code for our lint, so here it's just a hello world.

A message for the users which explains what the issue was. And then we have a run function.

Run function is a function which will have to emit lints. So it has a few parameters which are here to help you with emitting lints.

For now, the main one we care about is the reporter object, which is what can actually publish lints.

First of all, I can do reporter.report for offset, and I can pass the code I want to pass, this one.

And offset in the file, so we are going to write a lint at the very top of the file, offset zero and maybe for one of the characters.

So this should show a little bit at the top of the file.

But if I go here, you don't currently see it.

That's because I haven't yet installed fully the custom lint package on the example app.

For this, we have to also add an analysis option.

And then in here, we have to enable custom lint.

So we do that by doing analyzer, plugin, custom lint.

And while we're at it, we can also exclude code-generated files from analysis because we likely don't care.

So now if I save, we should hopefully see a custom lint log file appear.

And if I go back to the file, we see our lints appear.

Yay!

So just an L will work, nothing too fancy.

But yeah, the interesting thing is if we look at this log file here, it's where all your prints and if there is an exception, that's where they will appear.

And we also currently see at the moment VM service URI.

You can use it to maybe add breakpoints in your Lint if you wanted to. at the moment, you're not connected to the Lint plugin.

So you can do that by running the command attach to process, and you paste the URI in the log file.

And now the debugger is connected.

Which means that now if I had a breakpoint, and I go in here, maybe do something,

I can inspect the code of things.

You should be pretty used to this already.

Let's remove the breakpoint.

All right.

OK.

For now, our link rule is not doing much.

We might want something slightly more interesting.

So what we want to do here is we want to look for Dart classes in the file and maybe look for the annotation.

So for now, let's look for Dart classes.

So to look for Dart classes, we're going to use the analyzer.

And for this, customing offers ways to automatically interact with the analyzer.

So to do that, you can do context.registry.

And in here, we have a bunch of add listener equivalent to subscribe to specific Dart objects.

So for example, I can do add variable declaration, which subscribes to variables declaration in your files.

But of course, we don't really care about variable declarations here.

We care about class declarations.

So I can do add class declaration.

And every time the parameter object is a specific object corresponding to the type of object you obtain.

So here we get the class declaration.

And in here, we get information about classes.

So like the class name, whether there are extents keywords on this class, mixins maybe, maybe there are methods on it,

A bunch of interesting stuff.

All right.

So now we have classes.

We are able to iterate over classes.

So what we could do is we could modify our current lint to only show the name of every class in the file.

We could do that by just moving our report line inside the add class declaration and change this for offset to just be instead point at the name.

So if we look at it, node.name is a token.

So we're going to use add for token here.

All right?

And if I just save, we go back here.

We already see immediately the lint update.

As you can see, we have hot reload here.

Every time you do a change on your plugin, the changes are immediate.

But the issue is, if I make another unrated class here, we also have the warning appear on this class.

The thing is, it's not annotated yet.

So that's not really what we want.

So in that case, what we need to do is we need to search for whether the class has a specific annotation.

We could do that by doing the following.

Forgot the step.

Give me a second.

First, we have to define something that we call a type checker, which is an object exposed by custom lint.

You might be familiar with it if you just sourced Gen before.

So it's basically an object which enables you to verify that a specific variable is of a given type.

Because annotations in Dart are nothing but a constant variable of a given object.

So here is the RiverBud annotation.

It's just a const RiverBud of the RiverBud class.

So it makes an instance of the RiverBud class, which has a const constructor and a bunch of properties.

And so to check that we have an annotation of RiverBud, we just check that the annotation is of the type RiverBud from the package RiverBud annotation that we saw here.

All right.

So now that we define a type checker, we can use it to verify and obtain the annotation for classes.

We can do this by doing what I did before.

So we have our type checker here, and we use the method firstAnnotationOf, which returns the first annotation matching the type we defined.

And then if it's null, then we just-- that basically means there is no annotation of such type.

And we can just stop.

We just don't emit lint for this class.

And as a side note, using this annotation variable,

You can also do things like maybe get the content of the annotation.

Like you can do get field, keep alive, to bool value, which enables you to read this property of the annotation if you wish to.

But we don't care about this for now.

So if I save now, the warning on the another class disappears, which is what we wanted.

But still, we're not quite there yet, because the warning here shouldn't appear because the extent is actually correct.

Instead, it should appear on all the cases, like maybe if I have another class which forgot to specify the extent.

Or maybe a class where I did specify an extent, but I forgot to specify the wrong one, like object, for example.

In that scenario, what we could do is look for the extent keyword.

So I already told you before that we have the extent keyword information inside the

Node object, so I can do extent close here, which exposes a bunch of information about those.

Here, super class and all.

So I'm going to do that.

So this is basically a nif else about whether there is an extend close at all or if there is no extent, we do a warning on the class name, as you can see here.

Or if there is an extent but the extent is actually not the class we wanted to extend but instead something else, like we check the underscore dollar class name, then we warn on the incorrect extent.

So if I go back to the file here, we see -- oh, I forgot to remove this line.

We see that the warning appears on object here, and it appears on the class name here.

Which was great.

We got our link.

Yay.

So that's nice.

But the thing is, we still don't have a quick fix.

We can ignore stuff, but we likely would want to automatically fix the issue for our users.

So let's get going.

Making a quick fix is very similar to what we've done so far.

Basically we're going to make another class too, but just instead of extending Dart link rule, we're going to extend Dart fix.

So let's do that right now.

My fix extends Dart fix.

All right.

And inside our lint rule, we want to override get fixes to return a list of fixes associated with this lint rule.

So my fix.

All right.

And then once again, we have to override the same run method.

It has slightly different parameters from the lint variant.

That's because instead of emitting lint, we're going to emit source change in the Dart files.

So we have different parameters to deal with that instead.

So here's the reporter object is no longer a narrow reporter, but it's a change reporter.

And we also have two extra parameters, which is the analyser is the error under the cursor, and the others is the other errors within the same file, outside of the one under the cursor.

So what we could do here is we could do basically the same logic as here.

Like we could also call context.registry.class declaration to get classes.

And in here, if we wanted to define a quick fix, we could do the following.

Builder.

So I'm using a reporter and I'm using the method create change builder and I'm passing what's the word, title, I guess, for the quick fix we want to make.

So here I'm going to say extend this class instead with the correct class extend.

And the priority is how high this quick fix will show up in the list of quick fixes.

So if I save, I can go here, press the action keyword, and I see the quick fixes.

But for some reason, I see way too many.

I should only see example three here, because I click on the object.

And here, I should only see example two.

That's because we haven't checked yet that the class matches with the cursor.

So we need an extra one-liner here at the top of the function.

Intersect.

Yeah.

Basically, what we are doing in this if condition is we checked that the classes that we received overlaps with the warning under the cursor.

If it doesn't, we just do nothing.

If it does, then that means the class is actually the one we care about.

So if I save now, go back here, try again, now we correctly see only the quick fix for the warning.

And if I go on unrated classes, we don't see anything.

Obviously, we see the one, but it's not the same.

All right, last step.

Now we want to edit the file, because at the moment, we have a quick fix, but it's just not doing anything.

So for this, we can reuse the return value of createChangeBuilder.

So we can do changeBuilder.addDartFileEdit.

What this allows us is using the builder object, we can do edits on Dart files.

So I can replace some string of characters inside the file.

I can format some parts of the file, things like those.

Basically, text manipulation.

And so in here, I'm going to also want to reuse basically the same logic as here.

But instead of emitting a warning,

I'm going to emit the correct change to produce the correct output.

So I have a shortcut for this.

So that basically is the same thing.

If there is no extent, then I'm going to add one extent after the class name.

We see here we take the offset after the class name.

And if there is an extent, but it's not the correct one, then we replace the current extent with the desired one.

So if I say it one more time, try again, yay.

It's modifying our warnings.

Yay.

[APPLAUSE]

So as you see, it took us like 20 minutes, with a bunch of shortcuts, of course, to write a lint.

So it's actually not that hard.

And at any point, you can add prints, you can use breakpoints and all.

So I know that I went a bit fast on everything, and you likely missed some things.

But you should be able to slowly iterate and learn the API yourself.

Make sure to use print spread points if there is somehow at any point an error, like here, if I throw inside here, for example.

I throw exception.

The exception, there will be a red line at the top of the file showcasing the exceptions.

Here we have one exception per class, so we have four.

And the exceptions appear on the log file.

So everything should be debuggable over time.

All right.

So that's basically it for me.

Unless you want me to show you how to test things,

I'll see if we have time.

I'm not sure.

So yeah.

[APPLAUSE]

> > So maybe a quick question to start.

Can you give an advice for people who would like to do great live coding presentations?

> > Was it great, though?

Honestly, I'm not -- I wouldn't necessarily have good recommendations, but I would say just repeat a few times, make shortcuts like I did here.

In VS Code you can define user snippets, so go through your presentation a few times, when you see you have to type something, just make a shortcut for it and remember it.

And yeah.

> > Lots of practice.

> > Yeah.

> > Of course, thank you.

> > And remember the name of the shortcuts.

> > Yeah.

If possible.

> > Also, sorry, I didn't introduce -- please also welcome Guillaume.

> > Thank you.

Also, sorry, I didn't introduce, please also welcome Guillaume.

[APPLAUSE]

Thank you.

From the content team, we'll be here to ask the clever questions, because I won't do it.

So, if you have some questions, please feel free to use the Twitter account and the hashtag FlutterCon, as Greg and Simone said, so that I can forward them and ask them on Remy on stage, that we don't waste time passing the mic around.

So, in the meantime, I have a first question for you, Remy.

Do you... Is this possible to make this work with the mono repos and several versions of custom lint in different Dart plugins, for instance?

> > Several versions of custom Lint?

Technically, no, because the -- because when you open your monorepo, the version will kind of be shared between all packages, because, like, when the analysis is shared between every package of your monorepository, so having different analysis per package don't quite make sense, but, yeah.

Okay, because I know some people at BAM tried working with custom lins with a repo melos based package and had some issues with this and so we are interested in knowing if it will be supported at some point.

If that's about what, if it's not about the custom lin version but maybe dependencies versions. There are a few things that were done recently for this, but there are probably more things we can do. It's a bit technical, but ideally, yes, it will be supported in the future if I find a nice solution for it.

- Okay, thank you.

One other question.

Sorry for the...

You talked about the Dart lint rule and the lint rule and you said, okay, in this case we care about Dart.

Can you give some example of what would be a lint rule that doesn't care about the language you are writing your lint on?

- It's probably if you want to have a warning on the part spec.yaml, in this case, you don't want to make a lint on a Dart file, you want to make a lint on a YAML file.

We could technically offer already a built-in YAML lint rule.

I don't have one yet, but technically we could have one.

Maybe JSON files, too, whatever file you can think of exactly.

All right.

So the idea that lint rule is the base class to write a linting rule for any kind of file.

And currently, there is only a Dart lint rule extension.

But you could support more.

Yeah.

There is only a Dart lint rule and a lint rule class.

But you can look at the source code of the Dart lint rule.

It's actually not that complex at all.

A few lines of code at most.

So you can usually make your own.

All right.

We have some questions from the audience.

Do you know any known limitations with custom lint?

- I guess currently the one that was mentioned before about in a monorepo, if you have packages in the monorepo using different versions of the same package, monorepo currently, custom lint currently complains a bit.

Outside of this, I would say in theory

It should be fine, and basically it consumes slightly more memory than just using analyzer with no link rule.

But in theory it's designed to solve already most of the issues with analyzer plugin if you're familiar with it.

So unless you found a big issue, I'm probably not aware of it yet.

But yeah, besides the versioning thing could be one.

> > Okay, great.

And one last question.

Did you implement a layer on top of CodeBuilder package to help people implement custom fixes?

Can you repeat, please?

Did you implement a layer on top of CodeBuilder package to help people implement custom fixes?

No.

No.

Okay.

I mean, I assume you should be able to use CodeBuilder directly, because technically the fix API just takes strings.

So you take your code builder and you do to string and you should be fine

Great. Thank you

Thank you, Remy. Thank you very much for me
