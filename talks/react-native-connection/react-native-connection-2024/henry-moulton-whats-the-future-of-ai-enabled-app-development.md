---
slug: >-
  /talks/react-native-connection/react-native-connection-2024/henry-moulton-whats-the-future-of-ai-enabled-app-development
date: '2024-04-23'
title: What’s the future of AI-enabled app development?
author: Henry Moulton
video: '-3f0GIxS-iw'
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/-3f0GIxS-iw.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: react-native-connection-2024
allow_ads: false
---
[Henry]
Yeah, last talk, so please stay with me. Yeah, yeah, so, you know, I think software is eating software, but I think if it's the last talk of the day, you might as well spice up a bit and say software is eating software engineers. Hey, I am Henry, love humans, love computers, have always loved human-computer interaction, so how humans can interact with computers, so I'm sort of wondering, how will computers interact with humans, at Henry Moulton on Twitter.

As Mo mentioned, I am a principal engineer at Yonder, three years ago, I was at Amazon, and these co-founders said, hey, we're starting a credit card, and I was like, that's crazy, who would start a credit card? And three years later, I'm still there, and we've built a sort of challenger to American Express that you can use your points in and around London, and now the UK, and people really, really love it, and we've been using React Native all the way through, and like Mo mentioned, before that, I was a freelancer contractor building React Native apps, and before that, I had the pleasure of using Angular Ionic.

Just a quick disclaimer, this is not the opinions or work of my employer, so everything I say with a grain of salt, and, yes, there's nothing new under the sun, as they say. This is an advert from 1995, build programs without programming, see how layout lets you build real programs without writing a single line of code for free, or maybe $99.95. This is back when there was no app stores, or even really a functioning internet, and you would have to buy software by calling a phone number, and they would mail it to you. It was a really, really sort of different time.

Why that's relevant? Last year, I was up on stage at AppJS, and I was sort of looking at a new end-to-end testing framework, and I was putting together, if we have really, really good end-to-end testing, could it be possible that AI could be running your end-to-end tests or figuring out what end-to-end tests to run, and sort of finished with two sort of ideas. Does writing the correct tests become the most important part of our jobs, and does the specification become the product, the requirements, the natural text?

Because, you know, I heard there's a Flutter day tomorrow, well, bad news for them, I think React Native has one, and yet, I had a walk with Charlie, CEO of Expo last year in Krakow at AppJS, and he said something that just really reinforced me that the job's not done. It just shouldn't be this hard to develop apps. So this is a talk in three sections.

Firstly, how building software is changing, a little bit on agents, and then, you know, bring it back to us as software engineers, mobile engineers, jobs, and specialization and consolidation in the job market. So let's kick it off with how building software is changing. So I was born in the 90s, built in the 90s, I'm not an AI, born in the 90s.

Great year, 94, Forrest Gump, Lion King, Four Weddings and a Funeral, Pulp Fiction, but also there's this article I found that said the world's computers are talking to each other as the web spreads, calling someone a geek may yet become a compliment. Not sure it's happened yet two decades later, but that's Tim Berners-Lee, Sir Tim Berners-Lee, and yeah, so we have the sort of arrival of the Internet, you know, or how people thought the Internet would be, surfing the web, and that's what Microsoft's web page looked like. That was the best-selling computer of 94 looked like, the Commodore 64.

That was what Windows looked like in 94. That was what mobile phones looked like in 94, and if you fast-forward to the next decade, all of a sudden we get something that looks like this. I love this quote from an engineer at Motorola.

I worked at Motorola when the iPhone came out. Every single engineer knew this thing would blow everything else out of the water. It was one of the largest leaps in consumer tech devices ever.

That's an interesting question. You know, I won't do any hands-up because it's the last talk of the day, but how many of you thought you'd end up developing for the iPhone when it came out? I was a teenager.

The fact that, you know, there wasn't even an app store, the idea that I'd end up developing software for it didn't come across my mind at all, but, you know, Google followed suit with Android, and we were off to the races, and the mobile S-curve, the way that mobile adoption happened surpassed the PCs. Mobile phones, this new way of accessing computing was quickly overtaking PCs and just grew and grew and grew in a nice little sort of wave curve, as you can see there. And you can sort of see that there's a, you know, with every deployment, creation and deployment of a new technology, we have that sort of crazy idea and that frenzy, and then that deployment phase where we're sort of scaling and it's maturing.

So you can sort of see here in 2009, we had that massive uptake of iOS and very, very little of Android, and this is sort of the iOS Android market share in the U.S. You can sort of see as it's moved out towards 50-50. Not so much the case worldwide, but, you know, pretty stable. iOS has about 20-30% market share.

If you look, it's actually slightly rising since 2018, but overall, you know, the way that the mobile sort of wave turned out to be was two platforms, which, you know, when Meta was looking at deploying their applications to the Play Store and App Store, they just saw, well, we've just got to build something that you can build on both. And I'm just going to use this to take a quick sip of water. Yeah.

And, you know, this brought about some really, really great apps, you know, Discord and many, many others that now today we almost take for granted are built off this, what at the time seemed an absurd idea that you could build apps using JavaScript. But I guess the point is, you know, technologies come in waves. Waves have bubbles.

We've seen bubbles, you know, O1 and more recently, you know, the crypto bubble. Waves can come crashing down. I think we saw that in the last few years with tech definitely readjusting.

But waves are also a powerful form of energy and waves can be surfed. How you define a wave, I think, is really, really interesting. You know, are we in an AI wave or are we just part of something greater we can't even see?

There's some really great economists who have studied this. And, you know, you could call technology waves starting with, you know, in 1771, the Industrial Revolution and then going into the age of steam and then going into the age of steel, the age of oil, and more recently, the sort of ICT revolution where we've had everything since the 70s. I tried to find some way to encapsulate all that, but I saw there's some really fantastic videos from this investment firm called Sequoia, who hosted an AI summit.

And if you zoom into one of their slides, I've stolen it. So you've got, you know, 60s semiconductors, 70s systems, networks we start seeing in the 80s. And then, you know, by the 90s, you've got the Internet where you've got sort of your first early innings of websites.

And then in the 2000s, we start seeing, you know, web applications. And then in the 2010s, we've had mobile applications, which we're all used to using. We have been surfing the most recent wave of technology.

But if you compress all of that Internet and mobile usage that we've had over the last two decades with a lot of GPUs, about $100 million worth of here, you get this. What was going on? So three things to just sort of dive into.

So cloud computing and GPUs, lots of UI and user generated content, and then also AI research. And we're just sort of skirting over this very, very quickly. So cloud computing.

Did we finally figure out serverless? You know, this idea that you can scale up unlimited amounts of computation. Well, there's many charts I could probably point to, you know, you could point to the rise of AWS, GCP, Azure, etc.

But I found this paper from Meta called Hyperscale and Low-Cost Serverless Functions at Meta. Turns out, Meta has been scaling into the trillions of calls, their serverless functions inside of their private cloud. And I think this is a testament over the last two, three years that we've really been able to figure out a really great way to distribute and scale computing, which, you know, is the backbone of what we see today in training AI models.

So diving a little bit into AI research, I'm just trying to summarize it in just a few slides. Very, very difficult, but this is my best attempt. 2015, I remember reading this blog post from Kapathi, who at the time was doing a Stanford PhD, and he wrote this blog post, The Unreasonable, the Unreasonable Effectiveness of Recurrent Neural Networks.

And it starts with a very interesting first sentence. There's something magical, magical about recurrent neural networks, which reminded me of a quote, any sufficiently advanced technology is indistinguishable from magic. Very telling.

If I'd paid attention a little more to that, to this blog post, rather than maybe fiddling around with what I've been doing at the time, yeah, Ionic and Angular, I might have had a very, very different career. A few years later, we have the Transformers paper, which is one of the really fundamental academic papers, which has shaped a lot of the underlying architecture of AI models today. And then a few years later after that, we have the GPT-3 paper from OpenAI, which is starting to, you know, it's not quite as impressive as where we are today with GPT-4, but many people started looking at this and taking it a lot more seriously.

The following year, they took GPT-3 and fine-tuned it on public code from GitHub, and that today powers GitHub Copilot, which if I were to guess, above 50% of the room uses today. And then a few years later, governments start getting involved, everyone's saying the world is going to collapse and AI is going to rule the world. And Microsoft Research publishes Sparks of AGI.

We demonstrate that beyond its mastery of language, the model can solve novel and difficult tasks that span mathematics, coding, vision, medicine, law, psychology, and more, without needing any special prompting. But a big reason why ChatGPT grew to prominence, it was the first time they'd taken an AI model and really given a UI that people could interact with. And that's something that we've seen over the last, you know, sort of decade as well.

We, you know, I'd point to Dan's talk, Hot Reloading with Time Travel, which was the first time we really started to see that React could be used to make really interactive applications. And we're all familiar with, maybe all of us, or many of us are familiar with this equation that our UI tree is really just a function of its state. And if you're doing prompting, you're essentially creating the functions and, you know, querying for the large amounts of intelligence that these models are trained on for it to be returned as some nice JSON conversation.

So if you put it all together, you've got instantly scalable computation, unlimited intelligence, and declarative, generatable UI. Many people are calling this software 3.0. Software 1.0 is the software we're all used to writing. Software 2.0 was, you know, almost like a messy middle where we're starting to add some machine learning algorithms. And software 3.0 is this idea that you can write natural language, converse with an agent, and it's going to create the programming readable code for you. So moving on to agents, I'll take a quick drink. So I've played games.

I'm used to the bots winning. Whether it's poker or DOTA, I'm used to the bots affecting the in-game economy. Bots today, you know, particularly if you're a gamer, you're familiar, you're used to the idea that people developing bots can affect the win condition of a game and can also affect the wider economy of, say, an MMORPG.

I think many of us are getting used to the idea of bots, AI are going to change our economy. You know, you're seeing research and people publishing things like this, right? You know, 15 years ago, you'd have 10 engineers, one product manager, and one designer.

Five years ago, that's slim lined. You know, maybe you're using React Native and you have a lot more efficiency. And now it's gonna be one person.

It's gonna be an AI PM. I do think there's some truth in this, which is that I believe we as software engineers will be expected to leverage AI to increase the speed at which we build software. But, you know, if you swapped AI there with React Native, the same is true.

We're just, you know, rather than having lots of different types of specialist engineers, you can condense it into maybe one. But I think there's where I'm sort of seeing hype and a bit too much is this idea, you know, we're getting to maybe like 1000x productivity, which I think we're maybe just a little early on. But there's some interesting shoots I'm going to show in a second that maybe there's some progress towards some number of some massive amounts of efficiency enhancement.

This idea that you'd go from a 10x AI enhanced engineer, which many of us maybe are using today with Dart. We're not familiar with maybe some language. So we'll say, hey, I want to, you know, I know TypeScript, let's say, and I know what I want to achieve in Objective-C.

Can you take this TypeScript code and translate it over? And I myself have done that when using React Native. You've also got the idea of, you know, 10x AI product engineers, where you're utilizing LLM frameworks to create new workflows and new products.

And then more recently, we're starting to see this idea of a 10x AI engineer agent, which is the idea that you are instructing an autonomous agent, an autonomous bot, just like games to do something for you. And the crucial, I think, distinction here is that that can scale. It's not one versus one.

That can scale into the thousands, millions, just like we saw with Facebook serverless adoption. So early signs, we're sort of starting to see this. So many of you would have seen Devon, the first build as the first AI software engineer agent.

When I saw Devon, I was intrigued because they made some interesting claims. They made claims that they were the best AI agent on the market. And if you look at the title, that real world software engineering performance bracket Suibench.

And, you know, I think that's going to be, as I'm going to dig into, there's going to be many more agents on the market and things like Devon, because, you know, there's potentially real productivity gains for businesses to adopt these over, you know, essentially paying for software engineers. But what intrigued me was more the Suibench benchmarks. So what is that?

So it is a benchmark where an agent is then instructed to solve GitHub issues. It's a fascinating paper, how they've decided how to go about choosing which issues and what constitutes a good problem for a software engineering agent to solve. And there's a leaderboard.

And Devon's not part of it because they were unable to verify the results as correct. But more recently, the people behind Suibench have published their own agent using GPT-4, which resolves 12.47% of all issues. And if you notice, I think the 12%, OK, that's not going to be that useful for me today.

But it's not so much the point or the amount resolved, it's the progress. If you look just six months ago at the bottom there, it was 0.17%. So what I encourage us all to think about is just trying to not so much critique an individual point, but trying to understand what the curve is. Remember the early curves I showed you with mobile?

What's the curve we're seeing here? Because this is an expansive landscape. You know, there's people whose full-time jobs are to try and figure out what to invest in across all of this.

And it's difficult because so many people have their own opinion about what's useful. Many of them have big, bold claims. Adept is one from ex-OpenAI engineers saying that they are a new way to use computers.

We're building a machine learning model that can interact with everything on your computer. And I do believe to some extent that this is on the way. This is happening.

So I think a final idea here is what happens when you give GPT-10 full access to your machine? Just, I'm just going to leave that one up there and take another sip. So how does this affect me?

How does it affect us? Jobs, specialization, consolidation. So, you know, last talk of the day.

Let's, let's, let's, let's scare some people. So here's the percentage, the changes in engineering jobs of the last month, four months. And you can see mobile engineer in the red.

AI, machine learning up in the green. We are no longer the hot new thing. But, take heart is what I say.

The main thing I think we need to, we need to confront is the idea that just coding will no longer be enough. But maybe actually that's a massive opportunity for us to rethink about what it is to build software. In design, they say that all of design goes through a process of discovering, defining, developing, and delivering.

And when I look at the tools we have today across generating UI, generating design, generating code, I cannot help but feel that individually we should be starting to think about how we might do each one of these as a, as a, as one person being able to deliver or contribute across the full spectrum of, of this workflow. You know, I spoke with a designer of 20 years experience and they said, Henry, to do all that, you'd have to be a unicorn. But even before AI, there's, there's, there's people who do this.

They, they, they, they find gaps in the market of software that they want to go build. They design it, they market it, they build it, they, they monetize it. Um, the indie hackers community, I think, is an early snapshot of the potential productivity any one individual can have when, um, when, when it demands it.

Um, I think also something I think about a lot is during the last decade, the MBA was ridiculed by tech, but, um, as I'm about to explain, maybe actually planning strategy and a bit of management skill is actually going to be useful. Maybe the new MBA is master of busy agents. Um, there's a fantastic, uh, blog post by Christoph Nakazawa, who is, you know, creator of Jest, ex-React Native team.

Uh, it's a fantastic, fantastic blog post. I really recommend, uh, reading it, but inside it, he drew a fantastic Venn diagram of the responsibilities you might have as an IC and the responsibilities you might have as an engineering manager. And, you know, in the middle of that hiring, project management, mentorship planning, I don't think that stuff's going to go away regardless of how much, um, AI you add.

If we think about, um, the four Ds earlier, um, I also think, you know, being able to see that design and product management also intersect with that is incredibly useful because I think for us as mobile developers in particular, picking up a bit of design, picking up a little bit of commercial awareness can not be a bad thing. So, closing out on a more positive note, um, the internet and mobile connected us all. People could work and communicate from anywhere and many jobs were created across the world.

AI does swap labor for compute. It's, it's quite obvious that this is going to be ongoing and over the next few years we'll, we'll see many, um, AI agents attempting to replace the role of, of someone's job. And I do think when, um, when you've got that in the market, there'll be a return of specialization and a bit more sort of freelancing contract specific work where it's, it's a fixed price for the job.

Um, and yes, a lower floor does enable anyone maybe to, to, to write more code or to create software. But I think there's a much higher ceiling as to what any one individual can build. And these are changing times, but I would much rather know how to leverage computers and to be able to build software in this cycle than not at all.

What will we build? Who will it help? Thank you.

[Mo]
Thank you very much, Henry. Um, so me and Henry have had conversations around this for many, many, many hours. We had a lovely lunch together talking about all of the changes that are happening in the AI space a few weeks ago, I think it was.

And so it breaks my heart to say that we're running so behind schedule that we won't be able to have a Q and A. Um, but, um, you will be able to catch Henry at the after party and give him all of your AI related questions and, uh, have a chat with him. So once again, thank you so much, Henry, a round of applause.

[Henry]
Thank you guys.