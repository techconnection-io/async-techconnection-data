---
slug: >-
  /talks/frenchkit/swift-connection-2024/bas-broek-building-an-accessibility-culture-one-step-at-a-time
date: '2024-09-23'
title: Building an Accessibility Culture, One Step at a Time
author:
  - Bas Broek
video: xuZPwBbkoOs
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/xuZPwBbkoOs.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Bas
Good afternoon, everyone, how are we doing? Good first few talks? Good first experience at FrenchKid or SwiftConnection for those first time here?

Amazing. Well, I'm so happy to be here and talk to you about a topic that is very near and dear to my heart, as some of you might know. And that is accessibility.

And what we're not going to do today is learn all about accessibility APIs, but actually take a step back and understand how can we build an accessibility culture at a company? And we want to do that one step at a time. Because we've all tried to jump into that one project and not think about designing how to do that API and then it all went completely wrong.

So we're going to take it one step at a time. Why do we do this? Why do we do accessibility?

I think there's a lot of answers to this question, but I believe that it's pretty black and white. There is people that rely on apps being accessible. And otherwise, they can't use it.

So imagine yourself, you know, not being able to use your favorite music app or being able to text that friend. I think that's how we should think about building accessible apps. And with that, accessibility is kind of a you problem or, well, rather, it's an us problem as developers, as designers, as people building apps in teams.

Now, why do I say that it's an us problem? It's a you problem? Because you can make the difference.

Part of building an accessibility culture is getting, you know, input from higher ups and buy-in, but that still doesn't really get us anywhere, so we still need to be the ones that advocate, implement, verify, and improve. So where do we start? It's a good question.

And one that I unfortunately can't really answer. And I think a lot of the challenge about where to start is that we don't know what we don't know. Getting started with accessibility and getting used to what it means to build accessible apps is incredibly difficult.

And a lot of us might not have had the opportunity to learn about it in school or in university. Having said that, what we can and what we should do is plant seeds. This presentation for all of you, hopefully, is planting the seed of building an accessibility culture.

Making those few improvements that start rolling, you know, this idea. And, of course, once you do start making those improvements, you should share them with your team and kind of create that snowball effect for more improvements. Many of you might know a screen reader or voiceover on iOS devices that can read out the elements on your screen, and it's mostly used by people that have sight difficulties or are blind.

So we can start. We add accessibility labels everywhere. Great idea, right?

Well, it's a valiant effort. Labels aren't necessarily a silver bullet and do not encompass all of accessibility. And some things should not be labeled, as we will see later in this presentation.

So maybe what we'll do is take one step back and breathe for a moment. What if we made accessibility accessible? And what do we mean with that?

Well, let's try out what it means to use some assistive technology and how we can actually use it to understand accessibility and add accessibility to our apps. The first one is a tool called voice control, and it lets users interact with the screen by voice. What it can also do, as you can see here, to visualize labels on the screen.

And you might spot things that don't look exactly correct. Having said that, coming back to the screen reader mentioned before, some labels might actually be different, and there's an API to do that. Because double tap to dismiss this menu is not a great thing to have to say out loud to actually do that action.

So that's voice control. There's also one of my favorite tools, very low key on macOS, called hover text. And it is a great way to get a feeling of accessibility labels, both for elements that are text, as well as iconography.

On the left, we see what I would say is a good example. We have an icon, and it has a great label. So a user that would navigate to this using voiceover would hear close.

On the right, I would say we have another good example, but something that probably should not be an accessibility element. But hover text can really help us go through an application and understand where we can fix these kind of issues and what the state is. And note that this also works on the simulator.

So within macOS, running an iOS app or watchOS app or anything, we can sneak in there and get hover text working there as well. And you can set it up in system settings, accessibility, zoom. So if you take one thing away or start taking one thing away, this would be one great thing to set up.

And anyone can really do this and just use it as a tool. And sometimes also to just show in a demo when you have some small text and you want to enlarge. So that was hover text.

Now this is a clever tool that is part of voiceover, Apple Screen Reader. You can enable something that we call caption panel. And it will show at the bottom of the screen to output what was read out by voiceover.

So, if you're debugging or if you're wanting to test without sound on, you can see at the bottom of the screen what the output is of the screen reader. So it's a great way to keep an eye on the output and debug it. Why is this slide empty, you might wonder.

Well, because there is nothing to see. There is some functionality in voiceover, and it's called screen curtain. And it turns the screen off.

You cannot see anything. And I think this is a great example of users actually relying on these technologies, giving feedback and understanding their needs. Because if you are blind, you can't see the screen anyway.

Why would you waste valuable pixels and battery on showing the screen? But then it's also a really neat trick, if you want to do something fun tonight, to turn on screen curtain and actually navigate your app and see if you can make it work or if you get stuck. And then you'll know what users relying on it actually feel like.

So that's screen curtain. Xcode comes with a great tool called the accessibility inspector. And this is yet another way to inspect what your accessibility looks like in an app.

And as you can see on the right, or as you can see on the left, we've navigated to the button. And on the right, you can see a lot of details of everything that's going on. You see the label.

You see the type. And you see all the advanced information to debug and understand what the accessibility is set up like. And I won't go into the details of everything here, but actually the type is really interesting.

It's also something we call a trait. And it's part of the element you are exposing as an accessibility element. Because there's actually this thing called a braille display for users that might be deafblind.

And what it will do is Xcode or your program will know it's a button. And it will actually expose it in a braille display. But because it's not written as button and it's just a type, it will actually be concatenated to BTN.

And it will be localized, et cetera, et cetera. So that is accessibility inspector. Now when we talk about building an accessibility culture, this goes beyond testing, adding accessibility, and actually what you want to do is get more people on board.

So one of the things that we've done is creating good first accessibility issues that any new team members or maybe people from other teams that might be interested in diving into accessibility to pick up. Ideally these would not be major issues that your users have to deal with before they get fixed. But they can be a great way to get somebody on board and give them a great first ticket that doesn't leave them hanging.

Probably my favorite tip that I've received in the last few years is to make all your demos with assistive technology. So when you give that next presentation, do it with voiceover. Do it with voice control.

Maybe turn on screen current and really show the impact it has. And especially if you show a before and after, you can really create that clarity of the impact it makes. And then going back to the black and white idea of users relying on this and not being able to use your app if it isn't great makes the point come across really well.

You won't be able probably won't be able to do it all alone. So what you'll need at some point are sponsors and peers. Sponsors might be your higher ups.

Peers might be people in other parts of your company that can help you out. And talking about the demos that you might have given assistive technologies, hopefully there's been some people that said, hey, you know what? Tell me more about this.

I want to help. And at WeTransfer where I currently work, somebody I want to shout out is Lina, and she works on social responsibility. She's been really great in helping me set up trainings and everything that is not so much developer-like.

So taking a look at the bigger picture, we want to roll out training as well. We want to make sure that people can get over that first hurdle of accessibility where people don't know what they don't know. You might want to incorporate that in onboarding.

Maybe you want to do office hours for those users or those people in the company that do know a bunch about accessibility or invite speakers. And hopefully at some point, like those pesky IT tests that you have to take every three months, you can make this mandatory as well so it has to make sure that everybody is involved in accessibility. Actually, what is not accessibility?

Isn't kind of everything accessibility? When you think about it, localizing your app is accessibility. Dynamic type, making your text larger or smaller, accessibility.

Being able to autocomplete and not have to manually copy and paste your password in, that's also accessibility. Dark mode, you guessed it, accessibility. Sensory feedback like haptics or sounds, accessibility.

That's a lot. And maybe you might not be able to see the trees through the forest anymore after that. You can't do all of this at once.

There's so many layers to it. And I would encourage you not to try. As we said, one step at a time.

But think of one or two of these things that you might be able to take into your next meeting or your next demo or your next project that you're working on. And talking about the next project that you're working on, you're probably working with designers. Some of you here might be designers.

So what can we do to shift left, as we say, and see how we can get accessibility as part of more than just engineers? I think design thinking about labels of elements, thinking about sort priority, how should a screen reader navigate the screen? Traits to indicate if something is a button or static text or a summary element.

That's a workload you can share, especially with designers, to have that be part of the design phase to understand what we need to add to labels, what we need to add to elements and what the accessibility and infrastructure will look like. And it's a great way to share workload, but also knowledge and energy. And that kind of makes a weakness a strength, hopefully.

It's hard. So instead of trying to do it all right, maybe what we should try is to not do it wrong. If you don't know exactly how to get things right with accessibility from the start, at least don't try to do it the wrong way, like check the low-hanging fruit.

You should probably know and can understand that text sizes would be great to go smaller and bigger. If you have an image and it's read as IMG underscore 555.png, not ideal. And another trick you can use is if you don't know how to label something is to imagine that you're explaining it to a friend over the phone.

You have to go into settings, that's the app icon with the cog, and kind of visualize it that way. So don't build that car with all those fake buttons and a lot of touchscreens that nobody knows how to handle. Another really, really, really important thing is to talk to your users.

Users that rely on assistive technologies have special requirements and really know how to deal with handling a phone using an assistive technology. We might try to use voiceover and we can kind of make it work, but can we make it work with screen curtains? And does that thing really need to be a label or does it need to have a label, does it need to be exposed?

You want to try to work with users that rely on assistive technologies. They will give you super valuable feedback and will give you a better understanding of apart from checking boxes and making sure we pass some audit, that our experience is actually accessible and users like to use it. At WeTransfer we've worked with a company called Fable and they helped build trainings for us and the other thing they do is they put us in contact with users that rely on assistive technologies.

So when we build a new feature or have a new idea, we talk to those users and we get that input and we get that feedback. Apple Viz is another great website that you can go to and get input from the community relying on especially visual needs and then obviously all those results that you find, you can share them with your team, you can share them with the writer, company at all hands and share the accessibility understanding. But Apple doesn't write, right?

Well, what can we learn from them, right? They do a great job. They have great accessibility and we should be very thankful for that.

But we should also realize that it doesn't just poof, come out of nowhere. The accessibility culture at Apple is fantastic but scaling it is still a very difficult problem that hopefully in the companies that we work at might not be as hard to scale. But we can definitely take a look at what Apple does and learn from that and try to do it maybe even better where we can.

All right. Skiing. Accessibility is kind of like skiing and I like skiing and I like accessibility.

But not just that. When you build apps, you will be going downhill. You build an app, you release it to your users and it's up to you how you do that and how safe, right?

Do you have CI? Do you write tests, et cetera? But then once you get to the bottom, you have released and you might not have taken accessibility into account.

Taking the lift from the bottom to the top takes a long time. And it's often really cold. So what I'm trying to say is try to start yesterday.

Which is very unfair to say, but try to keep the process rolling. All right. It's been a lot of things.

So now what? As for all of you, go out there, start somewhere. Share your learnings.

Get that accessibility ball rolling. It will be like pushing a boulder up a hill. Which is not necessarily fun.

And it will be tough. And hopefully you can find some people that can help you push it up the hill. But unfortunately that's what accessibility is and probably will be like over and over again.

But make a mark. Leave the world better than we found it. It's like code, right?

We do it for others. We build projects. We build products for others to enjoy.

But we write code and we do that for our colleagues and we do that for future you. I promise you won't regret the effort of putting accessibility in, embracing it, and learning from it. It is worth it.

It is worth it over and over again. Because once you go to that next company, you will have to probably do it over again. Speaking of doing it over again, I am looking for a new job.

So if anybody wants any help, let me know. Hit me up. And I would love to make accessibility better at your company.

At WeTransfer, I don't know what will remain of the culture we built. Things go on, though, and I'm proud of what we've done. I believe in you.

You can do this. And hopefully we've just built maybe not an accessibility culture, but the start of an accessibility culture. And I count on you.

And one last thing. If you want to, feel free to come up to me afterwards. I would love to do some hands-on, fix some issues, and maybe you can show them off at your next meeting.

Thank you very much. And thank you, Bas.

### Ellen
Thanks, Bas. I wanted to start by asking, you mentioned that one place where you can really streamline this process is getting designers involved early. Do you know of any sort of tools or techniques that, as the designers are working with something like Sketch or something like Figma, that allow them to sort of annotate stuff for accessibility?

### Bas
I think we use Figma if we transfer, and Figma has a whole load of tools for accessibility. Excuse me. I don't know exactly how they work, how you download them, do you pay extra, I don't know.

But there's a lot of tooling out there that can help. You can also do it manually, right? You can kind of duplicate your design and add your labels there to indicate the how and what.

But, yeah, there's a lot of tools out there that you can use to make that work.

### Ellen
Cool. Some questions from the audience?

### Julien
Yeah, I'm going to rephrase slightly, but how do you feel about the European Accessibility Act? Quite a big seed, right?

### Bas
It's an interesting one. Because first of all, that's about finishing audits, like checking boxes to some extent, and not necessarily about going that extra mile and making an experience actually accessible. And then on the other hand, rules are great, but they will have to be enforced.

Because otherwise, why would we do them, right? I think in 2021, something similar went into effect for web, and web is not a great accessible place. So, I mean, I hope for the best.

I think it will help. But it won't be... I won't expect every company to be jumping, like, yes, now we need to do it, now we want to do it, now we want to hire a lot of people and take this seriously.

Because it really just still needs to start with us, with you. Maybe I'm proven wrong, hopefully. Let's see next year.

### Ellen
It's interesting. In the United States, under the Americans with Disabilities Act, people couldn't sue you if your app is not accessible. Domino's lost a whole bunch of money on that.

And that's something that I think people have used to sort of be like, okay, this is actually like a business problem, in addition to actually being something that humans want to use.

### Bas
Yeah, it does feel a little bit weird that it needs to be that, you know? But also, I guess it's better than nothing.

### Ellen
Yeah. It's definitely... You want the carrot, but sometimes you need the stick.

### Bas
Exactly.

### Ellen
I wanted to ask, so you mentioned that you guys use something called Fable at WeTransfer. I'm sure that they're probably some sort of paid resource. So for people who are more working on their own and are looking to figure out, like, how do I even figure out, like, what assistive technologies my users are using?

What's the best way to find out about that, other than, like, waiting for them to complain?

### Bas
It's a really difficult one, because it's also quite frowned upon to track it in apps, which would be kind of one way. But that's also, like, a chicken and egg problem, because, like, oh, only 1% of my users have it. So I guess it's not that important.

I'm like, well, you know, if you think that way, that number is definitely not going up. It's a difficult one. I would say social media, reach out, you know, try to get that kind of feedback actively rather than just waiting for it.

And, you know, again, as I mentioned as well, Apple Viz, free to go to and ask questions and get feedback from users. So that would be another good opportunity to look at.

### Ellen
Thank you.

### Julien
Well, do you have examples of apps with nicely integrated accessibility that we could inspire from?

### Bas
The WeTransfer app, for now. Well, Apple as well, right, has great apps. Spotify does well.

What else can I think of? There's an app called Be My Eyes, which is really interesting. What they do is solve an accessibility need.

So what users can do that have eyesight problems is they can call someone else that can see. So they might show you, I think the last time I helped someone, they showed me some letters that arrived in the mail, and they're like, what is the name on this letter? So that is not so much an accessible app, but it's an accessibility app.

So also definitely take a look at that one. And go take a look at your favorite apps, right? You can also learn from the apps that are not necessarily great.

### Ellen
Are there other accessibility tools? So you definitely mentioned like a Braille keyboard and voiceover and voice control. Are there other accessibility technologies that people should be thinking about as well?

### Bas
I think it's a good place to start. You have full keyboard access as well to navigate by keyboard, which is kind of built on top of voice control. You have assistive touch, which a lot of users might or a lot of us might remember like back in the days when we were worried that our home button would break, you could actually put a virtual home button on your screen.

Think about haptics, think about sounds. I think that might be more important than checking all the boxes of all the assistive tech. The last interesting one is, and I forget its name.

Switch control. Exactly. So this is really where you can navigate your phone with just one button, which as you can imagine might be pretty tedious, but try it out and you will understand that this is life changing for people when you can actually do this.

### Ellen
Watching people who are paralyzed and that's how they interact with their machines, it's really impressive to see how much people can do with just one button.

### Bas
And a recent addition as well is assistive, no, what is it? It's basically what you can do, assistive access, that's the one. You can reboot your phone or your iPad and everything is big.

So imagine maybe your parent or grandparent that might have difficulty because all the letters are very small. You can have everything in a grid system or in a row system. Everything is large touch points.

The messages app is optimized so you might say your keyboard is only emoji and simplify it that way. I hope to see some improvements in the future where our apps can actually opt in for it a little bit better, but I think that's also a really exciting thing. Also as we ourselves grow older and maybe at some point want to use that.

### Ellen
We're all getting older.

### Bas
But all at the same time, so, you know, no worries.

### Julien
Last question from the audience, there is a question about measurement, how do you measure how many users with disability you have and I would add a personal one because I struggle most of the time with accessibility to test. How do you automate testing? How can you have metrics like code coverage, code complexity related to accessibility?

### Bas
Okay, so first question, sorry, what was it? The first one is how do you know your audience? I don't want to know because again it's kind of frowned upon and Apple is kind of not really introducing APIs anymore that let you check which accessible tech users are using.

I do it because we should do it because it is important to individuals, right? It's not that, oh, it's only 5% so whatever. If we need to measure it, yeah, you can dig up some APIs to do it, but I don't think we should.

Second question, tools, automation is really tricky and the reason for that is you can check, you know, does this button have a label and is it like longer than a few characters, but if we label a button, you know, cow and it is actually a close button, maybe there is some AI tooling coming up that can hint at it being wrong.

### Ellen
What about UI tests?

### Bas
What about UI tests?

### Ellen
Can you set up your UI tests to make sure that you are using, rather than like selecting a particular identifier for a view, that you use the accessibility items to sort of tap through it?

### Bas
I would recommend against that. That's why we have accessibility identifier, which if you ask me should be called automation identifier.

### Ellen
I meant more accessibility labels rather than the accessibility identifier.

### Bas
If we go and use accessibility labels, we might change them in the future. Maybe that's what you want in your test breaks, but it's not necessarily wrong. They're localized.

Yeah.

### Ellen
I think one thing that I have done in the past is have sort of a shared set of strings where you basically say, okay, like here is basically a static let that points at the localized string that I am using, so that even if the copy changes and particularly also like if you are testing in a different language, it's still basically pointing to the right thing. It's always going to be the same thing in both places.

### Bas
I think it's something you could do to keep an eye on it, right? And to see, like, okay, if something breaks or if something changes, maybe a test will fail. I think it's hard to make clear in a test then, like, okay, why did it fail?

What should we do to fix it? But at the same time, hey, if it works for you, you should go for it.

### Ellen
Yeah. Absolutely.

### Julien
With his wise words, we stop here. Thank you, Bras. Thank you.