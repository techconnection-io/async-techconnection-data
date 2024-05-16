---
slug: >-
  /talks/react-native-connection/2024/mael-giret-enhancing-memory-performance-in-android-tv-applications
date: '2024-04-23'
title: Enhancing Memory Performance in Android TV Applications
author:
  - Maël Giret
video: Poo58mamLYg
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/Poo58mamLYg.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: '2024'
allow_ads: false
---
### Maël
Thank you, Mo, for the introduction. Maybe you will see me dance tonight after some beers. Now, I will show you a dance between performances and Android TV.

So, yes, I'm Mael from BAM. I'm currently developing a React Native application on TV at TF1. It's a French TV channel, one of the most popular.

So, today, I will discuss about the memory management issues we faced at TF1 and what was our journey debugging memory. But first, let me explain why we are using React Native at TF1. So, most TVs, like Samsung, LG, Sony, and most box, like Apple TVs, Google TVs, Fire Stick, are connected and capable of launching applications, like your phones.

Most of these devices run on Android TV, which is a version of Android for TV. Other run on web. And Apple TVs run on TVOS.

It's like iOS, but for TV. So, like many of your applications, we use React Native to share code across all of these platforms. And React Native Web to target web platforms.

And so, it allows us to deploy our application to almost eight different stores and a lot of devices. But the problem is that performances of these devices are really inconsistent. Some devices are worse than Motorola.

So, maybe you should consider using your TV and not buy a Motorola. It's simpler. That's why we need to monitor this metrics.

So, let me tell you about the day we wanted to launch our app into production, but the memory consumption was skyrocketing. So, as mentioned, as I mentioned, we have strong constraints. So, our memory consumption, the RAM, should stay below 200 megabytes on this specific device.

And our app were using too much memory, so we couldn't deliver it to our users. That was a problem. So, we need to reproduce it.

It's simple. First, we launch the app. So, welcome to TF1+.

Then, we select a program. So, it's Libra Fleur Rouge, a French program. And then, you launch the player.

So, you look at the video. And last but not least, you do it 100 times. Quite easy.

This makes sense because TV users never kill their application. Maybe you use your TV every day and never kill the application on it. So, we want our app to be robust and not consume too much memory if users are looking at TV every day.

So, to automate the process, we created a script using ADB. So, it allows us to reproduce the process easily and avoid taking time to do it 100 times manually. And with this, we can draw a graph.

And, yes, we have a problem. The memory is going up to 360 megabytes and the application crashed. That is not acceptable.

So, our first step is to, we want to debug it. So, our first step is to formulate an hypothesis because it's a general debugging advice. You have to do an hypothesis, test it, find a way to test it easily, and then iterate.

Maybe you find the problem and you correct it, you fix it. Maybe you do another hypothesis. So, in our case, the memory is going up to 401 megabytes and the app crashed.

So, we are not experts, not yet. But we can say, okay, memory is going too high, maybe it's a memory leak because there is a memory issue. And when there is a memory issue, we say, oh, memory leak.

But before diving into it, let's see what is a memory leak. But to understand what is a memory leak, there is another concept which is garbage collector. So, to understand how memory leaks occurs, we have to understand first what is a garbage collector.

So, we are on Android TV. So, on Android, the garbage collector can vary depending on the operating system version. But they all generally follow the same principle.

First, it identifies routes. It's called GC routes. So, it's the entry point of your app.

Sometimes, it can be activities, it can be static classes. But to be able to have a simple example, let's say it's our application. Then, this route have references to other objects in memory.

Imagine you have two screens, home screen and player screens. Maybe you have it with a React Native screen. And the screen also reference other objects to run the application.

And so, all these objects are reachable objects because they are reachable from GC routes. Let's say we have a player. We can show it in the green here.

So, for now, our app consumes some memory, but it is necessary to run it. But what happens if the user leaves the player screen? The player screen will not be referenced anymore by the application.

So, it becomes a non-reachable object because it's not reachable from GC routes. And all other objects referenced by your player screen become non-reachable. So, when the memory is still used at this moment, but when the system is running low in memory or when the garbage collector sees that there are a lot of non-reachable objects, the object can be removed from memory.

So, they explode. But what happened to our player? We had a reference from our application because maybe there is an architecture problem.

We had this at TF. Maybe there are an event listener in the application using the player. So, yes, the player is still referenced.

So, it's still reachable, and the garbage collector can't clean it. So, we have what we call a memory leak because we are not using our player anymore, but the garbage collector can't remove it from memory, and this is a memory leak. Okay.

So, that's the theory. But in practice, whether my node is reachable or not, I don't care. I want to know where my code is leaking.

So, how can I find it? So, maybe you can—I don't want to read heap dump like this. So, I didn't introduce it, but the heap is a part of the memory where you can have your memory.

And you can dump the heap with Android Studio, but, yes, it's quite hard to find. I don't see my code. I see bytes.

I see float. So, okay, maybe I can see an increase of bytes, but I want to see what is leaking. So, do we have a tool to find it?

Of course, yes. There is a tool named Leak Canary. So, it's an open source library created by Square.

It's like the software mentioned, but for Android. So, it's an open source library created by Square, and it reports memory leaks in your application and helps to find them. It's widely used in the world of Android mobile development, but not necessarily known to all React Native developers.

So, we will see how it helped us at TF. So, first, it's easy to install. So, there is a screenshot of the documentation.

You add the dependency, and that's all. No configuration needed. You can run it.

So, then you launch your app. You reproduce the problem. And, yes, we see our first pop-up from Leak Canary.

So, if you see this pop-up, you probably have a memory leak. It's saying for retained objects, there is a leak. So, let's look at logs.

You can find it in logcat or in a special Leak Canary activity. And we see a stack trace. And in this stack trace, it's little, but we will zoom after.

We see which object is leaking. And all the references to this object are underlined. So, if we zoom at it, we can see that player activity is leaking.

And it's retained by, wait, ZZAG.ZZH. So, yes. If you're lucky, the leak is in your code. So, you find your code, and you can debug it easily.

But we are not lucky. It's a leak that occurs in an external dependency. So, yes, it's hard to read.

But it also says where is which dependency is leaking. And we see it's in Android, in the media library, in media manager instance. So, it's kind of weird.

Is Android code having a memory leak? It's Google. It's a big company.

Maybe they don't do memory leak. Ah, no. We found there is an issue on Google issue tracker, and it seems to be that one.

So, yes, to let you know, there are a lot of leaks in Android. Sometimes, it can be more or less important. In our case, it was our player, so it's really important.

So, before thinking about fixing it, let's just remove the feature. Yes, we removed the feature, literally. So, yes, it worked.

We measure the memory again, and it's good. The blue line is under the red line. And yes, we couldn't go into production because of Google.

So, it would have been hard to find it without LeakCanary. Finally, Google released a new version with the fix, so we could update the dependency. So, we are good.

We can say memory leaks are easy to find because we found LeakCanary. Memory debugging is really simple to do. There is no problem.

No, it's not like this. It's one of the most challenging problem I have faced in my life, so, and we spend the day of debugging memory, so you will see why. Let's talk about another time, like two weeks after.

We wanted to update the application on the same store, so same device, same store, and people reviewing your app said, your app consumes too much memory. We are not going into production like this. Again, because we have LeakCanary, we don't have problem again.

Just a small reminder, we want to stay under 201 megabytes of RAM. So, we do the same thing as before. We use the problem with our small script, and yes, the problem is back.

Okay. So, let's formulate an hypothesis again. It's the same process.

We are experts in memory debugging, so the memory is going up again. It's a memory leak. No, it's not.

Because we have LeakCanary, it's not reporting anything, so it should not be a memory leak. And if we look closer to the graph, we see that the app is not crashing because when memory goes down, we look at our TV, nothing seems to happen. So, why is the memory is going down, but the app doesn't crash?

So, we said before that the memory leak is when the garbage collector cannot collect memory because we have references to object in our code that are left. But here, the memory can be collected. So, maybe it's not a problem with a memory leak, it's a problem with a garbage collector.

It doesn't run often enough, maybe. So, it's our second hypothesis that's a problem in the garbage collector. So, first step, we look at logcat, so to see logs about our application, about the system, to see if we can find some log about the garbage collector.

And yes, we find some logs, a lot of logs. It seems to run really often, and there are a lot of logs. So, this garbage collector runs, but it seems to collect nothing because memory still increases.

So, what's happening? We found a specific log occurring only when memory goes down, which is a memory warning called trimMemoryComplete. So, in Android documentation, we found that it's a log saying that the system is running low on memory.

Okay, why not? And our app will be the next process to be terminated. Oh, it's a problem.

So, we saw that the app wasn't crashing. So, all the memory is liberated if the app doesn't crash because if our process is terminated, the app crashes. We find some research a bit about this trimMemoryComplete log, and we found something in React Native core repository.

It is a function. So, we listen to system memory pressure events like trimMemoryComplete, and we respond to them. Not we, React Native responds to them.

And when a trimMemoryComplete event occurs, it calls the garbage collector. So, oh, yes, there is something with the garbage collector, but we are on React Native side. We are not on Java or Kotlin side.

So, it's calling JavaScript garbage collector because when you do React Native, you have JavaScript side with Hermes running your JavaScript code. So, it was a problem with the garbage collector, but it was not the Android garbage collector. It is the Hermes garbage collector because there is no—there is not one garbage collector, but two garbage collector.

It's kind of complicated. But, okay, let's look at it. Imagine you're creating a player.

It's a—I work for Teflon, so we have a lot of players. So, on JavaScript side, it will create a player variable, okay? But maybe our player is Android code because we use Android player.

So, it will reference a Java object, but maybe this player will also reference native object. So, like images, animation, SVGs, and C++ allocation, like string or other things. And your JavaScript code can also reference native objects.

Like, for example, when you do a fetch, there will be a native allocation, but your fetch is in JS. So, let's put number into it. Maybe your JavaScript object is very small because it's just a variable with almost nothing in it, but your Java code is a little larger because it does more code.

And the native object can be a lot larger because it might include images, SVGs, like I said before. So, for the moment, we don't see why your app is consuming 400 megabytes of RAM. But if we—what happens if we create 300 JavaScript players?

Maybe for player, it's kind of hard to understand, but like as I said before, it can be your fetch, it can be components, it can be a big state. So, it can happen. So, on JavaScript side, you only have 15 kilobytes of memory used.

So, Hermes only sees that and it will not run the garbage collector. But on Java side, your objects are still referenced. So, it has 300 kilobytes of code, but it's still referenced.

So, garbage collector doesn't run. And on the native side, objects are still referenced. So, we can't remove them from memory.

But if we look at our native object, there are 150 megabytes of native objects. So, yes, JavaScript is rating up to 150 megabytes of native object because Hermes only sees 515 kilobytes of code. So, in practice, how did we fix it?

So, we found an issue on the Hermes repository related to memory usage when doing API calls. So, we could reproduce the problem with an empty app that made only API call. And there were two problems.

One in Hermes related to fetch. This is linked to a leak in Wikmap. And the second problem that was Hermes isn't aware of native memory usage.

So, the Hermes team addressed the first issue, the issue in Wikmap, and it should be included in React Native 74. So, it's released today. And for the second issue, Hermes team added a method that allows native libraries to inform Hermes how much native memory a JavaScript object retains.

So, it's more useful. It's useful for native library maintainers. So, Hermes can take it into account for garbage collection.

On our side, we are not on React Native 74. So, we just run the garbage collector in the background. It was a quick fix, short-term solution.

And it works. So, yes, we have this in production. So, it concludes our second example.

So, to conclude with what I said with debugging memory, there is no easy way to debug it. Each time you debug something, it's a different thing. So, there is no magical formula that lets you debug everything easily.

But the main things that can help you in debugging memory are, first, locate where the problem is. Because we saw that it can be in JavaScript, in Java, or in native. So, first, locate the problem.

Because we lost a lot of time by not locating the program. Then you have to simplify your system. Because it can take time to reproduce problems.

Like, sometimes we run the script for three hours. So, it's better if you can automate the process and reduce the time. And last but not least, please install Leak Canary.

It doesn't cover anything, but it's a must-have for memory leaks in your Java or Kotlin code. And it's really easy to use. So, thanks for watching.

You can find me on Twitter or GitHub. For GitHub, it's an I, not an L. But thanks.

### Mo
Awesome. Come along now. Interesting choice of a GitHub handle.

Purposely misspelling your name is new. Okay. Cool.

Well, thank you for doing that talk. IATV is near and dear to my heart. So, it's cool to see that.

And I would ask you to dance on the stage right now. But we'll leave that for later, I guess.

### Maël
If you have some alcohol, maybe I can do it. I don't.

### Mo
I don't carry alcohol on myself, on my person. It's not encouraged. Cool.

All right. So, let's jump into it. And, again, for the audience, you can just reach Slido there.

So, generally, your experience on TV apps. And I think we went specifically deep into the topic of memory leaks and memory usage. But I'd love to just hear what are the biggest gotchas.

What has your experience been? Because I'm presuming you did mobile development before. So, what was the biggest gotchas and the biggest challenges going from a mobile development perspective into TV development?

### Maël
I think when I was developing from mobile, there were some issues on low-end Android devices. But performances on TV are sometimes horrible. So, for example, at TF1, we don't use FlashList, FlatList.

We have a custom list to have good performances. So, performances are a big issue. And also, the navigation, because you have to use your remote.

And TV remote. So, it's weird at the beginning when you use it for the first time.

### Mo
Yeah, definitely. There's a lot of gotchas there.

### Maël
But for the other side, it's like iOS or Android.

### Mo
Yeah. Very cool. Awesome.

So, let's jump into some of the audience questions. So, firstly, there's a question on Leak Canary. And if there's an equivalent on the iOS side, or are you finding that on Apple TV, there's generally just not that many memory leaks?

### Maël
Yes. I haven't seen from iOS because Apple TVs can take like three gigabytes of RAM. But it can be important.

But I never debugged memory on the iOS side.

### Mo
So, for context as well, Apple TVs are probably an outlier in the entire TV industry. Most devices will have 500 megabytes of RAM, and they cap you at certain amounts. Or if you go to setup boxes, it gets even worse.

Apple TV basically stores the same chips that they use for phones onto the Apple TV devices, which is extraordinary. So, I mean, stuff like this doesn't really apply as much, which is great. Yeah, just buy an Apple TV, I guess.

Morgan has a comment, I guess. Saying that the bug, I'm presuming the bug that's being referred to here is related to the Android bug with the memory leak was opened in 27, and the beta version fixing the issue was in November 2023.

### Maël
Yes. Yes, because we debugged it like in the end of November. And we were like, okay, so we have a leak for three years ago, the leak was here, and the fix is like two days ago.

### Mo
Wow. Okay. Well, love your maintainers, folks.

It makes you really appreciate every single open source maintainer that we have in our community, right? How do you get metrics for memory usage from Android and the native side? What's the way to access that information?

### Maël
Yes, I couldn't cover it in my talk, but with ADB, you have a lot of tools and with Android Studio 2. On ADB, there is a command that lets you see the native memory heap, the native heap, the Java heap, and also other memory, which is like a JavaScript heap. So you can find where is the problem and then debug in Android Studio.

### Mo
Someone asks, is Google solving these kinds of issues quickly? And the answer is absolutely not. It takes them six years to do it, apparently.

### Maël
Yes, and on TV, there are not a lot of users.

### Mo
How do you create a system in place and how do you prevent these types of issues happening in the future, long-term? Is there a strategy that you have in mind and the team has put into place?

### Maël
So now, each time we install a library like React Native SVG, or when we want to go into production, we have a script, not the script I showed, but the same type of script, and we run it every time to see, okay, we are at 150, it's good, or no, we have to remove React Native SVG, we have removed that.

### Mo
Okay, cool. Someone's asked me how I feel to be able to talk to someone about RN on TV, and the answer is eclectic. I feel absolutely great.

Thank you for asking. Biggest challenges, we've covered them. So we've looked at some of the challenges on doing React Native on TV, and there's a question on, and I think you just touched on this, which was consistent measurement of memory across the board, even if it's not garbage collector-related, but just tracking the memory, and there's systems in place, I'm presuming, that does that as well.

### Maël
How to do it consistently? Yeah, to consistently sort of measure the memory usage. I think it's a big issue because, for example, for garbage collector, depending on how the box is, not depending on our application, just the box, the issue can be there, and the issue cannot be there.

So sometimes I touch the box, I'm like, oh, it's hot, so the garbage collector will run often, it will not work. So I have to restart the box and say, okay, no, the fresh restart is good.

### Mo
Yeah, okay. Sebastian Lorber has an interesting question, which is, what would you have done if Google hadn't fixed it?

### Maël
Okay, so the real story is that this was an issue with an old library for ExoPlayer 2, and Google have launched new APIs for the player, like Media3, and so our player, it's not us that do the player, it's another team, migrated to the new libraries, and it's not the same dependency. But if we couldn't fix the leak, I don't know, maybe just remove the feature. It was something with Mediasession, so like for Google Cast or something like this.

### Mo
Cool. Question that's being asked is, is React Native adding a noticeable overhead when you compare to native development? I'd love to get your take on this, and I might chip in a little bit on this one as well.

### Maël
I think what I learned at TF1 is that we can do it, so if there is an overhead, it's not a big overhead. And on other TV apps, I will not quote them, but they consume much more memory and are native.

### Mo
Yeah.

### Maël
And I think the only thing to know on React Native is that your bundle is in your RAM, so it's good to have a bundle analyzer, and the bundle is small.

### Mo
And to chip in on this, I think especially on TV development, actually the gotchas and the issues that arise are more around, the overhead is more around the codes that the developers are writing, because we assume you can go in and use a regular list, and that will behave as you expect it, and the performance will be fine. But in reality, that's not the case, and you can implement a really bad list on TVs in just native Kotlin, as an example, or Swift is less of an issue, but in general with native Kotlin. And so it becomes a matter of creating hyper, hyper optimized components for TVs that are limited in the API functionality, because TVs use remotes, but they are heavily performance, so that becomes the priority.

Cool. Well, thank you so much for doing this talk. It was very interesting, and, yeah, we'll see you around.

Yes, thank you.