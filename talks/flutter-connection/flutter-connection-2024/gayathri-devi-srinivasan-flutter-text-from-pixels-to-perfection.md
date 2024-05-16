---
slug: >-
  /talks/flutter-connection/flutter-connection-2024/gayathri-devi-srinivasan-flutter-text-from-pixels-to-perfection
date: '2024-04-24'
title: 'Flutter Text: From Pixels to Perfection'
author:
  - Gayathri Devi , Srinivasan
video: xYIBjz7xMUY
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/xYIBjz7xMUY.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: flutter-connection-2024
allow_ads: false
---
[Gayatri]
Good evening to be here at Paris, a beautiful city. Now, let's get started with my presentation today. And before going on, introducing myself.

I'm Gayatri Devi Srinivasan, working as a mobile developer at DeGreed. And I'm also a tech ambassador for Women Techmakers Club. And I'm also a technical speaker and content creator.

So, but your 13-minute long talk on text, only the text widget? Yeah, of course. So, have you been in the situation where you need to create a multilingual e-commerce app, which will include your text rather than being left to right to being right to left?

And have you got to implement a social networking app, which will, like, generate user content with a distinct range of animations and custom fonts, which will make it more attractive? Yeah, these are some of the challenges a developer will tend to face while they are in some intermediate level or they tend to face based on their use cases. So, we do have some quiz planned at the end.

Be keen to the presentation. So, getting started with text rendering. First of all, we should be like, I will go through those slides where you will get to know, like, getting started with some basic example.

Like, we may all know Paris is a beautiful city. But what makes us beautiful? Like, each and every unique places like Eiffel Tower and Seine River.

So, these stuff are making it more beautiful and adding some range to the city. In the same way, these text and different kinds of text implementation, the components making the widget more attractive to match with the different use cases. So, I will walk you through the method and implementation available to utilize the text widget in more versatile way.

So, getting started with how you can control text layout using a paragraph builder. So, you can like utilize the usage of canvas based rendering for custom text layouts. Like, while you are developing a long paragraph of text explaining about some tourist place or giving a bio of yourself in your resume, you can go with the usage of like canvas based rendering.

And you also can use text shaping for complex scripting in multilingual languages creation of applications. And you do use improved handling of bidirectional text views. What is the main usage of paragraph builder?

So, there will be more precise control over text layout and the styling of text. And you can efficiently handle the overflow, half nation and line breaking between the text. And you can also create multi-styling and multi-paragraph styling for each individual text component.

So, this will be in the middle of slide. I will show you a code snippet where it will demo the usage of the components. It will like little bit shorter, but the implementation will be completely available in the repo, which will be finally shared to you during the conclusion of presentation.

So, here we have like used paragraph builder in order to set the direction of text and to set the width of the text and to add ellipses if the text got to overflow. So, by this way we can use paragraph builder on our text. Next thing.

So, measuring and optimizing in order to like monitor the performance of each text rendering on our applications because our application is completely made up of text components in most of the places rather than images or anything. Our application is completely filled with text. So, how are we handling and optimizing the rendering process?

So, we should like go with the approach of profile text rendering and we need to initially identify the bottlenecks or the difficulties what we tends to face after the utilization of those widgets and we also need to implement optimization of text. So, for instance we can like utilize the usage of stopwatch to monitor how the text in what time the text is getting rendered in an application. So, this is a simple code stipend which shows the implementation of the same.

Next, this was the major challenge faced by many developers nowadays because many of them are using many applications with a bundle of data but we don't have like a specific method which will handle those efficiently. For example, to handle a set of 20,000 large e-commerce site data we need to like show them, yeah sorry for that. So, we need to handle the large number of data but in what way can we show them or display them to our application more efficiently without any flickering or text layout problems.

The method which we can approach or follow is visualization and incremental rendering. So, through these methods we can able to avoid the flickering and text layout issues. So, this code snippet will give you a demo of how simply we can implement a visualization for a list of datasets which we going to use in our app.

So, facing with complex layouts and custom handling we can like go with the approach of text shadows and utilize custom fonts and community libraries which are available more on our Flutter repositories and we can combine text with rich media elements, layout strategies and by handling input and performance considerations we can able to utilize the text widgets in more complex way to create a user friendly and attractive UI interfaces. So, next moving ahead with everyone faces challenges on each and every implementation they are going to implement or how can we handle that. Like we can go ahead with debugging and troubleshooting with some of the text issues like through this we can handle text glitches happening in our applications by troubleshooting rendering glitches and layout problems.

There are three elements through which we can handle the text rendering issues which are first Flutter DevTools and debugging techniques available. So, first we need to identify what are the common causes for the text issues and we need to look on that in a more precise way. So, how can we enhance accessibility after like minimizing this debugging challenges.

So, first we need to set automatic semantic annotations and we need to expand on dynamic text scaling. So, based on device sizes the text scaling should be matched with the device configurations and we need to address color contrast with new tools and the text collection and feedback. So, this is a simple implementation which you can use semantic widget for embedding the text onto it to match with different devices.

So, enhancing accessibility through testing the accessibility like using the Flutter DevTools as I have told before you can emphasize the automating testing process. And how can we handle complex text layouts by using of enhanced text direction APIs and we can text align using the text align and text direction for complex scripting and using of adaptive widgets for layout flexibility. And we do also have the support for localization with our localization package available and ARB files and generator for streamlined management of text in different languages and Flutter Intel tools for efficient workflow.

What is custom fonts and typography? Okay, we are like utilized different languages to our app but how can we make it little more different? Not following the same font incomplete or all the apps whatever we are creating.

We do have to show some creativity in some gaming app and professional app. So, through font and custom fonts and typography we can able to achieve that. We do have web fonts and embedding and we need to go with the process of dynamic font scaling and responsiveness and kerning and ligatures, custom text rendering and shaders, accessibility considerations.

So, text animations and effects. We do have familiar with rich text animations which will give text effects with shaders and gradients and interactive text widgets like taking text along paths and curves. So, we need to like confirm with the thing before the development process that our text widget or whatever input we are giving to our application should be cropped platform text compatibility.

So, font fallback mechanism, text direction and localization process, platform specific text rendering differences, internationalization and characteristics. These are some of the key notes we need to be like sure about that is properly implemented. So, what are some of the best practices we can follow which will make the application more versatile efficient.

We need to go with separate text from UI elements using text widgets for easy localization process. Use clear and consistent naming conventions for translation keys and employ pluralization and gender specific languages appropriately based on language rules. Consider using a localization management platform for collaboration and vision control.

So, I will suggest some of the tryouts which you can give it a try or you can directly like go to the repo I have shared that you will get to know the code for those tryouts and the slides I have showed. So, these are some of the tryouts you can give it a try through which you can able to experiment different challenges from your text widgets. For example, try creating a simple app that displays a greeting message in different language based on the device locally and build a text widget that animates the color or opacity when clicked by the user.

Try to be like implement a text widget that changes the background color of selected widget. So, I have just gone through the walkthrough of what are the things available in Flutter. But you one should start implementing and experimenting on each stuff in an order to get to know in depth way.

So, now it's time for quiz and before that take a note of this GitHub link. So, you do have access to the code after our conference time. Okay.

So, now it's time for quiz. So, you can directly scan the code or you can directly go to the site and enter the code. Let's get started.

So, I think probably the first question is imagine you are designing text layout for a map of Lowry Museum. For precise control over text placement and styling which Flutter class would you use? Okay.

Going on to the next one. Okay. Next question.

So, you are building an app to display the daily specials at a cozy cafe near Saini River. How can you efficiently handle text overflow and line breaking while ensuring optimal performance? I hope everyone got the next question.

Imagine designing an app to showcase the artistic calligraphy at museum. Oh, it's 50-50. Okay.

So, here is the current leaderboard for the contest. So, let's there are four more questions to be. You are building an interactive app for exploring which Flutter feature allows.

Okay. Okay. It's 50-50.

50-17. Okay. Yeah.

So, the next question is on screen. Consider debugging text rendering issues can feel like navigating the streets of Marais district. Which of this is not a common cause of text rendering glitches?

Okay. The next question. Making your app accessible is as important as ensuring everyone can enjoy the e-filter which Flutter DevTools feature can assist you in testing the accessibility feature.

The final question. For a multilingual app that caters to tourists visiting Paris, which approach is recommended for managing text resources for different languages? The final one.

Okay. Who is the Nico B? Great.

He's the winner. And the second one to have the spotlight is free. Great.

Okay. The winners can come over the stage and collect the swag. Yeah.

The top two. Yeah. Congrats.

Thank you so much. Thank you. And the bonus winner is Albert.

Yeah. And you can connect with me through my Twitter and LinkedIn handles for any queries on the code or any Flutter related queries. And thank you, everyone, for your time and making it more successful.

And thanks to Flutter Connection for this opportunity. Thank you.

[Simone]
Thank you very much for the quiz. It's super interesting to have this interaction and also for the plushes. So for the plushes, by the way, we have to thank Flutter which helps communities like ours.

And they sent us the swag that Masahiro and Gayathri Devi gave you today. So thank you to the Flutter team and Google.

[Romain]
So maybe one question. So we have a question. What would be a good practice for text rendering testing for a large variety of devices?

Do you have some tips?

[Gayatri]
Yeah. So actually we do have the option to texting the text rendering or text display process for different devices in our Flutter DevTools. Like while debugging your application before like you are going into the profile mode testing or release mode testing, you can just on the debugging process test the display range of each text on the screens using your Flutter DevTools options.

During the debugging process. That would be the best approach, I think.

[Simone]
And how to handle the ARB translations to change the style of the arguments?

[Gayatri]
Okay. So you can dynamically pass the styles for each text widget which you are trying to pass it dynamically. For example, if the username is getting to be displayed only after signing up, so you can dynamically pass based on some condition the text styles to particular text widget.

So through this way you can like implement dynamic text styling.

[Romain]
Another question. What would you consider as a low hanging fruit that every app should support from the start? So the minimum.

That's the way I understand the question. Sorry if it's not that. But the minimum feature among all you said that is like the MVP of the text features.

[Gayatri]
The minimum consideration key points which we should be on mind before creating an application, considering only with the text widget is like the text scaling for different devices. It should be responsive. That should not be like text overflow for different screen sizes.

It should be handled with like text overflow with ellipses or some random emojis to make it more attractive also. So the final point is like through dynamic scaling, like instead of passing all at once, we can go with the approach of dynamic text scaling and styling process which will make the application more optimized.

[Simone]
And do you think you can use semantics to, for instance, improve the SEO on the web?

[Gayatri]
Yeah, for sure. We can like use the go with the approach. Yeah.

[Romain]
Maybe I have a personal question based on the text rendering. You talked about the text sizing. Yeah.

And which is the best way for you like if I have a big text and easy to do overflow? Sorry. No, no, no, it's fine.

Okay. Easy to do overflow or the container to maybe like if I have a container of a certain height and the text is too big, what is the best way to do overflow or to make the container bigger?

[Gayatri]
Okay. So that should be a way like we do have the canvas rendering process through which through that approach, we can able to get the text height of the widget. So based on the text height, the container will be dynamically expanding or shrinking its size so that we can handle it.

For example, consider a circle in the center of it. We are going to display a good afternoon message. So for tablet, the circle like if the size of the text tends to be like little bigger, the circle will start to like increase its radius based on the text height.

So based on the text painter height, we can like dynamically increase or shrink the size. So the canvas rendering approach will be better.

[Simone]
I think that's cool. Right. Thank you very much.

[Gayatri]
Yeah. Thank you all.