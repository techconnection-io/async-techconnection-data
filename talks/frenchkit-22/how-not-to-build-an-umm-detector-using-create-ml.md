---
slug: >-
  /talks/frenchkit-2022/yono-mittlefehldt-how-not-to-build-an-umm-detector-using-create-ml
date: "2022-09-29"
title: How (Not) to build an Ummm Detector using Create ML
author: Yono Mittlefehldt
video: 45hxH7-p5IM
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/45hxH7-p5IM.jpg
slides: null
tags:
  - Core ML
  - AI
year: 2022
conference: frenchkit
edition: "2022"
allow_ads: true
---

0:00:35.9 YM: Okay. Bonjour.

[laughter]

0:00:40.1 YM: My talk is how not to create an 'Umm' Detector using Create ML. All right, before we begin, there's a little disclaimer. To prepare for this talk in this project that I created for it, I had to listen to many, many, many hours of audio and listen specifically for uhs and umms. I hear every single one now.

[laughter]

0:01:05.5 YM: So, back to the disclaimer, Should you experience any of these side effects after attending this talk? Well, no refunds. Oh man it's wild. Okay, and speaking of mistakes, we're gonna be doing a live demo against the better judgment of many people smarter than me, and it's going crazy. It's already off to a good start. So what is this live demo doing? It's actually listening to my audio right now. It's analyzing it by running a Core ML model, listening for umms. Oh my gosh.

[laughter]

0:01:40.8 YM: And it's making a prediction every half a second, which is... Is that what's doing it? Oh man. Okay. So I have a story as to why this might not work in this situation. It works without a microphone. It works away from here, but it's counting my shame nonetheless. [laughter] It's gonna be fun. So who am I? Along with Alice, I'm the co-creator of [Gus on the Go](https://www.gusonthego.com/). This cute little guy right here. I am a freelance software developer specializing in computer vision and iOS. Notice I said computer vision, not audio, which explains this wacky thing going on right now. I'm a tutorial writer for 'raywenderlich.com' and possibly my greatest personal achievement to date is as a child, I once operated the volcano on a float at a NASA parade.

[laughter]

0:02:35.0 YM: Well, besides FrenchKit.

[applause]

0:02:36.4 YM: Thank you. Thank you. All right. So story time. Not the parade but how I got here. A year ago, I was at a conference and I was sitting next to a friend of mine who is a podcaster, and he... Between the talks, he was editing some audio for his current podcast, and I was very interested as I am in a lot of things. So I asked him, "What are you working on?" And he told me, "Editing my podcast." I said, "Oh, that's cool. Do you have tools that automate a lot of stuff for you? Or do you have to do it very manually?" And he said, "Yeah, there's a lot of automation involved, but I wish it could detect the umms for me and cut them out automatically." I said, "Well, you know what? I have an idea of how you might be able to do that, but I don't have any data." Well, he had lots of data, so he gave it to me. So why would you want to even do this? Well, besides this material for a conference talk. So who needs this kind of stuff? Well, we've already mentioned podcasters. Show of hands, how many people in the audience have a podcast? I can't see you, but I'm assuming. Wow. Okay. A couple. Okay. How many people are lying about not having a podcast?

[laughter]

0:03:41.7 YM: There we go. There we go, more. All right. So obviously podcasters could use something like this, and to generalize a little bit more, audio editors. Public speaking trainers, does anybody else have any other ideas. I need... I'm looking for product market fits. So I need all the help I can get. Okay.

0:04:00.1 From the audience: Teachers.

0:04:00.8 YM: Teachers. There we go. That's not bad. Maybe YouTubers too, right? Who knows? We'll figure that part out later. First, we'll write the code and then we'll do the marketing. All right. But speaking of code, this talk is not about code. There will be a little bit of code in there to appease those of you that expect it, but it's more about a thought process and the thought process about how I go about creating a machine learning model, analyzing the results, and then determining what needs to change to make it better. So how do we detect umms? Well, what is an umm anyway? It's a single syllable something, right? It's kind of like a word but isn't really, it's just sort of there. It's a filler between when we are trying to figure out what we're going to say next. So if it's like a word, maybe we can use speech recognition. And for speech recognition, we have the option to use Apple's Speech Framework, which is fantastic because it's built in. It's easy to use, and it falls under Apple's privacy policy, which is pretty good.

0:05:10.2 YM: So how do we do this? First, we create our audio engine. This is the code that I talked about might show up, but isn't the main part of the talk. We take the input node from our audio engine. We take the output format of the input node. Now, that's a weird naming convention, but if you think about it, you have this input node, which has an input from the microphone and has some sort of output, which has a format. So that's where it comes from. But naming is hard, right?

[laughter]

0:05:41.7 YM: All right, so we install a tap on our input node, giving it the format we want the buffer size, and we send the audio buffer to our request. What request? Glad you asked. It's the SF speech Audio Buffer recognition request. Naming is still hard. And we can write all this code and test it out, but it doesn't work. It doesn't work because Apple's speech recognition API automatically filters out filler words. Like, umm, like, uh, sometimes like not always like, but uhs and umms. Because when you want to transcribe something, you don't want the umms and the uhs in there, so it automatically filters them out. And we didn't actually have to write any of that code to test this out because we could have just asked our watch and found out we could create an umm detector or not how to create an umm detector or my favorite an M detector, which I guess is useful for James Bond.

[laughter]

0:06:39.5 YM: Okay, I lied a little bit. There's a kind of a hack to make it work, and that's if you create a contact named umm.

[laughter]

0:06:49.9 YM: Because Apple's speech recognition software is programmed to look for contact names. However, it allows detectors for umms, but only kind of, because it only detects an umm, if it's in part of a speech that could be replaced by a person's name. So if you're saying, "I'm going to go see, umm, Johnny." It might detect it there, but if you're gonna say, "I want, uh, car," it's not gonna detect it there. Additionally, I couldn't get outta work. So it's a mixed bag. All right, so back to our question. How to detect umms? Well, how about machine learning? But what is machine learning? Machine learning is the science of getting computers to learn without being explicitly programmed. And if you think about it, that is the dream. That is what all software developers strive for because if you're anything like me, you're lazy. You want something to be done for you. You don't wanna do it yourself. Imagine being able to tell a computer program what it should do and let it figure out how to do it itself. That would leave us more time for beach vacations, gaming, or if we're being absolutely honest with ourselves, more coding.

0:08:00.4 YM: All right, back to machine learning. What do we need for machine learning? Well, who here loves math? 'Cause you need lots of math for machine learning, you need a data set. You need a way to train a model, and you need a way to test the model. Now, the last two things are where people tend to trip up a little bit. Well, math, maybe math too, but the last two things trip you up a little bit. But these are taken care of for us with Create ML in a very easy fashion. And the interesting thing is, if you don't like math, Create ML takes care of the math for you too. So you don't need all the stuff to get started. You mainly need that data set. So this is probably the most important part of the entire thing because if you've ever heard the idiom garbage in, garbage out, it's especially what machine learning models do. If you give them garbage, they just give you garbage back. So we take raw audio files.

0:09:00.8 YM: And in this case, we wanna cut them up into one second segments because the way Create ML works, it works on segments that are at least 0.975 seconds. And if you have exactly that, you might be a little bit off. So it's better to take one second segments and have it analyze and train on those and analyze them later. But that seems like a lot of work, cutting them into one second segments. Luckily we can use open source tools. I'm not going to explain all this, but it'll be on the slides later and you can read through it later. That command allows you to create all these thousands of one second segment files from our main audio file. We need to sort them into categories. For example, we want at least two categories, we want it clean. This is an example of clean audio.

0:09:42.1 Charles: Oh, they, all the little...

0:09:44.9 YM: That was Charles. He did not say umm once, so therefore it was clean. And here's an example of umm.

0:09:52.4 Charles: Umm.

0:09:53.9 YM: Did you hear it? I heard it. Okay. So now we have our two categories that we wanted to... Sorry. We have our two categories that we want to split up our files into. But we quickly notice something when we start going that there are other examples of things that we don't know what to do with. For instance, there's silence. If there's a podcast with two hosts, half the time there's gonna be silence because the podcast hosts don't talk over one another. And what you'll see is pause like, here's an example of silence. Did you hear it? Great. Okay. Addition to silence, there's uhs, which is not quite an, umm, there are unknowns and unknowns are a little bit like the audio are cut in a weird way. So if there's an umm, at the beginning of a file, was that a true, umm, or was that the end of a word that ends in, umm, like some, fulcrum or if you're British mum, if it ends in an uh, that could be the beginning of a word, like unknown umbrella. Understand in this case, it didn't play, in this case the video, or sorry, the audio, it was Joe laughing, but kind of sounded like an uh and if I can't tell what it's going to be, a machine learning model's gonna have trouble too. So we're just gonna categorize those as an unknown and not use them at all.

0:11:17.9 YM: All right. This seems tedious, right? Well, I had a lot of time on the plane. Think about this. A podcaster records for about an hour. In that case, there'll be 3,600 files per podcaster. If there are two hosts, there are 7,200 files for a single one hour recording. That's a lot to go through. I did a lot of this on the plane and I used the touch bar. Everyone's favorite Apple device. When you're in preview mode in the touch bar, it'll display the audio wave form as you're going through quickly and you can easily see when there's silence and when there's not silence. So I could get rid of half of those audio files very, very quickly. I miss you touch bar.

[laughter]

0:12:00.1 YM: All right, so we've sorted them into categories. We have these five categories now, unknown, umm, uh, silence, and clean. We need to leave some for testing, which is not hard because we've gathered a lot of data. And now we're ready to train our model. We're gonna open up Create ML for the first time after we've sorted out all the data sets. We're gonna create a sound classification project. We're gonna set the project info. You can use your name, you don't have to use mine. We're going to add the data set with this big plus button is they make it pretty visible for you.

0:12:32.4 YM: How does the data set look like though, or the training data look like? Well, we've categorized it into these categories and we have to just keep them in this kind of structure. We have our training data, and then we have the various categories with each example underneath those training categories. And that's how it determines which file belongs to which training category. Initially we only had two categories. We had the clean and the umm, and then we found out that we had an uh category too, which from our listening, we adapted. However, some simple experiments taught me that uh and umm, a separate categories was not a good idea because uh is actually the beginning of umm, so that would trip up the machine learning model. Additionally, we don't have very many examples of "Uhs" and "Umms" to begin with.

0:13:17.1 YM: So when we split them up into separate categories, we have even less for the machine learning model to learn from. So it's better to actually combine them together into a single "Uh" class, but we're still gonna call it an Umm detector, 'cause it's a better name. Alright, so we've added... We're gonna add the data set. It tells you how many classes we have and how many items we have in all. Over here it talks about validation data and it says it's auto split from the training data. Validation data is the data that you hold aside, during training, you don't look at it, and then after a training run like an epoch or several iterations, you test the model on the validation data to find out how it's doing. This way, it knows if it's actually learning something or if it's having problems. It's very important. We hit that green train button and it's off to the races, it first extracts the features from the audio files, and then it actually starts training. And here, after our first attempt, we get 100% training accuracy, which is a little bit fishy because you never get 100% in Machine Learning ever, but it's okay, we're gonna ignore that for now. And the validation accuracy is 91.1% which seems pretty good, right? Okay.

0:14:23.7 YM: Subjective testing, we took a piece of the audio and we listened to it. At the beginning, it says, "There's an "Uh" with 84% confidence." That was a lie, it was wrong. Later on, it does get a couple of "Umms" correct and a couple more incorrect, so subjective testing says, "It's okay." Objective testing, we can take a look and have our test set, which it's never seen before, made up of cleans and "Uhs", and we run it through our test data process. It's the same thing as the training data, we just add it separately, and then we run and we get... Instead of accuracy, we get this confusion matrix optimally named 'cause it's confusing. Instead of giving you accuracy it gives you precision and recall for each category. Well, you can... I promised you no math, but here's some math. And if you take that confusion matrix you plug it into this formula, you can calculate the accuracy. However, I've done this for you, you don't have to pull out your calculators. It's okay.

0:15:21.5 YM: When we do it on our data just now, we get 89% testing, which is pretty good. So it works. Alright, sort of. We have three problems. We have a voice diversity problem. If you look at [chuckle] this audio thing, it works well for audio recorded by Charles and Joe. Charles and Joe look like this. It works well for me too. I look like this. You might notice some similarities between Charles, Joe, and myself. We are all adult white males with deeper voices, which is a problem. If you're listening to podcasts only with white males, hosts, maybe you need to expand your horizons for a little bit. The problem is, it did not work for my wife and it did not work for my children. They could not get it to detect anything. Okay. Additionally, we have an unbalanced data set problem. We have one "Uh" or "Umm" for every 13 clean audio files. Take a look at this chart right here. If we look at how many clean examples we have, and we look at the total and we divide it, we get 92.5%. We got 89% testing accuracy. Theoretically, the model would have done better if it just guessed clean for everything and didn't even guess "Uh" at all. That's not good. It did learn something, but it didn't do a good job. Okay, the third problem we have is labeling data is a manual and time-intensive problem, and in order to solve the first two problems, we have to tackle this one head-on.

0:17:00.0 YM: So let's continue on with attempt number three. And we're gonna talk about augmented data. So, this is just synthetic... We're gonna synthetically change our data to make the model more robust and hopefully make it work for my wife and children. We're going to randomly change pitch of some samples, we're going to randomly add white noise, we're going to ideally do this on the fly, but we can't because of Create ML so pre-baking is okay in a pinch. Alright, so how do you do this? Well, you can use Apple's audio frameworks, if you desire, or you could just use this open source tool, SoX, which is a sound exchange. It has many sound manipulation features and you can install via Homebrew. It seems kind of easy. So here's an example of how to change the pitch by 400% and decrease the loudness by 10 decibels. Here's an example of how to add white noise. Again, this will be online, you don't have to figure out how to do it now. And if you wanna use this in a Swift program, you can use this function, which I found on Stack Overflow, which we know works perfectly every single time to run external commands and I actually tested it so it actually does work. Alright, so here's an example of changing the pitch.

0:18:15.2 YM: Okay, it didn't play, but I'm just going to tell you it was Charles, he sounded like a chipmunk. Let's say, "Hi, I'm Charles, blah blah blah." Okay. Here's an example of Joe talking very low and louder, so it was clipping, "Hi, I'm Joe". Alright, that's essentially what you had. Okay. So with our augmented data, we've added a bunch more data in addition to augmenting the data. We didn't augment the clean data 'cause we have more of it than we need. We augmented only the "Umms", and so now we have a one to three ratio, so one "Uh" or "Umm" for every three clean data. We add the new augmented data set to our Create ML project. We also change the model in this respect, and we change it from Apple's audio feature print to VGGish.

0:19:00.0 YM: The reason we do this is it works, oops... The reason we do this is it works better for problems with a certain amount of data. What I found is the accuracy of Apple's audio feature print went down significantly when I added this much data, but the VGG started to increase in performance. The Apple audio feature print Core ML model is five kilobytes, whereas VGGish is 4.6 megabytes. The reason is, is there is actually more to the model for Apple's feature print, Apple's audio feature print, but it's baked into the OS, so it doesn't have to ship all that. It just has to ship the classifier at the end, which is why it's much smaller. However, 4.6 megabytes is not too bad, so we can continue. Okay, when we train, we get again, 100% accuracy, very suspicious, but our validation accuracy has gone up to 95.7%, so it's definitely improved with our augmented data.

0:19:49.1 YM: We... That was supposed to be after that, sorry. This is all out of order. Okay, here we go. So subjectively now what we see is that uh, that phantom uh, in the beginning has now correctly classified as clean. It got more uhs and umms correct this time and there's still one that wasn't right. So it's gotten much, much better overall. If we look at our objective testing, we run it through our test set again, we plug this confusion matrix into my formula earlier and we get 96% accuracy, which is significantly better than before. All right, so what does this do for us? It improves the accuracy and robustness of Charles and Joe recorded audio and my audio, it improves the accuracy for women and children. This actually started working for my wife and children, which is great. But let's keep going. How can we make this better? We need more data, or if you're a Star Trek fan, this is a really bad joke. All right, where do we get more data? Well, you could record your own audio, but that's just one more person, so you're not gonna really help with voice diversity. You can find more podcasters, but again, that's not super easy. There are only a few of you who raised your hand, even though I think some of you are lying.

0:21:00.6 YM: Maybe open source data sets. So doing a quick search, I found LibriSpeech, which is 1000 hours of English speech, but it's based on public domain audio books. And most people, when they're reading audio books, they're not inserting uhs or umms, they're reading what's in front of them, so that's probably not a good idea. There's the HarperValleyBank, which is a simulated contact center calls to a bank. Unfortunately, calls are 8 kHz on telephone, so it's really bad quality and probably not gonna help us very much. Then there's The People's Speech. I heard about The People's Speech on a podcast. You might notice a theme. It's licensed for academic and commercial use, so we can actually monetize our product finally, once we figured out the market. It has 30,000 hours of transcribed audio with diverse speakers, very important. Two terabytes of data. That is a lot of data, that is actually too much data.

[laughter]

0:21:55.9 YM: So what can we do with this data? We have too much data. We can use what's called active learning to decide what we want to use from this data. And what we wanna do is we wanna run the model on a subset of the data. We want to determine which uhs and umms the model is having and clean audio the model is not super confident about. So if we return something with 50% or 60%, we want it to identify those samples and then train it on those. And optionally, rinse and repeat, you can do this many times in order to improve your model. All right, so I created a Swift CLI to run inferences on the audio. I sort the files into confidence levels, like I said, in buckets of 10%. So we have clean 50, clean 60, uhs 50, uhs 60. We start with the least confident files, we listen to them, add them to our data set. I generate about two and a half hours of data with this, but I only used about 13 minutes because it got tiresome and I got... And it was working okay, so I figured, "Good enough."

0:22:55.0 YM: All right, after we've added our active learning data sets, we now have more data. We have another 800 samples or so, and we can start training again. So we're gonna add our active learning data set to the Create ML project. We're going to retrain. Our validation accuracy has gone down a little bit, and that's okay though. We're going to objectively test again 'cause it's very important to always test your model. And this time we get 94%. Why did the testing go down? Well, our test set is comprised of Charles and Joe Audio, not everybody in the world audio, so we've hurt the chances of it detecting umms on Charles and Joe, but we've increased the general effectiveness of the model overall.

0:23:37.6 YM: But wait a minute, I said this title is How Not To Create an Umm-Detector, not How to Successfully Create One and Monetize It. Well, are we really using the right tool for the job? At the very beginning we talked about how uhs and umms are kind of like speech, but they're not. Ideally what you'd have is a speech recognizer that doesn't filter out these uhs and umms and detects them for you as opposed to doing it the way we do it, because this method has some problems. Let's take a look at some problems. If you pronounce the as tha, which a lot of Americans do, I don't know about other people, but like, "Give me 'tha' banana," there's a chance that it's gonna detect that as an umm. A as 'uh' similarly give, "I want to drive uh car." It's the same problem. And then as we talked about before, words that begin in un or um, that's gonna make all this a little bit trickier. Different accents may also be troublesome, so it might not work as well for British English or Indian English or people that speak English with other accents than Charles, Joe, and myself, and people that I got the data set from on The People's Speech, but it worked well enough.

0:24:49.5 YM: So, whew, we've talked about a lot... Oh, before we talk about the summary, why is this going really, really crazy? Well, I trained the model on data recorded into a microphone in a quiet setting, no reverb, no echo, and on The People's Speech, which is in a room a little bit different from this one. Here we have my echo flying around the room, I'm breathing heavily into the microphone, it's getting super-confused. It's hearing a lot of things it hasn't seen before, and so it's saying, "Probably an umm, I guess," which is why you don't do live demos, but it's a good example as to why it might not work in a real situation. You want to collect data in the same way that you're going to be using it later on. All right, so we've talked about speech recognition, we've talked about collecting data, we've talked about training models in Create ML, we've talked about metrics for analyzing our models, very important, augmenting data to improve our models, active learning, and told a lot of bad jokes, and I apologize for none of them.

[laughter]

0:25:53.1 YM: All right, so what's left to do? Get more data I guess!

All right, currently, this is the repo where I'm going to put a lot of this stuff. Right now there's only a link to the slides for the presentation. I've been working with DagsHub for a few months. They're like the GitHub for data scientists focused on machine learning. So in addition to versioning code, they also have version data, which is very useful for reproducing experiments and stuff like that. Oh, one more thing. Yeah, in my umm counter, I created a micromanager singleton, I know you all love singletons. They're awesome. But I created a microphone manager singleton, and when you instantiate a microphone manager singleton, you get to name it a micromanager. All right, Peter.

Merci.

[applause]

0:26:43.8 Greg: Thank you Yono, I love those interactive presentation.

0:26:53.6 YM: Oh man. 294, beat my high score.

0:26:56.4 Greg: Yeah, I was wondering if you will reach the 300 category.

0:27:00.6 YM: Sadly no. Next time, next time.

0:27:05.4 Greg: It's too late.

0:27:08.3 Simone: Yeah. Very technical question... On a scale from zero to greatestFiniteMagnitude, how, much are you annoyed by Umms after this project?

0:27:18.4 YM: So annoyed. I hate them so much, so. No, it's fine. It's something that's... I actually, I heard a study where they said that people who say, "Uh" and "Umm" a lot tend to be a little bit smarter because they were using that as a way to collect their thoughts. They weren't just saying the first thing that comes to their mind. So they were actually filtering the stuff that comes out afterwards and they needed that placeholder while they were doing it. So I like to believe that that's the case. So if any of you say "uhs" or "umms" a lot, just think about you're smarter than the average person. [chuckle]

0:27:50.3 Greg: Lots of people should say "Hmm" more often maybe.

0:27:53.3 YM: Yeah. I don't know what you're 'uh' talking about.

0:27:57.8 Greg: What was your level, technical level, uh, in machine learning before working on this project?

0:28:03.1 YM: I have a decent amount of experience, but as I said before, in computer vision, so I have zero experience with computer audio or audio beforehand. It was nice to play around with something new and just be able to get something to work fairly quickly and easily. The interesting thing though is after I looked into it a little bit of how it might work in the background, it's actually probably using some computer vision in the background that I don't even know about, that VGGish model that I talked about is actually a computer vision model, and so it's more than likely converting the waveform into a spectrogram and then analyzing the data that way, which is why it needs fixed sizes too.

0:28:44.2 Simone: Umm... [chuckle]

0:28:47.7 Greg: This one wasn't really...

0:28:47.8 YM: I'm so sorry. It's a disclaimer. I said no money back. Right?

0:28:53.5 Simone: Unbelievable. I won't ask questions anymore. How long was training this model with the tools you had?

0:29:01.9 YM: Oh, that's a great question. So, training models actually fairly quickly. What happens is, if you remember in the beginning there was that extracting feature section, right? What that was doing, it was taking all of the audio files and converting them to vectors of numbers. And then it was only doing the machine learning training on those vector of numbers. So it didn't need to re-extract all those features each time. And that's actually one of the longer parts of the training process. So it could extract the features ahead of time and then run 25 iterations really, really quickly, of training without any problem. Like if I clicked go on... This is, M1 MacBook Pro Max or so, it finished training in like 17 seconds or so.

0:29:41.1 Simone: Okay, awesome. And then you said that the size of the final model, if you want to to use that in Apple for instance?

0:29:50.1 YM: Yeah. So that was, if you use Apple's audio fingerprint, which is only available since macOS 12, I believe, that one is 5 kilobytes. So it's very, very small. It's only the classification. It's like the... If you think about a machine learning model as a bunch of layers, it's only the last couple of layers and that's why it's only 5 kilobytes. If you use the VGGish... Oh. So, and the reason is because the rest of that model is already shipping with iOS. If you look at the VGGish, it's 4.6 megabytes or so, and that's because it has to include the entire model because they're not going to include that with everyone's iPhone that may or may not use it. And Apple uses theirs for other reasons too.

0:30:26.9 Greg: What do you think of Create ML compared to TensorFlow?

0:30:31.5 YM: Okay. That's a good question. So, I like it for jumping in to something very quickly. For me, it's very good for getting an MVP or a proof of concept. For instance, if I had to go through TensorFlow with this whole thing, it would've taken me a lot longer to get started. But Create ML allowed me to try something very quickly and get a result that proved to me that it could work, even though it's not something that normal people do. So I mentioned that I have training in computer vision. It's not training officially at university or anything like that. It's more, I taught myself, read up a lot of stuff. And so I don't have the hangups that... Okay, hangups is a bad idea. Let me... That sounds negative. I don't have the training that official machine learning scientists or data scientists have that say, "Don't do this way, this is stupid." I usually just get an idea. I'm like, "Let me try this, lets find out if it's cool or not," and sometimes that's an advantage, sometimes it's not. So, but I get to learn that way, which is great.

0:31:30.0 YM: Create ML allows me to learn much more quickly because I can just try some stuff quickly and find out whether or not it works. If I were to continue down this road, I would be interested in trying something with like TensorFlow or Pie Torch to be able to have more control over the entire process. I mentioned during the augmented data section that ideally you would do it on the Fly and you can't do that with Create ML here. TensorFlow or Pie Torch will allow me to do my data augmentation on the Fly. So it's not seeing the same thing every single iteration or every single epoch. That would be helpful. I believe you can also do that with the Create ML Swift APIs. But this was just even easier than getting started with code at all.

0:32:12.1 Simone: Yeah, I see. A question from the audience. How do you debug this?

[chuckle]

0:32:20.5 YM: I think that's a whole other talk. Debugging machine learning models is notoriously difficult because they're essentially black boxes. So the best way that I can say to do it is follow the scientific method. Try changing one thing at a time and see how that affects the output. Make hypotheses, test them in a certain way that makes sense. So for instance, in this case, my hypothesis was because I only trained on deep male voices, that's why it wasn't working for women and children. My way to try to test to see if that was true was augmenting the data to higher pitch or not to see if that would reproduce or produce other results that would help work for my wife and kids. And when I saw that it worked, it wasn't great initially, but it worked a little bit. I saw that it was making progress, so I knew that my hypothesis was likely correct and that's how I continued down that path of then, "Okay. We need more samples from other people, more diverse samples in order to get a much better model for everybody as opposed to just white males."

0:33:21.4 Simone: All right. Thank you very much.

0:33:23.4 Greg: Thank you Yono.

0:33:24.0 YM: Thank you. This was fun.

[applause]
