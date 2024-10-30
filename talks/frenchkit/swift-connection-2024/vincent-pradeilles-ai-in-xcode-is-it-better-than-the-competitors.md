---
slug: >-
  /talks/frenchkit/swift-connection-2024/vincent-pradeilles-ai-in-xcode-is-it-better-than-the-competitors
date: '2024-09-23'
title: 'AI in Xcode: is it better than the competitors?'
author:
  - Vincent Pradeilles
video: YszBJrrpZM0
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/YszBJrrpZM0.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Vincent
Hello, good morning. So I don't know if you've heard, but a few months ago, Apple, they made quite a few announcements on AI. I think it was one of the main topics.

But there was one announcement that was especially for us developers. It was finally the introduction of AI tools in Xcode. And Apple, when they announced it, you could say that they sold it quite hard, because they used words like they've created specialized coding models that capture expertise only Apple can provide, like latest APIs, language feature documentation, and simple code.

So when you see that, you're excited. You want to try it. And you want to know, does it deliver on the promise?

And the question is, how good are these tools compared to the other competitors, which are also available for software engineers? So unfortunately, as of right now, Swift Assist still isn't available. I had the hope that maybe when they finally released Xcode 16 and Sequoia last week, maybe by working a bit in the weekend, I could find it and I could talk about it.

It's not available for now. So we'll have to just put it aside until a few months. But something that's been available since early July, or even early June, is predictive code completion.

So if we can just turn on the lights for a few seconds, and by a show of hands, can you raise your hand if you have used predictive code completion in Xcode 16? Okay. So a few people, but maybe slightly less than half the room.

So not that many people yet. And so the thing about predictive code completion is that it has a very obvious competitor. Copilot from GitHub, which has been available for a few years now.

And what might not be that widely known is that you can use it as an iOS developer, because in VS Code, you can open a Swift project, granted it does feel very, very weird to open your Swift project with VS Code, but you can do it, you can use Copilot, and it does give some interesting predictions. So I wanted to put the two tools together and try and see, okay, how does what we have in Xcode deliver compared to the competition? So before I go into the comparison, just one thing to keep in mind.

The two tools have a big difference, is that predictive code completion runs locally on your Mac. That's why you need an M1 or more chip. That's why you need to have at least 16 gigs of RAM, then they removed it.

But there are some requirements because of that. And Copilot, it runs in the cloud with the advantages in speed and compute power, but the potential issues with privacy. So things to keep in mind when we're going to see the comparison.

So I picked five typical use cases, the most basic use case you can have as a developer for code completion and code prediction, and let's see how the two tools compare. So first one is being helped to implement a data model. So Copilot, you start to write a struct which is called address, and then very quickly, it gives you this prediction, which you can accept or not, and you have a few properties being defined, which makes sense in the context.

Now let's see how it goes in Xcode. Before I start the video, I want to say it's been recorded in real time. There is no slowing or anything added.

So you create a new line, and you have to wait a bit. There is no loader. That's one of the main issues I have with the features.

But then it gives you something, and the other lines, they went by a bit faster. So for this example, honestly, the two predictions are very similar. Xcode took a bit more time, but it's not terrible, and Xcode did suggest to use let, which is arguably slightly more appropriate.

Now let's move on to something else. Let's try to implement a mock, something super useful but also super boring to do. So typically a use case where we want to have the AI do the job for us.

So you do it with Copilot. It works quite well. It suggests a data which is valid.

The end is cut, but of course there was the closing parenthesis and everything at the end. And in Xcode, also, it works quite well. You can notice that Xcode is slightly more neutral in what it suggests.

For instance, it's not San Francisco, it's any town, so it takes less of an opinion. But it works quite well, and this is very usable. So for this one, they do the same.

Now let's try to implement an array of mocks. So Copilot does it in one go and does it super fast. It's perfectly valid.

Xcode is kind of interesting because first it wants to use the previous mock, and then eventually it adds more elements to the array. So a very interesting and valid approach. The mock is also a correct mock.

It does take a bit more time because you need to wait a few seconds every time, so you get there a bit more slowly, but still faster than if you had had to switch to VS Code. Now let's go to something a bit more complex, implementing an API call. So Copilot, it goes straight for the completion handler with the two optionals, which is really not great.

And that's where I would have expected the AI in Xcode with the promise of implementing the best practice that only Apple can provide to do better. Unfortunately, it only did slightly better because it did suggest using the results over two optionals, but it still suggested a completion handler as the base ZIP approach, which to be honest, I was a bit disappointed when I saw that. The good news is that at least for both, if you start to correct by writing async in the header in the signature of the function, then it does manage to generate the rest of the code accordingly, both for Copilot and for Xcode.

We can still see a slight error with Xcode, which doesn't deconstruct the tuple, which will lead to errors later, either for the developer or the AI. It's an error which is easy to fix, but still it's a bit disappointing that it's happening. And finally, last example, implementing the body of a view.

Same thing, having a base is super useful, and often you will be referencing stuff from another file. So Copilot did pretty well. I was wondering, is it just because it was most probable for a type called address?

So I went and completely put garbage into the type, and Copilot did well, like it handled the random names correctly, so Copilot does reason across files. Unfortunately, Xcode here didn't shine at all, because it seemed that it understood the address to be some kind of collection, maybe because there was an S at the end, I'm not sure, but at least this code doesn't build, so it's not a good prediction, and if you go and change the content of the address in the other file, it doesn't change anything. So this is a bit disappointing, but at least it does show us that the AI in Xcode seems to reason inside the file, but not across files, so it's good to have that in mind, because knowing the limitations of the tool helps you make a better use of it.

So what should you take away from this talk? After having used the predictive co-competition feature over the summer, my take is that it gives equal or worse prediction than Copilot, but it takes longer to do it. So you might not want to go into something where you need a lot of heavy lifting with it.

And there are some UX quirks, like there is no loader, and you end up waiting, and maybe nothing will happen, and you feel a bit like an idiot, so I do hope they will add it at some point, because it feels a bit lacking there. Now, it's not all bad. There are use cases, like creating more that work relatively well.

You don't need to switch to a third-party tool, because I said you can use VS Code, but who's going to do it in real life unless there is a strong need for it? So that's still nice to have it in Xcode. And sometimes it makes good prediction.

Like here, with Swift testing, for instance, it did generate the correct code with the correct syntax, which it didn't at the beginning of the summer, so maybe there were some improvements. Or also, when you use the regular code completion, it suggests values for the arguments, and that seems to work quite well, I guess, because the scope of the problem is a little bit simpler than just generating arbitrary code. So at the end of the day, if you're looking for a tool that can do a lot of heavy lifting for you, it's probably not what you're looking for, but it makes a good job at generating predictions without extra effort.

If only 20 per cent of them are good, that's still a win, however, be careful if you're onboarding junior developers, because the fact that the predictions are shown in the look and feel of Xcode makes them feel more trustworthy, even though they shouldn't. So please let your juniors know, because since the feature is on by default, I think it can be a bit tricky. And hopefully it will improve over time.

And finally, if you're enthusiastic about AI-assisted coding and you want to see a sneak peek of what SwiftAssist might look like, I would recommend looking at an IDE called Cursor. You might have heard about it because it did a bit of a buzz two or three weeks ago. And it's very similar to what SwiftAssist will do, basically, you can write a prompt inside your code, and it's going to do a query for you to an LLM, here it's Cloud 3.5, and it's going to automatically pass the answer and write the diff in your IDE. So it's kind of cool, it gives you a glimpse of maybe what IDEs will look like into the future. It's not more powerful than copying and pasting code from Cloud or JGPT, but the integration is pretty nice for testing, it can be pretty useful. And that's what I had for you today.

### Zino
So in the example that you took, address is very standard, boilerplate, that kind of stuff, so AI is expected to work rather well on the things that are super common. Absolutely. Have you tried on more exotic structures, or more, you know, like, do you feel like it can learn from other things than just the statistical, more common things?

### Vincent
Yeah, so the impression I got from the AI Unix code is that since it thinks only inside the file, or it seems to think only inside the file, that puts a strong limitation. Because the context of your project, for instance, a complex project, one file is definitely not enough. So I didn't give it a try on a very large project, to be honest.

But when I see how it kind of struggled a bit with simple use cases, I have a hard time thinking that it would shine with much complex use cases. So I feel it makes sense, for instance, when you want to interact with the APIs from Apple, where Apple can manage to embed as much context as possible in the training, in the data that they show during training. When it's your own code, it's a bit more complex.

So that's why I would kind of see it as kind of like maybe a way to have, like, the doc suggesting things to you, for instance. Whatever the doc can help you with, I guess I would say that this tool from Apple can help you. But when it's your own stuff, I would be a bit more cautious.

And you're right, that's for mocks. When it's basic data, so we need to give it strings, basic types, it's fine. But if you need to create other types to create an object, then it might get a bit more complicated.

Maybe you could solve it by being a bit smart about it and structuring the code so that you build from basic stuff and then more complex stuff. But yeah, you will run into some limitations, yeah.

### Audrey
So Vincent, speaking about context and about things you want to add, did you try, like, adding some more, like, trying to decorate the function? So adding more documentation about the parameters, the return parameters, and maybe what the function will do? Because you had an example where there was a completion block, which was disappointing.

And maybe suggesting that it should return a sync function?

### Vincent
Yeah. So I had quite stuff around the documentation. If I remember it correctly, predictive concatenation wouldn't generate a comment for you.

But you could write a comment and it could help it understand what's going to happen. In the case of async, arguably it's going to be faster to write the signature yourself than to write the prompt for the documentation. But yeah, you can give it some kind of hints about what you would like to see for a comment.

### Audrey
Yes, indeed. Thank you.

### Zino
There's a question from the audience that I'm going to rephrase a little bit. So right now, right, the big thing with Apple is it's on device. Yes.

It's on device, on device, on device. So ultimately what you said, let's wait for them to get better. It's going to learn about your own coding style and suggestions based on your own coding style.

Do you imagine a future where you can share that thing for best practices in a team? Like, is it something that you see is possible down the line?

### Vincent
I guess you could. I don't know how they implemented it. You will see that when you install Xcode 16 on Sequoia, you download the basic foundation model which is around two gigabytes.

But you could imagine that there is some fine tuning happening on the device. And so maybe it could share, like, the final layer plus the offset for the weights of the base model. Now, the question would be, how do you merge that across a team?

But yeah, you could imagine it happen. I couldn't find a lot of information on how it's implemented under the hood. But I guess if you want it to be adopted, yeah, being able to have something just like for a linter, you want to have a configuration.

So maybe you could have some kind of configuration file. The hard part with AI is that it's not, like, the weights are not human readable. It's a black box.

It works. But you cannot make any sense of it. So but it would be interesting, I think, to see how the ideas will evolve.

That's why I wanted to show cursor at the end. Because I wouldn't feel like I would use cursor for everything iOS related, even though it's kind of nice. But it does give you a glimpse of what might be the standard feature of an ID.

Maybe 20 years ago, there was some ID that introduced, like, syntax highlighting and coloring. People were, like, wow. And now it's just, like, basic.

So it gives you a trend of where things are going. I'm quite hopeful for Swift Assist, because this approach of basically the tool is crafting the prompt for you to an LLM that's hidden from you, and then it parses the answer and shows the diff in the code, it's kind of interesting. It's kind of powerful, because it takes away the annoying part of copy and pasting and stuff like that.

So that's something that I'm more optimistic about. And it might be also that because it can get more context, or maybe the model will be more powerful than what it does. So I'm waiting to see about it.

I do hope it will be better. I was a bit disappointed by what there is in Xcode, just because copilot is so good now just to name this one. And so it felt like it arrived and it felt a bit like a few years behind compared to what the competition can do.

But picking up speed is quite fast in AI, so you never know, it could change at a few months' notice.

### Audrey
Thank you, Vincent.

### Vincent
Thank you. Thank you, Vincent.