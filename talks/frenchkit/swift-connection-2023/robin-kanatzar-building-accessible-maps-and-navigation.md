---
slug: >-
  /talks/frenchkit/swift-connection-2023/robin-kanatzar-building-accessible-maps-and-navigation
date: '2023-09-21'
title: Building Accessible Maps and Navigation
author: Robin Kanatzar
video: o8iTIaFaP3o
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/o8iTIaFaP3o.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/63c88b6afb914e3faf50cbfd113b34bb/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---
Does anybody here remember having to use this?
For those who aren't French, how about this?
A paper map on a road trip.
Do you remember how challenging this could be?
And do you remember how many times you got lost?
Thankfully, over the past few years, our paper maps have transformed into digital maps on our smartphones.
This fixed a lot of problems.
It removed a lot of frustration.
But it didn't make life easy for everyone.
There are people out there today that really struggle with digital maps on our smartphones.
They struggle to understand them,
And they also struggle to interact with them.
So in the spirit of accessibility, we want everyone who uses our app to understand exactly the same information no matter what.
To do that, today I will give you some best practices to improve the accessibility of the maps and navigation in your apps.
Best practice number one, challenge why you have a map in the first place.
Do you have a real reason for displaying your information in a map format?
Or do you simply have a set of data that contains longitude and latitude, and you said, what the hell, let's put it on a map.
I mean, that's what everyone expects anyway.
So ask yourself to find that reason why you are using a map format.
And if you don't have a good reason, delete it.
Delete it and find a better way to communicate the most important information to your users.
Take for example, Facebook marketplace.
Every one of these search results here has a precise longitude and latitude, but Facebook didn't use this as an excuse to display them immediately on a map view.
They know the most important information for me is the photo of the item, the price, and description. They already know that I made a filter where I only want to see search results within a 10 kilometer radius of my house. So there's no value added by seeing these mapped out on a map view. This was a very good choice by Facebook.
If you, however, in your app, you say you do have a good reason to use the traditional map format, then challenge yourself again.
Challenge what kind of map you really need to show.
Out of the box, a map view is going to let users pan and zoom and scroll all over the world.
And this gives them phenomenal cosmic power.
But do they really need it?
Is this interesting to them or is this more of a distraction for your users who struggle with maps?
So think about what is it that you need to accomplish with your map and then give them the most simple version of the map that does just that.
In practice, this could mean deactivating unnecessary gestures.
This could mean limiting the scope of your map.
And this could mean hiding useless annotations.
Only show the most useful ones on your map. so far as to even showing an almost static version of your map if no user interaction is necessary.
The more complicated your map gets, the more you run the risk of overwhelming these users who struggle with maps.
And we want to avoid this at all costs.
So for that I propose best practice number three, which is to let your users choose to see your map. an app and seeing a full screen, colorful, annotated, movable map first thing is a lot.
And this can be overwhelming.
So why not start out with a format that's more easy to digest for a diverse audience?
And then give your users a way to access the map only if they want to see it.
A good example of this is in the Airbnb application.
When I search for a rental location, the search results are returned first as a list.
And it's only whenever I click this map button here that I will see the same information displayed on the traditional map view.
So this is a great compromise for your users, because those who struggle with maps are not presented with one first thing.
And those who do like maps, they're only one button click away from seeing what they want.
So great compromise.
At this point we've challenged why we have a map in the first place.
We've challenged what kind of map we need.
And we've arranged our app so the user chooses to see the map only if he wants.
At this point we can talk about what's inside the map.
Best practice number four is to expose your map details to assistive technology.
So this goes back to some basic principles of accessibility.
But you can't interact with what you can't reach.
And you can't understand what isn't clearly labeled.
So in this best practice, make sure the accessibility focus can actually get to the annotations on your map, and that each of your annotations has an accessibility label.
Now I know what you're thinking.
Accessibility labels?
It's like accessibility 101, why am I still talking about it now?
Well, this is why.
If you forget to add your accessibility labels, someone using voiceover on your map, scrolling through your annotations is going to hear map pin over and over and over again for each one of your annotations and they aren't going to understand a damn thing.
So we want to make sure to add the accessibility labels.
And even though it's elementary, there are apps on the store right now that have forgotten to do this, that have an experience like that.
But we, we're better than that, we're going to take care of all of our basics, we will have accessibility labels.
And that brings me to best practice number five.
Take care of your accessibility basics.
Everything that you already have on your accessibility checklist can be applied to your map view.
So this means making sure you support portrait and landscape mode.
Making sure your text can get bigger with dynamic type. sure you meet the minimum contrast ratios with your colors.
And making sure that the touch targets are big enough as well.
Once we take care of all of these basics, the elementary part, we can start looking at stuff that's more interesting.
Like the user experience.
If you've never used an app with an assistive technology like voiceover or switch control, it's pretty slow.
It is slow and it's clunky.
But when you get to a complex UI component like a map, it gets even slower and even clunkier.
So what we want to do here, we want to do what we can to simplify and streamline the user experience when they're using assistive technology.
There's many ways that we can do this.
The one I'll talk about today is to add a custom rotor item for your voiceover users so that they can more easily navigate among the annotations that you have on your map.
If you've never heard of the rotor before, it's this super cool secret hidden menu that you can find whenever you have voiceover activated.
You make a gesture to activate it, you take your pointer finger and your thumb, then you make a gesture like you're opening a tiny little doorknob with those two fingers, and you will see this menu.
This menu contains things that you would want to change, settings that you would want to change on the fly as you're exploring different applications.
And we as developers, we can add some custom stuff to this menu.
So that's what we'll do.
Imagine you have a map with three different types of points of interest.
Let's say the red are parks, the blue are hotels, the dark blue are hotels, and the light blue are restaurants.
With voiceover on, I'll move the accessibility focus through each and every item, hearing the accessibility label, until I finally find what I'm looking for.
So it takes a lot of time.
And I'm only looking for parks in this scenario.
So what we can do to streamline this is add a custom rotor item called parks.
And this is going to change our accessibility focus so it will only land on the annotations that I've classified as parks.
So now when I go through, it's only going to highlight the red ones, and I'll be able to find the park I want that much quicker and that much easier.
Now you may be thinking this could be complex in terms of code to add, but it is very easy to add.
In your code, you're already going to have some sort of an array that contains your MK annotation views for all of the annotations you want to display on the map.
From this you can make a subset of only the annotation views that are parks.
Then you can create a UI accessibility custom rotor, give it a name, like parks.
And inside you add just a tiny bit of logic to show how to choose the next and the previous annotation view for the accessibility focus.
Finally, you take this custom rotor item and you assign it to a property called accessibility custom rotors, which is present on UI view, but we are going to assign it to the one on our MK map view directly.
And just like that, you've added a menu item and you've made the experience that much better, that much quicker for your users of VoiceOver.
If we move on quickly to the navigation part.
Navigation is pretty complex, and most of you are not going to be rewriting Google Maps turn by turn directions within your own app.
Instead, you're probably going to outsource this to either Apple Maps or Google Maps.
And that's completely okay.
If you give the user some options.
Best practice number 7 is just that.
Give your users some options when they want to navigate maybe to Google Maps, to Apple
Maps, but also give them the option to copy and paste the address so they can paste it into their application of choice.
It may be an app you've never heard of, but it really meets their needs in terms of navigation.
The last best practice I have for you today is to test with real people who use assistive technology.
In terms of� compared to other UI components, the map doesn't have a lot of guidelines or regulations when it comes to how to make them more accessible.
So our best resource here are real people.
Find the people that use assistive technology every day, that use your application, and really sit down with them, get their feedback, learn, and you can iterate to make your maps more and more accessible.
There it is.
There's the text on the screen.
Anyway, to bring things to a close, I've given you eight best practices to make your maps and navigation more accessible.
There's so much out there to do.
But these eight will at least give you a good kick start in the right direction.
And yeah, that's it.
I'm Robin Knatzer.
And it was a pleasure getting to talk to you today about accessibility.
Thank you so much for your attention.