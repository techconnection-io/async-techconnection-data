---
slug: >-
  /talks/flutter-connection/flutter-connection-2025/alois-deniel-bringing-flutter-to-the-terminal
date: '2025-04-04'
title: Bringing Flutter to the terminal
author:
  - Aloïs Deniel
video: kapNyGawf70
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/kapNyGawf70.jpg
slides: null
tags: []
year: 2025
conference: flutter-connection
edition: flutter-connection-2025
allow_ads: false
---
[Aloïs]  
Hey. So the terminal, that's the topic today for me. So bringing Flutter to the terminal. That's original special, I would say. So before starting to explain all of that, I want to talk a bit about myself. I'm Alois, I'm a French software developer. I work for ClickUp right now. I'm also a Google Developer Expert and an open source contributor. I have far many two packages to maintain, so sorry for that. I know there are a lot of issues, but I try to keep up. Just a small notice, ClickUp is hiring Flutter experts, so if you are interested in joining ClickUp, don't hesitate to reach out to me.  

So why the terminal? Recently I started to use more and more the terminal as my main tool. It's my main tool today when I work because I've completely switched from Visual Studio Code to NeoVim. Yeah, I know everyone's going to Cursor right now, but I'm going in the opposite direction with NeoVim. So if you don't know what is NeoVim, NeoVim is an IDE that you launch in your terminal. You can do all of what's possible in Visual Studio Code but from the terminal itself. It's quite fun actually. And there are lots of other tools that you can use in your terminal and they have a fancy UI. We call them terminal UIs or TUIs. So complex UIs like that, which are fun. I found them fun at least. This one, for example, is a Git tool. So instead of using a UI like GitHub UI, for example, you can use this kind of tool. And Tmux is the tool for managing the tabs and the processes and all of that. So I spend like 90% of my day into the terminal today. And it made me a better developer, which I wouldn't expect like two years ago, if you would have told me that I would use the terminal as much as that. I would laugh because I'm more visual guy. I work with Figma most of the time for designs and all of that. So it's fun, but as a developer, actually it made me more productive because it forced me to use more the keyboard and to be better at touch typing and all of that stuff. So it's a real improvement for me.  

And I started to ask myself, how do you develop this kind of UI? Because terminal is actually just a buffer where you send characters like, when you use it for CLI, you can see that it overflows and go to the next line and that's it. But actually, if you fill the whole terminal with characters, you can start to think about building UIs. And that's how these UIs are built. Because you can also style each one of these characters. To style a character, you simply have to use a special escaping code that you place before your text and it changes the current style. For example, if you put the escaping character and 1, it turns the text to bold. You can do the same thing for underlining the text or making it italic, for example. So you can start to play with all of that to create different things. And you can also use specific characters to mimic graphical user interfaces. For example, you can use the characters like the borders, and you can build boxes out of these borders. You can use the space to layout, to move the boxes on the screen as well. And if you repeat this and refresh it, you can actually do a really animated user interface that you would have with a graphical user interface, which is fun.  

Now the question is, I have the principle, you draw characters, but how do you build UIs? How do you create widgets and place them in this terminal? Well, and if you are using Go, Rust, C++, Python, you have already really well-known frameworks to build these T-UIs. You have BubbleTee for Go, for example, which is really famous. You have Ratatouille for Rust, FTX UI for C++, and Textual for Python. But for that, there's no equivalent yet, and that was frustrating to me. But there's a small package which is named Dart Console which helps you with all the escaping code and all the basic functions like getting the terminal size or the really basic changing the title. For example, you have functions to interact a bit with the terminal, but it's still really basic. You don't have the widgets to place them in the UI. That's why I tried to start experimenting with it. And I created a package which is named FTUI for that. It's available on GitHub, on my GitHub, if you want to check it out. It's still really experimental. I'm trying to rebuild it currently to add more Flutter stuff to it. But the whole idea is to use the exact same code that you would use with Flutter to render UIs in the terminal. So you use the exact same widgets, the text, the code, the container, the columns, the rows and everything. You simply put it in the context of FTUI and it renders as character in the terminal. So obviously this slide deck is built with FTUI, which was a good test to see if it works well.  

And a few examples, for example, to build a text, you can see it's exactly the same as in Flutter. You can create text spans, you can put text styles with font styles it's exactly the same syntax but it renders in the terminal instead. Same for a decorated box for example you can put a color and it would paint the background to blue and you can then put the text in into black so it renders well. Same for stacks. You can build a layout with stacks. You can create position widgets and put them into a UI like this. So basically everything that's available in Flutter, my goal is to have an equivalent in the terminal. Sometimes it renders not that well in the terminal because it's not adapted. If I take a shadow, for example, it does not make sense in the terminal. It will be simply ignored. That's what I want. At least I want that you would be able to copy the code from Flutter and use it directly so that you don't lose time to learn a new set of widgets just to build small apps like this.  

But all of that is just a fun project, a side project, actually. It's in active development, obviously, like I said, but it will never be a professional package I would develop. Don't expect any commitment from it. It's just built for fun and to me to discover new things. And actually to build a simple thing like that, I had to dig dive into the internals of the Flutter framework to, for example, mimic the same layout algorithm that you find in the Flutter internal code to replicate it in the terminal. So you have to really understand well how Flutter works. And if you don't do this kind of project, you will never invest so much time and energy to try to understand this low level stuff. So this kind of fun project that you are involved into and that are completely different from your day to day job are, in my opinion, the best way to become a better developer, to learn new things and to improve in your craft. And finally, I hope that this fun UI makes you want to use your terminal a bit more. I see them as pixel art for images. I find them fun to use, fun to manipulate. And yeah, again, just try a bit, a few tools and I can guarantee you will become a better developer if you learn to use these tools. You can follow the project on GitHub. This is my email if you want to join ClickUp. And you can find me on X or GitHub or YouTube. So don't hesitate to reach out.  

[Vadym]  
We have like three questions and one of them is really top-voted. So how do you justify spending time on these kind of projects to your wife? Seriously?  

[Aloïs]  
I have a kid now, so I can relate. It's difficult, but if you don't have the time, don't force yourself. You have to want to do it. But what you can do if you don't have time outside of your job is that you can propose to your company to work on different tools that could help to be more productive inside of your day-to-day job. And you can maybe experiment different things this way by proposing different things.  

[Vadym]  
Yeah. I mean, we all should go outside of the comfort zone and find some time. That's life. Something to sacrifice. Exactly. Yeah. Do you support key inputs? These brought me conflicting memories about C and the N cursors. It is cursors?  

[Aloïs]  
Maybe mouse cursors.  

[Vadym]  
Maybe it's mouse cursors. It's N, but probably mouse cursors.  

[Aloïs]  
Oh, yeah. Maybe. Yeah. Actually, I was typing on the keyboard to switch between slides. So, yeah, it supports key inputs.  

[Vadym]  
Cool, yeah, that's short and cool. And then, what's the purpose of using Terminal when you have all the already available IDEs?  

[Aloïs]  
Not really, I did not want to dive too much into these details, but these are the most portable UIs in my opinion, because you can connect on a server, for example, and use NeoVim to debug your code from your machine to the server with your local terminal. That's one way to use it, for example. And they are also extremely performant because it's just a matrix of characters instead of a matrix of pixels. So it's a lot lightweight compared to a graphical user interface. And it's really reactive and also this kind of interface does not have animations most of the time because it's a constraint and it's actually a great advantage in my opinion because when you want to be productive and you know really well your tool you don't want to have an animation each time you do an action you want to go straight to what you are expecting with the keyboard shortcuts that's why I like it.  

[Vadym]  
I mean I agree yeah much simpler much straightforward that's what I appreciate in people as well and here I want to thank you and I want to say let's connect now because you know I'm real people so round of applause to Luis. Thank you.