---
slug: >-
  /talks/flutter-connection-23/akanksha-singh-making-your-flutter-apps-accessible
date: 2023-06-02T00:00:00.000Z
title: Making Your Flutter Apps Accessible
author:
  - Akanksha Singh
video: NFX_zqJEGJA
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/NFX_zqJEGJA.jpg
slides: null
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

Our next speaker sadly couldn't be here with us today because of travel reasons.

But she's here with us through Google Meet.

So please welcome Akanksha.

Akanksha, it's your turn.

[APPLAUSE]

[ Applause ]

> > Hi, everyone. So, welcome to my talk, making your Flutter apps accessible. And I want to thank organizers for helping me in delivering this talk remotely. So, let me start with a quick intro. My name is Akanksha Singh. I'm a software and community builder, mentor, and speaker.

So let's look at the agenda for this talk.

So I'm going to start with giving a brief overview of what is accessibility, why it's needed, and then move on to discussing problems faced by people with disabilities and how we as a developer can ease their life by making apps more accessible.

So let's start with accessibility, what exactly it is.

So accessibility stands for ability to access and benefit from some system or entity.

Over 1 billion people, which is around 15% of the world's population, lives with some form of disability.

In context of technology and internet, accessibility focuses on ensuring that digital content, websites, applications, and electronic devices are usable by people with disabilities.

Adding accessibility to your apps not only benefits people with disabilities, but it also helps in improving overall user experience.

The WCAG standards, which is Web Content Accessibility Standards, have 12 to 13 guidelines, and these guidelines are organized under four principles, which are perceivable, operable, understandable, and robust, and on these basis of these guidelines, they have a testable success criteria, and the success criteria are at three levels, like A, AA, AAA.

So looking at the key aspects of accessibility, the first key aspect is perceivable.

So by perceivable, we try to ensure that the information and the content can be perceived in different ways, accommodating various sensory abilities.

For example, providing captions or transcripts for videos to assist individuals with hearing impairments.

By operable, we need to try to make interface easy to operate for individuals with various disabilities.

This involves designing intuitive navigation, providing alternative input methods, and avoiding time constraints that may hinder users with certain disabilities.

Next is making apps or making the information understandable so it's clear and understandable to a wide range of users.

This involves using plain language, providing clear instructions, and avoiding complex jargon and ambiguous content.

The last one is robust.

So by this, we try to ensure that digital content and technologies are compatible with different assistive technologies and devices, such as screen readers, screen magnifiers, and alternative input devices.

By considering these principles and implementing accessible design practices,

Developers and designers can create inclusive design experiences that enable individuals with disabilities to access and interact with information, services, and technology on an equal basis with others.

These are the major types of disabilities that we're going to have a look at today.

So starting with visual impairment.

Visual impairment can be either complete blindness, it can be low-level vision, it can be colorblindness.

So different types of visual impairment have different needs.

But considering just some aspects, what we can do is we can try to have semantics which helps the inbuilt features like TalkBack and VoiceOver to assist users in using their way to navigate the application.

So another thing we should take care of is font and UI component size.

So it should be responsive.

And with the help of the accessibility features and options that are already there in Android and iOS, we should try to make it in a way that it can be adaptable to any screen size.

Then we should also take care of the contrast ratio.

So the color contrast ratio should be at least 4.5 is to 1 between the text and the background.

And we're going to check that later.

So yeah.

So starting with fonts.

So these are some of the accessible fonts that one can use.

So these are considered more accessible than others.

Then we can also provide options to change font settings in our app.

And we can use bold to add emphasis rather than italics or uppercase.

About the contrast ratios, as I mentioned, contrast ratios would be around 4.5 is to one between the text and the background.

And there's this website, contrastratio.com, where you can check the contrast ratio so that you would choose the best contrast ratio for the colors and the text and background that you're using.

It would be nice to have different themes or options so that users can change accordingly and have a better user experience.

Also, we should try to reframe using just color to give out the information, because in case of people with visual impairment, it will not make sense at all.

So it's better to always include error messages, so that if people with visual impairment use talkback or voiceover feature, they will be able to hear what the error actually is.

So that's one thing.

Now moving on to hearing impairment.

Hearing impairment can be deafness, or it can be aid-induced hearing loss.

So for people with hearing impairment to make apps more accessible, we should try to include captions in video or audio if it's there.

We should use visual and vibrating alerts.

Screen blink for notifications will be helpful and adjustable volume.

So yeah, visual and vibrating alerts will be very useful for people with hearing loss.

And the next one is mobility impairment.

So in mobility impairment, we can consider users who either have complete paralyzed body, or they have a missing limb.

Or it can be just a temporary cast or brace, just for a short duration.

So for each case, the requirement will be different.

But majorly, what you can keep in mind is to check touch target as big enough, wherever necessary. try to have voice input support, and try to add auto-completion, use auto-completion widgets, so that they can easily enter input.

We should also use search bars that have auto-completion, and easy input support can be provided by using drop-downs and pickers.

Eye gaze control can be something a bit difficult to achieve, but it can be explored, make app more accessible to people with missing limbs and paralysis.

So yeah, that's about mobility impairment.

Moving on to cognitive impairment.

People with cognitive impairment can be, the dyslexia is one of them.

They can either have ADHD or something similar.

Alzheimer's, so what can be done for people with such impairment?

We should take care of the font, font like OpenDyslexic for dyslexia.

The layout should be very simple and minimal.

And the contrast ratio as discussed, it should be 4.5 to 5, which is standard.

And try to avoid distractions by using less animations and auto-completion so that they don't have to just to reduce the burden of typing and inputting values.

Reduce user input requirements by adding pickers and drop downs wherever possible.

So these are the dyslexia friendly fonts, like dyslexic and open dyslexic that one can use.

So moving on to some accessibility options that are already there in iOS and Android.

So these you can explore.

Accessibility options, there are a lot of them in iOS.

So checking out the accessibility options that are already present in the target platform is a must.

This gives you a good idea of what options are available, and you can keep these in mind while building your app.

It is good to keep experimenting and enabling these features to test how your app interacts.

So these are options in iOS, and there are a lot of them in Android as well.

The accessibility options in the emulator are quite less.

So it's recommended to use a physical device if you want to test with the accessibility options.

Then we also have Accessibility Scanner by Google that allows you to scan your screens.

And it provides suggestions to improve the accessibility of your app.

So it checks if the app has -- if the widgets have content labels, if the touch target size is appropriate, if the items are -- and text and image contrast is right or not.

So a lot of things can be checked by accessibility scanner.

For iOS, Xcode has accessibility inspector.

So you can use accessibility inspector in Xcode to explore different-- get different information.

And yeah, so these are two options for Android and iOS.

Just some basic things that you should at least do is [INAUDIBLE] font size by setting the text scale factor so that it is consistent throughout the app, even when the settings have highest font size settings.

So in accessibility settings, if the user sets it to be highest, then it will be able to scale.

So that's one thing a developer can do.

It's simple to just add this property.

Then the contrast ratio should be 4.5 is to 1 for small text, and at least three is to one for large text.

So this is recommended by W3C.

And about the touch targets, so minimum interactive region around any widget is called the touch target.

And for Android, it is 48 db, and for iOS, it's 44.

So you can set these values by setting the property

KMinInteractiveDimension, in iOS and came in interactive dimension in Android.

So this way it sets the standard touch target.

So it's easier to click on those instead of just having a very small icon and the clickable area is less.

So that creates problem.

So that's about touch targets.

Moving on to semantics.

So what semantics is-- semantics are widgets that annotate the widget tree with the description of the meaning of the widgets.

So when the Flutter renders the widget tree, it also maintains a second tree, which is called semantics tree.

And this is used by mobile device assistive technologies like TalkBack and iOS VoiceOver.

So each node of this semantic tree is semantic node, which might correspond to either one widget or it can be a group of widgets, and each semantic node is linked to semantic configuration, which is a series of properties that tell mobile device assistive technologies how to describe a node and how to behave with the node.

So we will discuss some semantic widgets and have a look at some code as well.

So to start with, we have these merge semantics, exclude semantics, block, and index.

In merge semantics, it is used to merge all the child semantics into one, which allows screen readers to read aloud everything at once.

So let's look at this example.

So here, if we use merge semantics for this whole column, so if the user, when they enable the talkback feature or voiceover, it will read all of the information, which is name, hour, and email, hour@gmail, all at once.

So there can be cases where you want the talkback feature to read aloud, so widgets together.

So in that case, you can use merge semantics.

Then we have exclude semantics.

That is used to drop the semantics of the descendants of a widget.

So there can be cases where you don't want the talkback feature to read aloud something.

It can be an image that TalkBack feature, if you haven't added all text, then it might just read image or something, which won't make sense.

So there can be cases where you don't want the screen readers to read aloud, or you just want them to exclude those widgets.

So in that case, you can use exclude semantics.

So here you can see we have a ListViewBuilder, and we have used exclude semantics for our text.

So when the talkback feature is enabled, then it will exclude that one and it won't read aloud third text.

So yeah, there can be cases where you wanna exclude semantics.

So there you can use that, and then we have index semantics.

So it's used to make announcements about the current call state.

So the automatic indexes would give, like as you can see in this example, we have index semantics and for spacer.

So if we use index semantics, the spacer, like for when the talkback feature is enabled, it might even announce that.

So that can be skipped easily with index semantics.

Then block semantics can be used in the case where we have a dialogue or something.

So if a dialogue or alert box is showing on the screen, then the semantics for the background should be disabled.

In that case, we can use block semantics.

Now, talking about all the semantic widgets and everything, how you can debug or how you can see if it's working properly.

So if you enable the show semantic debugger, if you enable it to be true, then you will be able to see how or what labels you have set and what target area has been covered, if the merge semantics is considering all the widgets together or not.

So it's easy to test with this and easy to identify how things are working.

And next thing I wanted to talk about is a package by RebelApp Studio, which is accessibility tools, which can be very useful for just getting information on how your app is behaving.

So it has some features, some checkers, that can help you easily identify if you have done those things or not.

So you can use accessibility tools package.

So current accessibility checkers in the package are semantic label checker.

We have a tap area checker, a large font overflow checker, and input label checker.

These are some basic things that should be considered to make app more accessible and can be easily done with this package.

So yeah, those are some of the important things that one should think about when they are making an app.

So yeah, so this is an official accessibility release checklist by Flutter team.

So you can read about it more and explore more into it.

Yeah.

So pretty much I wanted to just -- why this talk, I wanted to focus more on why it's important to consider all these things.

And to conclude, I would say accessibility we should always prioritize.

It not only empowers the users who have certain disability, but it also improves the user experience for all the users.

In conclusion, creating accessible Flutter apps is not only a legal and ethical obligation, but also a tremendous opportunity to reach a broader audience and make a positive impact on people's lives.

By following the practices we discussed today, we can build more inclusive apps that empower individuals with disabilities to fully engage with technology and enhance their overall digital experience.

So let us commit to making accessibility a fundamental aspect of our app development journey and strive to create a more inclusive and accessible digital landscape for all.

So that was all about accessibility.

These are some of the resources.

And yeah, that was all for this talk.

If you have any questions, you can connect with me on Twitter @thebitcoderjedi.

You can DM me if you have any questions.

I would love to discuss more about accessibility.

And yeah, that was all for this talk.

Thank you.

(audience applauding)

- Thank you, Akanksha.

[APPLAUSE]
