---
slug: >-
  /talks/frenchkit/swift-connection-2024/john-sundell-a-practical-guide-to-swift-performance
date: '2024-09-23'
title: A practical guide to Swift performance
author:
  - John Sundell
video: ofXGwYHr-ZM
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/ofXGwYHr-ZM.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### John
Hi, everyone. It's so, so great to be here and thanks for that wonderful introduction, Greg. I'm so happy to be here today to talk to you about Swift performance and specifically to share a lot of practical tips on how I think we can make our code faster and more efficient.

Because I think that all of us, we really strive to write code that is as fast and as efficient as possible. After all, no one has a goal to write slow and inefficient and wasteful code. But at the same time, we usually have a lot of other goals with our code as well.

We want our code to be reliable and easy to test and easy to work with with our teammates and so on. Follow the latest Swift conventions. So at the same time also, it can sometimes be hard also to know what is kind of good enough when it comes to performance because there's a very big scale between being as fast and efficient as possible and being horribly slow and wasteful.

And in practice, I think most applications, they tend to fall somewhere in the middle. They're not maybe the most optimized they could possibly be. They're not like the fastest program you've ever run on your machine, but they're also not horribly slow.

And also, when you work with a different app and you are interacting with it as a user, the performance tends to vary quite a bit between different features. Some features might be really fast and well-optimized, and other features might need some more work in order for them to feel really, really smooth. And because of all of these factors, because we have different priorities with our code and it can be hard to define what is a good performance target for our codebase, our work around performance sometimes tends to be a bit reactive, like we only work on performance when there's an actual issue.

But I think that if you practice a little bit, you can get really, really good at writing code that is sort of fast by default. When you commit code to your repository, you kind of know its performance characteristics and it becomes more predictable as a result. So that's exactly what I want to talk to you about today.

And when talking about performance, I think it's very important to separate synchronous code from asynchronous code, because when we optimize these different types of code, we need to focus on quite different things. When we're focusing on synchronous code, our performance optimizations tend to focus a lot around the raw speed and the scalability of our code. So for example, how fast is each function call and how do our algorithms scale according to the number of inputs?

And when we work with asynchronous code, on the other hand, our focus tends to be a lot more around task orchestration. That is, do we run things on the main thread or on a background thread? Which operations do we do first?

Do we do some prefetching or caching and so on and so forth? So that's what we're going to talk about. And let's start by diving into the synchronous domain.

And the first topic is going to be all about learning more about the performance characteristics of the code that we write. So let's dive right into a code example. Here we have a class called item storage.

It stores the items for a given application, like data models. And it has a private property, which is all of the items currently added to the application. And it uses that private property to sync with the database, maybe do some network calls and so on.

And then we've exposed as part of the API this computed property called user added items. And this user added items, as we can see, it takes that all items array and then it performs a series of transformations on it. It performs a map in order to load the comments for a given item.

It then sorts them according to the date so that they're easy to display in the UI. And it then filters them based on whether the user indeed added these items to the application. Now, if we zoom in on this computed property here a little bit, let's see how it actually works in terms of performance characteristics.

And then I think it's useful to think about its time complexity. That is when we use the big O notation to kind of describe how a given algorithm scales according to the number of inputs. So if we look at map, for example, from the standard library, that is O of N.

That means that it's going to scale linearly according to the number of elements that we need to iterate over because we need to transform each one. Sorting on the other hand is O N log N because it can't just do a linear search, it also needs to compare the different items for sorting. And then finally we have filter, which is O of N also because it needs to iterate through the entire collection in order to filter out the elements that we don't need.

So if you look at this particular implementation here, when we're working with a algorithm that sort of has linear-ish time complexity, it's usually very useful to think about how many inputs am I currently working with and can I minimize that number of elements. So if you look at our code here, we can see that the last operation we're currently performing is filter. But filter will naturally reduce the number of items we work with.

So a performance optimization here would be to actually do the filter first before we do any mapping and sorting because it's kind of useless to do mapping on an item that we're just going to throw away anyway. But I think maybe even a more important aspect of this particular implementation is how we've designed our API. Currently it's a computed property, which is a really nice feature of Swift and makes it easy to call or access, which is a dot syntax.

But because we're performing some significant computation here, this can actually hide some performance problems that actually can occur if we are accessing this property too often without knowing that all this computation happens. So in this case I think it would be more appropriate to actually turn this into a function instead because that indicates that some kind of work is being done, some kind of computation that is not just constant in terms of time complexity. That might seem just like a little detail, but let's take a look at a call site to see where this can become really, really important.

Here, we're accessing that item storage API from before, and currently we're using the property-based version. Just looking at this code briefly, we might not see any issue. So in code review, we might just approve this and everything is great.

However, if we dive a little bit deeper and look more closely, we can see that we are in fact accessing this computed property multiple times in the scope. And because we're performing all of that mapping and sorting and filtering for each time that property is accessed, this is wasting a lot of work. And even worse, actually, is because we're iterating over all those items in our for loop and then accessing that computed property inside of the for loop, that means that we actually have O of N squared time complexity here, which is not great because our function here or our code will scale exponentially according to the number of inputs.

So for users that even maybe just have like 1,000 items, this would be really slow and could really cause some performance issues. Now let's switch over instead to the function-based approach, which we refactored into, and we can see that it actually makes things a lot more clear. Here we can see that we are actually performing multiple function calls, which will probably catch our eye a little bit more, and we will realize that whenever we have a duplicate function call like this in a given scope, it will probably be better to store the result in a local constant and then access that constant instead throughout our function.

And with these optimizations that we've now done, we've not just like slightly increased the performance, but we've actually made this execute over 150 times faster if you have 1,000 items, which can make the difference between something being blocking for the user and actually being super smooth. So that's really great. Next up, let's talk about call site-driven optimizations, because most of us, we work on applications, and when we work on applications, we shouldn't just consider the code, the implementation of the APIs we design, but also how they are used.

And let's go back here to the item storage and take a look at another call site here. Here we have some code that is run when our app is first launching, and we can see here that we're accessing that user-added-items function from before. The only difference here is that what we're only interested in checking is whether that return array is empty or not, and that's kind of wasteful, performing all that sorting and mapping and so on, just to check if the array is empty.

So we can optimize this by creating a dedicated API that would instead be much faster to run at app startup time. For example, something like this. We could create a contains any user-added-item function that just returns a Boolean as to whether the user has added any item or not.

We've just currently taken the filter from before and just put that in here, and then we're just checking if that is empty before returning. But it turns out that we can actually optimize things further by picking the right standard library algorithm for each specific use case. In this case, running a filter means that we will run through the entire array no matter what, but we don't need to.

We can instead call contains and pass in the key path as our predicate there to return as soon as a match was found, because that's really all we're interested in, if the array contains any user-added-item or not. This will make it much, much faster when we now implement this particular function in our call site right here. In fact, if we have 1,000 items and the user has added one item in the beginning of that array, this could potentially be 1,000 times faster, which is pretty remarkable.

And we're talking now about code that is run at app start-up time, which, of course, is a really crucial moment when we want to launch the app as soon as possible. Finally, when we talk about synchronous code, let's talk about avoiding duplicate work. And another way to express that would be to say that we're going to talk about caching.

That is, if we can make something fast, that's really great, but if we can avoid calling that function altogether, that's going to always be even faster. So caching is something that we tend to use quite a bit when working on our app's performance, but it can be a little bit of a double-edged sword. The benefit of implementing caching is that it can really help speed up operations that are repeated, because we can return a cached result instead of having to recompute the result from scratch, but there are several downsides to keep in mind when we start implementing caching within an application.

For example, caching very often causes additional memory usage, because we have to keep our cache also in memory at the same time as our other data. It can also cause stale data to accidentally be used if we're not careful, because we can run into the classic cache invalidation problem when we have updated our data, but the cache hasn't been cleared, so we return the wrong data. And then it can also make performance issues actually harder to diagnose, because you might get a bug report from a tester or from a user, and they say that there's a performance problem in a part of the application, but when you try to reproduce it, you don't get that same error because you had a warm cache on your device.

So we should definitely not treat caching as a silver bullet, and also implementing caching doesn't actually make things faster, it just helps us avoid duplicate work, which is also a good thing if we can implement it in a good way. So let's go back again to our item storage that we worked with now for a while, and let's see what it could look like if we were to add caching here. One version would be that we could add a property called cached user added items, which is an optional array, and then we check if that optional array is not nil before actually doing our computation, and if so, we return it, otherwise we perform our computation and then cache the result before returning it.

Kind of classic caching setup here. But there's also different variants of caching we could explore that perhaps aren't technically caching, but they achieve the same result. For example, we could do pre-computation, oh, we also have to remember that we have to reset this property every time that the user added items is modified, because, well, that would otherwise create this problem where our cached results are different from the actual results.

But pre-computation is another technique we could use. Here for example what I've done is I've changed the user added items API to be a stored property instead of a computed one, and because of that, it's going to be really, really fast to access, there's no computation needed, but now our computation instead happens when we're actually adding an item to the storage. We're then checking if it's a user added item, and if so, we append it to that other array, otherwise we just append it to the all items one.

This has other kind of trade-offs. Here we have to eagerly load our comments. Before we were doing that lazily when the user added items were accessed, and we also here still have that problem where we have to ensure that our data stays in sync.

So different trade-offs and different kind of pros and cons for these different approaches. But there are other ways to kind of utilise the concept of caching on a more local level that we might not even think about as caching, but can also make a huge performance improvement when used well. So here we have another function here.

This one is an extension on sequence where all the elements are of a type article, and here we have a function for returning those articles sorted by word counts. Now currently, this is implemented in a quite simple way. We're just calling the sorted API and passing a closure where we're checking the word count for the first element against the word count of the second element.

The problem, though, is that both of these two API calls, well, they're O of N in terms of time complexity, and since we're doing repeated calls on each sort iteration, that's going to waste quite a lot of work. So this call site looks simple, but it can actually be improved quite a bit with a little bit of some caching or pre-computation. So here's the second version where instead what we're doing here is we're starting by creating a dictionary from article ID to integer, and then we're iterating through the sequence in a separate loop where we're computing the word counts, and then we use those results in our sorting algorithm which can be actually up to two times faster.

It can sometimes be a little bit counterintuitive because we have to do two loops here through the sequence, but it ends up being faster because of the word counts call. So that's also important to keep in mind when working with performance and trying to make things as fast and efficient as possible. Now let's switch gears and talk about asynchronous code instead, and here I want to start talking about how we can utilise concurrency to make our code faster.

Because we have to remember that just because we're writing asynchronous code doesn't mean that it's necessarily concurrent. It will probably be concurrent in relation perhaps to other threads, but internally it might still be quite sequential. So let's take a look at another example here.

Here we have a search service actor, and this actor is responsible for implementing search within our application. This is a music application, so we have our search results consist of songs, artists, and playlists. And currently our back-end is set up so that we will perform each network call for each one of the different model types.

So to reuse code, we've written this generic function called entities matching query which takes or returns a type T conforming to an entity protocol, and then in our actual search API, what we're doing, we're querying for songs, artists, and playlists by calling that generic function for each one. Now let's zoom in on that results matching query function to take a look at how we could optimise it. Currently, we're using async await for each one of these calls which is really great.

Code looks very nice and clean, and it's easy to step through when debugging and so on. But because we're performing an await between each operation, that means that this operation is not actually being concurrent. It's actually just sequential.

We're performing one, then the other, and then the other, so first songs, then artists, then playlists. And because these operations don't have anything to do with each other, they could easily be parallelised. Writing this kind of code in the past was quite difficult, and we had to use different techniques to synchronise our state between different threads and so on.

But with Swift concurrency, this is really easy to do. All we have to do is replace our await calls with async bindings and let the compiler take care of orchestrating that for us. Now each of these operations will be performed in parallel in the background, and then we will perform a single await when we're consuming the result which is when we're creating that result struct from before.

So with these optimisations in place, we haven't really made our code more complicated or anything, but it's now up to three times faster because we can perform all of those three operations in parallel concurrently, which is really great. Finally, let's talk also about how we can make operations non-blocking even if they are not using async await and Swift concurrency. Here we're working with a view controller.

This one is a text editor view controller, and it stores an attributed string which the user can edit using, for example, a text editor text view. Now within this view controller, we have a function that is called save text. This save text function is going to run on the main thread or the main actor because it's within a UI view controller which inherits the main actor isolation from its superclass UI view controller.

Now, this code here is going to do a bunch of different things in order to first validate the text, then encode the text into data, and then finally store that text using a data controller. And we can kind of infer here just by looking at the code that validate and encode will both have O of N-like performance characteristics. How can I say that by just looking at this code here without looking at the implementation?

Well, that's because we know that in order to validate the string and in order to encode a string, we have to iterate through it. And that means that the longer the string is, the longer it's going to take to run. So it's kind of O of N-like, at least.

It could be even worse if it does more kind of operations on it. So that means that the longer the text will be that the user is working with, the slower this will be to run. And because we're currently on the main thread and the main actor, that means that we will block the UI, block all the animations, all of the interactions and everything while the save operation is happening.

Now these kinds of issues can be particularly problematic because when we're doing our debugging and development, we might be working with slightly shorter text and we might not be noticing that this is actually a performance issue. But since we know that this can grow in size, that the text can be an arbitrary size that the user has entered, it's good to keep in mind that perhaps this should not be actually be blocking the user, perhaps we should use a different approach here instead. Because we wouldn't want our most loyal users who are writing super long text using our app to always be running into performance problems and have their UI be blocked.

So how can we do that? Well let's write a new version of the save text method that is instead using a detached task. When we're detaching a task from the main actor or from the main thread, that is going to be run on a background thread instead, which is really great.

And now we can perform our operations in the background instead and then have the result be saved. But of course it's not as simple as that. We still have some other things we have to keep in mind.

The first thing is that our validate function is still synchronous, so it's still going to block the execution even though it's now running in a background thread. So there's some potential optimisation improvements to be had there. Secondly, we have to await when using our text encoder now, and that's because we're accessing the text property from the view controller, which is still isolated to the main actor.

But perhaps more importantly is that because we are now storing our data here with the data controller asynchronously in the background, we are introducing a potential risk for race conditions because any time we go off into an asynchronous context, we can have multiple tasks being run at the same time and perhaps some data will be saved that wasn't actually the latest version. That would cause data loss in this case, which of course wouldn't be really great. Would be pretty bad, actually.

So how can we fix all of these issues here without necessarily making our code super complicated? Let's take a look. What we're going to start with is we're going to start by having a stored property called save task, which is going to keep track of the current task that we're using for saving.

We're also going to implement a did set on it so that we're cancelling the old task when we assign a new one. That's going to make sure that we're not running two tasks in parallel. Then we're going to still implement save text that we did before, but now instead still using a detached task, but we're going to now save the result to that save task property.

And that's going to ensure that also the previous one gets cancelled because of the did set we just took a look at. Next we're going to capture the current text by value instead of referencing it as a property. That means that we don't have to go back to the main actor and the main thread just to retrieve the text.

We can just capture it by value into our closure, and the closure will keep a local copy of it. And because we're cancelling an old task when we start a new one, we wouldn't be saving any old text or anything like that. Next up, let's take both of our validation and our encoding, which are both synchronous operations, and wrap them inside of separate tasks instead.

That's going to make it possible to run them asynchronously even if they're actually synchronous operations. Then what we're going to do is we're going to wait for the results of those two operations by accessing the value property of those two tasks. It's kind of like using async let, but for APIs that don't support async await, which is pretty neat.

And then we're going to check if our current task is cancelled. That's a very important step to do because if we don't do that check with task is cancelled, then our code will still keep running even if the task has been cancelled, so we have to manage cancellation there ourselves. And then finally we will call our data controller just like we did before to store the data that the user has saved.

And with all of these things in place now, we have struck a nice balance between unblocking the UI so the UI can keep running the animations and do interactions, the user now can save any number of characters, any length of text without causing any real performance issues, and we still don't have a problem where multiple save operations will cause any kind of data races or race conditions, which is really nice. So to recap what we talked about today, we talked about how we can write code that is faster by default by keeping in mind performance characteristics of the code that we write, and we've seen how it can make a really big impact when we scale up the number of elements that we're working with depending on how our code has been written and the order of operations.

We've talked about how we can use call sites in our application to drive our optimisation work, because unless we're working on a library or shared SDK where we don't know about the call sites, we can always look at the call sites in our application to decide how to fine tune our code for the maximum performance without going overboard and optimising things too much. We can also use caching and other techniques like prefetching to avoid duplicate work so that we're not performing the same operations multiple times for no good reason. In the asynchronous domain, we can utilise concurrency, especially now with async await, to create code that runs in parallel as much as possible without being overly complicated.

We've also taken a look at how we can make operations non-blocking, especially when we're working with storing data, with accessing the file system, networking, and any other things that can take a different amount of time to complete, by moving them to become non-blocking instead, we can also ensure that our UI stays responsive. Finally, when talking about any kind of performance, I think it's very important to always remember that when we are working with performance, we should always measure our work. We should not make too many assumptions, because we will always be surprised about the different performance characteristics, and we need to measure on device and in release mode to ensure that we're actually measuring the real thing, not running in the simulator in debug mode, which will have very different performance characteristics than on device in release mode.

That's all I had for you today. With all of these tips, I hope that you can also get started with writing code that is faster to run, kind of out of the box, so you have to spend less time working with a time profiler, less time figuring out performance issues, even though we sometimes have to do that too, by kind of keeping these principles in mind, and hopefully, our code will be fast and smooth and efficient as a result. Thank you very much.

Thank you, John.

### Greg
So, we can stop the Q&A.

### Ellen
Yeah. I really liked the talk. I think one of the questions that I had as I was sort of running through, I like your idea of fast by default, but I think one of the things we're always taught to do as programmers is avoid premature optimization.

How do you draw the line between saying, okay, I want to make sure that this is fast by default versus like I am basically going down a rabbit hole trying to fix problems that don't actually exist yet?

### John
Yeah, that's a very, very good question, and I think a lot of us have been taught that premature optimization is the root of all evil, and therefore, we kind of avoid doing it at all costs, and sometimes, that kind of also gets translated as I'm just not going to focus on performance at all when I'm developing my code and then just deal with it later, kind of if performance issues actually occur, and that might seem like the most optimised way to work with performance issues, but that way, you kind of always have to go back and fix things after the fact, and it can be kind of wasteful in terms of time because you have to get back into that context, you have to figure things out, maybe get bug reports from users, run the time profiler, figure out where the call stack is the heaviest.

It takes a lot of time, right? What I want to do when I'm working on my code is I want to strike a nice balance between not optimising too much prematurely but also not trying my best not to commit code that I know has potential performance issues, right? So I think how to strike that balance is the premature optimisation happens when you optimise for use cases that just never materialise, so that usually happens if you start optimising immediately when you start writing your code, that could definitely be the premature optimisation, but if you do it as the last step, if you will, before you maybe create that pull request, then you are kind of striking that nice balance between not doing it too early in the development process but you're also not committing code that has kind of known performance issues, so that's usually what I strive for.

### Ellen
Cool, thank you.

### Greg
Thank you. We have a question from Dean. Swift 6 would have catched those race conditions, how do you feel about those concurrency checks additions to the compiler and the overhead for developers?

### John
Yeah, so I think it's important here to separate race conditions from data races, so Swift 6 helps us identify potential data races, not race conditions. Race conditions can still happen. So what's the difference?

Well, a data race happens when two threads or two concurrent operations access the same memory at the same time, so they either perform a read or a write at the same time, and that causes data corruption because you just can't have those two mutations happen at the same time so you end up with these kind of bad access errors or some other low-level kind of error in the stack that can be really hard to diagnose, right? So with Swift 6, the compiler is helping us identify those potential data races by saying, hey, this is, you're violating kind of the actor isolation model here, you need to make sure you have a sendable type which can actually be mutated concurrently and so on, and those checks can, in the beginning, I will be honest and say that I pretty much hated them, because especially when working on a kind of mid to large-size project, it was like a lot of work to make code compliant with it, and I'm still working on it on some projects. But at the same time, I want to keep an open mind where I remember back when I learned Swift and I went from Objective-C that didn't have optionals, and I remember I thought optionals were such a headache, because I was like, I know this is not going to be nil, why do I have to prove it to you, compiler?

And I think we might look back on Swift 6 the same way, which is like, oh, I remember back when we didn't have, you know, data race safety in Swift, that was the before times, that was like when the dinosaurs were walking on earth, right? But time will tell, right? I think there's a risk with Swift, because it pushes so many checks to compile time, they will go too far, and it will just become really hard to work with.

I'm not sure if Swift 6 is across that line or still in the realm of being, making us productive, time will tell, but I'm trying to keep an open mind on it, and I think it has already identified some potential bugs in applications I work with, so that's good, and yeah, I think time will tell if it will be a net positive or a net negative, but so far I think it's working out quite well. So you can still have race conditions, and that's when the order of operations is not predictable, so in my demonstration here with the text editor, you could have the user press command S, for example, on the Mac, or press save in the UI multiple times, and because those tasks would be running in the background, you could start five, six different tasks, and the order of which they complete is unknown, and even in Swift 6, that would be the case, so that's something we still have to think about when we're writing asynchronous code.

### Ellen
Is that sort of the actor reentrancy problem, where you sort of, if you're doing work after something finishes, then you have to sort of check, like, hey, did this change while I was waiting for this to come back?

### John
Yeah, that's a very, very good point, and, like, I think when most developers, myself included, started working with actors, you kind of thought, oh, great, the actor will just take care of everything for me, and I don't have to worry about anything any more, I can just, like, do a wait, and actor will solve it, right? But yeah, absolutely, you have the reentrancy problem, which is when you go and perform an asynchronous operation inside of an actor, and you come back into the actor, well, something else might have happened in the meantime, right? Because that operation could have taken, like, let's say, you know, two minutes to complete, and the actor is not just going to sit there and wait for two minutes and block the thread, it's going to accept other requests in the meantime, which is good, but it also means we have to still think about race conditions, even if data races is not as much of a concern any more with actors.

### Greg
Last question. Okay. From the audience as well, from Nathan, in that text-saving sample you showed, was there still a possible race?

### John
No, I don't think so, because we're checking the task cancellation before saving, the only potential race is that we could actually perform validation and encoding that we would then throw away, there's a trade-off there of doing, like, work eagerly versus waiting, so another approach would have been to block the UI, for example, to set the save button to, you know, is enabled false, and then wait until the save is complete, and then re-enable it. Sometimes that is the right approach as well, it depends on how costly the encoding and validation operations are and what kind of trade-offs you want to make there, but I think in this particular use case it would be pretty safe, but, you know, you could always be surprised and then have to fix something, so I guess, like, you know, the kind of things I showed today and the principles that I tried to follow in writing code, it doesn't mean that I never create any bugs and all my code is super optimised, absolutely not, it's just that I try to think about performance earlier in the process so that it's more kind of, like I said, fast by default, it doesn't mean that it's always fast, so there's always, like, bugs you have to go back to figure out and there's always need for performance optimisations, it will just be fewer than if I would not think so much about performance from the get-go.

### Greg
Perfect, thank you.