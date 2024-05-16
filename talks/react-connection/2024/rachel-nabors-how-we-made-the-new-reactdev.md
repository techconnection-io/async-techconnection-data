---
slug: /talks/react-connection/2024/rachel-nabors-how-we-made-the-new-reactdev
date: '2024-04-22'
title: How we made the new React.dev
author:
  - Rachel Nabors
video: Cn72zHJnEZs
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/Cn72zHJnEZs.jpg
slides: null
tags: []
year: 2024
conference: react-connection
edition: '2024'
allow_ads: false
---
[Rachel]
I'm Rachel, a formerly React core member, previously I've been head of developer advocacy or education at AWS's Amplify team, worked at Microsoft Edge for a little bit. And I was also the developer evangelist no one asked for for web animations, which was back when I worked with Mozilla and MDN and worked on the web animations API. That was when I originally spoke at LaConf a decade ago when we didn't have Wi-Fi in Paris.

I remember that was a problem. It has been ten years, and my French is just as bad then as it is now, but I did do some Duolingo before I came. I will spare your ears attempting to give this talk in French.

That's as much as I'm going to hazard. I'm much better with German because I just have to sound angry and it works. French, it has to sound just it sounds lewd by American ears.

So I cannot. I will blush too much. So anyway, in 2018, I actually got into Vue.

I'm not actually a React person. I'm more of a Vue person. I got into Vue because Vue had animations built in, and, you know, me being the animation wonk, I was into Vue, and I found React difficult to learn.

I bought multiple courses, I tried to work through them, and I would always get 20 minutes into a web pack configuration and kind of rage quit. I'm not that smart. I get tired and frustrated easily.

People are like, oh, you're smart. I'm like, not really. I'm just easily discouraged, if you know what I mean.

But I saw at this time, even though React was hard to learn, most six-figure salaries required a React background. But React was hard to learn even for experienced folks. Even people with computer science degrees would say things like, you know, I can't understand it.

You know, I feel like you have to follow Dan Abramov's tweets or read all the GitHub commits. And I thought to myself, oh, gosh, if only React was as easy to learn as Vue. Vue had had a huge documentation push that was led by Sarah Trasner, and it was very community-led and awesome.

But if more people could learn React the same way they learned Vue, that means more people like me could have six figures. I'd see more people like myself building intergenerational wealth, inhabiting the web development community. That's a great lever to pull.

If only someone would pull it. So I decided I'd join the React team in 2019, move to London, where I live now. And I was a developer advocate documentation hybrid.

Pro tip if you're joining any company over 100 people, don't join as a hybrid. Because then people who build career paths will just quarrel over which one of these metrics of success you are or are not hitting. Don't be a hybrid.

That was my first mistake. But yeah. So I joined in 2019 to democratize the React education and make it easy for anyone to get a world-class React education straight from the team.

So this is how I spent my pandemic. I don't know what you did. Some people had kids.

Some people traveled the world. I pushed this thing out. I built it with a few friends, with friends in the React community.

Some of them you know. I'm curious. I can kind of see you out there.

Raise your hand if you visit React.dev at least once a week. Hey! Oh, sweet.

And raise your hand if you learned React using React.dev. We need to get more young people to come to these conferences. That is another thing. We've aged.

We've aged. I think they're all on TikTok. But before I could work on React, is Rumpelstiltskin a German or French fairy tale?

I can't remember. It sounds German. But before I could work on React, I had the task of turning around React native stocks.

They were like, welcome to meta. First spin this straw into gold. And I'm like, oh, my god.

Okay. I don't know anything about mobile development. I barely know anything about React.

Sure. Yeah. You know, if I can teach people how to animate with a web animation API, I can do this, too.

So I started where I always do, because I didn't know the people who were using React native. I asked the React native community more about themselves. And they said to me that what they were looking for was more freshman material on React.

Many React native people, they didn't even know JavaScript when they had to learn it. You come in as a Swift developer on this team, and they're like, we use React native. Okay.

Well, what's React native? React native says, React native. It's like React, but for mobile platforms.

All right. Let me go read the React docs. React docs are like, React is just JavaScript.

Oh, god. They go to Mozilla, and they're like, okay, now I'm learning JavaScript. And then they have to work their way back from that, and I was like, damn, why are you doing this with a six-figure salary?

I'm like, okay, yeah, that makes sense. They wanted more visual content. We'll get into what exactly that means.

When they say visual content, they meant that they wanted to see what the code would output on the page. And we're not asking necessarily for illustrations or diagrams, but I used to be an award winning cartoonist, so I gave them some of those, too. I also really appreciate the independent cartoonist scene that you have here in France.

I've always deeply admired the French comic book creators, so shout out to all the artists that I used to work with in my first career there. They wanted more in-depth content on specialized topics and up-to-date component API documentation, and of course, this is the big one, interactive code. I also ran a bunch of surveys on both the React community and on the� and I'm sorry for the sibilance.

I can hear that there's sibilance. I don't know how to stop it, but I'm not going to mess with the mic. Anyway, the development surveys that I ran, one of them I found out that turns out 41% of React developers came from a mobile background.

That's a lot of people who aren't familiar with the JavaScript community at all. Some of them, 10%, had no experience with programming at all. React Native was their first touch point.

First step, though, was to speak to more people. The React Native documentation was assuming that everyone who was reading the docs was already familiar with React and that they had a web background. So we went through� I went through and added these switchers to add context based on where people's background was coming from.

Design systems for mobile devices are called different things and referenced differently. Also added a React refresher so that people could ramp in quickly. They didn't have to go read all these other docs first.

Like, React's not that difficult to get the basics, and linking back to the React documentation throughout can help people get things in context. And of course, added interactive sandboxes, courtesy of Expo. Thank you, Expo.

Anyway, because the docs weren't built from source, that meant that the API references would fall out of date as React Native was updated. So I ran a documentation drive and let the community help, because everyone always wants to help in the React and React Native communities, and we went through the source code and updated all of them from scratch. That was pretty cool.

Brought in experts, such as guest writers that we know and love. One of them, Cady, she's going to be speaking tomorrow, probably standing at this time and place. So if you're here for a React Native conference, check her out.

She did the security section. And we also added colorful illustrations, which turned out to be very popular. And then, in July of 2020, boom, React Native.dev launched. It used to be GitHub.io slash meta slash it was very sad, and that's where the documentation lived. I mean, would you take that seriously? And it's a version 0 still?

Yeah, no. It's slightly now it's more legitimate. It's a real thing.

So the reboot, all of these things that we did, by the way, they increased user satisfaction with the documentation by 70%. So that's thumbs down versus thumbs up. People started slamming that thumbs up button a lot more after this launch.

That's pretty good. The whole effort took about six months. So with that success, I spun all that straw into gold, I was allowed to do what I came to do.

Work on the actual React documentation. So that was pretty exciting. Turns out that React docs have a huge responsibility with 86% of developers in 2020 claiming that they got started from the old docs at React.js.org.

That's a huge lift. So the project officially kicked off May 27th of 2020. The very start of the pandemic, you know, I said, how did you spend your pandemic?

I still have my mindfulness journal. It literally says played StarCraft at work, kicked off React educational materials reboot, and got to talk to some friends, et cetera. That was how I was spending my pandemic, playing StarCraft and working on this.

It was fun. And just like with React Native, I started with the community and asking them questions. You'd think I'd be like, oh, I know what the React people want.

These are my people. No, no, no. Never assume you know what people want.

You have to ask them. This is the biggest mistake that I think most people building for other people make is they assume they know what someone wants. And the only way you can really know what somebody wants is to ask them.

And even then, they might not know what they want. So it's open to interpretation. But you should usually start by just asking them.

And the results were very similar to React Native, you know? Except for this. They definitely were like, why is it still teaching class components?

Because the function components documentation was buried three layers deep and in multiple places. Where is the hooks reference? Great question.

More visual content, please. And of course, interactive code. Which wasn't very common back then, but the Svelte documentation had them.

And everybody really liked that. So this is what it looked like. I had Dan Abramov over during one of the lockdown lifts.

I was like, Dan, do you hang out with weird, unsavory people? And Dan was like, of course not. And I said, good, you can come over and I'll make tea and put some cookies out and there will be Post-its.

And it started this way. This is how we worked through all the content that was in Dan's brain. We tended to communicate a lot in sketches, which actually turned out to result in making a new friend.

So doodling was an important part of my journey with React. I would doodle a concept for the team and be like, is this how rendering works? And they'd be like, oh, my god, no.

And I'd be like, okay, okay. What about this? And this is how we communicated.

I even came up with some rather interesting ideas for visualizing state changes. I was thinking I was working a bit with Brian Vaughan on what state notation could look like in a possible variation of the DevTools. But what came out of all of this was this little guy, who is inspired partly by Ikea instruction manuals.

He became colloquially known as React head. And he started to show up in those notes that I was making of what I was learning from Dan. Oh, yeah.

This one. It keeps going. You can see I used to be a cartoonist.

We often ended up describing React as being a waiter who is, you know, serving people things that they had requested. And in the end, they ended up looking very polished, and some of them made it into the documentation. I was really pleased with how it came out.

Now, we ended up with a huge spreadsheet of content. This isn't all of the content that we made, but when you write a book, you usually have a spreadsheet. No one just sits down and is like, I wrote a book.

Usually, you have to skeleton out what does it look like? What are the points you're going to hit? Where is the content going to go?

And if you've worked with an editor, this is what you get if you built a technical book. And we had one of those for the React documentation as well. It was a big lift.

We went to beta in December 8th of I think this number must be wrong. It was not 2020. I think it was, like, 2022.

I forget which. But anyway, it was a while later. We went to beta.

It took a while. And React had made their debut. See this is what it looks like actually on the site.

Cool. And we also had this awesome diagramming system created by the Maggie Appleton who sometimes speaks at these events. I unfortunately can't tell you to go see her talk later today, but you should have her by sometime.

Anyway, she did an amazing job turning my sketches and doodles into a proper diagramming system. And one of my favorite bits is that we changed all of the examples, which were kitten based. I'm very sorry.

They were kitten based. And sometimes Star Wars was in there. We had Sylvia Vargas, another awesome human being in the React community, Sylvia Vargas was tasked with taking all of the examples and fitting them to an international audience.

I don't much like the idea of American open source owned by Meta propagating American pop culture. There are very few cultures in the world that don't get a Star Wars reference. I actually consider that a flaw, not necessarily a good thing.

Because it's pervasive, you know? And it also says this was written for a certain person. You should get our in jokes.

You'll also notice, for instance, that there are very few examples that speak to female nerddom. My little ponies, neopets, et cetera. Most examples speak to the traditionally male American pop culture references.

Star Wars, Star Trek. So we expunged them. All of the examples reference things that anyone anywhere in the world can appreciate.

Scientists, cuisine, countries, different civilizations, languages. It celebrates the sum total of humanity rather than leaning on you getting a reference that only 16-year-olds in American high school would get. It was part of the inclusivity goals of the documentation.

That they would be universal. Also added interactive sandboxes made using code sandbox. These were a real game changer, actually.

Because it turns out people learn by doing. They learn by doing, not by cramming. And one of the problems with all of those courses I used was that they were forcing me to cram knowledge into my mind.

Just to study over and over and over. And that wasn't making it stick. The reason is that you need to actually be quizzed frequently.

It's spaced repetition. Having to use the skills that you're learning. And there's a great book called Make It Stick, which dives deep into this, but I just explained the whole shtick.

You do not need to read it now. Just know that quizzing works. So we had to build quizzes into the documentation.

So now, because of these editable examples, we would be able to add these we'd be able to add these examples at the very end of each chapter, as well as in between. We have these little challenges. They're not blockers.

We're not going to prevent you from progressing. You can go ahead and do them. And they're all directly from Dan.

And the hints, it's like getting mentorship directly from Dan himself there. They're so good. And in testing, almost everyone challenged themselves to do these as they were progressing through it.

It was lovely to see that people really liked them. But how did we know if any of it was working? These all sound very nice.

But did these things work as well for React as they did for React Native? Were people getting the function components through this? Well, I mean, they were.

The alpha testers, we did do alpha testing as opposed to just dumping it on the community. We held it back, brought people, showed it to them, asked them beforehand, you know, how likely are you to recommend ReactJS.org? How likely are you to recommend the thing that you just interacted with?

And comparing the before and after, they were three times more likely to recommend the new documentation. So, yeah, I guess it did its job. In 2023, March 16th, the docs were announced mission complete.

The tutorial was added and the API references were completed as well. If you're worried that you might need to learn how to do things with classes, don't worry. Because we put everything at legacy.reactjs.org.

You can still access the old site. It's still there for you if you need it. It's not going to get updated, though.

And here's the fun new landing page. Huzzah! The docs shipped with over 600 interactive examples.

This part actually, whew, that was a lot of work. 600 interactive examples. Oh, my gosh.

And in beta, impacted 8 million developers who got to learn with the new documentation. It was in beta for quite some time. So, I'm glad that it was released and not hidden behind a door.

Now that they're public, hope you'll love them. I want to give a shout out to the French React translation community here for making these available to people in a language other than English. Another very important part of the effort was to ensure that the translation community could continue to do their great work to make sure that the React documentation is available to everyone everywhere.

Anyway, I wanted to say that the work we did with React Native, it went a long way to impacting what we were able to do and know would work with React itself. I just wanted to give a shout out to the people who participated in the React Native documentation and all of our surveys and for your patience. Without the React Native community, I don't think the React documentation could have been as good as it was.

I love seeing these two communities come closer and closer together. And thank you for helping make the docs great.

[Christophe]
Thank you, Rachel.

[Rachel]
I think I come over here now, do I?

[Christophe]
Come on, you want to come up?

[Rachel]
I see a piece of tape here. That must mean I sit here.

[Christophe]
Either that or that takes you off camera. I'm actually not entirely sure about this.

[Rachel]
You know, the fun thing about being the first to go is we get to learn with me. Anything that can go wrong is going to go wrong with me.

[Christophe]
That's what you do, though. We learn with you.

[Rachel]
Yeah, that's true.

[Christophe]
Yeah, that's true. How was that? Do you like that talk?

Yeah? Go to these docs. I don't care how long you've been doing React.

Go to these docs and use the entire learn section, apprendre in French, through the entire thing. I guarantee you're going to get better at React, however good you think you are right now. And half of it will be, oh, that's why, you know?

Like, stop ignoring dependencies on use effect. You're always doing it wrong. There's never a single valid reason to do that.

Yes?

[Rachel]
I highly recommend if you're interviewing for a role, just go through the chapter headings of each one and go through the examples. It's a really good way of preparing yourself for the ha, gotcha questions on interviews.

[Christophe]
If you're adversarial about it, yeah.

[Rachel]
There are many companies that are. I don't know that I'd want to work for one of those, but I'm not sure. Are French companies adversarial?

[Christophe]
We have as many jackasses as everybody. It's actually sort of the national ethos. But we do have, like, good interview processes as well.

[Rachel]
You were a great audience, by the way. They told me don't expect any laughs at all from a French audience, but I guess we have some out-of-towners here.

[Christophe]
It's early in the morning, yeah. Coffee still. So, yeah.

Okay. So, do you want to get started with the questions, Romain?

[Romain]
Just a point. Don't forget to post your question directly on the Slido, and you can also write it in French if you are not confident in French. We will translate it for you.

[Rachel]
I can use my Duolingo skills.

[Christophe]
Yeah, yeah.

[Romain]
Do you want to get started with something, or? Yes, I will take one question. Do you have any idea about how much user interact with interactive example?

[Rachel]
Well, I don't have access to the Google Analytics anymore. So, I can't answer that. But I can say that when I was watching people, I would run, like, user research sessions where, you know, person comes in, I say perform a task, and I just kind of watch them.

And from what I understand, once people realize that they're interactive, they're unable to stop interacting with them. People will interact with the examples on every page.

[Christophe]
Yeah, it's a bit like when you're writing your own game, and you start fiddling with it forever, even if it's not done, just because you can. Yeah, those are pretty great, honestly. And the challenges are pretty great.

Actually, making sure that the French translation for the tabs in the challenges did not cause too much overflow was a challenge in itself. But I had to rephrase some of these.

[Rachel]
Maybe you should have given the latter half of the talk. We should have been, like, now over to you about the challenges of translating them.

[Christophe]
Yeah, it was fun. So, what would you say maybe was, like, the hardest challenge in bringing those docs to life?

[Rachel]
Shipping them.

[Christophe]
Yeah. Getting out of beta, you mean? Getting out of beta?

Or even just getting to beta?

[Rachel]
Getting to beta. The React team has a lot of people staring at them, and they can be very shy about releasing things that aren't perfect. So, there's a bit of self-consciousness and convincing the team, like, no, these are really good.

The community should have them. It's like, oh, but the API reference isn't done, and I don't know if this metaphor is really quite good. It's like, no, no, no, no.

Look at the numbers. Look at the testing. Like, it's good.

It's good. We should go. We should go.

That was the hardest part. The content was actually probably could have launched six months earlier, but the hardest part was overcoming the team's fear of failure.

[Christophe]
I think they've done some progress in that, because when I see the state of new pages being published, it's very much MVP, and so I think they probably made some progress into getting stuff out earlier.

[Rachel]
I think also that it's more of a community effort inside the team now. You have more people contributing to the documentation, and part of that is because of the way we set it up to make it super easy for team members to contribute. You make a markdown file.

You add examples using a special kind of MDX, and it's very easy to just build new versions of the site. So after going to beta and after launching, now it's really easy for team members like Luna to add and release new pages. So I'm happy to see people contributing to the documentation regularly now.

[Christophe]
Yeah, it's moving reasonably fast, on a basically weekly basis.

[Romain]
You know developers love to write documentation. Do you think they can be trained to write documentation, or is it really something dedicated to content creators?

[Rachel]
You know, that's a great question. I find it writing documentation is a bit like acting. You know, you could say some people have a gift, but usually it comes down to wanting to do it and practicing, and you know, you will always get better with practice and study, and people who seem gifted at it probably have practiced more.

But you, Christophe, you translate, you translated Dan's writing before and after the documentation.

[Christophe]
Yeah, and like the prior docs.

[Rachel]
Did you notice a change in Dan's writing skills?

[Christophe]
Oh, for sure. We mentioned that yesterday at the speaker dinner, but it was obvious that the phrasing, like there was a lot of like best practices in terms of educational writing that were sifting through, like using simple phrases, not using too many pronoun back references, spaced repetition, rephrasing of the idea multiple times in the same explanation. It all, it was very manifest, and it was not the way he used to write.

Although he always wrote like pretty well in terms of pedagogy, like the original Redux docs were pretty great from that standpoint, for instance. But you could see there was clearly taking into account a lot of other best practices that he might have been unaware of. So for sure, yeah, the writing style changed very much.

[Rachel]
Yeah, one of the best ways to get better at writing is to work with a great editor, too. I got better at writing when I published my first book and had an editor going through and challenging the way I was conveying ideas. Same with MDN.

It's definitely something that helps to have another person there to push and pull with. And so if you want to become a better writer, the best thing you can do is work with a writer you really admire, and they will help you acquire some of their skills.

[Romain]
Final one, maybe? Yes. Did you plan to add some gamification, for example, to, I don't know, winning badges or things like that, or maybe to save the progression when you start learning React?

[Rachel]
You know, a lot of people ask us that. Like, oh, oh, you've got challenges. You're going to block people from progressing until they show their work.

It's like, no, because there's many different ways to accomplish the same thing with React. There's no one right way. And so we have no way of testing, like, you got to, you know, like, how you achieve it is less important than that you were able to achieve it.

Sometimes you can achieve things, you can achieve goals in ways that are not really good. So we didn't want to create any sort of gating mechanism. And also people learn nonlinearly, so forcing them through a linear progression is just not working with how people's learning styles are.

We're not adding any badges or anything like that. It would be I don't think it would actually make it easier to learn React. I think it would be fun to do.

But let's leave that for the Josh Comos and the Kent C. Dodds and their courses.

[Christophe]
Yeah, they're pretty great, too. You can't put everyone out. Even there it's not blocking.

If you look at Josh. Even the GitHub project space are just, like, for extra credit, but it doesn't prevent you from going forward.

[Rachel]
No, it's a docs project. It's not a course project. We're just trying to get the information out.

We're not trying to build a new courseware system.

[Christophe]
Anyway, yeah. We've got a lot of great questions, but we have to move forward with the schedule. That's why the breaks and the hallway track is for.

So please go find Rachel with your questions. Thank you very much, Rachel. Thank you for having me.