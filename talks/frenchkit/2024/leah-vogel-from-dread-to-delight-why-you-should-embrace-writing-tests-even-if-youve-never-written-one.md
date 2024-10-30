---
slug: >-
  /talks/frenchkit/2024/leah-vogel-from-dread-to-delight-why-you-should-embrace-writing-tests-even-if-youve-never-written-one
date: '2024-09-23'
title: >-
  From Dread to Delight: Why You Should Embrace Writing Tests (Even If You’ve
  Never Written One)
author:
  - Leah Vogel
video: r0luDOTLxUQ
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/r0luDOTLxUQ.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: '2024'
allow_ads: false
---
### Leah
I'm going to get my bearings for a second. This is a cool clicker that I've never seen before. Let's see if I can figure out that forward goes forward or not, or backwards.

Backwards is forwards. Okay, I'm probably holding it upside down. Aha.

Okay. So hello, everybody. I'm going to start from the end, which is actually the beginning.

I'd like to thank everybody who has been instrumental in getting this conference together, whether it's the organizers, fellow speakers, definitely the sponsors as well, and of course the audience, because without an audience, there is no conference. So thank you all for being here today. That's a hand for you.

So I like to start my talks off usually with some kind of interactive web-based thing where you guys answer a bunch of questions, but it's a short talk today. So we're going to skip that. So I do want to know, though, with a raise of hands, who has never written a test?

Can you raise your hand? Don't be shy. That was me not long ago.

Wow. How many people love writing tests? How many people hate writing tests?

Okay. So we have a few addressable groups here today, and that's what we're going to talk about. Who am I?

My name is Leah Vogel, as we said. I started iOS development back in 2012. The picture of me is actually the dinosaur.

I'm currently the director of engineering at Chegg, which means that all of the mobile development of the company is under my purview, but basically on my day-to-day job, I tell people who tell people what to do, but I'm still an iOS developer at heart. That's where I started, and that's how I identify, that's how I feel, and then I listen to talks about technologies that I've never touched before, and I'm like, okay, one day I'm going to try that. It hasn't happened yet, but I'm always inspired listening to things and hoping that I'll get there one day again.

Other fun things about me. I am a lefty. This is my first time in France.

I actually had this great idea that I was going to walk on the stage and I was going to say something in French, and everybody was thinking I was going to speak French, but my accent was so bad, I figured, no, I'm not going to do that. An embarrassing picture is bad enough. It's better than my French accent.

I have six kids. Yes, so I'm very good at managing edge cases and concurrency and crashes. That's right up my alley.

I used to be a teacher, actually, before I was a developer many years ago. I was mainly a math teacher, and English is a foreign language, and my hobby now is public speaking, and this is my opportunity to go back in the teaching role again. And I love books.

I really, really love books, whether they're science fiction or fantasy or work-related. Currently, I'm reading a really cool book called Tubes, A Journey to the Center of the Internet. It's kind of cool.

And I also just read Wool, which is the first of the Silo series, so that was fun, too. Okay. What are we doing here today?

If you read the short part of my talk, the description is we're going to talk about why we're testing, and hopefully be a little bit inspirational to those who don't write them yet, which I see as the minority, and to those who hate it, maybe hate it a little less, and what we're going to do is first talk about my first job, where I learned what a test even is, more about whose job it is to test, what testing exactly is, and why we need to do it.

A few next-level things to discuss, new technologies that have come out, and a quick summary. And so a lot of you in your development lifecycle, you start out at the beginning of the feature feeling really happy, and then you start getting into the groove of things, and things are going great, and the development's going fine, and then if you work at a company like mine, part of the definition of your feature is that you have to write tests, and then you start going, oh, God. And this is how you feel.

So the aim of this talk is to make you feel maybe like this, or if we're being more realistic, like this. Okay. Disclaimer.

I'm not going to be telling you how to test, how to write the tests, and I'm not going to be telling you how to get buy-in from your leadership. That's a whole discussion in itself. I'm trying to slow my talking down.

I usually talk way too fast, and I use a lot of emojis, so let's do it. All right. About my first job.

The first job that I worked in, and this is in humor. That's the emoji. The first job that I worked at, you've all had your first position, unless you haven't started yet, and once you do, you'll know there's a lot of strength in the people who are teaching you about your first job.

You learn a lot of things, and you accept them that this is how things are done in the industry as opposed to this is how things are done at this company. For instance, I learned that you must do all UI programmatically, because that is the way that things are done. Another thing that I learned that is really important is that you must use Git only in the command line.

This is very important, and this is how things are done. Another thing I learned is that Objective-C has the best syntax. It's got its square brackets, and it's got its at signs and its asterisks, and very intuitive and easy to learn.

Client developers always know what they're doing, and their code is always correct, and, of course, what do you have QA people for? Developers don't test their code. What was Glide?

Glide was the first company I worked for. It was a video messenger. I don't know if anybody here had heard of it.

It was really big in the day, and I really liked working there. I was very fortunate to have such a great first job, and one of the features I worked on one time was something called super emojis. That's what our product manager called it, and it meant that when you send a single emoji message, it should pop.

That was my feature. I had to make the emojis pop. This is kind of what it looked like.

When you would send a single one, it should pop. If you send more than one, it should not pop. So I started writing my code.

I'm like, okay, this is going to be my method. Everybody remember Objective-C? Okay, so I'm going to check if it's a single emoji, and I'm going to check that it's exactly one because single equals one.

This is very important information to store for later. And then check if it's an emoji. I didn't write that complicated code, actually.

I took it from Stack Overflow, and there we go. And I ran it, and the emoji didn't pop, and I thought, well, what's wrong with it? I checked if it's an emoji.

It's a single emoji. Why isn't it popping? So it turns out that a single emoji is actually a count of two.

So I modified the code, okay, so now instead of checking if it's one, I'm going to check if it's two. Now it's going to pop. Boom!

It popped. I was so happy. I went to my team lead.

I said, yay, look, I finished the feature. He said, I bet you didn't. I said, yeah, I did, and I showed it to him.

He says, well, watch me kill it. And he put in a flag, and it didn't pop. I said, what on earth is going on here?

Why isn't the emoji popping? He goes, aha, this is a teaching moment. He used to love that.

And he said, this is a teaching moment. Now, his style of teaching was very interesting. It wasn't usually just like, okay, he's going to give me a lecture.

Usually his teaching moments look like this. This is an actual thing that he would do. He would make a Morbo from Futurama.

He would quote the terrible thing that you did. He would put it up next to your computer, and everybody would see that thing that you did. This is one of my Hello Core data.

Okay, so back to the teaching moment. He says, let's write a test. And I said, well, what's a test?

He says, come on, you're a teacher. You don't know what a test is? I said, okay, well, what's a test in this context?

So he says, well, first of all, your code is bad. He was a great teacher. First of all, your code is bad, and you need to split it up.

So let's split it up between, first of all, checking if there is an emoji, and then we'll check if it's a single emoji. So this is the emoji code, which I stole from Stack Overflow. And now he says, now we're going to write the test.

So how do you write a test? First, you set up your variables, and then you set up your assertions, and then you run it, and you wait for the wonderful green check mark, which was amazing. So I said, oh, that's so cool.

He goes, now look what happens. So then he put the flag in, and of course, as expected, it failed. I said, but I don't understand.

Why is it failing? He goes, this is part of the teaching moment. No, I don't understand, because I already knew that 2 equals 1 is a math teacher.

But I did not know the next part was much more complicated. So I'm like, what on earth is that all about? And he said, listen, it's because stuff we're not going to talk about right now.

I will tell you, though, in Swift, much easier. So fix the code, fix the test, everything worked, and it was wonderful. So this was about two years into my job there at Glide.

I was there for four years. And, uh, yeah. Okay.

And then we did some kind of pivot. Has anybody here heard of the wrist cam? So you can see it was wildly popular.

Made a hardware pivot and decided to make a band for the Apple watch that had a front-facing camera and a rear-facing camera. It's actually really cool technology. It's also kind of ugly and really, really thick on your Apple watch.

And if you've ever been in a company that was a software company and pivoted to hardware, then you know what comes next. And it's time to look for the next job. Okay.

So now we're going to talk about a little bit more about testing. When I got to my next position, which is a company called OrCam. OrCam builds assistive technology.

What you see here is some stuff for people who have visual impairments. They also do things for people who have hearing impairments. And the job of the model is to help people with visual impairments The mobile team was to write the companion apps for the hardware devices, and it was using a lot of Bluetooth, really interesting.

And when I got there, I heard that people would keep talking about the testing, the testing, the testing, not in the mobile department, but more in the firmware, in the embedded, in the machine learning parts, and I'm like, what are they talking about? Now, I didn't know that there was a test. I wrote a test once, but obviously they're talking about something else.

So because I was confused, I thought I would do the thing I know how to do. I'm gonna ask my little brother who knows everything, because he will be able to tell me. And so I said to him, hey, you know, at work they're talking about testing, and I'd like you to give me some more input about that.

And he's like, what, how have you survived as a developer for four years, and you don't even know what testing is? That's just the way it is. So he sent me some stuff, and I did some learning, and I got really excited about it, and I wanted to start implementing it, and I started working on the test, and then I started evangelizing it to my team, and my team asked me the great question, why, why do we wanna do this?

And that was really a good question. There's a, if you've heard of Simon Sinek, he's got a great talk called Start With Why, and usually when you start with why, you have a lot more chances of getting people to agree to what you're doing, as opposed to telling them what and how, tell them why. So I didn't really know why, so I decided to look into it.

So here I'm going to share with you, if you don't know already, some good reasons why we should write tests, one of which is craftsmanship. Most engineers like to pride themselves on being good craftsmen, or craftswomen, or craftspeople, as it may be, and writing the test actually helps you focus on what's important, what's not important, figuring out edge cases. It actually helps you restructure your entire architecture, as like, even the most basic example of the emoji code, separating it out into two methods, and making sure things are solid, that goes a long way, when you start thinking about testing, and how you're going to make your code testable, using dependency injection, mocking, stubbing, whatever you need to do, to be able to test it in a good way.

Another very important reason for testing is reliability. Now when I say reliability, it's not only the fact that your code works as it is, but it lowers the stress of thinking in the future about refactoring, touching legacy code that, you know, it already works, you know the kind of code, everybody's got that in their code base, if you're working in the old ones, like, oh, there be dragons, don't touch that, it works. But if you have a good test that tests the business logic and the flow, then it should lower your anxiety of changing something, because you just run the test again, if they pass, everything's good.

So that's really important, and also it gives you the ability to release with more confidence. So you write your new feature, or the server makes a change, everything's still passing, and it saves you a lot of time from hunting and fixing bugs. Another very important thing is about ownership.

So as I said at the beginning, developers don't test code, developers should test their code. If you think of the analogy of a person who doesn't test their code, it's kind of like a chef, who makes the food, doesn't taste it, gives it to the food critic, and says, ah, so how is it? And you have no ownership over the thing that you did, and when you take your code, and you write your tests, and you check your quality, and you make sure things are worth, first of all, you have the ownership of what you've done, and additionally, you save a lot of back and forth loops with QA, oh, I found this bug, oh, I'll fix it, oh, I found this other bug, like, why didn't you just test your own code? So that's really important, is to be able to have some more ownership on things that you do. All right, so different types of tests.

There's the most basic unit, ha ha, basic unit called the unit test. The unit test tests a single method, and then we have the integration test that tests how things fit together, you know, like a whole kind of flow, and then the end-to-end tests that go all the way across the board. So if we were to take something, for example, like an input validation or something, right?

So the unit test would be that the input that you put in, and you parse it in whatever validation that you're trying to work on, and then if you have your integration test, you say, okay, so how does that fit in with other parts of business logic, and end-to-end is the entire flow from the UI to the server, back and forth, et cetera. There are different schools of thought of how many tests you should write in each part of the pyramid. So this is the previous conventional one.

You write a lot of unit tests, fewer integration, fewer end-to-end, and the reason why this used to be the pyramid most likely is because unit tests run very quickly. They're easy to write. End-to-end tests usually take a lot longer to run, but that doesn't necessarily make sense because there's another school of thought that says we don't really need to write a lot of unit tests.

You really need to write a lot of end-to-end tests because that really tests the whole flow, this way and that way. I kind of like the middle way, which is, oops, which is spend a lot of time on integration tests. Why integration tests?

Because those are really the core units that you're developing for. Another question is, so who's supposed to write the tests? Well, we already said that developers should be writing tests.

If you have an automation team, most likely they'll be writing the end-to-end tests or the UI testing. There's question of integration tests if it should be developers or QA. Sometimes it's a combination, sometimes it's developers, sometimes QA.

I think that it's valuable for the developers to be doing it. Unit tests obviously is the responsibility of developers, and if you're an indie developer, you know whose responsibility it is. Okay, so I got people on board.

We're like, okay, so now let's do it. So where do we start? We had a huge code base, a bunch of different libraries, a bunch of different frameworks that we developed.

So what's the best place to start if you have no tests at all? So in my opinion, the best place to start is some kind of shared resources or something that's going to be used a lot. I would say it's not great value of testing something that's gonna happen once in your app ever, but it's something that you're going to be reusing a lot.

And in my case, at that specific job, it was Bluetooth. Bluetooth was the core of everything that we did. We had multiple apps, the Bluetooth library, which by the way, I got to be the one who rewrote it in Swift, which was fun.

And so I said, okay, test the Bluetooth. Anybody here ever work with Bluetooth? Can you run Bluetooth on a simulator?

So I was like, oh, well, I finally decided how we're gonna do the test and where I should start, but I can't run Bluetooth on the simulator. So it forced me to go, okay, so what's important? What do I have in my Bluetooth manager that is important to test?

So I had to extract that and figure out what it is that I wanted to make a protocol. So this is the Bluetooth protocol that my Bluetooth manager was going to implement, and I could have my block Bluetooth manager implement, and therefore be able to write all kinds of tests without actually being dependent on any kind of Bluetooth because I just wrote my own code and decided, all right, now it's connecting, now it's disconnected, et cetera. Now I could check the UI flows, the business flows, et cetera, okay, so did it, wonderful.

All right, let's keep going. Then I arrived at Chegg. I've been at Chegg for about four years, and it's my first position that I'm actually not hands-on.

So that means I write very little code. Last code I wrote was about two weeks ago. I fixed a typo, and before that, I don't even remember what it was.

And joining Chegg was a real difference for me because until then, I had only worked at startups, and Chegg is a corporate company based in America. And so one of the first things I noticed is that Chegg had a lot of tests. I mean, here's a picture of some of the, this is the CI, and I will draw your attention to that number over there.

This picture was taken a while ago, but there was a lot of tests going on, and not my little sorry emoji test. For those of you who are not familiar with CI, something to look into, there's some common CI names. When you have a whole team of a lot of people and automation and stuff, you can do a lot of cool things.

One of the things we used to do is after the CI jobs would run, we would send a message to Slack with how many tests passed, how many failed, what was skipped, whatever. You can go inside to the reports. One of the reports, things that we use, this is called Allure, and you could really check the health of your app, checking the red, the green, seeing what's going on.

Okay, so it was really cool to join a place with the testing culture. However, I do wanna say there's a warning. You don't just need to be writing tests for the sake of writing tests.

I saw a nice quote that I liked recently. Be careful what you incentivize, because that's what you're going to get. So there's the companies who incentivize lines of code, and people write garbage code, because you need to write a lot of lines.

People, you know, hours in the office. So people come to the office and drink a lot of coffee, socialize with their friends. And if you're just incentivizing for writing numbers of tests, then that's not really a good idea, because you might not be testing the right things.

The important thing about writing tests is that they're useful. You wanna write useful tests that give you value, that give you confidence, that, you know, make your code better. All right, so as I said, I wasn't writing code, but back in 2021, we had a hackathon, and I'm like, oh great, I get to be a developer again.

So I was on a team of people, and I got to be one of the iOS developers. There were two iOS developers. He decided he's gonna do all the UI, I'm gonna do all the backend.

That worked great for me. I was never really great at UI. And we did an app called Spaces, which was very relevant at the time.

This was during COVID, and this was about reserving office space. And we, our backend guys, you know, they worked on the architecture, and they did a lot of stuff. And we wrote this app, and it was really cool.

And I thought, wow, this is a really great opportunity to try something new. And the new thing I wanted to try was TDD. Recently, I heard that Daniel Steinberg mentioned something about ADD, anger-driven development, or RDD, rage-driven development.

But I just wanna talk about TDD, which, as we all know, is tequila-driven development. Now, if you haven't tried it, it's a lot of fun. So these are actually my laptop, and my little brother who knows everything's laptops, and we were working on some kind of code together, fueled by tequila, and it's fun.

Jokes aside, TDD is test-driven development, and the idea of test-driven development is that you actually write the tests before you write the code. So the red-green-yellow thing, red-green refactor, is you write the test, you run it, it fails because you haven't written the relevant code yet, then you write the code, you run it again, then you keep fixing it, iterating it, et cetera, until you get it into the place that you need it to be. Together with that, there's another benefit of testing.

It allows you to be unblocked. So when I was working on the Hackathon project, my code was ready before the backend code, and I'm like, wait, well, how am I gonna check the flows and everything? And this is how you do it.

You mock things. Now, you have to be careful about mocking. You don't need to mock everything.

You need to mock the important things, especially if you need to get unblocked. So for me, it was server code. There are frameworks for mocking as well.

You don't necessarily have to do it from scratch. I did list the Objective-C one here just because I'm a dinosaur. At Teg, we use Cuckoo.

Anyway, I bet you're wondering what happened at that Hackathon. So this is what happened, but it was a lot of fun, and I feel like it was winning is in everything because I definitely unlocked the achievement of TDD. There's another question.

Sometimes you don't need to test. Sometimes it's an idea just not to test. When would that be?

One of the times I feel that testing is not necessarily a great idea is if you're running a whole suite of A-B tests, checking a feature in different variations, you don't need to write a test for every single one of the variations for a test that you're running for two weeks necessarily. Write a good one for one of them, and you kind of wing it for a little while. Don't quote me.

Another thing is if you're writing code that you know is definitely throwaway code, like you have to just write a POC and to show it to somebody, obviously don't waste time testing. We recently were working on a new feature that had to be developed very quickly, and we were fairly sure that it's never gonna make it to production, and we didn't write any tests for it. It actually did make it to production, and we actually did have a production incident that we would have known about had we written one test to test the most basic flow, but it happens.

Okay, I'm gonna speak briefly about some of the new technologies that have come up. This has been mentioned quite a few times throughout the conference already, Swift testing. It was even in the great video at the beginning.

This was announced this year at WWDC. I'm not gonna go into detail about it because there's a lot of people in the audience who raised their hand that they love testing. I should have taken a picture and said anybody who has questions, speak to these people who actually do it.

But it's nice. It's got a nice clean syntax. Instead of using assert, it uses expect, and it's got its hiccups, but looks promising overall, and I think that one of the promising thing is, and it's just reiterating that testing is very important, and people are putting time and effort in making new frameworks to make it possible.

Another thing that's come out is AI. Should you use AI to write your tests? Maybe.

Do you use AI to do your other things? Maybe. It still needs a lot of supervision.

We were looking into tools recently for the automation team that actually have a way to write descriptive, just what you want your test to do, and it's supposed to just do it automagically. We haven't signed with anybody yet. Nothing's been great.

But just to speed things up, and when you have a class, you can actually feed it into AI and say write unit tests for these methods. That's pretty quick, but I don't know how much value you're gonna get out of that. So it's something to look out for.

I'm sure in the future it's gonna get better. All right, let's sum this up. So why am I giving this talk?

Otherwise known as what's in it for me? You know, when you're sitting here in the audience and you're listening to this talk and you're saying, you know, what is this? So I had been working in the industry for a while before I even heard about testing.

I know that someone had told me that in France, testing culture is very strong, which I saw by the raise of hands. But saying that, it's not always something that we love to do. And it's something that is very important.

And sometimes it's just important just to check a box. And I feel that it's really more than just checking the box and saying, okay, I did the test. I feel like if you understand why you're doing it and how it actually helps you as a developer, then it makes it a lot more palatable.

Okay, so bottom line is, I love that animation. Okay, so that's it for me. And yeah, keep calm and write tests.

Thank you very much.

### Julien
Thank you. Thank you, Leah.

### Leah
Oh, one second. I can't believe nobody has done this yet, but something that a lot of speakers like to do. So I have some help here, please.

So everybody need to raise your hand and say hi. So, hi.

### Julien
Okay, well, do you test it and do you validate it? Oh, do I validate? Okay, yes, I'll validate.

### Leah
Okay, thank you so much, everybody.

### Ellen
So I am a huge, huge advocate of testing, so I could probably ask you questions about this all day. But I'm gonna, other than complimenting you for the invention of tequila-driven development, that's pretty great. I wanted to ask sort of what your opinions are on a couple of things that I think different people have different opinions about that they've come to through their experience, and I'm really curious what your experience has been.

So in terms of when you have interaction tests, I think there are some times where you can have interaction tests that involve the UI versus what I call headless interaction tests where it doesn't involve any UI. What do you find to be a good balance of those things?

### Leah
Well, to be very, very candid, the UI ones we have the QA engineers handle, and the headless ones we have the developers do. So they're that kind of balance. Okay, fair enough.

### Julien
Okay, so pretty much the same question from the audience, with a specific question on snapshot tests. What would be the line, developer, QA team?

### Leah
Again, so in the company that I worked at, that was QA's responsibility. We actually recently had somebody on the animation team write a really cool thing that automates all the snapshots. We wanted to do it to use it for localization as well.

I think that there's value for developers learning how to use all these tools because it's just another thing to add to your toolbox, and you're not always gonna have the privilege of working in a company that's got an automation team, and sometimes the developers are going to be having to handle that all by themselves. So it's good to know how to do both UI testing and snapshot testing on your own as well.

### Ellen
And I'll note, you won't always have a QA team either. So I think one of the things that you talked about was sort of like trying to make sure that you're testing the happy path, where it's like we know most people are going down this direction. Obviously, there's kind of an infinite number of bad paths.

How do you figure out sort of which ones that you wanna test versus ones where you're starting to get diminishing returns?

### Leah
That's a good question. So one of the ways that we deal with testing at the company that I work at is that QA is responsible for writing test cases. And so they often are already thinking about all of the very unhappy paths, and sometimes as a developer, you might like, how did you even think of that?

They say like, I've seen a job requirement that the QA engineer's gotta have a criminal mind. So not all developers have a criminal mind.

### Ellen
My favorite QA guy I've ever worked with has said that he finds the best bugs when he's been testing something for like two hours and just starts doing the dumbest thing he can possibly think of. And then all of a sudden, he finds the craziest bugs that you can possibly find.

### Leah
I find that there's a lot of value of once you've like uncovered a crash, if you're using tools like Crashlytics, et cetera, and you find, oh, I'm gonna fix this bug, writing a test for the bug is good, and then you're covering obviously a path that you hadn't thought of previously. Yeah, for sure.

### Julien
Well, a new QA engineer will test it exactly every time in the elevator of the app to test the offline mode.

### Ellen
I did that too one time. We had a streaming app, and the way that I tested it, dropping the stream was riding an elevator up and down. We did that too in Glide.

### Julien
You said you wouldn't talk too much about money today, but well, the audience seems interested. So what's your takeaway to optimize a test course? So writing it maybe more quickly or less, if needed?

### Leah
Well, I don't know. I don't know. There are people now who are saying, okay, AI's gonna change my job out, and I'm gonna write all my code using AI, and I'm sure you guys have tried it, and most of the code is really bad.

So if the regular code is bad, the testing code is probably gonna be along the same lines. However, it's getting better, so I'm not discounting it, because as AI gets better and trained better, then I assume the tests will get better too, and who knows, maybe it'll turn out to be really useful soon.

### Julien
Soon enough, yeah.

### Ellen
Yeah. So you talked about one particular incident in which you had some sort of code that you thought was gonna be thrown away, and it's like, JK, that's production code now. Do you feel like that's given you any sort of second thoughts about things where you're like, you're more likely to write something that you, test for something that you initially sort of assess is throwaway code, but if it's like, oh, okay, oh, crap, that's now a production code.

### Leah
Yes, okay, so I guess it really depends on the situation, but I would say if there's something that has any inkling of perhaps getting to production, at least write a test of the most critical flow that you know, if this fails, this was literally an API call. There was nothing. There was nothing, and the API changed under the hood.

It was like, and it was a third-party API. It wasn't ours, and it was just like, it doesn't work. So if we had that one little sanity test, we would have caught it before the users did.

### Ellen
Yeah, I think one of my favorite ways to think about testing, and where to start with it is, if people are coming after you with torches and pitchforks, if it breaks, start testing that first.

### Julien
Another kind of torture, metrics, and Jeff is asking, what do you care about? Code coverage, number of tests, something else?

### Leah
Okay, so code coverage is tricky because it's hard to measure exactly what you're testing, and again, you can have code coverage where you're testing all different kinds of unit tests, but you wanna really get the integration, so even if you had the entire app more or less covered by unit tests, you might not actually be writing meaningful tests, so I think that you need to think about what's really useful, what is crucial for your app, what's really gonna make a difference to your users at the end of the day?

### Ellen
The canonical example of this in the United States was when the Affordable Care Act was first enacted. This was like the national marketplace for health insurance. All of the contractors who had been working on it had been working separately, and they had a zillion tests of each of their individual components, and then when they tried to actually make all the components work together, it completely blew up.

### Leah
It's like that picture of the bridge, you know? The bridge, and it just doesn't connect at the end. Everybody built their part.

### Ellen
Yeah, or like the thing where it's like, oh yeah, we've got two unit tests and zero integration tests, where it's someone who presses a button to open an umbrella, and the umbrella opens, but then the top of the umbrella just flies off into the space.

### Julien
Well, I think you also know the picture of the two windows that you can open at the same time. Yeah, yeah. Pretty much the same, yeah.

Did you succeed in introducing TDD in your teams?

### Leah
No. No, but the people who do it, they really like it, but it's hard to convince people to want to do it.

### Julien
So tequila one, or?

### Leah
Oh, the tequila works fine, yeah.

### Julien
Thank you, Leah.

### Leah
Thank you, thank you all. As you all know, it's immensely satisfying to see all those green checks when the tests pass, so keep testing.