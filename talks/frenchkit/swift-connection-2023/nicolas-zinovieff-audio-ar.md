---
slug: /talks/frenchkit/swift-connection-2023/nicolas-zinovieff-audio-ar
date: "2023-09-21"
title: Audio AR…?
author:
  - Nicolas Zinovieff
video: 0M2kQ0qcpTM
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/0M2kQ0qcpTM.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/0252a90b57a444308baf6a8996dc3181/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---

Yeah, I kind of hacked the conference and decided to piggyback on the whole vision thing and talk about a very dear topic of mine.
Audio augmented reality has been around for a long, long time.
So I'm going to tell you why you should implement it and tell you that it's actually pretty easy to do.
So just to start, who am I and why am I doing this talk?
People who know me know that I do code.
I'm mostly known for that.
They usually don't know that I used to work in movies.
And I actually have a piece at the MoMA in New York City, so if you want to go and look for my name.
But I do not have any kind of artistic talent,
So don't expect anything fancy.
I'm just here to try and tell you that you should take care of the audio thing, both for the whole accessibility thing, which is very important to support at least two senses when you try to do something.
And I do have a passion for data representation.
And audio is usually underrated in that department.
So the objective of this talk is to actually make you think about it.
There won't be a lot of code shown, but I can show you some code afterwards if you want.
We're going to talk about history, and then we're going to go up the ladder 1D, 2D, 3D.
There is no 4D yet, but Apple has a few more years ahead of them, so who knows?
History-wise, augmenting reality started with sound.
You were working somewhere, and you would hear the bells calling you to the town hall or to church, tell you things that you cannot see.
More recently, we have attention capture things, like your phone that's ringing.
It's your appliances that ting when they're done.
So the whole augmenting reality through audio is all around you and you tend not to think about it.
You can do it very simply and you should.
Let's start with mono.
Mono, you can play with the kind of sound you're playing and the volume.
Side pet peeve, very important, volume doesn't mean anything.
You have your slider, your volume slider.
The way that works is way more complicated than that.
And those who know me know that I'm a math head.
So basically when you have one watt of power plus 25 dB, it means 300 watts of output.
Just remember two things when you talk about dB.
One, most people don't know what it is, so don't even think about it.
And second, it's an exponential scale, which is going to come back in some later slides.
But if you do plus 3 dB, you actually multiply the power by 2.
So it is not as simple as just moving a slider left to right.
It's going to come back when we talk about environments.
But if you're a physics head, just a side note, it's actually funny if you take decibels applied to noise. you realize that it's in kilograms per second cubed, which kind of translates to the speed of the pressure change on your ear.
And that actually makes sense.
Some notable examples of using mono in your UI or in your applications or in the world around you, you have the obvious one, which is the UI feedback.
If you go volume up or down, and you can hear the beep, beep, beep, beep, you can have the ting for notifications, but you can be a little bit smarter.
Like if you ever played Mario, which I guess most of you have, the music speeds up to tell you that you don't have much time left.
And if you have a recent-ish car, you will hear the radar that tell you how far you are from the thing behind you.
So take these inspirations and use them.
You can play on the speed of the sound.
You can play on the pitch of the sound.
And you can play on the volume, quote unquote, of the sound.
It's fairly simple to do.
Just play a sound and tell your users what's going on in your application.
Especially when you talk about 3D environment, if you have a window in your Super Vision Pro that's behind you and it's doing something, your users will not look at it until they hear a sound.
So think about it.
An example, I'm the department head of development tracking in school and I decided to offer as a gift with a diploma to the students the music of their studies with me.
So you kind of hear it, right?
All the low notes are bad grades and high notes are high grades and it's just like, you know, a way to represent their studies with me.
I don't know yet if they're grateful for that, but I kind of hope so.
And it makes me laugh so much.
And when I beta tested it on the students, they were like, I didn't realize that during
COVID, for instance, there were a lot of low grades and you can clearly hear them in the music.
Let's move on to 2D, also known as stereo, because somebody someday realized that we actually have two ears.
It's kind of like, it's the forgotten thing.
You don't see very often stereo used in notifications and stuff, because basically it's just mono left and mono right.
And you can see that it's very easy to implement, and there's very few things you can do with it that you cannot really do with mono.
That's why it's not really the important one.
But again, the code is fairly easy.
Everything you can do in mono, you can do in stereo. most of the music or the mp3s or the WAV or whatever you're trying to get is usually stereo but badly used. I was looking for examples, notable examples of stereo stuff and it turns out that I actually found only two. You have the music, like the Beatles were the first major band to use stereo as part of the composition of their tracks and today the only time stereo is used to augment to reality and try to attract the attention of the user is when you play FPS games and you hear the sound coming from the left because there's an enemy there to kind of force you to move left and right.
It's kind of 3D, but it's 2D and a half.
And I could not find any other good example.
So mostly it's mono for notifications and stuff, and sometimes 3D.
And stereo is kind of like that weird not really used thing, unless used as a basis for the rest of it.
Because 3D, right?
3D is actually marketing.
Why is it marketing?
Because most of us only have two ears.
So we don't do that, right?
We only have two ears.
So you simulate 3D, just like you simulate 3D for your eyes, you simulate 3D for the ears.
So stereo is kind of that hidden thing.
And I'm gonna tell you how to use stereo to simulate 3D.
Remember something, sound is a pressure wave. so it follows inverse square law of power, so if you go twice as far, it's you have to divide the volume by four, right?
You just go one over distance squared, and it will give you that, and if you actually use decibels, which is, that's why we use that, every three meters, you divide the power of the sound by two, so that's why we use decibels.
And if you want to do the left-right thing, well, you all remember trigonometry, right?
You just go slightly left, you take the cosine and you apply a percentage of the power left or right.
Okay?
That is fine, and it's also a complete lie.
Because that's not how sound works.
At all.
Different frequencies carry different power.
We're more sensitive to some frequencies than others, so the inverse square law doesn't work for every frequency so you have to figure out which law to use for which part of the spectrum. You also have to take into account the echo like in this room or the reverb that kind of stuff and you have interference right if you have if you ever used a white noise machine you know what I mean. If you want to roll out your own thing you even have to take into effect the Doppler effect right like a sound that's coming towards you is higher pitched than the sound is going away from you. The math is actually pretty hard, so please don't use that, use the slide before. Inverse square law, a little bit of trig, you'll be fine.
If you try to make it too realistic, you will end up in one of these pitfalls and the sound is actually going to sound fake, and that's worse than just simulating the thing simply. So what are my options? I want to do some, you know, like audio augmenting reality and I have four options. You can do an actual 3D environment if you work for the Vision Pro or if you work for, you know, a 3D, full 3D platform, then you can use Reality Composer, you can put a sound on a piece of 3D that you move around and it's going to recalculate for you and that's great.
But if you played with the Vision Pro SDK, you will know that doing an actual UI in 3D is very complicated.
Designers haven't figured it out yet.
So we're going to have to wait a little bit for that.
The option two, which is the most common one and the one I'm going to talk afterwards, is to use the standard AV foundation audio framework.
It comes with a bunch of caveats that you have to pay really some attention to.
But for the most part, it's pretty easy to use.
You can use-- so historically, we tended to use OpenAL, which is a very known framework for that, or AudioKit.
But if you've been to the two Harvest talks before, with trying to sideload some huge libraries and stuff, it's third party, right?
So you may end up hitting a bug that was not visible until production, or it's kind of hard to evolve.
I would recommend AudioKit these days, which is fairly well known and fairly easy to use in a 3D environment.
Or you can roll out your own equations for the position of the sound, right?
If you feel lucky.
A little bit of code.
So it looks big, but it's actually very simple.
It's just a graph.
You have your sound source.
You have the environment node which gives you the where in 3D space things are.
And you have a mixer in the middle.
That mixer is to make sure that you have only mono sources.
3D environment tend to not work really well if you have stereo sources, because then you have to take into account the position and the angle of the left and right of the source, in addition to the left and right of your own ears.
So we do not do that.
If you use standard libraries, they will always tell you to use mono sources.
That is very important, and that is why there is a mixer there.
Otherwise, it would be a simple graph with one source and one environment, and that is it.
You plug them together, and you plug the environment to the output of the Engine.
You start, and everything works just fine.
I actually had a demo for that, but if you want, I can give it to you.
My Swift UI is horrible, but it works.
And we're not going to do that today, because it's short.
It's the end of the thing.
So we're not going to do that.
One last thing to remember when you play with that, try to move only one thing.
If you have several nodes that have some sound, try not to move all the sound sources, because it's actually a very-- because of the math behind it, it's super heavy to compute.
Try to move only the listener.
And I know it's a dirty trick, but you just inverse the problem.
You put some negative x and negative z in there, and you just move the listener position instead of the source of the 25 sounds that you have in your scene.
An example, because I actually did that in 2012, it's an app that is probably still in the store somewhere. we had something to listen to a story that would continue when you reach certain points of interest.
And the idea was, how do we get the person to navigate a city without watching the screen?
So guidance by sound, and that would mean that the story would come from the direction where you were supposed to go.
And once the story, because if you are too slow, whatever, like you would hear like some river sounds coming from the direction where you're supposed to go.
It works super well and the beta testing was great.
Unfortunately, it never caught on.
That's why you probably never heard of it.
But it was a super fun project.
And if you look for HYC on the store, you might find it.
That's it for me.
Thank you.
And thank you for attending the conference.
[APPLAUSE]
So questions from the audience. the most important one being, what's exactly in MoMA?

- I'll let you find it, but it's a piece with a lot of, okay, so it's a visual and audio piece with a lot of transitions.
  It's based on Ken Burns and stuff.
  And it's not, obviously, because I have no artistic talent whatsoever.
  I just was the tech guy, but the artist wanted my name on the thing. and I discovered it like six months later when I received a letter saying
  "Hey, you're the official owner of a piece of the MoMA, how should we conserve it?"
  I'm like, "Are you for real?"
  I thought it was a scam but I have my name there.
  Did you answer that it has to be saved on the iCloud?
  Yeah, no, it was before that.
  I actually have to maintain a 10.3 computer machine somewhere in a VM and stuff, just in case the thing just blows up and they have to redeploy it.
  Alright, I had to ask this question by Hervé, which you mentioned in your talk.
  I just read because it's awesome.
  You didn't mention binaural audio, which is a great way to emulate 3D audio.
  Yes.
  Don't you believe in this technology?
  Question mark.
  Explain your answer with spherical harmonics.
  Alright, so, yes indeed.
  Thank you. So, Binaural is a system of simulating 3D using, well, more than two speakers in the thing.
  But, it's not that I don't believe in the tech, I think it's just too expensive to make the helmets that work and that you can sell to a public that will care.
  Most, like if you go in the subway here in Paris, right?
  Most people have the wired crappy earbuds.
  So, then again, we used to say the same thing about VR helmets and now people are way more interested in VR helmets, so who knows.
  I think binaural is super interesting thing from a math and physics standpoint, but it's kind of too good.
  Yeah, it's too good.
  So we have obviously this very huge device arriving Vision Pro.
  What do you think about this?
  Now that's what I call a loaded question.
  Okay, so we've had several false starts in VR and in AR.
  It comes down to cost, it comes down to critical mass, it comes down to the quality of the applications that are going to be on that thing.
  And the problem is, it's kind of a chicken and the egg problem, unless designers start focusing real hard on how to do some best practices for these apps, it's going to be rectangles in space.
  And that, in my opinion, will never take hold because it just replaces the screen, which, you know, fair enough, you want to have an 8K display and you can't afford it, you can put it in your vision.
  But then you have the sync problem.
  If there are two people trying to see the same screen, you introduce a lot of problems around it that the screen solves better.
  It's kind of like with the binaural thing.
  The solution we have is way cheaper and solves the problem way better.
  When designers start to find some normal-- just like the iPhone normalized the touch interface, when we have some normalization of interfaces that work only in an AR or VR space, it's going to take off.
  I mean, I'm not a marketing guy, so I don't know if-- like if I say, all right, yeah, no, the Vision Pro should be like $800, because that's the only way to create critical mass.
  Sure, but is it going to?
  I don't know.
  It's more complicated than just talking about costs or critical mass because no one's actually played with it in a real environment and the only thing we can think about is, oh cool I can go on my couch and see a huge screen for me and watch a movie.
  Yeah, but I can do that in a theater and I can get a big TV and share with my family. So right now it's, we're gonna have to wait and see and I'm sure that designers will do a fantastic job of trying to find things but until we're at that point it's going to be tricky to sell that to people and it's going to be tricky for developers to invest the 200k just paying two developers and one designer to work on an application just in case they can't sell it. Like recouping that investment is going to be hard so it's going to be the big companies first or the independent designers who try things and I think it's going to come from that side rather than that side.
  Do you actually, are we actually able to hear the demo?
  Or do you have the file on the computer?
  I do have the thing, I can show it to you on the laptop itself, but it won't go through the thing.
  But it is a very simple thing, just pans left and right, and has a piece of sound that spirals around you.
  So the further it goes, the lower the sound, and left, right.
  It's not super interesting, it's just...
  > > And it works in 5.1 and 7.1 and stereo.
  > > All right.
  > > So thank you very much.
  > > Thanks a lot.
  > > [ Applause ] > > [APPLAUSE]
