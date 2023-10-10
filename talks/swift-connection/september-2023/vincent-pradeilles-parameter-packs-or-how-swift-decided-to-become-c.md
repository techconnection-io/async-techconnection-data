---
slug: >-
  /talks/swift-connection/september-2023/vincent-pradeilles-parameter-packs-or-how-swift-decided-to-become-c
date: '2023-09-21'
title: Parameter Packs or How Swift Decided to Become C++
author: Vincent Pradeilles
video: aVtRv_zkglI
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/aVtRv_zkglI.jpg
slides: null
tags: []
year: 2023
conference: swift-connection
edition: september-2023
allow_ads: false
---
Hello.
So I'm the last person standing between you and the after party.
But before we go to the after party,
I want to talk to you about a new feature that was added to Swift this year called Parameter Packs.
But before we talk about Parameter Packs,
First, let's talk a bit about SwiftUI.
Let's just see, show of hands, who has written SwiftUI code since the four years since it has been released.
So I don't see anything, but I expect a lot of hands to be raised because it's been four years.
And if you've written SwiftUI since 2019, you might have noticed that you can put up to 10 child views into a parent view.
Everything is working fine.
But if you add an 11th one, then you get this very weird error, extra argument in call.
And the reason for this is that if you look at the way SwiftUI collects the child views into something that the parent view can manipulate, it's done through a structure called view builder, and if you look at the doc, you would see this.
You would basically see an overload for every number of generic argument you can have up to ten generic arguments.
So that's where this limitation of 10 subviews, 10 direct child views comes from.
And what's funny is that if you were to see that kind of code into a pull request, maybe you would be like, hm, not the best kind of code.
But still, SwiftUI is built entirely on this.
Same for Combine, same for Eric Swift.
And the reason was that up until recently, there was no way in Swift to have something that would approximate variadic generics.
So being able to have an undefined number of different generic arguments.
But this has changed recently because if you've used Xcode 15, whether it was the betas or the final version we have now, you might have noticed that now you can provide
11 child views to a SwiftUI view.
You can even provide 16, you can even go all the way to 31 or 32.
I stopped there because after that we're getting too small, but basically the limit you would have is probably the number of arguments a Swift function can have, which there must be a number, it must be a very big number, something like 2 to the power 16, something like that.
And if you look at the code, at the documentation, you will see that now the Mayfield build block has changed its signature.
Now it looks like this, and we can see some new keywords that were not in Swift until a few months ago, repeat and each.
And so this feature is called parameter packs, and it's what we're going to see now.
I'm going to show you four different use cases of parameter packs in order to introduce this new syntax and try to make it as approachable as possible.
So let's start with use case number one.
Let's say I want to implement this function, group in tuple, that can take an arbitrary amount of arguments of arbitrary types and it groups them into tuples.
This is basically what the build block in SwiftUI is doing.
Let's implement this using a parameter pack.
So we define a function, same syntax as usual, and then we're going to define some generics.
But this is where we use the new keyword each.
So each allows us to declare a parameter pack instead of a generic type.
And you can really see a parameter pack as a vector of generic types of undefined length and the length will be defined at compile time.
If you provide two values, there will be two generic types, if you provide ten values, there will be ten generic types, et cetera.
And so you declare it with a keyword each and you declare it where you would declare a simple, a scalar generic type.
Then you need to define your argument list.
And this is why you need to use another feature of parameter packs which is called pack expansion.
So you use each to declare the parameter pack the first time and then to use it, you use the keyword repeat, and then you say repeat each T. And what it will do is that at compile time it will turn, it will basically display all the types you will provide in a comma separated list. And this is what Swift calls parameter pack expansion.
Then you need to define the return type of the function. So we wanted to return a tuple with all the elements. And the way we define the type of the tuple is the same than for the argument list. We do a pack expansion. So we say repeat each T. And if I call this method with an int, a double, and a string, it will return a tuple that has four types, double and string.
Then we need to implement the function.
So we're going to return a tuple, and to build the content of the tuple, we're going to use an expansion, but a slightly different one, because this time we're not using the type, but the actual value.
So the argument value is called a value pack, and we will also expand it using the keyword repeat.
We say repeat each value, and it will take each value we provided when calling the function
And put them in a comma separated list.
And so this implementation is working.
And this is conceptually how SwiftUI can now handle an undefined number of child views.
Now let's try� and so, yeah.
Remember this is what you can achieve with this code.
Now let's move on to the second use case.
Let's implement a function that I called make_pairs that will take this time two lists of arguments
And then it will pair the first element of the first list with the first element of the second list.
It's basically a zip function.
And you can see that the types are completely arbitrary here.
So let's implement this function.
And, yeah, I wanted to return this.
So let's implement this function.
So like before, we need to declare a parameter pack.
I'm calling it first.
But this time I will need more than one parameter pack.
Because I want to have two lists of arguments of arbitrary types and the types don't have to match at all.
They are completely independent.
And so I need to declare a second parameter pack.
You are absolutely allowed to do it.
You can have more than one parameter pack in the function.
Then you need to declare your arguments.
So we will take two lists of arguments, first and second.
And to build the type of each of these arguments, we will do two different pack expansion, repeat each first and repeat each second.
This allows us to call the method with two different lists of arguments.
The only requirement is that they will have to be of the same length.
Then for the return type, we are going to return a tuple, a tuple of tuples that will contain the pairs, and for this we'll do something new, we will still use the keyword repeat, but this time we will use more than one parameter pack inside this expansion because we will say repeat and then a tuple of each first and each second, and this is what allows us to compute the return type which will be the types of each element in both argument lists according to their indices.
And then we need to implement the function.
And you will notice that very often there is a nice symmetry between the return type� between the implementation of the return type and the implementation of the return value.
Because we are basically substituting the type parameter pack with the value parameter pack.
So we return a tuple.
A tuple of tuples.
And so we repeat.
And this time we return tuples of each element in the first list of values and each element in the second list of value.
And with this code, you can implement this kind of function, which can be a nice helper.
You imagine, for instance, you're writing tests and you have expected and actual values, this kind of things.
Or inputs and outputs.
Now let's move on to use case number 3, which is going to be more interesting.
Because up until now, we've seen that we can gather stuff in a tuple, that's great when you are SwiftUI, but most of the time you will need at some point to also iterate over the values to do something with them.
And it's an interesting syntax to see how you can iterate over the contents of a parameter pack.
So this time I want to implement a function total count that takes as argument an arbitrary amount of collections and returns the total count of each of the collections passed as an argument.
So here the first call site would return 3, the second 5, and the last one 8.
And as you will see when you want to iterate over the content of a parameter pack, this is when the fun begins.
Because we don't really have a for loop, actually, there is no for loop to iterate, so you have to use other creative means.
So let's see how you can do it.
So I implement the function total count.
I'm going to say it takes an arbitrary number of collections.
I need to add a generic constraint, so I do it just like I would with a regular generic.
You could also use a where clause, just like you would with a regular generic, it's really up to you here.
Then you define the argument you take, so here there should be no surprise, it's the same strategy than before, we say repeat each C, so repeat each collection.
For the return type, we don't use the pack because we are aggregating into a simpler piece of data, we are just returning an integer, the total count.
And now let's try and implement it.
So we start with the initial value, we return it, and we do something in the middle, of course.
And since we don't have a for loop, what we have to do is to create a tuple, and each member of the tuple will contain the side effect that will increment the result.
So you can see it's a pretty creative way of iterating over an array, over a vector.
And so the code looks like this, you see a repeat, you build a tuple, result, plus, equal, each collection, then you call the property count on the collection.
What's nice is that even though you are creating a tuple, Swift lets you omit the two top and last parentheses, so at least it can look a little bit more like Swift code.
And what's funny is that what do you do if your iteration is more than just one line?
But here it's easy, it's just one line.
Well, as you can imagine, this is also where the fun begins.
Because it's not a problem.
You can define functions.
So you can define an inner function and call it.
And basically, you have moved the contents of what would be the body of the form that you don't have into this inner function.
Maybe you could even write a macro that you would call for.
That could work.
I didn't try it, but it might be possible.
But this is the best you can do as far as Swift 5.9.
And if you look at the Swift proposal, Apple will tell you everything is under control.
Because all list operations can be expressed using pack expression by factoring code into a function or a closure.
So I'm not telling you you should do it.
Apple is telling you this is the way to do it for now.
And it really shows you that my understanding is that the goal of this feature was to lift the limitation of SwiftUI more than anything, and then the rest will be added, they are looking to add a proper for loop later.
And so with this, you can implement this kind of call sites.
And now for the final use case, let's imagine that we want to implement an R equal function that takes two lists of elements and checks that they are equal respective to their indices,
So the first two are equal, then the first second, et cetera.
Which could be very useful in tests to build a version of XCT assert equal that would work with argument lists.
And when you want to implement an R equal, usually you want to implement short circuit evaluation in the sense that as soon as you found two elements that are not equal, you want to return false and not keep evaluating the rest because you know that the end result will be false anyway.
And as you can imagine, when you want to implement this short circuit without a proper for loop, so without access to the break keyword.
Once again, this is when the fun begins.
And so you're gonna see that the intention of it is quite interesting, because we will implement the function r equal.
So it's going to take a parameter pack of elements.
They have to be equatable.
So the elements, the first two elements will have to be equatable of the same type, same thing for the second one.
But we can have, for instance, an int and a string.
We are not limited to the same type, so that's a great improvement over regular generics.
We build the two argument lists.
This time we use the same parameter pack because we want the types to be the same because if they are not the same, we cannot compare them anyway.
So if they're not the same, we already know at compile time that the result will be false.
And we return a Boolean.
And so how do we implement this?
The way to do it is to use the throwing mechanism in a creative way, in the sense that you will define an inner function throw if not equal, that as the name suggests, if the two elements are not equal, it throws an error.
And then use the same strategy than before, and you make a do block.
You do the repeat try throw if not equal.
If something throws, then you return false.
And if nothing has thrown, then they were all equal, and you return true.
So this is what you do when you don't have a for loop.
You write this kind of code.
So it's kind of interesting to see.
But once again, this is to my knowledge the best approach we have today.
But with this code, you can write this kind of nice helper, which could honestly be pretty useful to make, for instance, testing code have a little less boilerplate.
So as a recap, parameter packs, they are a new feature of 3.9, so introduced at WWDC and then officially available since one week ago in Xcode 15.
They lift a long-lasting limitation of Swift, the fact that we couldn't define an undefined number of generic types.
They are quite powerful when you need to write framework or tooling level code.
Using parameter packs in app level code I guess will be less frequent because the use case will arise less often.
However, as we've seen, the ergonomics are not yet perfect, even though there is an initial proposal to introduce a proper for loop to be able to iterate properly, even though iteration is possible, you just have to write dirty code, basically.
And that's all I had for you about parameter packs, so a bit of shameless promo, I have several content online, including a newsletter, and if you subscribe to it, you get some free content automatically, and I work for a pretty cool app called PhotoRoom, it's on the App
Store, you can check out our website if you want to learn more.
Thank you.
[ Applause ]
[APPLAUSE]
Do you see a real use case for this feature of Swift for regular Joe coding out there?
I guess it's the kind of feature you don't use every day, definitely.
It lifts this long-lasting limitation.
I would say every time you have boilerplate code,
And every time you find yourself writing, like, variable 1, variable 2, for lack of a better word, you might want to use a parameter pack.
This tends to happen a lot in testing, because testing is really like boilerplate-y.
I hope it doesn't happen too much in your production code.
But if it does, you can also use parameter packs.
But it's something that was mostly done, I guess, to lift the limitation that Apple encountered and other libraries encountered before.
Eric Swift also encountered the same issue, so it combined.
So I would say it's important to know about it, because this way, whenever you are looking at an API and you see this each repeat each, you're able to make sense of it.
But you will definitely not use it every day, and you will use it much less often than generics, which are pretty useful.
And the need for a generic arises much more often than the need for an undefined number of generics.
>> We have again lots of questions from Slido.
Thanks, everyone, for using it.
One question from Jerome.
>> Who could it be?
>> I don't know.
Who's that guy?
Can we use parameter packs in macros?
>> That's a good question.
Best way would be to try.
So I can tell you, when I prepared this content, it was with Xcode 15 beta 8.
And if you were to use a parameter pack on the struct, for instance, the compiler would set fault.
So that was annoying.
I've checked just before on the release candidate.
They have fixed it.
So in the proposal, they say that every place you can use a regular or scalar generic type, you should be able to use a parameter pack.
So I would say it should be.
But because there is some complexity with the feature, it might not work.
It might be supposed to work, but it might take fault also.
It's a pretty new feature.
So you can expect some bumps in the road.
And do you know if there's an impact on the compile time whenever you use this feature?
That's a good question.
I would expect to have a small impact, yes.
Because basically, my understanding is that what's happening is that earlier in the compilation, the pack is expanded and so turned into a new source code, basically, that will be compiled.
So it will probably make compile time a little bit longer, even though it might be negligible.
However, if you compare it with the alternative, for instance, for the total count function, which is to use any, you might win a bit at runtime.
And you might also want to keep in mind that what I'm saying doesn't make any sense unless you have measured and make sure is actually the case because optimizations are a black box.
So it might make your code a little bit longer to compile, but it might be a bit like--
I haven't heard people complaining about it the way they did with generics back in Swift 3, basically.
You have another technical question?
No.
So a non-technical question for you.
I guess lots of people here know you through the different social medias where you are.
Would you have one advice in 2023 for a developer out there who would like to start creating content, any kind of content related to code?
That's a good question.
I would say starting with something very simple.
When you think about it, for instance,
John Sandel, he started by posting screenshots of code with text written over it using preview, because you could notice that the arrows were the arrows that preview basically generates.
So I would say start with something simple.
For me, it was mostly the animated code that worked well.
So start with something simple.
See what sticks, basically.
And when something doesn't work, it's
OK to just let it go and try something else.
It's harder when it's yourself to be like, OK, my idea didn't work, and it's not like me.
I suck.
It's harder to make the distinction.
They would say, yeah, try things.
Don't put too much pressure on you.
See what sticks.
And if it works and you enjoy doing it,
Basically, that's when you know that you're onto something.
Great.
Thank you, Vincent.
Thank you.
[APPLAUSE]