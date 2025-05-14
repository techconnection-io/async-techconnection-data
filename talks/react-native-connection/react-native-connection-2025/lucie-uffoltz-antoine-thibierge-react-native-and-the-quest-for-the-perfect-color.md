---
slug: >-
  /talks/react-native-connection/react-native-connection-2025/lucie-uffoltz-antoine-thibierge-react-native-and-the-quest-for-the-perfect-color
date: '2025-04-02'
title: |

  React Native and the Quest for the Perfect Color
author:
  - Lucie Uffoltz
  - Antoine Thibierge
video: QPszEix4pRA
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/QPszEix4pRA.jpg
slides: null
tags: []
year: 2025
conference: react-native-connection
edition: react-native-connection-2025
allow_ads: false
---
[Antoine]  
Thank you. So, let's talk about color. You all know this screen. This is the wallpaper of macOS Sequoia. And why does Apple choose to display this wallpaper? Well, as you can see, there's a lot of red in this picture. Apple has a technology that can allow it to display more green colors than on other computers. So if you are in a store and you see a Mac computer and another computer, you will see better color on the Mac computer. So you will buy the Mac computer just because they have a better color technology.

[Lucie]  
There is a second fun fact about colors. Just as Britta said earlier today, there will be a new law in Europe called the accessibility act. This law will basically enforce more accessible features within our apps. One of them concerns colors and contrasts. Here you have an example with two buttons, one blue and one green, and both of them have a label written on it. It's in white, and your eyes can perfectly read what's written on the blue button, but not what's written on the green button. That can be explained through contrast, because the blue button has a darker shade, and you have a high contrast with the white level, but the green button is light. Wouldn't it be great to know directly through our code whether our colors are accessible or not, and not just rely on our subjective eyes? I'm Lucie and this is Antoine. We have two other people who have been sort of introduced earlier, Tico and another Antoine. We work at Theodore Apps on the quest of the perfect color for the past year and today we want to show you the result of our research.

[Antoine]  
So to talk about this, we use this framework. So we are going to introduce you to the problems with the color, then our ID to fix all those problems, how do we validate this ID, and then how do we implement it. So, first, let's take a closer look at our problems. And the first problem is that React Native is behind in terms of color technology. This graph is a representation of all the color that our eye is able to see. But it would be too costly to display all those colors on a monitor. So, the standard was to display only a small fraction of this color. And that was the sRGB standard. And this is the standard on pretty much most of the devices that you have around us today. And that's the standard that we have access to in React Native. In React Native, we don't have access to any other color outside of the spectrum. But there's a new standard, the PS3 standard. And on all the iPhones since the iPhone 7, the screen is able to display PS3 colors. But we can't display those colors in React Native. There are more and more API that can give you access to these colors. For example, in Tailwind, in modern browsers like Google Chrome and Safari. And even in our chain enemy, yeah, in Flutter, they have access to color in PS3, and we don't have access to color in PS3. So we should do something. In the future, we will have another standard, the red 2020, with even more color. And there's Safari and Google Chrome on it. You can have APIs to access the color. But you will probably not find any screen that can display this color.

[Lucie]  
If we go back to our accessible problem, actually the color APIs we have in React Native contain the bug. Here we have our blue and it can be expressed through different APIs, RGB, X and HSL. If you take a closer look at what RGB is, you can see that we have three numbers and each one of them represent a proportion of color. Now, we compare it with our green button, and we have no way through this API to know which one has a lighter shade and if it's accessible or not. Then we have X. X is basically the same thing. You still have your proportion of color. It's just written differently in X API. And finally, you have HSL. HSL is a bit different, though. The first number corresponds to the hue, and in the common speech, it would be the colour. So is it blue, is it green, is it violet, and so on. The second number corresponds to the saturation. So that means whether our colour is pure or whether it leans towards grey. And the final number is actually what interests us. It's the luminance, so the lightness of the colour. Is it possible to know with HSL if our buttons are accessible or not? Not at all. As you can see, we have the exact same number for the lightness for both colors, even though we can see that the green button is lighter than the blue.

[Antoine]  
So, now, how can we solve those two problems, the API problem and the colour space problem? Well, for us, the reply was to use OKLAB. OKLAB is a colour space invented by Bjorn Ottosson, and it is described as a perceptual colour space for image processing. What does a perceptual color space mean? A color space that is representing what our eye is able to see. Contrary to RGB which represents the proportion of color and how color will be displayed. And for image processing, it means that this color space is great to make computation on color. So for example, lightening or darkening a color. Finally, OKLAB is also an API, so we can express color using OKLAB. This is the example for the green color. We can express it using also OKLAB. So how does OKLAB help us to solve our P3 integration problem? Well, first, to understand that, let's take a look at this beautiful cube. This cube is a representation of all the colors that are present in sRGB. So as you can see, there's a red, a green, and a blue. And so that's our three dimensions that allow us to represent all of the colors. On a P3 device, you will have access to more colors. You will have access to more colors. So as you can see, there's still a red, there's still a green, and there's still a blue. So with a simple transformation, we can still get a cube and still use RGB to express color, but that won't be the same problem because the coordinates won't be the same. As you can see here, the red is straight in RGB, it's not as red as the red is straight in P3. So, what would it look like if we implement this? So, a developer will write a PS3 color on a PS3 device. So on this device, no problem. For the developer, you will just need to write the color like this with display PS3 and the color using RGB. But then, what would happen on non-pc device? Because there's still a lot of non-pc device. So we need to make sure that we can still display a color. So to understand what color we'll be displaying, let's go back to our graph. So, for this color, for example, that is both in sRGB and p3, that's pretty simple. The developer will write the color in p3 and will just make some computation to find the color equivalent in sRGB. So as you can see, the numbers are a bit different. And that is the case for about 50% of the color. For 50% of the P3 colors, they are also in sRGB. But what about the other 50%? For the other 50%, that's the tricky part. For this color, for example, we cannot find the direct color in sRGB. So we will need to use a gamut mapping algorithm, which is an algorithm that takes a color from P3 and is finding the best color available in sRGB. So, what will happen? A developer writes display B3. Then, we will compute the color into OK lab. Because OK lab is a great color space to make computation on color. So, we will with the gamut mapping, we try to find the best color available will work best with OKLAB. And then we will use this algorithm and we will find the best color available. So as you can see, the colors are a bit different because in sRGB, you can't have access to the display P3 color.

[Lucie]  
The second question we need to ask is whether OKLabs solve our accessibility problem. And the short answer is yes. Here you have both colors written in OKLC. Each API is basically OKLab but in color coordinates and you have the lightness included. And as you can see, you don't have the same number for the lightness. For the dark blue, you have a number that is below 50, while for the light green, you have a number that is over 50. Which means that the label written on it should have the contrary. White has a lightness over 50, so we can read it on the blue button, but not on the green button. Now, what's the difference with HSL, you may ask? Here, you have the difference. It's a graph with X axis you have the hue and Y axis you have the lightness. And Ocala represents exactly what happens in your eyes, which means that depending on the hue, we cannot see the same range of lightness. For instance, for green, you would see a larger range of lightness compared to a light blue. However, HSL has decided to put everything in a square and therefore to pull those colours to fit that square. Now we put our colours blue and green on top of that. Again we can see that the blue and green are on the same line for the HSL representation, which is not the case for Eau Claire representation. An example, a consequence of that is the gradients. To compute the gradients, you will need to fix the lightness and to know to predict which hue comes next. And because we have those colors that has been pulled to fit that square, it struggles to find what color comes next accurately. In case you cannot see it correctly on that gradient, maybe you can see it more here with Ockelab gradient next to it. On the Ockelab gradient, we have a result that is smooth, whereas on the HSL gradient, you have some colors that have been grouped together, especially in the red and blue areas. So, all in all, OKLAB allows us to first have P3 colors directly in your apps, but also to solve our accessibility problem.

[Antoine]  
So now, how do we make sure that implementing OKLAB into React Native is the best thing that we can do? Well, the first question that we ask ourselves is where should we implement it? And the reply was, obviously, reanimated. We thought about Reanimated because it has an API called InterpolateColor. And with this API, we need to predict the next color. So OKLAB would be a great fit in it. And so it could allow us to get the feedback from the community if we implement it in Reanimated. So, we wrote on RFC, and we were just about to publish it when we had a call with Ricardo from the React Native core team. Ricardo will talk to us later. And he told us that they have been trying to implement this support to React Native. And they were lacking this gamut mapping algorithm to have the retro compatibility with sRGB. So he was interested in us implementing OKLAB into React Native. So we throw away to the garbage our ILC for reanimated and we prepared a new one for React Native. And for those of you who are impatient, a quick shout out to D4VD who has implemented OKLab into Reanimated, so you will be able to play with that soon.

[Lucie]  
The second question is which algorithm we should use for the gamut mapping. A quick reminder for a colour that is in P3 but not in sRGB, you would need the gamut mapping algorithm to try to find the best available colour in sRGB. Here you have an example of an image in OkaLab, and everything that you see in black are actually colours that exist in P3 but not in sRGB. So you need your gamut mapping algorithm. But depending on the algorithm you choose, you can have really different results, and some of them can even be weird. So the first check we need to do is, does the algorithm produce good colours? Two algorithms to stand out, clamp and CSS4. Here you have the result for both of them on the red. Maybe you don't see a big difference in the audience. We have a second example here with the green. Tremendous difference between those colors, just slight differences. So we need to find what are the pros and cons for each solution. For clamp, it's clamped its values, it's just as its name says. So basically we'll be really performing because everything will be done in one go. However, we've noticed that sometimes it can have the worst possible results, but again, it's just slight differences, so it's still acceptable. On the other end, we have CSS4, and this algorithm is already widely adopted since it is the one used on the web. So, we do know that it's working perfectly fine. The question we need to answer now is, is it performant enough? If it is, we don't need clamp anymore. We can just focus on CSS4 algorithm.

[Antoine]  
So, to know if it's performant, we ran a benchmark on a Samsung J3. A Samsung J3 is the worst device you can have. It's a low-end device from 2017, and just opening Google Chrome, it takes about 10 seconds. So, users are used to have a laggy experience with that. So we ran a benchmark on a code in JavaScript for colors that were in P3 but not in sRGB, that were needing the gamut mapping algorithm. And we found out that to compute the best available color, it took about 800 microseconds for 99% of the color. So we found out this was pretty good results for such a lag device. But then we ask ourselves, should we do it in C++? And we have a talk earlier today, so you are actually wondering, is the C++ really more performant than the JavaScript one? Yeah. Of course. The C++ algorithm is 20 times faster. This benchmark we run it on Mac M2, but we are confident that also on another device it will be more fast. Faster. So, with these results, we have that the CSS4 algorithm produces the best visual results, is performant enough, and is already widely adopted. So that's what we propose to implement in React Native. And that's what we propose to do in this RFC. And you can scan it and have a look at it. If you want to delve deeper into the colors, that's what we propose to implement in React Native.

[Lucie]  
The next step is the implementation. And we have a three step to implement it. The first step is what we have actually begun to do is to convert P3 colors into sRGB. So it's basically using our gamut mapping algorithm. This is an example taken from the web, but you will be able to use P3 colors through your APIs. The second step is to create a JavaScript API for OKLAB, and again, an example taken from the web. We would be able to use OKLAB API directly in your code as a developer and to perform, to compute some algorithm or to modify your colors as you may wish. And the final step is to create a community package and this time is directed towards libraries. So again, the example for reanimated. And the goal here is to create the API for Ocala, but in C++ to make things faster.

[Antoine]  
And so we need to implement that and soon it will be your turn to make better apps with better color. Thank you very much.

[Mo]  
Awesome. Well, really cool work on this. It's great that it's in progress, and I think there's gonna be some really cool results. It's one of those things where it's like, you kind of look at it, and you're like, "Doesn't matter." But then when you actually see it in an app, I think it really makes a difference, and like the visuals just pop so much nicer. So I think it's gonna be very well received, and there's gonna be a lot nicer looking apps, just from the subtleties of it. So great work, great work on this. I'm going to-- I didn't do a fun fact, as you might have realized for them, because I didn't know how to do two fun facts before someone goes on stage. I tried to think of a good way, and it just didn't come up. So I'm going to-- tell you a little bit about both of them or the fun facts that I forced them to give me last night. So, Lucy, you organize a Korean movie festival.

[Lucie]  
Yeah, each year.

[Mo]  
On the Champs-Élysées.

[Lucie]  
Exactly. And this year is the 20th edition.

[Mo]  
And again, you haven't organized it for 20 years yourself.

[Lucie]  
No, no. I'm not that old. It's been four years for me and I quite enjoy it.

[Mo]  
Nice. Who, other than the French people in the room, okay, how many non-French people are there in the room?

[Lucie]  
Maybe with the club. That was a good idea, I think. Cool.

[Mo]  
So the non-French people in the room, who's not been to the Champs-Élysées? Okay, you should definitely go to the Champs-Élysées. It's like an iconic road. There is a movie theater there. Great movie theater. You should go there, definitely. Especially in October.

[Mo]  
Do you have like a discount code or something you're going to share with people afterwards?

[Lucie]  
No, sorry.

[Mo]  
Okay, fair enough. Cool. So yeah, if you're in Paris in October and you want to see some Korean movie festivals, hit up Lucy. Probably not for a discount code, but yeah.

[Mo]  
Antoine, you said you're dabbling these days in improv comedy?

[Antoine]  
Yeah, so that was actually the first time on stage that I had to say something intelligent.

[Mo]  
Can you say something unintelligent now, just to give us a little taste? Please keep it PG.

[Antoine]  
Yeah, I don't know. That's like the one thing you need to do for improv.

[Mo]  
Come up with it on the spot.

[Lucie]  
During the rehearsals, sometimes you would do improv and improv some jokes, and I was just feeling so scared that you would do the same, but on stage, because I would not know how to react. I don't know how to do improv.

[Antoine]  
So that's how I feel. I feel so sad because all of my jokes, you should just look at it and just shrugged.

[Mo]  
Did he do improv during the talk?

[Lucie]  
No, that was fine.

[Mo]  
Alright, cool. You mentioned, so on your slides you had some negative numbers for colours. What was that all about?

[Lucie]  
Yeah, they were on the slide where at the end we show what is the implementation and you have an example with what happened in the web right now. And here you can see that you have P3 colors and just next to it you have sRGB colors but with negative colors, negative numbers. And in fact, those numbers are negative because they don't exist in sRGB, but only in P3. So that's how we know that we need to apply also our gamut mapping algorithm anyway, because that doesn't exist. And if it doesn't exist, it will just crash maybe.

[Mo]  
Okay. That makes a lot of sense. Okay. Fair enough. Someone's asked if Figma actually supports P3 colors, because they're wondering, like, how would a designer represent a P3 color to you?

[Antoine]  
Yeah, I think they handle it. More and more devices like Adobe, for example, they handle it, of course.

[Lucie]  
I had somebody from Theodore Apps, because we also have a design team, who after our real soldiers just sent me a screenshot, they said, oh, now I understand why it's in Figma. So there is the option, yeah.

[Mo]  
OK, so that makes sense. Just wait for the day your design team comes and asks you for P3. Now you know how you can implement it when it's actually implemented. How do you know in code if a device is P3 compatible or not? Is there a way? I guess maybe not in React Native APIs right now?

[Antoine]  
On iOS, it's simple. If it's above iPhone 7, it's compatible with PHP. On Android, there's a new API. An Android API that tells us that. Of course, for the older version of Android, we can't see that. But then we will just assume it is not. I don't remember exactly the same. But is WideGamut supported or something like that?

[Mo]  
OK, gotcha. Cool. Have you considered colorblind options in this proposal? And will the gamut algorithm function kind of work in a similar way for handling colorblindness.

[Lucie]  
So you mean the different colors between red and green, for instance?

[Mo]  
I guess there's a bunch of different types of colorblindness as well, as far as I'm aware.

[Lucie]  
I don't know if there's a one-shot algorithm for it. It might be a bit out of scope. I don't know the answer to that myself. So I think the goal with OkaLab was to make it, of course, more accessible, but for that kind of precision, I'm not sure if it can say, "Oh, if you have that color of blindness." Yeah, I mean, sometimes it depends really on the color blindness, because we spoke a bit earlier at lunch with some people, and there is some people who want more saturated colors, while others want less saturated colors, and that would be possible with OKLab easily, because it has that, but... Other than that, like the red and green, I don't know if it would be that easy to take into consideration.

[Mo]  
Okay, fair enough. This is an interesting one. Is there an algorithm to do the reverse of the gamut calculation? Can you go from sRGB to... to P3?

[Antoine]  
Yeah, of course, but it would be just very simple because all the colors in sRGB are also in P3. So we just need to do the calculation the other way around. It is a matrix multiplier.

[Antoine]  
Yeah, it is basically a matrix multiplier with a few non-linear functions. Nothing crazy.

[Mo]  
I don't watch Monty Python, so someone's trying to make a joke here. I'll say it and if it means anything to you guys, laugh. If it doesn't, we'll just move on. Okay. Since you told us what your names are and what your quest is, what is your favorite color? Question mark, hashtag Monty Python. Sounds like a very British joke.

[Lucie]  
I have no idea.

[Mo]  
Whoever asked and you put your name as anonymous, just pretend like you didn't make the joke. Cool. Awesome. And on that note of Monty Python jokes, we'll wrap up the Q&A here. You folks are around, so if anyone has any more questions about this, feel free to chat with them at the coffee break or the after party. Big round of applause for Lucy and Antoine. Thank you.