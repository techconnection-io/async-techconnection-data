---
slug: >-
  /talks/swift-connection/september-2023/danijela-vrzan-string-catalog-better-way-to-localize-your-apps
date: '2023-09-21'
title: 'String Catalog: Better Way to Localize Your Apps'
author: Danijela Vrzan
video: 7XVhDu74v0c
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/7XVhDu74v0c.jpg
slides: ''
tags: []
year: 2023
conference: swift-connection
edition: september-2023
allow_ads: false
---
Hello, everyone.
My name is Danijela Vrzan.
I am a Croatian that currently lives in Canada for about four years now.
I was a civil engineer before I started to completely switch my career, change it altogether, and become a developer.
I work for a company called The Score for about a year now, and I also write articles on my blog, , danielaversan.com, , which you can see right there.
And also, you can find me on Twitter @theversan.
I still call it Twitter.
I don't think I'll ever call it X.
Also, I write articles for Codeco, the previous Ray
Venderle, as you all get used to the name.
I am also a boot camp mentor for this cohort, which is super exciting.
And today I'm going to give you a presentation on string catalog, or how to localize your apps in a better way than we used to until this point right now.
So I wanted to start with a short story or introduction.
So this is an entrance to an exhibition in Toronto called Little Canada, where a bunch of people got together and in 10 years they built small Canadian cities like Toronto, Montreal, Vancouver, like the miniature versions of these cities.
And it's really an awesome exhibition, it's a pretty large one.
And the thing that I wanted to point out is this is like the entrance, the first when you arrive there, and there's a big green screen with like different languages and like saying hello in different languages.
And one thing that I noticed as a Croatian, it's not very common to say hello in Croatian language in Canada or like anywhere outside of Croatia, really.
And I saw this big doberdošli, it's a hello in Croatian.
And it felt, I don't know, it felt kind of good, you know?
Being welcomed in your own language.
It felt nice and warm, so I was very nicely surprised by that.
And so, just like that, you know, saying hello in different languages, so this is like a hello world.
Please don't, this is like, I think this got translated by Google Translate or chat.
If there's something wrong, please don't yell at me.
So you know, when you're localizing your apps, I see some people laughing, that's probably because I wrote hello world, sorry for Canada.
Yes.
So saying hello in different languages when you're building your iOS apps or any apps for the Apple platform, like MacOS apps, watchOS apps, it can make a huge difference for the user, you know?
I remember the feeling when I saw hello in Croatia when I was entering that exhibition
I saw.
So that's how your users would also feel, you know, when they see that there is their native language in the app that they want to use.
Because not everyone in the world speaks English.
In fact, there's a lot of people who don't speak English whose native language is not
English.
And even if they do speak English, a lot of people actually choose to use the app in their native language.
So some fun facts that I found on the website called Ethnologue.
It's a very popular website that has different statistics on different languages in the world, how many spoken languages and things like that.
So there are 7,117 known spoken languages in the world.
Which is a pretty big number.
Although it's like a little side note, like 90% of them are spoken by less than 100,000 people.
When you say it like that, it's not really kind of a big deal.
And there are at least 3,688 with an established writing system.
So even though there are 7,000 languages that are spoken, not all of them can be -- have a writing system.
So you can't localize all of them; right?
So this website also has, like, a top five languages, like, total speakers in the world.
So if you see, top one language is English, and English is used pretty much in most countries,
I would say, as like a business language.
And there's a lot of people, you know, who do business with the states, and so it's kind of good to know to speak English, right?
And there's 1.45 billion people speaking English.
Not necessarily, you know, their native language. one is Mandarin Chinese with 1.12 billion, Hindi, Spanish, and then Arabic on the fifth place. Now, if we take a look at the native speakers, it's a little bit different. So they change places. So Mandarin Chinese is spoken natively by 1.3 billion people. Now,
English is not on the first place anymore. There's more native speakers who speak Mandarin
Chinese. And those people might choose to use your apps in Mandarin Chinese rather than
English. And then on the second place, we have Spanish as well. Still a large number of people. And then third would be English and we have Arabic and Hindi. Just quite interesting.
So, you know, localizing our apps makes them accessible and inclusive to folks, you know, who don't speak English.
And there's a lot of people.
I always remember my mom, because she always asked me, hey, Danila, I want to use this app, can you make it?
I was like, mom, I'm pretty sure that app like that already exists on the store.
It's like, yeah, but it's in English, and I don't know how to speak English.
So she's a perfect example of someone who might use the app, but would rather prefer to use it in, like, Croatian, her native language.
So we're going to start and take a look at how we used to do localization in Xcode 15 and before.
All the Xcode versions below it.
And then we're going to see how we're going to use it now.
So let's take just a quick look.
So this is an app called Posture Pal by Jordi Bruin, he's an awesome indie developer, and he always makes sure to localize his apps in as many languages as he can.
I participated in localizing this one in Croatia, it was quite an interesting experience.
So as you can see, I believe starting iOS 13, people are able to choose a language specific to the app.
So if they are using, I don't know, their phone in English, they might choose to use a specific app in a different language.
So here you can see there are quite a lot of languages.
So in order to localize a string, there are a few options, you know, you can do -- you can do -- write a localized string key.
So this is either SwiftUI or UI kits or even storyboards can be localized as well.
And you can also use NS localized string to have your string localized.
You can add a comment to a string, you know, this is for when you send the strings to your translators so they know the context that the string needs to be localized into, because different languages have different context.
And we're going to see that a little bit later, I'm going to show you what I mean by that.
So when you are localizing an app in Xcode and you search for a string, you get a template, so you can choose a strings file or strings dictionary file, both depending on what you're doing right.
And then this is how the strings file looks like.
It's usually called localizable.strings.
It's just a file that has a lot of strings, depending on the size of your app.
And then you have some comments, and then you can, you know, translate in different languages.
And then the string dictionary file looks like this.
Horrible if you ask me.
It's really horrible.
It looks like a file, but it's trying to figure out what the hell is happening here.
And then when you open the localizable folder, depending on how many languages you have, it looks like this, it's just a bunch of L project files, and you have to look at every file.
Of course in Xcode they're all lined up, but this is a lot of folders, a lot of files.
But now, starting with Xcode 15, it brings us something called string catalog.
And it's really cool.
It's also back deployable to any OS.
So if you are using Xcode 15, it doesn't matter what your iOS, MacOS, you know, version is, it's back deployable.
It's super easy to merge your old -- to create a string catalog from your old localizable strings file.
It's just like a one button, and it automatically moves everything to string catalog.
Of course, there might be some things you have to, like, make sure it's working correctly, but it usually is.
And also, as you can see here, this is the official developer Apple website.
They put a note here saying that in Xcode 15 and later, string catalogs are the recommended way to localize strings, and the earlier version in Xcode, you still use strings and strings.dix file, because, of course, string catalogs are not available, but when you can, you know, use Xcode 15, move over to string catalog.
So we're now -- so as you can see here, this is Xcode 15.
This file and string dictionary files are now marked as legacy, so Apple is pushing you to use string catalogs, so this is how you create a new string catalog, and we're no strangers to catalogs, we already have an asset catalog, a syncing catalog, different catalogs for different things depending on what you need them to, and now we have another one called string catalogs.
And it's just an XC strings file.
I'm going to show you how it looks like in Xcode and how to work with it.
In the background, it's actually a JSON file, which you'll also see a little bit later.
Okay.
So, I'm doing something that people usually -- I'm going to do a live demo.
Ooh, yes.
Thank you.
Thank you.
I need the support.
Thank you, I need the support.
Okay.
All right.
I know it's a little bit small, and I'm going to do my best, I'm going to try to zoom in what I'm pointing, so you should all be able to see everything.
Okay.
So this is a small, quite simple app that I made for this occasion.
It's here.
Let me just -- okay.
It's called Librium, just a random name.
A few strings scattered around.
It's like you can order, you know, books.
You can see how many orders you have in progress, how many books are already delivered.
There's one book on today, I ordered a book today.
You can cancel an order in progress, there's three books, there's five books already delivered.
And you can see it's not localized, because it says one book, three book, five book, which is not correct, right?
And then you can start a new order, choose how many books you can buy with a stepper, cancel buy and tap to learn more.
Just a few strings that I want to show you how to localize.
There's some specific use cases here.
Okay.
It's quite a simple app, so I'm just going to show you some code a little bit.
So you can see...
Okay.
Command.
Let's zoom in.
A little bit more.
Okay.
All right.
It's just one big file with a lot of things, so I wasn't really, you know, trying to make this much worse or anything.
Okay.
So, all right.
So you can notice that, you know, I have text components in UI, just, you know, regular text strings.
I do not -- I did not move my strings in a specific, like, constant file, which is what you would usually do, but, you know, it's all just in there in code.
If you notice right here, there is a text that says, with a property that says verbatim.
What this means is, so since this is a name of the app, I do not want to have that localised.
So on any language I want to say Librium.
So that is how you can make sure that this does not get localized by putting it over the bottom.
And then you see there's a text and then I have a comment.
And this is, as I said, to help your translators know what exactly are they translating.
And I've been on that side, so I can tell from the personal experience what it means to get a bunch of strings when you have absolutely no context on what exactly are you trying to localize.
And it's easier a little bit in English, but it's actually quite hard to know that in Croatian.
And Croatian is a very hard language.
We're different.
I'm going to show you how pluralization works in Croatian.
It's quite an adventure.
Yeah, you see text, orders, there's some comments.
I just hardcoded these values.
Forgive me.
I have some, like, card view. button, you see button, and there's just regular string in there.
And then I have a few other files, you see here I have some string concatenation, just in the regular text.
So that's pretty much it.
That's my code.
So now we're going to add a string catalog.
And string, okay.
String catalog.
Go next.
Let's hope this works.
Okay.
And it's right there, if you can see.
I'm going to zoom a little bit.
This is a cool feature that I learned today.
It says, you know, see, localizable right there.
And this is your localizable file that's going to hold all languages and all your strings.
So because I created it and it's something new, you can see right there it says empty string catalog.
So how it works is when I build the app, it's going to get populated.
Magic.
It's really cool.
No more manually writing your strings, making sure they are there.
And as you saw my code, right, there's just regular strings.
I have a string in a button, just title, and it picks up all those strings because they are all localized, localizable, right?
Is this going to work?
Yeah.
You see right there in the initializer, they are all localized string keys, so they're all automatically localizable.
So this is how it looks like.
I'm going to zoom in a little bit.
So this is English, which is the default language.
You can set different default languages, but that's usually the one.
And these are all of my strings, as you can see.
This is that� this is the number right there.
Book by� you see I have two� two cancel strings that I declared as localizable strings in the code.
It's the same word in English, but it can mean different words in languages like Croatian.
It's not the same word.
That makes it a little bit complex to, like, localize when you don't have a comment saying,
OK, what exactly is this?
So this is an order in progress, and this is order new.
So that makes it much easier.
As you can see here, we have the status on that home page.
And it has two arguments.
So you can also localize that.
I'm going to show you exactly how to do that.
So if you want to add more languages, you can click here on this plus button.
And you're going to see there are a lot of languages. there's even more.
A lot.
I mean, you don't have to localize in all of them.
And some languages have different versions.
It's a lot.
So most common languages probably to localize an app would be first English, of course, and then probably
Spanish, French, Italian.
Maybe like even you saw like Mandarin, Chinese, Hindu,
Arabic, which are more prominent, which are more used by other folks.
So I'm going to add a Croatian here, because I'm sorry, I don't know French, so I'm going to use a Croatian here, and you're just going to have to trust me, it's correct.
So when I add a new language, and you can see right here, it's just being added in the list in Xcode here, and it says 0%, because I have not localized anything.
So you can see here what is the percentage of localized strings.
And also right here on the right side, as you can see, there is something called state, and there are a few different states, so because I just added this Croatian localizable file, it says new.
And it's new, because I haven't done anything yet.
There are also other that we're going to see there.
If you change a string in your code, it will say stale, or if you change it here, it's going to say needs review.
So it's going to let you know what's going on so you know.
And this is for a developer, you know, during development.
This is not something for, like, translators, because it's something in Xcode.
Okay.
All right.
So what I have right here is the number of books, right?
So I'm going to just try to visualize this a little bit in the keynote to show you.
OK, so in English language, it's one book.
So when you're localizing and making sure the pluralization is correct, it's one book.
And then for everything else, it's books. you append the S at the end.
You know, three books, four books, many books, right?
Hello, Croatia is, well, a little bit different.
So this is a book in Croatian.
So you have one book, and then two, three, and four.
It ends with an E. And then five, six, seven ends with an A again.
But 11 to 19, it's all A. And then when you come to 20, it goes back to being A and E.
Yeah.
I wonder how I learned.
It's very different.
And I'm sure there are other languages, you know, who do the same thing.
Okay.
So that is something that I wanted to, you know, show you, visualize to you.
And string catalog actually made sure that is implemented.
Apple engineers worked on it, right?
So when I click here, very big plural, it's actually going to show me in Croatian localization for a single book, for a few books, which is two, three and four, and then for other, which is the other.
So all three possible localizations.
So you know, if I click here, so it's like this.
And then back to this.
Try to code that in.
Okay.
So that's it.
So very bi-plural.
And the same thing here, you know?
So it's this variable, it's going to show one view and other.
And it's going to show you that for different, you know, every language is a little bit different, so it's covered for all of the languages.
And I'm glad I speak Croatian, because I can show you this.
It's really cool.
Okay.
Then we have a buy, which is just regular.
And then we come to this specific use case, which is a cancel button.
Now, a cancel button is, so we saw in the app, so there's order in progress, so we can cancel an order in progress, and there's a new order which you can cancel as well, cancel that screen.
In English it's cancel, cancel, but in Croatian it's actually not.
It's two different words that mean the same thing, but not really.
It's a little bit hard to explain, but it really depends on the context. it's two different words, so that's why you can't have, like, one word, you know, cancel, but that's something, you know, if you give your strings to translators who speak that language, they will tell you that probably.
If you give them enough context, you know, what is going on.
If you're giving just a string, you know, and they're going to tell, hey, I can't use this, I need this, and you'll have to adjust your code like that.
And then you can see right here there is a comment that I wrote, you know, this is a button for cancel order in progress on the home view and this is a cancel button for current order before placing it.
So it helps the translators.
Now you can see here, right, the state change, so when I change the -- when I added the plural, it marked them all as green, because I changed and that's okay.
But here, because I added pluralization, but I haven't changed anything, it says needs review.
So what you can do is just click here on this one and mark as reviewed.
And it's going to get that green check mark.
And you can do that for all of them.
Okay.
All right.
Now another thing that I wanted to show you as well is this one.
So we have two numbers in here.
Croatian languages, yeah, fun.
What we have to do here, so you can vary by plural on the first argument or on the second or on both, which is quite cool.
And in this case, the translation for Croatian for the first part, "Status in Progress" is the same for doesn't matter how many books, is there one or 20 books.
But it's different for the second argument where the book is delivered.
There's three different versions of the word.
And then you can just, you know, take the second argument and just change it here.
What you want to do is just delete everything after the second argument and just add here, you know, whatever the translation is.
Okay.
And one other thing to show is this step to learn more.
Now on iOS devices or maybe on watchOS as well, you tap to learn more; right?
But on MacBook, you don't tap your screen, no matter how many times you try.
It's a click to learn more; right?
So Apple engineers also took that into consideration.
And so there's something called vary by device.
As you can see, there's iPhone, iPod, iPad, Apple Watch, Apple TV.
There's also Mac, so I'm going to click Mac.
And so if I'm developing this app on both, like, iPhone, iOS and MacOS, I can actually
And make sure that this says click to learn more.
It's pretty cool.
And then as you see as I'm typing here, these states are changing.
And then one final thing.
I'm going to just show you� so I'm going to change this string in the code.
And just completely change the string.
And there's no such thing as too many books, right?
And build again.
So every time you build, it makes sure to update everything.
So if there's anything that needs review or something that's, like, stale or different things, you know, it's going to tell you that.
So there are a few bugs in this, in StringCatalog, of course, and Xcode is fairly new, it just got out last week, right?
So this was supposed to be marked as stale, but it's not.
Yeah, okay.
You just have to trust me.
It says stale, right?
And that's pretty much it, you know.
And then when you want to give this to your translators, it's just a strings file, just a JSON, right?
And you can see right here.
That's how it works.
Okay.
So that's pretty much it.
And so if you want to learn more, of course, the best first step would be to watch the
Discover String Catalogs, the WWDC23 video.
It's really awesome.
And they explain everything, even the migration from the old way to the new one.
I really suggest watching it.
And yeah.
[APPLAUSE]
>> Thank you very much. So we can move to the Q&A.
All right. Many questions.
So, actually, I think the most interesting one is, how the hell do you zoom in your screen?
>> Actually, I learned that today.
It's an accessibility feature in Mac OS.
There's a zoom option.
And then there are different ways to zoom, but the default one is holding a control and just swiping on the touch pad.
It's really cool.
I'll be using that more now.
It's been in since 10.0.
Yeah, I learned it today.
You learn something new every day.
[LAUGHTER]
When using localizations, there's many hubs who use third-party frameworks to download the localization.
For example, there's Localize or Phrase.
Do you know if we can already use and support directly the format of file here?
I haven't tried it, so I'm not sure.
I know, for example, at work, we use Sorcery to generate all of the files.
I haven't tried it, so I'm not sure honestly if it will work.
But as long as you have localize of the strings files or any types of dot strings files, which I think most of-- even if you use third party frameworks, you should have that.
I think the migration should be easy.
Can you use this also for--
I mean, different languages for different build configuration, for instance-- sorry, different translations different build configurations.
>> I think you can.
Just in the next quarter's settings, you can make sure that's all working.
Yeah, it can be.
>> Considering you've been to the other side of translation and doing the localization for the developer, do you have some best practice to give us?
For example, I don't know, if the app is really large and we want to have some modules or I don't know, to better make it... to make it really easier for translator to work with it.
Good question.
I mean, there's like... I would say there's like easy way really, because what translator gets is just a bunch of strings. probably something that a developer can do better is make sure that every string has a comment.
Even simple strings, you saw like a cancel button, you know, might be something that you don't really consider something as a cancel button, you know, it's -- you don't really need to describe a cancel button, right?
But in fact you saw that you actually do for some languages, so just make sure every string has a comment in there.
Because that really helps.
And is there like some exception, because I know in my code I've made some pretty standard okay translation, and at some point is there any use of really simple word like okay or cancel, we don't expect them to have different translations, but should we have a different localization for every use or...
It's hard to know that, right, because I speak like Croatian and English, but I don't know anything about other languages.
And I'm sure there are languages that are more complex than Croatian.
So I would say maybe the best idea would be to have all those separate strings and just make sure you add the context to a translator.
It can be the same string, but it doesn't have to be, right?
Okay, so I have another question which is a bit more awkward.
You know what day is it today?
>> Who asked that?
>> Actually, no, I did.
>> Do I have to say?
>> Yeah, if you want.
>> It's my birthday.
[ Applause ]
>> All right.
Yeah.
There was the final.
All right, yeah.
There goes the final.
That's a very cringy moment of the conference.
Oh, wow.
[SINGING HAPPY BIRTHDAY]
Thank you.
I have to vlog it?
[SINGING HAPPY BIRTHDAY]
Thank you.
We are extremely sorry for this.
We know it's stressful, but yeah.
This is a big cake.
You will eat it backstage.
Yeah.
All right.
I'm leaving with the cake, sorry.
All right, thank you very much.
Thank you so much.