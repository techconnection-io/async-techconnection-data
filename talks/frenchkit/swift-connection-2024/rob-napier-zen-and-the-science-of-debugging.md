---
slug: >-
  /talks/frenchkit/swift-connection-2024/rob-napier-zen-and-the-science-of-debugging
date: '2024-09-23'
title: Zen and the Science of Debugging
author:
  - Rob Napier
video: abZsSwC9aqA
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/abZsSwC9aqA.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Rob
It's been a good day, yeah? We've learned a lot, Swift 6. This is the last talk before you are released to dinner, and if it pleases you, the bar.

And I am the one thing standing between you and that release. My work is cut out for me. If I do my job correctly here, you will spend the next little bit pleasantly entertained, and maybe you'll think about it later at the bar.

What button does the thing? Who knows? Many things I say today, they may seem kind of simple, even basic.

But I'm saying them because they're the kinds of things that people forget when they're in the moment, right? When they're struggling with a very difficult bug that they don't yet understand. And you may feel you know these things, and that's good, but my hope is the next time that you are staring down that really, really hard bug, that you will remind yourself of this talk and the things you already knew.

At the end of the day, there is a difference between the way you think about programming and the way you think about debugging. Programming is a creative art. People often disagree with me, but I want to convince you, we imagine something, and then we reach out, and we make it exist when it did not exist before, right?

We make it real. That's art. That's what it is.

It takes a certain mindset. Debugging is not like that. Debugging is not about imagining how things might be.

Debugging is about figuring out what actually is. What is true. It's not art.

It's science. And when you want to really debug a very hard problem, you need to do some science stuff. What's science stuff?

The scientific method. We're going to ask a question, do some research, formula, blah, blah, blah, blah, blah. You all know the scientific method.

But I often find that people stumble before they even get kind of onto this loop, right? Before they get into the science loop, you first have to do something that isn't in the loop. You have to accept that you don't know something.

This is really a huge stumbling block. I have people come to me and they go, Rob, you know, I've done everything correctly, but my program doesn't work. I hate to state the obvious, but then you did not do everything correctly.

That's what correctly means. So the first thing you need to do is figure out what does this program do? Not what it's supposed to do.

Not what the spec says it's supposed to do. Not what the product team says it's supposed to do. Not what the comments or the function names say it's supposed to do.

You need to figure out what it actually does, right? And to do that, you need, at least for a little while, to give up hope. I originally named this talk, you have to give up hope, and my wife said don't do that.

So we got a different name. But you have to let go of the hope that you're about to find the answer. You have to let go of even wanting to find, or excuse me, how to fix the bug.

You need to focus on just understanding. Before we get into debugging, I kind of want to talk about those things that you wish you had already done. The actual debugging parts of this talk actually only help when you have a bug.

But you can do these things any time. You should. A dear, dear friend of mine went off into the desert to learn how to track animals.

Only in America. Yes, that's a thing people do. Okay, so he tells me, you know, you get started, and he went out in the middle of the night to track animals, staring at the ground, and he says, you think you can't find tracks?

And he says, there's tracks everywhere. The problem isn't finding animal tracks. The problem is finding the tracks you were looking for.

There are just so many tracks. The same is true of our logs. We log so many things.

And they are filled with warnings and errors. And there's all these things that could be wrong. But are they the thing that's wrong for this bug?

Ideally, if your app is doing what it's supposed to be doing, if the user is happy, there should be no errors in the log. There might be some warnings, but there should be no errors. Everything's working.

But we all know Apple frameworks throw a lot of warnings and errors on us, even when everything is working. So we also do that. And so here we are.

Sometimes weird things look normal. Excuse me, sometimes weird-looking things, sometimes a thing that is normal, looks very weird. So this is a good time.

I mean, well, not right this minute. It's dark, but maybe tomorrow. Well, after you get back from the conference.

But look at your logs. Sit down and just read them. Start at the top.

What's normal look like in your app? Now, there's a side benefit. I have found so many performance problems by just reading the logs and seeing that we were making duplicate requests or, no lie, migrating the entire database twice.

Because it works, but it wasn't supposed to do that. So I don't mean that just because it always does that, that it's right. But you would like to know what your app always does.

That way you don't chase ghosts. But finally, finally, that hard bug comes. You cannot reproduce it.

You've tried to fix it. It just keeps coming back. You've already spent a lot of time on it.

Now you know it's a hard bug. Now, sometimes you might know it's going to be a hard bug from the first moment you read it. Maybe it takes you a while.

But eventually, you know. It's time to do some science. At that point, I recommend stop, take a breath, put everything in its place.

Start a journal. Now, it can be on paper. I actually use paper quite a bit.

It can be a text file. It can be a fancy writing app. I actually use Obsidian as well quite a bit.

But whatever you like. I actually write a lot of times on paper and then copy it into Obsidian. It's just easier to write.

But whatever works for you. Keep it simple. People get wrapped up in their tools.

Don't get wrapped up in your tools. Just keep the journal. I always find that no matter how many notes I take, and I take a lot of notes, I always wish I had taken just a few more notes to remind myself what I did.

You're keeping track of all of those things you've already done. I ran a test. Great.

What was the setup? What device did you run it on? What was the OS?

What did you do? And that way, when you see what the result was, later you can go, oh, wait. All the times I ran it on a device that was running this version of iOS, I had the problem.

That's what you want. The other thing in your journal is put everything you are always going to need and are always looking for, put it at the top. I always have the link to the bug.

Because I never can find the bug again. What is the number? I can't remember.

What is the file that will reproduce it? Maybe the steps. Just write them out quickly.

But everything you need and are going to look at all the time, just put it at the top of the file. That's the great thing about computers. We can edit files.

But take a second. Get yourself organized. If I have one superpower, it is patience.

And I have solved a lot of bugs. Just by reading log files. Line by line.

Learn to do boring things for a long time. So a few seconds per line, it is a thousand lines. It is about an hour.

Maybe two. Read them. Even taking notes.

Things that you think will take forever, take like four hours. Seriously. Maybe they take two days.

But this is a bug you have worked on for months. Do the simple thing that is going to take a little bit of time. And remember, back to letting go of hope, you are not almost ready to fix the bug.

You have made 100 changes and none of them fixed the bug. This is not going to be the one. I'm sorry.

You're not there yet. It's possible, very likely, most of the time, the actual change you make will be tiny. How many bugs?

Large, huge, crazy bugs. I used plus one. But it may even be obvious in retrospect.

But you're probably not there yet. Until you've got that understanding. So what you need to do is you've got to get rid of all those demands.

There are going to be people yelling at you. Just fix it. Shut up.

Just fix it. And you're going to have to breathe, prepare, understand. Right now, you are ignorant.

But we can do things to make yourself slightly less ignorant over time. And that's progress. That's how you have to define, like, where are we on this bug?

Well, I had these questions. And now I have some of those questions answered. That's how science progresses.

Now, at the beginning and several times after, I want you to go read the bug report. I mean, no, actually read it. No, seriously, all of it.

The sheer number of times that I have seen somebody come to me and say, hey, you know, I can't fix this bug. It's like, well, let's go read the bug report. And we go through it, and they realize that they've been chasing the wrong symptoms.

Because that wasn't actually what the bug said. The number of times I have personally read the bug report found a comment, a page down, where I said the answer and then had forgotten the fix. You'll understand when you're older.

If you take nothing, nothing away from this talk, this, I cannot stress this enough. I started experimenting. I'm doing stuff.

I'm making changes. Nothing works. Nothing makes it better.

Nothing makes it worse, either. Sometimes you're in the wrong directory. Sometimes you're not loading it onto the simulator, even though you thought you were.

When you're working in big, complicated projects, sometimes you're not linking the things in. Your best friend at this moment, I'll tell you a secret. Fatal error.

If you can't crash it, you don't control it. And then you definitely can't fix it. Somewhat related, sometimes there are more objects than you thought there were.

I mean, how many great murder mysteries are involved? There was another such and such. True for bugs, too.

The number of times I've had, oh, that's not the view controller. I thought it was a singleton. Oh, turns out you can have two of those, and you're looking at the wrong one.

Back in the storyboard days, ever have, like, there's one that got made by the storyboard and one you created in code, and you're looking at the wrong one? One's on the screen, and one isn't? Yeah.

That's when that little identifier comes in real handy, when you print out your objects in the debugger, and it prints out that crazy number. That's great, because you want to make sure that number's the same as long as you're running the program. Yeah.

Make sure you're doing what you think you're doing. I want to talk about a big tool. Well, actually, kind of a small tool, and kind of the smallest tool, really.

On Stack Overflow, where I spend an inordinate amount of time, many questions, eventually we get around to asking, will you please make what's called a minimal reproducible example? I need the smallest amount of code that actually does the thing. And how do you get to that?

How do you get to the smallest program that still has your bug? Well, you chip away at it and everything that isn't your bug, and then your bug has nowhere to hide. It's awesome.

You get down to a few lines, and they fail. It's really easy to find the bug then. Except when it's not.

Have you ever had one of those bugs where literally you're looking, you know it's this line of code, you can see everything, there's nothing else, and it's still, you don't know? Yeah. Those are hard.

That's... I hope most people here have encountered git bisect. I'm not really going to talk a whole lot about it.

Go research it if you want to. It is incredibly useful, but there have been many, many, many talks on it. The short of it, if you haven't used it, is it allows you to go into git and say, this commit worked.

And this commit didn't work. And then it helps you find, you know, the one that made the change. That's awesome.

That is very, very useful when you want to find a regression. Like, it used to work, and now we broke it. Or sometimes it used to be broken, now we fixed it, and we don't know why.

Sometimes you do it backwards. Those are bisections in time. But there's another type of bisection.

You can bisect in space. And what I mean by that is I mean deleting a code. You want to delete code.

A lot of it. Like, most of it. If you can just keep deleting and deleting and deleting your code until only the bug remains.

And it's so strange. There is a really, really easy approach to this that people resist. I don't know why.

It's called test apps. Test app. Please.

Just make a little program that only has the pieces you need. I almost feel like I shouldn't have to say it, but I find I have to say it so much that I'm saying it to you. Build little tiny programs.

Make a little go over and copy over what you need. Now, you can go that way or you can go the other way. You can delete code.

I mean, just brutally. Just keep deleting things that aren't being used and comment them out or whatever you want. Keep making your program smaller.

This is so much easier to work in. You can iterate on them. You can build them in ten seconds rather than ten minutes.

Test programs let you experiment really fast. And another thing you can do with them that I really love is what if the bug were the spec? You needed to make this bug happen.

I mean, it's doing it, yes. But what if people came in and said, no, I want it to crash at this point with this stack trace? How would you do it on purpose?

Often you can find the bug just by trying to invent the bug and you'll find, well, that's where the code is that's causing the problem. And again, you can do these things in little tiny apps a lot easier than in your whole massive multi-module project. Another approach, test apps can just be unit tests.

You can just pull it over into a test case and try it there. See if you can reproduce the problem in there. Now, this gets people confused.

They get hung up at that point. They suddenly think we're testing. We are not testing.

We're doing science. They're really, really not the same thing. People then want to write a good unit test.

This is not the time. They want to, well, in order to do this, I have to refactor the code to make it testable. Not the time.

You're just experimenting. You can hack on the code. You can just put whatever random test data that you need, you can hard code it into the code, right?

You're all programmers. You can just change the code. We have Git.

You can get back the stuff. It's not going to hurt anything. And it was a test app, remember?

Test apps. Do not get bogged down at this point in like the future, right? We're not, we have no attachment right now.

We're just trying to learn. Eventually, you probably will want to write a test case. A good testable TDD tequila thing.

But in the face of a hard bug, you're going to need a lot of experiments. You're going to need a lot of records. Anyway, spend no time at this point writing good code.

Worst of all, do not explore a testing framework. Please. I've seen so many devs in the jaws of a very difficult bug.

They squander all their time messing around with a test harness rather than testing. We all love frameworks, don't we? They make automations or visualizations or whatever.

Those are things to do later, right? Not now. Do not get distracted by infrastructure.

We're doing science here. You do not need to spend six hours learning some new testing framework. You could do a lot of tests.

You could do a lot of experiments in six hours. Just do it. Stop procrastinating.

Now, there is a productivity thing you should be doing. You will, in this thing, have a set of test analyze loop. It doesn't have to be automated.

It may be that the pattern is up arrow, change that last number, hit enter, and then copy the result over into a spreadsheet. That's a fine loop. Make that loop really fast.

Yes, if you had to do it hundreds and hundreds of times, yes, a little shell script would help you. But you will spend more time relearning Z shell syntax, which we've all forgotten, than just doing it. Just do it. Now, there are tools that can help you. This is Alfred. This is probably the most useful automation I've ever written.

It just does two things. One of them types my testing username. The other types my testing password.

Because I do this. It's that simple. Tell application system events key stroke my account name tab.

That's it. Find those things that you really are doing a lot and that you can solve with nothing. Make those fast.

Another one, sim control. Gosh, I love sim control. If your test case needs to uninstall the app every time and you're going in there and you're pressing holding and then delete, you can uninstall apps, by the way, directly from the command line. Yay! Another one that I use a lot is cd sim. Oh, I'm sorry. My alias for this is cd sim.

But you can ask, where's that silly long path to the app bundle? Really, really useful if you're running your test and you want to see what the database does. That sort of thing.

Anyway. These are the tiny tools you do want to build because they help keep you focused. A lot of hard bugs are also race conditions.

By their nature, race conditions are really hard to reproduce. That's why we call them race conditions. Well, that's not why.

Anyway. It's a bit like hitting a bullseye. And there are two ways that we can hit more bullseyes.

We need to hit a lot of bullseyes. So we can do two things. We can actually make the bullseye target bigger or we can just throw a lot of darts.

And so my first thing I like to do is throw a lot of darts. And I use this technique, which is make a bunch of tasks. About 10 is usually enough.

And then in each task, run your function a lot. The one that seems to have some kind of problem. And the thing you're going to discover really fast is your thread-safe code does not like being run in parallel.

Now, it may not have data races. It may not have crashes. But it may not behave correctly.

I've seen so much main actor code or in the old days, dispatch async main to main. The problem is you keep creating... It doesn't like getting called while that other block hasn't run yet.

And this gets a lot more common in Swift concurrency. So it turns out that you can still have all kinds of race conditions, as we learned earlier today. Or you can go the other way.

You can just make your targets bigger. So this is another technique I use a lot with Swift concurrency. Um, anytime you have an await.

Everywhere you have an await. Put a random length task sleep in there. Right after the await.

You can do it before. It doesn't technically matter. But I always put them after.

You can't put them in random places. It matters where they go. They have to go immediately after an await.

Because every time you have an await, you're going to give up control and something else is going to run. You don't want that to happen anywhere other than places you just gave up control. And this finds a lot of interesting little bugs.

Another thing to do. Make the network bad. We often test on really fast networks.

But requests can take a long time in the field. I mean like a minute. Like sometimes more.

Usually not more than a minute. They usually time out. But they can.

Most of the bugs actually show up after just a few seconds delay. Just, you know, if you threw five seconds in there, they would show your bug. That said, what I usually use, what I love, is network link conditioner.

Which you'll see. This is built in. Make friends with it.

It's down in the developer tab under settings. And you can set it to my favorite, which is 100% packet loss. This, by the way, confuses people.

This will not cause reachability to say you're disconnected. Because you are connected. Well, you can send packets.

They won't be delivered. But you can send them. And reachability only checks whether you can send them.

Not whether you're, quote, connected. So this is great because it also shows you, not only does it suss out a number of interesting bugs, it lets you see where you have really bad user experience. Say when people go into a tunnel.

And 100% packet loss is really common in those cases. Other tool I use. I actually don't use this as often.

Because I have proxy man. And proxy man lets me do about ten times more things. But this is built in.

It's really nice. Runs right on the device, too. Now, I've talked a bit about letting go of attachment.

But at some point, you need to come back to the point of it all. Which was to actually fix the bug. Don't forget that.

So I recommend every, you know, few days. Because it's going to take you a while. Go read your journal.

Remember the journal? Reground yourself. Where are we?

What are we actually trying to solve? What are we doing? Is the thing I'm doing right now, am I just off in the weeds somewhere?

Get back on track. Now, don't second guess yourself all that much. You don't have to do all that.

But a couple times a week. Get yourself back on track. Okay.

So finally, you find the bug. Yay! Find the bug. It's time to be an artist again. You're going to be an engineer.

You're going to solve the bug. But there is danger. There is peril at this moment.

Imagine you have this code and you're getting this out of bounds crash. Right? In the field.

That you can't reproduce. You've never seen it. Really common.

I mean, I think we've all seen one of those. So you do the classic thing. You add a guard.

Make sure it's in range. Return if it's not. No more crash.

Ship it. Done. Market.

Please don't do that. Please. I want to ask you not to do that.

Getting an out of bounds exception means that something is deeply wrong. A key assumption has been violated. And that's why out of bounds exceptions crash the program.

Because it's a deep assumption that this index had something to do with this array. If it's out of bounds, it doesn't belong to this array. They're not related.

It couldn't be out of bounds if they were related. But even if it's in bounds, it's still not related. There are worse things than crashing.

I had this bug once. Enterprise chat app. Used to work on.

You would pick a person to chat with. And due to an indexing problem, you might connect to the wrong person. It said you're talking to Alice.

But you're actually talking to Bob. And I want to stress, this is an enterprise business system. People lose their jobs over this kind of bug.

Ask them if they'd rather it had crashed. They'd rather it crash. Yeah.

And you throw that skip this code in there. Awesome. But how do you test that?

What test case do you do to make sure that the rest of the program works correctly? When you skip some code that clearly was important. Or you wouldn't have written it.

I see these code bases. And they just become workarounds on top of workarounds. Right?

Of everybody kind of working around the fact that this other thing is doing weird stuff. And then this one ignores and then skips. And then we also need a workaround.

Please stop that. Now, you've got to keep going. You have to actually find the bug.

And this is true of any precondition. I mean, if you're getting a, you have a force unwrap. Well, why did you think it was okay?

If it wasn't okay, it should always be that it legitimately could be nil. Or, and that's fine and normal. Or it is a hard error.

It's not okay to say, well, I don't know, maybe it's nil. And it shouldn't be. But if it is, I should return.

You shouldn't return. But I get it. I get it.

You just want the app to stop. Please just make it stop crashing. And people are yelling.

And the customers are upset. And I get it. I get it.

And you're going to just ship something. But they're not even Band-Aid fixes. A Band-Aid, the point of a Band-Aid is you put it on a wound so that the body can heal itself.

Programs don't heal themselves. They're, that's not how anything works. Quick fixes are whiskey, right?

Now, they might be necessary. They take the pain away. And maybe they're going to help you get through it so you can actually fix the problem.

And sometimes it's all you got. But they make the problem worse. But sometimes, even with all that, even with all that, sometimes you're just not even going to fix it.

You will never find the root cause. All you got is whiskey fixes. And maybe just whiskey.

And sometimes that's enough. Maybe the bug doesn't happen that much. Maybe you just move on.

It's time to get back to art and actually ship some real code and make some people happy. But if you do that, I'm going to ask you just one more thing, right? Leave a note.

Say clearly what the hack is and why. Link to the issue. Sign it so your team will know who was involved.

So they can come talk to you. You know, get some history. Because sometimes the git history gets jumbled and this lets them know.

If it comes from some blog or some Stack Overflow post or some forum post or something, please link that so people know why you did this really weird thing. Admit it's a weird thing. Then people can adapt to it.

I forgive you. I get it. You just got to make the stuff ship and stop crashing.

But please leave a note. And that's my talk. The advice is simple.

It's easy to forget. It takes practice. It takes patience.

And sometimes it takes a little letting go. Did I mention you should really keep a journal? Thank you.

### Ellen
I think we should start with some audience questions. Because I think there are probably going to be some good ones.

### Julien
Actually, this is some kind of magic effect. Did you already face a moment in which you try to fix a bug, you don't manage to find the root cause, the misconsumption, et cetera. And then you just take a short break.

### Rob
Oh, certainly. Oh, all the time. This is a common problem I have in interviews.

Because when I'm going in for an interview, they always go, well, we want to just see you work through this. And we want to see your process. Like, how do you think?

And I say, well, I think in the shower. And nobody ever lets me finish the interview. But oh, absolutely.

And that's why I say these things often go on for days and weeks. And I've worked on single bugs for many months. Very difficult bugs.

And you're thinking about it all the time. But often, it's very true. A short break can help you a lot.

Also, the classic rubber duck is a real thing. Another really classic thing is formulate an excellent Stack Overflow question. In the process of writing a really, really good Stack Overflow question that you're proud to post, you will discover that you know the answer.

So it's about formalizing, actually, right? That's a wonderful way to say it. And you could write it in your journal.

Here's what I know. But very seriously, the formalization. And again, back to science.

A lot of science is figuring out, what am I even asking? What really is the problem?

### Ellen
Yeah, putting it into a format where you are taking what you've been working with and you explain not just what you see the problem is, but everything that you've tried to fix it. Often, somebody else who hasn't been neck deep in the problem is able to be like, oh, did you try this? And you go, what?

Oh. No, I did not. No, I did not.

### Julien
A question from Herve. What is the worst and most difficult bug you had to face?

### Rob
Oh, do we have time? Because it's a doozy. We had exactly one laptop that got one-way audio.

I worked on a voice app. It was kind of like Skype or something. But we would get one-way audio where one person could hear the other, but they couldn't hear each other.

But only when the person was running Cisco VPN. And only when they were on VPN. And we spent months and months.

I was at Cisco at the time, and it was a Cisco employee, so we were very lucky. But I mean, I had his machine in hand. It was the only machine that ever had this problem.

And I could make the problem happen 100% of the time on his machine and not on any others. So I started to do science. I started to break it down.

What could it be? These were the old days when you could easily boot Macs off of other Macs. So I would boot his machine off my hard drive.

No problem. I'd boot my machine off of his hard drive. Problem.

Wow, OK. So I did a full clone of his drive and took that away. It did not have the problem.

A full, perfect carbon copy, cloner copy didn't have the problem. Only his drive. Literally this one.

After six months, by chance, I noticed that there was both a readme file in the directory and a readme file. And they had different capitalizations. Did you know that you can have a case-sensitive file system?

I hadn't realized that you could have a case-sensitive file system. And more, why would that even matter? Because if you had Cisco VPN, we dynamically loaded a library to help us deal with Cisco VPN and get your audio working.

And we had a typo in the capitalization of the name of the library. One character change. In six months.

Six months. And six months.

### Ellen
That's pretty brutal. I mean, when you have a bug like that, where it's just like, this seems to be affecting a vanishingly small number of people. But this is driving me so insane that I need to know what is happening here.

How do you decide how to prioritize whether to keep going down the rabbit hole or whether to be like, you know what? This is unknowable. It's gremlins.

It's aliens. I don't know.

### Rob
Cosmic rays. Whatever they blame. And that's always up to, and I say I worked six months on it.

I clearly did not work full time on that. It was the constant, wait, could it be this? It was not that.

And then, you know, three weeks later, is it this? And I would say a lot of, in terms of priority, obviously, priority is going to be driven a lot by your product needs more than your personal interest, unless you're me and I get away with working on whatever I feel like it. And so I will dive in.

But still, at the end of the day, yeah, you have to pick your battles eventually. And it was literally one machine.

### Ellen
I would have absolutely just thrown the machine into the river.

### Rob
Vix, we're going to shred your machine.

### Ellen
I'm putting this in the sun. Have a nice day. Never do that.

### Julien
And maybe the last question from the audience. This is a specific one to Crashlytics. What do you do when you have a crash?

It points to nowhere as a question, but I think when you don't have a clear stack trace not to start with.

### Rob
You have nothing to start with. Yeah. Your lips to everyone's ears.

I wish I had an answer. There is the ones where you just got nothing. And I'll tell you, when you got nothing, you got nothing.

And you just start hoping that someday it will come in. Those are actually not all that uncommon. And what you want to do is start putting them in a bucket and looking for the one that finally comes in and finally has something.

The hardest thing I find is then figuring out that these and that the two are the same. A common problem is people bucket too much. They bucket based upon the last thing that happened.

And the trouble is the last thing that happened is often not the cause of the problem. I'm chasing a bug like that right now actually in the Android space. But we get out of memory in some obscure situation.

And the thing is, the thing that requested memory, the last thing that asked for memory and crashed the app is not the problem. It's something else ate all the memory. And so the problem is not in the crash stack.

Often in those cases, you're going to have to just take lateral thinking. You're going to have to find, you know, I'm doing enormous amounts of analysis of what could you do in the program that would cause it to suddenly try to allocate enormous amounts of memory? Or is there anything in the program that slowly allocates memory?

But I wish I had an answer to the two line stack trace. And... Me too.

### Ellen
I think sometimes you can put like some kind of logs in. I know that Crashlytics has some level of just like breadcrumb logs. I've had those bail me out a couple of times where I'm just like, how did you even get into this situation?

### Rob
Oh, oh, oh, oh. But I should tell people this, though. Because it used to be in the talk and I took it out because I just ran out of time.

If you have just impossible stack traces, stack traces that are stupid, they make no sense. Like that can't be happening. A thing that makes stack traces that cannot happen is memory corruption.

Straight up, something is stomping on memory. And rewriting things. That will absolutely lead to these weird impossible stacks.

Once you go, okay, maybe it is in fact memory corruption. Now you have tools again. You can start to use, there are tools in Xcode.

If you go into diagnostics, you can use the address sanitizer to try to find things. You can put in memory guards to try to see if you can force the memory corruption to happen. You can go, just because you know it is memory corruption, that's not going to, memory corruption is hard to make happen in normal Swift.

It happens in Swift land in kind of three places. One is you are going to C code, which may be underneath a lot of stuff, but it is usually C code. It is unsafe, which usually isn't actually the cause because usually unsafe usages are done pretty well.

But the most common cause is two things running on different threads accessing the same memory. And that will lead you to those impossible things. So you start doing analysis of, do I run anything on the wrong thread?

And that will often find it.

### Ellen
Thanks, Rob.