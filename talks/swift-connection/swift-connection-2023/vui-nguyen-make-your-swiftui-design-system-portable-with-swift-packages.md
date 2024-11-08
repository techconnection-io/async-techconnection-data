---
slug: >-
  /talks/swift-connection/swift-connection-2023/vui-nguyen-make-your-swiftui-design-system-portable-with-swift-packages
date: "2023-09-21"
title: Make Your SwiftUI Design System Portable with Swift Packages
author:
  - Vui Nguyen
video: g1BB64RGm5g
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/g1BB64RGm5g.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/7ef905fbd6564801887f6d81dbef2cc4/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---

This is my first time visiting Paris or France, so thank you so much for having me and welcoming me and I want to thank the organizers for putting together this amazing conference and also thank you for all of you for staying until the end, so I hope you will find my talk useful.
All right.
So welcome to my talk.
Today I'll discuss how you can make your Swift UI design system portable with Swift packages.
My name is Vui Nguyen.
So before I dive into my talk and what it's about, let's discuss what problem we're trying to solve.
For example, I have my own freelancing company called Sunfish Empire.
I have a couple of personal apps in the market, but they don't share the same branding or theming, so what if I wanted them to?
And what if I want to make it easy to reuse design elements across the code base of all my apps?
For example, here's a sample project I put together for this talk.
The top line there is Apple's default system font in regular weight and the bottom line shows my custom font in regular weight.
What if I want to display my custom font instead of the default Apple font in my apps?
And here's another example also from my sample project.
The top line displays Apple's version of the color teal, but I don't want my apps to show that.
I want my apps to show my custom version of the color teal like what you see in the bottom line.
So how would I do that?
So what's one possible solution?
Well, oops.
Sorry.
Why did that not work?
Excuse me.
Okay.
So one solution is my talk, and since you're assuming you're interested in hearing my solution, so let's dive in already.
All right.
So what we're going to cover today is I'm going to introduce the problem and give you a short introduction to myself.
I'm going to demo the solution, and I'm going to talk about how I set up my Swift package and project.
Then I'll discuss how to create custom fonts that you can apply to text, and how to create custom colors that you can apply to text, and how do you create custom colors that you can apply to shapes.
And I'll end with some resources that you can follow up.
So what does my talk cover today?
Well, we're going to build a design system.
So this design system is an SDK that contains my project's custom fonts and colors, and we want to be able to apply those custom fonts and colors to multiple iOS apps for consistent branding and theming.
To do that, I created or extended view modifiers to take custom fonts and colors, and I want to match Apple's view modifier syntax whenever possible.
So I came up with this solution while working on a project for a Fortune 50 company.
While working on a sample project for this talk, of course, I had to take out the proprietary stuff.
But this is why matching the Apple view modifier syntax is so important for client-facing libraries.
And this solution is good for Swift UI views.
And other things that we're going to cover is we want to make our design system portable.
And that way we can achieve code reuse or modularity by building the SDK as a Swift package, and we're going to start by building our Swift package and iOS project in tandem just to keep it simple in the beginning.
So these are the things that my talk is not going to cover.
Now I have a lot of respect for designers and accessibility experts, and unfortunately
I'm not an expert in either of those things, so I can't go into either of those topics in great depth, but I will have a few resources at the end that you can use to follow up.
So again, my name is Vuy Nguyen.
I've been a software engineer for over 20 years.
I've been an iOS mobile developer for over ten years, including cross-platform and native iOS.
So please don't throw tomatoes at me for being cross-platform before.
I am a leadership fellow for women in code mobile.
And this talk is a solution to a problem I solved at a previous job.
And I've never seen this solution anywhere else, so I thought I could help other people by sharing it with all of you.
And I'm going to play a fun game with you called two truths and a lie.
I want to motivate you to stay until the end of my talk when I will reveal the answer.
So take a look at the pictures on these slides.
I might give you a clue.
So which one do you think is the lie?
Am I allergic to cats?
Do I sleepwalk?
Or do you think I once swam with sharks?
So here's a little demo of my project.
Now this is a kitchen sink app I built to demo the different ways you can use my design system library.
You can apply custom fonts and colors to text, both foreground color and background color.
You can also apply custom colors to shapes in different ways.
So let's start by going over setting up the Swift package and project workspace.
Since we want to start by creating a local Swift package that you can build in tandem with your iOS project, you do this by creating a directory within your iOS project workspace to hold your local Swift package.
You do that by going to Xcode file, new package.
I named my directory local packages, but you can name it whatever you like.
And you want to place that Swift package into your new directory.
And you want to add your Swift package to the same workspace as your iOS project.
Next you want to add your Swift package to your frameworks.
So you do this by selecting your workspace in the targets list, and then in the general window tap on the plus sign under frameworks.
Then select your Swift package in the frameworks window, and if you do this correctly, your
Swift package should now appear in your list of frameworks.
Next in order to test or run the correct Swift package or iOS project, make sure to create a separate scheme for each.
Now if you set up your project correctly, you will see both your Swift package and your iOS project in the same project workspace.
But the each will live in their own space and they're not going to overlap one another.
So in order to do a quick recap, in order to create your Swift package and project setup, you want to add your new Swift package in the same workspace as your iOS project to start.
Make sure to add your Swift package to frameworks.
Create two schemas, one for your Swift package and one for your iOS project.
And then check your project layout to make sure that your Swift package is inside the same workspace as your iOS project.
Now that we've got our project setup, let's discuss how to create custom fonts that can be applied to text.
As you can recall from the demo, we want to be able to display custom fonts like this.
So let's start with the SDK usage.
Here you want to import your Swift package into the file that you're going to use it.
Here's where I add the code to display the two different text boxes and I create a variable called font size so I can use it throughout the view.
And here is how you use both the regular Apple system font and the custom Sunfish regular font.
Notice how you use the same font modifier syntax to display both.
I'll show you how this is done.
Now we'll go into the SDK implementation.
First we'll start by finding a custom font.
I went to the website , fontmirror.com, and found the Bellota font.
You want to look for a free license.
And you want to look for different weights of fonts, in this case regular, light, and bold.
And just a warning that if you use fonts that don't have a free license, they won't load an Xcode.
Instead, they'll just load the default system font.
And non-free fonts that you paid for might work, but I haven't tried that yet.
So now that you've found your fonts, you want to import them into your Swift package by placing them under your sources slash package name in your Swift package.
And then in your package.swift file, make sure to add your font files there.
And they don't have to be in their own subfolder called fonts, but they must be in resources in order to be found later.
Next we want to load our fonts by registering them with the font manager before we can use them.
So we do this by taking all the font names in the package bundle and registering them with the font manager.
The sunfish font name is an enum that represents the file names of the fonts.
I did this to avoid using string literals in the code.
So notice how the font view modifier to add the custom font looks similar to the font view modifier to use Apple system font.
I'm going to go through each of these steps to implement the custom font view modifier in more detail over the next few slides.
So for the SDK implementation, we want to start by creating a sunfish font enum to represent our custom font.
Sunfish font is an enum with associated values, size for font size, and sunfish font weight to represent the font weight.
This enum is what allows us to type dot sunfish into the font view modifier for the text box.
Notice that when we call sunfish font dot name and the font weight is regular, it returns the regular version of the sunfish font.
Next we extend font by overloading our font dot custom function to take a sunfish font.
And then next we create a view modifier to take in our overloaded font dot custom function.
Finally, we extend view to take in our custom view modifier.
And this last step is what makes it possible to call the custom dot font view modifier.
So to recap, in order to create custom fonts that we can apply to text, we start by finding the fonts we want to use.
We import the fonts into the Swift package.
Make sure to register our fonts before we can use them.
And then we want to implement our custom dot font view modifier.
And just a warning, again, if you see the Apple's system fonts instead of your fonts, go ahead and review the last few slides to see if you missed anything.
So next we'll discuss how to create custom colors that we can apply to text.
As you can recall from the demo, we want to be able to display custom colors on text like you see here.
And once again, you want to start by importing your Swift package into the file that you want to use it in.
And here's a code where I display the two text boxes.
And once again, I create a variable called font size so I could use it throughout this view.
And here's how you display text in both the regular Apple teal color and the custom sunfish teal color.
Notice how you use the same foreground color view modifier to display both.
So I'll show you how to do this in a moment.
For the SDK implementation, these are the steps.
And I will go into each of these steps in more detail in the next few slides.
So first you want to start by finding an image with the colors that you want.
And I chose a drawing of pumpkin seed sunfish to represent the colors of my company's brand.
And pumpkin seed is a type of sunfish.
And we want to add our assets catalog to our Swift package and place it under the resources folder of the Swift package.
Again this is important since we made resources a directory in the Swift package earlier for the Swift package to be able to find our assets.
So next we will add a color in the assets catalog.
It can be any color.
This will change later.
Then you want to tap on the color and tap on the show color panel while on the attributes inspector.
Notice the dropper in the color panel which we will use in the next slide.
So next you will use a dropper in the Xcode color panel and tap on a spot in your image to update the color in your assets file.
You can make the dark version of your color the same as any appearance or different depending on your company's branding for light or dark themes.
So notice how the foreground color view modifier to display the custom color looks similar to the foreground color view modifier to use Apple's color.
In this case we only need to extend the existing Apple modifier taken our custom color.
So I'll go through each of these steps in more detail over the next few slides.
So first we want to create a sunfish color enum to represent our custom colors.
This will represent the colors that we had just created in our assets catalog.
Next we want to extend color to initialize color from sunfish color.
So you use sunfish color enum to point to the custom color in your assets catalog.
Next you'll want to extend shape style to use your custom color initializer.
And color such as a sunfish color is a concrete type of the shape style protocol.
This means you don't use shape style directly.
Instead you extend shape style so you can use one of its concrete types like sunfish color later.
So now existing Apple view modifiers like foreground color that take a shape style can now take a sunfish color.
So now the foreground color view modifier can take a shape style of type sunfish color.
Now let's move on to background color.
Notice how Apple's version of the color pink.
It looks more magenta in my opinion.
So I want to use my version of the color pink which is what you see in the bottom line.
Once again you'll want to import your Swift package into the file that you're going to use it in.
And I set font size so I can reuse it in the text.
Now we've already gone over how to implement the font view modifier.
And once again see how the background view modifier looks the same for both displaying
Apple's pink as well as our custom sunfish pink.
So how do we do this?
Guess what?
The code's already been done.
Expect some excitement.
All right.
So all the steps that we need to take have already been done.
To extend the background view modifier method, we've already created a sunfish color enum to represent our custom color.
We've already extended color to initialize color from sunfish color.
And we've already extended shape style to use a custom color initializer.
So that means existing Apple view modifiers like background that take a shape style can now take a sunfish color.
So this is kind of what I said before, but now view modifiers like background can take our sunfish color.
So to recap, in order to create custom colors that we can apply to text, we first want to start by creating or finding the colors that we want to use.
Make sure to import those colors into our Swift package.
Then extend shape style to include our custom colors.
And then we can easily extend existing Apple view modifiers to take custom colors using the extended shape style.
And this works really well for the foreground color view modifier and the background view modifier.
Next we'll cover how to create custom colors that we can apply to shapes.
So here we want to draw a rectangle and fill it with our custom teal color.
So see how we use Apple fill view modifier syntax, but we are passing in our custom color, not the standard Apple teal color.
And good news, once again, all the steps we need to take have already been done.
So in order to extend the fill view modifier method, we've already created our enum.
We've already extended color to initialize color from sunfish color.
And we've extended shape style to use our custom color initializer.
So now our fill view modifier can take a shape style of type sunfish color.
So now our fill view modifier can take a shape style of type sunfish color, sunfish teal.
Now let's fill a circle with our custom color and draw a border around that circle with another custom color.
So in this case, we're creating a completely new modifier instead of overloading or extending an existing Apple view modifier.
That's because there is no way to natively fill and stroke border at the same time, so we're building that ourselves to use our custom colors.
So since we are implementing a completely new view modifier, most of the steps have already been done except for the last one.
So to implement a custom fill view modifier with a stroke border, we've already created a sunfish color enum.
We've already extended color to initialize color from sunfish color.
We've already extended shape style to use our custom color initializer.
But now we need to extend the shape class by creating a custom fill method that can take shape style of type sunfish color.
So under the hood of our custom fill method, we're actually calling Apple's stroke and background view modifier methods.
Because those methods take in a shape style, which we've already extended to include sunfish color, this means we can now call our custom view modifier method and pass in our custom sunfish pink to fill the circle and custom sunfish brown to draw the circle's border.
And this last step makes it possible to call the custom fill view modifier.
Now on to our final example, we want to draw an ellipse with the border in our custom sunfish blue and the background of our shapes view in sunfish yellow.
Here we are calling individually Apple's stroke border and background view modifier methods, but we're passing in our custom sunfish colors.
And once again, all the steps we need to take have already been done.
So to extend the stroke border and background view modifier methods, we created our sunfish color enum, extended color to initialize color from sunfish color, extended shape style to use custom color initializer.
And that means existing Apple view modifiers like stroke border and background that take a shape style can now take a sunfish color.
So to recap, in order to create custom colors that we can apply to shapes, we first find or create our custom colors.
Then we want to import those colors into our Swift package.
And this allows us to easily extend existing Apple view modifiers to take custom colors by extending shape style.
This process works for the fill modifier, the stroke border modifier, and the background modifier.
However, we needed to implement a custom new view modifier that can take custom colors through the extended shape style, and that was for our custom fill modifier that includes the stroke border parameter.
So I've gone through a lot of examples, so now it's time to share some resources I used for my project and my talk.
Here's a couple about creating Swift packages, since I went over Swift packages a lot, and you can follow these if you want more details.
I also talked a lot about view modifiers, so here's some resources if you want to learn how to work with view modifiers.
There's a very useful one from Hacking with Swift, and I want to give a shout out to Daniela, a fellow speaker at SwiftCon for writing a really great tutorial on view modifiers for
Codeco.
And Apple has some great guides on view modifiers as well.
And here's some resources for design and accessibility.
I want to give a shout out to Susanna, who is a member of the Women Who Code Mobile community, and also Terry, who was a fellow speaker with me at Swift Toronto, for helping me find these resources.
And I'll give you a moment if you want to take a picture of this slide.
This is the link to my sample project.
So for the moment I know you've all been waiting for.
You want to know the answer to which is the lie.
So let's see if you're right.
Okay, two truths and a lie.
Am I allergic to cats?
Sadly I am, even though they're very cute and adorable.
And I actually don't sleepwalk, so that's kind of a relief.
But I think I can say that I once swam with sharks.
I put these two pictures up to kind of throw you off a little bit.
But I went to the Sea Life Park in Oahu, Hawaii, and that was where I got to both pet a dolphin and snorkel in a pool with baby sharks.
So I count that as swimming with the sharks.
So a very specific question, but did you succeed in using your custom fonts in previews?
Custom fonts in previews?
Yeah, yeah.
She's tried previews.
Yes.
I guess my question would be what is the challenge that they're talking about specifically?
So I assume that it's, well, that was the question actually.
So I didn't have more context.
The answer is actually, did it work for you?
So let me see if I understand what this question might be.
So there is a way to, there was a way I was able to test my custom fonts and colors with.
Has my microphone been off?
Yeah.
Okay.
No, actually it's, yeah.
Okay.
Can you hear me better?
Yeah, yeah.
All right. , so in the library itself, you can, and this is what I did, create like a test view file and use your library that way and test it in the previews.
And it does work?
Yes.
I was about to read the question from the audience, but I received a notification from my daughter trying to buy something in the app store.
So I said yes, because I haven't had time to see what it was.
I think it was something Roblox related, you know, if you know Roblox.
You know what it is.
Why not just do an extension on color?
Do an extension on color.
The reason that that's a good question.
And the reason is because let me see, let me answer this slowly.
There was a reason for that.
The view modifiers, they take the shape style protocol.
So you had to extend shape style, not color.
Actually, can you make animations into a separate Swift package project?
Like implement an animation modifier, for instance?
That I've never tried that.
So like an animation that will take custom colors?
Or not necessarily, but yeah.
I think if someone is willing to do that, that would be very interesting to see.
And one last question is not related, but it's more about your role as a leadership fellow for women who code.
Can you tell us more about that?
And also an accessory question, which is what do you think are good suggestions for a woman who would like to involve more in the community and get her voice heard?
Sure.
So let me share a little bit about women who code for those of you that are unfamiliar.
It is a global nonprofit organization.
And women code's mission is to empower women to excel in technology careers.
And as far as how to get involved, women code has both in a lot of places local in person chapters, which were very active before COVID.
And, you know, some are trying to pick it back up again.
And we also have several global technical tracks, tracks by technical stack, tech stack.
And so I am the leader for the global track for the mobile tech stack.
And I would recommend one really great way to excel in your career is to get involved in a community like women who code, because there's a lot of opportunities to volunteer, to give talks, to give back.
And those are all wonderful ways to really grow as a software developer and to grow in your career.
So yesterday we also discovered there is a dormant women who code in Paris.
It was active a while ago, of course, before COVID, and after as many things kind of reduced the activity.
So it could be a good opportunity to, well, reboot that.
There is still some communities in Paris that are not mobile focused, but developer focused for women, especially the Le Duchesse.
So if you're interested, it's not mobile.
Once again, it's cross technologies.
But this one is still active.
All right.
Thank you very much.
Thank you.
Thank you.
Thank you.
Thank you.
