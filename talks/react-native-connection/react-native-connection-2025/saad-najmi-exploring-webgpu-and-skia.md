---
slug: >-
  /talks/react-native-connection/react-native-connection-2025/saad-najmi-exploring-webgpu-and-skia
date: '2025-04-02'
title: Exploring WebGPU and Skia
author:
  - Saad Najmi
video: C9iSk-361ZE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/C9iSk-361ZE.jpg
slides: null
tags: []
year: 2025
conference: react-native-connection
edition: react-native-connection-2025
allow_ads: false
---
### Saad
  
All right. Hi, guys. I'm going to talk to you all about exploring WebGPU in Skia, or in other words, how to do a cool custom UI in React Native. So, entering myself again, my name is Saad Najmi. I'm a senior software engineer at Microsoft. I work on Microsoft Office for Mac and iOS. I started out as a native developer, and then over time I started doing React Native, and now you might know me as one of the maintainers for React Native MacOS. But for this talk, I'm actually talking about more of a side project that I picked up at the last conference I was at, which is I wanted to see what is this whole WebGPU Skia stuff about, and can I get it running on MacOS?

So, let's start with the inspiration. On developer Twitter/developer YouTube, I'd see lots of really cool flashy demos and animations. And I consider myself a pretty good expert of all the style props and transforms and what you can do with React Native, but I didn't know how to do any of this. And that kind of worried me because I maintain one of the platforms, I want to make sure you can do things on Mac too. Over in Apple land, I'd also see that they started doing cool animations where they have Siri glow and then morph when it gets your results or in their WWDC demos, they had this like ripple effect you could add to SwiftUI. And I also didn't know how these worked. So I wanted to investigate. And the first question was, how are they doing these things? And the answer is, they're using a GPU. If you don't know what a GPU is, it is a graphics processing unit. It's a part of your computer that renders all your graphics. It looks like that if you have a Windows computer, but it's also on your phone, also on your Mac, also on your laptop. And most UI developers like me don't really have to interface with this. That's pretty low level. You kind of leave that to other people. But it turns out we're missing out because there's a lot of cool stuff you can do with your GPU.

So let me talk about that SwiftUI ripple effect demo again. And just so this is a demo that I took from Apple's WWDC talk in 2024. If you've never seen any of Apple's demos, they're pretty great. They're very informative. I'm going to give you like a quick and dirty summary. So that ripple is run by the GPU, and it's basically, there's a thing called a shader, which is a program that you can run on your device. The input is, in this case, a SWIFT UI layer, which is just a bitmap of something you rendered, and the output is the same layer modified. So you can see if I mess with some of the parameters, what that ripple is calculating. And in this case time is a parameter, you can see each frame as the animation is going. Let's go dive a little deeper into that shader.

So the shader is written in Apple's graphics programming language called Metal. You don't need to know too much about how this works, but you can see that there's position and layer as the two arguments. Position is the pixel that you're working on, layer is basically an image bitmap, and then you have a bunch of extra custom parameters for calculating the sine wave. The first two blocks are just doing some math, figuring out a sine wave, figuring out how much the color should change, and then you apply that color change to the pixel that you're working on, and you return that. And because this is a GPU which has hundreds or thousands of cores, this is happening in parallel for all the pixels that you have. So with this, you can calculate like one pixel, one color. How do you get that to your app?

So SwiftUI has some nice APIs for hooking up shaders to your UI. In this case, we have a view modifier where we get most of those custom parameters hooked up. We haven't done time yet because the GPU is not animating this. You're doing that in UI land. So next, there's another SwiftUI API for adding a keyframe animator. I don't write SwiftUI code. It's one of my sad parts of my life. I wish I could write more of it, but whatever. But it was really cool to see that with not that much code, you could write this really high quality animation. And that was pretty cool.

So we're going to step away from that Ripple demo for a bit. I'll come back to it. But I want to talk about GPUs for a bit and give it a bit of a history lesson. So the history of GPU technology is a long history of lots of different standards and words and abstraction layers and vendor lock-in trying to break those abstraction layers. And the latest in that chain is something called WebGPU. And to explain why WebGPU is interesting, I need to explain how we got there. So I don't write GPU code. I got all this from a blog post that I have referenced, and I'm going to summarize what I learned. If any of you have actually written any OpenGL or DirectX, you'll probably see that I'm saying something's wrong, but please forgive me.

So let's start with what I call phase one. This is in the beginning. You had DirectX, which is the Microsoft-specific GPU language that you can use in Windows. And then you have OpenGL and a bunch of variants of OpenGL, which is supposed to be an abstraction layer that you can run on more platforms. OpenGL is C-based. It had a lot of global state. So if you want to do something, you set some global variable, and then you remember to unset it. And that makes it not very portable. You could take the same code, run it somewhere else, and depending on the global state, you might not get the same result. And in this phase, there's a lot of competition of GPU manufacturers and software not always being aligned. Sometimes people would try to do vendor lock-in where there'd be a feature that's only in DirectX. Sometimes you'd try to then bring it into the next spec of OpenGL, like OpenGL 2.0. But then 2.0 has old stuff and new stuff, so it becomes bloated. Eventually people said, "Let's make a small version called OpenGL ES." But that's yet another one, so now we have another standard on top of 1 and 2. And it's kind of a mess. The XKCD, there's 14 competing standards, kind of comes to mind here. Just as a side note, OpenGL ES is what eventually turned into WebGL, which is a thing you can use in your browser. So, yeah, this is not a great phase.

So phase 2 is when people start to try to unify this. So the Kronos group, which made OpenGL ES, they made a language called Vulkan. And they said, let's skip the abstraction layer. Let's just go write directly to what the GPU is doing. The API is the driver. That means it's super powerful, but also it is not fun to write as a human developer. And in fact, you as a human developer are not supposed to write Vulkan code. It's supposed to be what middleware, like game engines, like Unity targets. So Apple, in their true Apple form, looked at that and said, "Nah." And they said, "We're just going to make our own language called Metal. And you know what? We're also not going to support OpenGL. So you can't do anything on our platform unless you use Metal." So this is kind of... Okay, fine. Why would you use Metal? Metal has a nicer API as well. You saw a bit of Metal code in the beginning. But now you have two computing standards. Two is better than five, but still, that's not great. And then over in Google land, they created something called Angle, which is the almost native graphics layer engine. And if you think I'm joking, this is the GitHub page for that repo. And this guy's job is to convert open GL calls into either Vulkan or Metal or DirectX depending on your platform. So we have some unifying layers and some modern things, but it's still kind of divided. And what we really want is for all the people to agree on what is the right best thing with the nicest API, which is exactly where we get WebGPU.

So, WebGPU started out as a W3C proposal. That's the Web Standards Committee. It got all the big companies like Mozilla, Google, Apple, and Microsoft to agree on the API. It's heavily influenced by Metal, so it has a nice API, but it runs everywhere Vulkan and Metal runs. And you know all the big companies agree to it, so it has future kind of lock-in. And so this is, like, when I read this, I thought this would end with, like, oh, now there's 16 competing standards. But then I felt like, oh, no, this is actually just the good one. It's stateless. It doesn't have all that global C state. It's in JavaScript. So it's the language that people know how to use. And it's, despite the name being WebGPU, it's actually a native library. You can go and link it into your native app if you like. The reason it's called web is because it was a web standards proposal. So there are three implementations that I know of of WebGPU. There's WGPU that Mozilla wrote, Don, which is what Google wrote, and if you go into the WebKit repo, you can see that Apple is working on an Objective-C/Swift version. We're going to focus on the middle one because that is what React Native WebGPU uses. And you heard me right. There is React Native WebGPU. The wonderful people known as Christoph and William went and made a turbo module where you can use Don on React Native and render WebGPU everywhere React Native runs. And that's pretty cool. I've never seen like this kind of 3D animation glowing, sorry, shiny helmets in React Native before. And so this is actually where I was introduced to WebGPU. And the first thought I had was, "Can I do this on macOS?" The answer is yes. It was surprisingly easy to do this on macOS. I've ported a few libraries. This was definitely one of the easier ones and I didn't expect that. I got the app running. All of the web GPU code examples just worked because every layer of this was already cross-platform by design. And that was very pleasant.

Let's talk a bit about how this library works so that you get a better idea of how I ported it and how you can maybe port your favorite library to macOS. So the highlighted part, that's basically a platform native view that could be a UIView in iOS or an NSView in macOS. And it has some information to go render everything inside of it in Metal. DAWN is the cross-platform C++ library that Google wrote that translates the JavaScript web GPU into Metal, or on Apple. And then the part that React Native Web GPU does is the binding layer or the turbo module, which is mostly just a thin platform layer to get the C++ to talk to the platform native view. And so most of these things are already cross-platform. So the part that I needed to work on was basically the thin platform layer to expose Metal context.

So, I'll go over kind of the simple steps of how you port the library to macOS. This is going to be a little bit cluttered, so bear with me. So the first step is you add a macOS test app. You can't port a library if you can't test it. We have a library called React Native Test App that helps with this. It generates native app for you so you don't have to worry about it. There's this used everywhere in the community, so I won't talk about it too much. The second step is I needed to go add macOS to the dawn build matrix. Dawn is a C++ library. It was built with CMake or Ninja. Can't remember which one. I didn't really have to think about this too hard. I just looked for everywhere where it said iOS and then I added an extra case for macOS and it kind of just worked. The next part was to rename any code that was iOS to Apple. This is not a functional change, this is just a name change. And this is for two reasons. One, correctness, because now your code is not running on iOS. But two, to tell future developers, this is not just iOS code, there are more platforms, you might need to think a little bit more. And then finally is the actual porting of UIKit, aka iOS code, to AppKit. On Apple, the way you do this is with iftefs. In some libraries, there's lots of iftefs. In this case, there's only like three to five. I gave an example of one that I had to do.

All right. So over in the community, there are people who are starting to build on top of WebGPU. A library I thought was really cool is TypeGPU, which lets you use TypeScript with WebGPU. And this is especially great because instead of counting your bytes in your array, you can just tell TypeScript to do that for you and give you a TypeScript error. And of course, this runs on Mac OS 2.

Okay. So, I showed you a bunch of cool demos. How can I use this? Your app is a bunch of buttons and widgets. It's not like spinning helmets. And this is where I'll say this library in particular is still in technical preview. Web GPU is kind of rolling out across the ecosystem. So, I think it's something to keep a bookmark on, see if you can experiment with it. But it's maybe not something you use directly right away. And also, if you have an app with buttons and screens, how do you integrate graphics processing in there? How do I write a shader there? And this is where I think we're still missing one piece of the puzzle, which is a UI library with buttons and widgets and everything. And that's where Skia comes in.

So Skia is a 2D graphics library that Google wrote. It is older than WebGPU, and it is what... It powers Google Chrome, all the system native views in Android. It powered Flutter for a while before Flutter switched to their own rendering engine. And you can do things like render shapes, render text, render SVGs. You can render videos. And then for all those things I mentioned, you can apply a shader to all of them. And that was the thing that got me very interested. Because the whole thing that... the reason I'm here is because I saw shaders and I thought those were cool. How do I do that?

The newest backend for Skia targets WebGPU so that your Skia code will render to Don, which will then render to Vulkan or Metal. And that makes sense. Google's old graphics library uses Google's new graphics library, and it all kind of makes sense. So what's missing is the React Native layer so that you can use it in React Native. But turns out, people are already way ahead of me. William and Shopify have this library called React Native Skia where you can take all those things you can draw and use it in JSX. And because it's all in JavaScript, you can use it with your favorite libraries like Reanimated and Gesture Handler and whatever else you can think of. And this is where, if you've ever seen the "Can it be done in React Native" series on YouTube, or seen all those fancy animations in the beginning, this is what they're using. They're using React Native Skia. I didn't quite understand how those animations worked, but now I do. And it's because this library is insanely powerful and runs everywhere. And, of course, it also works on macOS because it turns out I can follow the same exact steps, port React Native Skia to macOS, and those are both merged, so you can use both React Native WebGPU and React Native Skia on your favorite macOS app and run all the existing demos. I was pretty happy about that.

So remember that ripple effect I showed you that was in StoO50y? I wanted to know, could I write that in Skia? So I tried it. I took the metal shader and I just basically copy and pasted it into Skia and changed it so that it's in Skia's shader language. Then I thought instead of making view modifiers in SwiftUI, could we use reanimated to drive the clock and could we use gesture handler to figure out where you tapped? And then the answer is yes, you can. You get the same ripple effect in your React Native app. And I thought that was really cool because I was like, wow, it looks exactly the same across both. And this is when it all just kind of came together for me.

Okay. So same question again. How can I use this in my app? Should I rewrite all of my app in React Native Skia so I can put shaders everywhere? And I think the answer to that is no. Because the power of React Native is that you're using platform native views. You get some accessibility guarantees. And if you're rendering everything in Skia, you're kind of skipping that whole layer. And you're kind of closer to Flutter at that point. So I think the better use case is for things like flare or animations or interactivity. Maybe you want a bunch of confetti to pop out when you click a button. Or maybe you want to have like a nice glowy animation around part of your app. Or maybe you want to make like a very interactive widget. So I think that's kind of the better use case for Skia. And then the second question you might have is, what if instead of writing in your shaders in Skia, you just go right to Metal or Vulkan or DirectX directly? And there is, like, I can see the argument for that, but currently in the React Native ecosystem, I don't think there's an easy way to do that. You can't write metal shaders on top of UIKit and all the base views in React Native Core are off of UIKit. You'd have to go find a library that renders SwiftUI and then use that. And then also you'd have to write your shaders three times in three different languages: in Metal and Vulkan and DirectX. So I think if you want to do cool, flashy animations, your best or the fastest path to victory is by using React Native Skia. But the most important part is to have fun. This all was because I wanted to see cool, flashy animations on my app, and I thought I would share with you everything I learned along the way. Thank you.

I'd like to thank a couple of people. First off, Software Mansion for making Reanimated and gesture handler, and for porting those to macOS, so that when I got around to porting the test apps, those just worked. If those didn't work, my life would be hard. I'd like to thank Oscar, who is overdoing React Native Vision OS. He actually ported WebGPU to Vision OS first, and I keyed off of a lot of that work to get Mac OS working. I'd like to thank William and Christoph for doing cool stuff, and especially William for having so many videos, making really cool things with Skia. I have a few links to the things that are referenced. I'll see if I can share those with you somehow. I realize other people put QR codes, and I wish I did that, because that is very useful. All right. Thank you.

### Mo
  
Thank you very much, Saad. You really had a can it be done in React Native moment there on stage.

### Saad
  
Yeah, that was basically the idea.

### Mo
  
Yeah, that was good. It was very, very cool. So you mentioned that the port was originally done into VisionOS, how much work and how much similarity is there typically between VisionOS libraries and macOS? How easy is it once something is there for VisionOS?

### Saad
  
So VisionOS has an easier time than macOS because unlike macOS, which has a separate library app kit, VisionOS just uses UIKit, so your UI views all work. And so the real work was just adding VisionOS to the build matrix, which thankfully the build tool that-- I can't remember if it was CMake or Ninja, but whatever what it was that supported it, so you just kind of had to pattern match wherever there's iOS, there's VisionOS, and then it worked.

### Mo
  
Cool. Very cool. There's a question here that I think is like centered in the late 1990s early 2000s, where someone's asking how does Microsoft feel about your involvement in Mac OS, it feels quite outdated like I'm a Mac I'm a PC ads type of thing.

### Saad
  
I wasn't around for this, but I think when Microsoft announced Microsoft Office on Mac, it was a very big moment. And I think Windows and Mac may compete, so I don't know if that's really the case anymore, but Microsoft Office runs everywhere. It runs on Mac, it runs on iPhone, it runs on Android. And so the ethos of my team is really... If we have a thing we want in Office, then we have to go make it work on all the platforms they support, which includes macOS, which is why React Native macOS exists. We wanted to do something in Office, so we had to make it work everywhere. I don't think there's a, like, Microsoft is fully, you know, they created React Native macOS for a reason, and they're totally happy with it.

### Mo
  
Even more shocking than that was when iTunes was released for Windows.

### Saad
  
I don't remember that, but I will believe that.

### Mo
  
Yeah, there's the videos of it. If you're iTunes on Windows, Steve Jobs took the mic out of Windows, but you'd expect that. What were the steps that you took when you ported React Native Skia to React Native Mac OS? What was that like?

### Saad
  
It was the same steps. Oh, okay. The difference is that I did the add a test app last in that it's still in PR because I couldn't merge it because I couldn't get the test to pass. So it turns out the React Native Skia library is a lot bigger than the React Native FGPU library. So it has a lot more end-to-end tests. And I wasn't quite able to get that all ready before the talk. But it was the same thing. Like, William wrote most of both libraries. He had the same kind of JavaScript script to build either Skia or Don. So it was the same work to add it to the build matrix. He had the same kind of class names of iOS platform context that are renamed to Apple platform context. He saw me do it once for WebGPU. So it was easy for him to review me doing it for Skia. It was a very similar experience, just like one level up. and mostly a time thing. I think the Skia macOS support only landed last week because it took me a bit of time.

### Mo
  
Yeah, fair enough. Is there something you think that is still sort of very difficult to achieve or unachievable in terms of the visual effect space inside of apps? You talked about the ripple effect, didn't you? example. But is there still something that you think would be significantly easier to do in SwiftUI compared to on React Native?

### Saad
  
This is where I'm sad that I don't write more SwiftUI, because I think to be a good app developer, you have to know what's happening in all the spaces. I have a very good idea of what's happening in React Native. I don't have a good idea of what's happening in SwiftUI Jetpack Compose. And I think the best way to learn is by doing. Then I could know what things work better there and what things don't work better there. And unfortunately, I'm one person with a limited amount of time. That's very fair. So I can't answer that question, basically. I don't know.

### Mo
  
Cool. Someone's left a comment. It's not really a question. They've just said that they don't know if anyone is working on React Native for IoT and embedded systems. Do you know anything about that?

### Saad
  
No.

### Mo
  
Cool. Well, I guess nobody's working on REC native for IoT and embedded systems, so... Glad that's cleared. Awesome! Do those have screens? Like, do you have UI on there? Oh, I guess they do. Depends, I guess. Maybe.

### Saad
  
Yeah, okay. I don't know.

### Mo
  
Cool. Awesome. Saad, thank you so much. We're going to have a proper sit down for the panel. So I will relieve you of your answering of questions duty. And then we'll see you back here in a little bit. So big round of applause for Saad. Thank you.