---
slug: >-
  /talks/frenchkit/swift-connection-2024/nicolas-zinovieff-data-data-its-everywhere
date: '2024-09-23'
title: Data? Data! It's everywhere!
author:
  - Nicolas Zinovieff
video: f_4JQIuTqRg
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/f_4JQIuTqRg.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Zino
Thank you Simone. So yeah, we're going to talk about data because data is super important. First question of course is, why?

Well I come from a math and computer science background so I like numbers better than feelings and when I talk to people about what they use for data they go like, oh I like this better and I'm like yeah, but how fast is it? So when I offered to measure it, I just did and it seems like a very important trait of data mining, right? Because if you've ever done that, changing the underlying structure of your data storage is something that has a huge impact on the rest of your application in development.

A few words about how I approached the problem because math, again, I took one gigabyte of data and I would write the data to disk and I would read the data to disk and try to manipulate it and I would measure how fast it went or how much memory we used. A couple of things to note, generation is random every single time because some of the frameworks that we use cache some results so you might have some speed up by caching as was mentioned in the previous talk. And so every time I run the test, the data is fresh and new and cannot be cached.

A few words about the baseline, so for reasons that will appear evident after a while, it's the last Mac mini Intel version that you can buy, it has plenty of RAM and SSD. As I said, it regenerates the data set before each test and I wanted to try a new framework, it's about a year old, it's called Benchmark. It's promoted on Apple's website that allows you to measure things with a very high granularity in terms of bytes that you use and milliseconds up to microseconds of run time on the CPU wall clock and that kind of stuff.

And so it was an excellent way to try that framework, right? Let's start with the old school way of doing it, before all the cool and fancy frameworks we used to just write text to the disk and do our manuals, Qlite stuff. I wanted to see how well it held up.

For reference, so if you just read a JSON, I picked JSON rather than PLIST because JSON is a little bit more modern, but once you read the whole data set, so the one point something gigabytes of data in RAM, it takes about the same amount of RAM and the same amount of time to calculate the average for that particular student in that particular class, right? Which makes sense. And as we're going to go through a lot of numbers, keep in mind that once the whole data set is loaded in memory, it takes about 36 milliseconds to calculate the average for that student in that class.

And serializing the whole thing to disk or reading it whole from the disk takes about 10 seconds. First question, if you want to use JSON or if you want to choose between JSON and Qlite, so if you've done a little bit of computer science, you know why databases were invented. That's exactly for that.

So we don't have to read the whole text file to find one little piece of data. And it makes sense, right? So it's 800 times faster to use the database for reading, but because of the way the database is structured, inserting data in a database is slightly slower than just writing the whole structure to disk.

So you will have a little bit of performance hit when you try to use Qlite manually, but you will have a huge speed bump when you try to read data out to disk. Side notes on that, please, please, please, please batch your write operations. If you do not, see, that's the big, big, big pink slice.

If you batch by 100 or by 1,000, it's the two smaller slices on the left, right? It's about 10 times slower if you go one by one than if you batch them by 100 or by 1,000. But you don't have to make super complicated stuff, just batch the commands.

Next up, I wanted to check if a modern framework that encapsulates on that prevents you from writing your own Qlite wrappers and your own SQL code would make any difference. I picked, not randomly, I picked Blackbird because it's fairly modern, and the approach was interesting, right? It is optimized for writing less code rather than having more speed, which was a nice and bold thing to claim, so I wanted to check it out.

And it actually bears fruit because it's three times fewer code than manual Qlite, and as you will see later, it allows me to write that piece of code super easily and to debug it, most importantly, super easily. Here are the numbers, right? So in terms of memory, because of the scaffolding and the way Swift works, you have to encapsulate and to wrap every single property and to make sure that the type safety is managed correctly, you have schema versioning, like if you upgrade your data manipulation methods.

So it's about three times, it uses about three times as much memory. Remember we're talking about a few megabytes, a few milliseconds, so it's quite okay. And in terms of speed, we have the same story, right?

It's about three times slower to use a framework like this rather than just writing your own Qlite code, but it is full async await compatible, it manages migration between your schemas and that kind of stuff. So in my opinion, it's totally worth it. You just have to make sure that you understand the tradeoffs of using such a library.

And then we have the official way of doing things. So core data, which is, by the way, turning 20 next year, and its successor, Swift Data. A few words about that, if you've, can you raise your hands if you ever try to use Swift Data?

Okay. About half. So it makes sense to try that out because under the hood it's Qlite, right?

But it's also core data. If you have ever hit a bug using Swift Data, you will see that you more often than not end up in a core data function. So it's a wrapper, mostly a wrapper array on core data.

Here are the numbers. Swift Data is about 10 times slower than core data. And core data is actually faster than manual Qlite.

By a good portion. It's about twice as fast as writing your manual Qlite code to use core data. Okay, at this point you're like, oh, okay, you're just bashing Swift Data.

I'm not. Swift Data has an objective in mind that is very different from what I was trying to do. I was trying to serialize a huge bunch of data and read a huge bunch of data, and it is meant to deal with small UI elements.

So it is not the same purpose at all, which may explain why these results were so drastic, right? At this point in the presentation, you're like, you know, you haven't told us what to choose. And yes, and I won't.

I will just give you various points to help you choose. If you go with Qlite and core data, you can know that they are mature and they work, basically, but they have the old syntax. It's C and it's derived from Objective-C.

So if you're not familiar or if you're not at ease with these old idiosyncrasies, and we saw a couple of things like that in the intro, right? Don't use it. Also, it is super hard to debug because it is a huge piece of machinery and you have no source code.

So again, right, it's about being at ease with that. If you want to use something like Blackbird or other Qlite libraries, they're great for rapid development. The same thing that took me two days because of a stupid bug because core data requires an application environment that talks to core services, took me two days to debug that.

I wanted to have a CLI tool. The same thing took me like two hours in Blackbird. So for rapid development, that's probably one of your best bets.

And Swift data, despite the numbers, I don't hate it, I don't think it's bad. It's just you have to be aware that it's a work in progress and the differences between Mac OS 14 and 15 are so huge that there is no way today to tell you if it's going to be the right choice down the line for now, right? Test it.

See if it works for you and use it if you want. A couple of words about Benchmark. If you like data, like I do, try it out.

It's super interesting. It gives you very fine granular data on your run times and memory that you use up to the megabyte for some things and up to the microseconds for some other things. So it's nice.

But it has a lot of idiosyncrasies, like it has one cycle, it can generate some leaks. So be careful with it. It's not ready for primetime yet, but it works super well for people who like numbers like I do.

A couple of bonus rounds and then I'll leave you with that. So obviously, Intel versus M1, right? M1 is twice as fast.

Kind of expected. A more interesting bonus round is that SQLite is actually faster on Intel than it is on M1 for reading, but slower when writing. Why?

I have, you know, some inkling as to why. I'm guessing for the write sections, probably it's the speeds that make the difference. And for the reading part, it's because 20 years of optimizations for, you know, I386.

So there's probably a lot going on in there. But it is very consistent. SQLite is super fast on Intel for some reason.

And I know that you guys want to talk to me about SwiftData. Come and find me afterwards, I can tell you about it. It is not that I don't like it, it's just that I don't know what to say about it because the results were super inconsistent during the tests, right?

Sometimes it would write the thing to disk and then the memory would go up from 3 gigabytes to 7 gigabytes after the writing was done. I have no idea why. And so that was my talk about data.

And I'm not even too long. Thank you. Thank you, Zino.

Sorry, it was a lot of numbers. You are surrounded. I am surrounded.

Yes. I surrender.

### Ellen
So how did you... So I'm a little bit curious about the benchmark framework. I know that you were sort of saying it's really good for, you know, for, you know, working with a CLI.

Were you able to use it? And you said that there was a serious problem because you weren't able to spin up core data without access to core services. How were you able to eventually get benchmark to work with that?

### Zino
So I cheated by trying to build a SwiftUI application. Because when you write a Swift package that includes SwiftUI, it somehow magically spins out an application rather than a CLI tool. So there are some things going on under the hood that you can cheat with.

But if you try to go the, like, pure CLI, you will not get, like, Swift data is actually kind of the same because it's based on core data. It will just tell you you can't do that outside of a core services context. But it will tell you that after it crashed a couple times.

### Ellen
Yeah.

### Zino
So, you know. But, yeah, if you're in doubt when using, when testing that kind of thing, try including some SwiftUI code. Because then macOS or iOS interprets it as an application rather than a tool.

### Ellen
Cool. I just want to point out, Zeno's wearing a shirt that said, Ne me posez pas de questions si vous n'êtes pas prêts de rentrer à la réponse. Which basically means, please don't ask me a question if you're not ready to listen to the answer.

### Julien
Sorry. And this is a good transition with the next question from the audience. Uh-huh.

How about Realm?

### Zino
Okay. All right. So, how about insert any multi-platform technology here?

The thing is, as you can see with Swift data and core data and SQLite, the more layers you add, the more trade-offs you get. So, I'm sure Realm is super convenient when you're trying to do some multi-platform stuff or when you're trying, because you know that kind of stuff. I'm sure it is.

I haven't had to write a cross-platform application for a long time, so, super happy about it. So, it kind of is unfair to compare performance and memory from something that's meant to be cross-platform versus something that's meant to be native, because you lose all the optimizations. That's why I didn't include it.

I'm just saying, test things before you choose, because it has a huge impact on your development cycle. Anyone who's ever had to retool the whole low level of your application, you know what I mean. Test things, make the best show you can, and have an escape hatch somewhere.

### Ellen
Yeah, I think, speaking of Realm, they recently deprecated their major sync SDK, so, good luck with that. Another question I had was, there was a slide in there where you said that Swift data is more designed to use with sort of smaller data sets, where it's mostly just one screen being displayed at a time.

### Zino
Not necessarily data sets, but smaller extracts.

### Ellen
Okay.

### Zino
Smaller manipulations with the database.

### Ellen
So, what you would say is maybe more like, maybe sections of the data set?

### Zino
Yeah.

### Ellen
Okay.

### Zino
So, my guess is that, because, and that particular test, because it's serializing one full gigabyte, 1.2 actually, but it doesn't matter, it kind of goes, like, if you imagine something like a social feed or whatever, where you have small views that encapsulate a long piece of data, my guess from the way it works and kind of crashes I got, is that it's optimized for that. Like, small queries that give you one or two or ten objects, rather than I want to grab the whole thing and do some heavy calculation. And it was not meant for that kind of test, right?

Like, if you are trying to do what I did, like grab 7,000 students and try to calculate the average grade for one of the students, certainly that is not your friend. Because it has to load the whole data set at some point. So, yeah.

Okay.

### Julien
Have you tried to benchmark it on a real physical device and did you find a huge difference?

### Zino
Yes. It is all on a physical device, it's Mac OS rather than iOS. Running the same code on iOS yields the same kind of results.

I just got my new iPhone, so I haven't tried on it, and my old iPhone is an SE generation 1. So, again, I thought that the benchmark would not be fair. But in the limited tests I did, it is fairly accurate.

You see the same kind of delta. If this thing is three times as fast, then this one is going to be three times as fast on all platforms. Okay.

### Julien
Thank you, Zeno.

### Ellen
Thanks, Zeno.

### Julien
Thanks a lot.