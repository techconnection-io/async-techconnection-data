---
slug: >-
  /talks/frenchkit/swift-connection-2024/eric-bariaux-blink-them-to-death-using-embedded-swift
date: '2024-09-23'
title: Blink them to death using Embedded Swift
author:
  - Eric Bariaux
video: 61A46nZmCLE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/61A46nZmCLE.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Eric
My name is Eric. I'm officially a software engineer, but really I'm a geek. I like to play with technology, sometimes to do useful things, sometimes to do a bit less useful things.

I don't feel like a dinosaur, but I've been around for a while, so I've used quite a few different systems over the years. I am not, however, an embedded systems engineer or an electrical engineer. In fact, I discovered the embedded world only a few months ago when, back in April, Apple published a blog post on Swift.org pointing to the GitHub repo with the embedded Swift examples. This talk is about my journey with embedded Swift over the last few months with its ups and downs. So let's first take a look at embedded and some of its limitations, and for that, I want to compare a small embedded chip. This is an RF chip that's used, for instance, in the Apple TV remote control, and we compare that with an Apple Watch Series 0, so the original one released nearly ten years ago.

In terms of processor, we're looking at a single core 32-bit versus 64, not a big deal. Clock speed, we're talking 64 megahertz versus 520 megahertz, so we already see that there is an eight times speed difference between the two. Memory, we are talking 256 kilobytes versus 512 megabytes, so that's a 2,000x, and in Flash, one megabyte versus eight gigabytes, so it's 8,000x.

So we see that, if you want to bring Swift into the embedded world, we really need to do something. Reduce everything that's overhead at run time, the memory footprint, and the code size. And so embedded Swift is Apple's official answer to this, and it is basically Swift, but with limitations.

So it's a subset, not a dialect. And the way it does it is that it adds a compilation mode that adds some constraints in order to achieve the reduction goal that we mentioned. How does it do it?

Well, it removes basically everything that's dynamic. So no dynamic reflections, no existential types, no generic instantiation at run time, and of course, no interoperability with Objective-C, which requires a run time. So with that, we get a minimal run time library, which is mainly concerned about memory management.

We don't need to include metadata about the types, so no run time, no metadata required. It also uses a reduced Swift standard library, so for instance, codable is not available. And it does aggressive dead code stripping, so only bundling really the code that is required for execution.

In practice, it's a few compiler flags. You need to define the target for which you're compiling. You need to enable the embedded mode, which is still experimental to this day.

And you need to do a whole module optimization for the dead code stripping. And so the embedded Swift manual indeed says that it's a compilation mode where we produce an object file, much like another compiler like C compiler would do, and that it needs to be linked with the rest of the code. And the linking is not done by the Swift compiler, it's done by the toolchain of your target environment.

And the user manual goes on to explain the different steps required for embedded development. And we can see that Swift is only a small part of all that's required. So there's a compilation, and then using the output of that compilation for the linking.

OK, let's switch gears a little bit and see how, if you want to start embedded development, you could do it. So the first thing I would do is install the development toolkit for the board that you're targeting. Don't think about Swift.

Just install that and test that it works. And in embedded world, the hello world is blinking an LED. This is the board I'm using, so it's an NRF 52 840 developer kit, so you have buttons and LEDs and all that stuff to play around.

And there, SDK comes as an extension for VS Code, and so you can stay within VS Code, have code completion, and have UI to trigger the build and debug and all that kind of stuff. And so you test that it works. Next step, go to embedded Swift, and look at the examples that Apple provides.

In the example repository, you have quite a few different examples, depending on the board that you're using. So you have stuff for ESP 32, for Raspberry Pi, PyCrew, for NRF in this case, which is what I'm using. And so if you look at the readme, the first thing it says is you need to make sure to use a nightly tool chain of Swift.

And that is still the case, even with Xcode 16, so I would highly recommend to do that. And so you look at the readme, and you execute, sorry, you go to the website, you download the latest snapshot. So you look at the readme, and you execute all the commands that are required to test the example, the main one being make sure that you use the tool chain that you just downloaded.

But I don't know about you, but typing these kind of commands in a terminal to develop something, that's not what I want to do. And so the next step that I did was try to set up a proper environment for the development. And so there are a few tricks, but I managed to have VS Code with the normal NRF connect SDK tools and the Swift extension, and I have a blog post explaining how you can do that.

And with that, I could, with one button, trigger a build, package everything, flash it to the board, connect to the board, and I can see on the console some debug logs. So that was, for me, a good starting point to go further. And so going further, you start with the examples provided by Apple.

Again, let's take a closer look, for instance, this is the blinking LED, and so you see it looks like normal Swift code, except there is this GPIO pin configured DT and LED zero. So where is this coming from? That's coming from the bridging header.h. This is a standard C header file. It's used by the Swift compiler to Swift C interrupt to basically make available in the Swift world the C construct. And so there are some includes for the SDK that is used here. And there is the LED zero that's declared as a static variable, which is a structure representing basically the pin to which the LED is connected.

But this doesn't look very Swifty, it's just Swift as glue code to C. That's not what we want. So let's try to fix that.

And we'll create a struct that will encapsulate the C calls. And we want to make it reusable, so we pass the pin to which the LED is connected. And in C, that's the pointer to a struct.

And so in Swift, we need to use unsafe pointer. So that might be a bit less known to people doing regular iOS development. You don't use that every day.

And there is a full suite of unsafe something. It's documented in Swift C interrupt documentation from Apple, so that's not really a big deal. And with that, our main function looks a bit more Swift.

But if you look in the SDK, they say that you're not supposed to use a pin before you have checked that the GPIO is ready. So we want to handle that case. And we create an error.

And we make the initializer throwing. And it doesn't build. But the Swift compiler gives a pretty useful error.

And the issue is that throws is the same as throws any error. Any is an existential. Existentials are not supported by embedded Swift.

But it's easily fixed with a feature that was introduced in Swift 6, which is type throws. And so you just add the type in the throws clause, and that works fine. But until now, I just ignored the error that was thrown, and so now I want to catch it and print something to the console so that I know at least that something went wrong.

And it fails again. But this time, it's not the Swift compiler telling me what to do. It's the linker that is nicely telling me error code 1.

Okay? So this got me into a rabbit hole where I was trying to understand all the build system. It's not SPM or Xcode.

So it's a completely different build system. I wanted to pass some arguments to get some more information. And then I went into trying to understand compilers and linker and linker script.

And I was puzzled, and I didn't find anything. And then someday, I looked at the repo again, and there was a commit by an Apple engineer that says fixed incompatible PIC setting. PIC stands for position independent code.

And with that, the code worked, and I have a nice blinking LED. Yay! So to be honest, I have no idea if it would have taken me a week, a month, six months, or never to find that issue.

So yeah. Thank you, Apple. But that's just an LED.

So I want to have a button, and I want to have all kinds of stuff. And so you just keep going at it. You hit some issues, you try to work around it, and eventually, you got some code that looks like Swift, where you can instantiate a class, you can have a button, which is generic, because you can have generic at run time, but generic specialization at compile time works okay.

And you have a trailing closure to do the handler when you push the button. So to me, that's the kind of level that I would like to program with embedded Swift. So in summary, if you want to go that route, which is really fun, I would say start by picking a board that you want to work with, install their tool chain, make their example work, then go to the Swift.org website, download the Swift tool chain, start from the example of Apple, and grow your code from there. You will certainly need to learn a few more things, like the SDK of the board you're targeting. You will need to read some C code and understand some concepts about embedded development. I was a bit stubborn, and I wanted to discover by myself, but use the Swift forums, use the community, go to GitHub.

There are plenty of things out there. And things will improve. Embedded Swift is still very early development, I think, and there is a useful link on the Apple website with the status of what's currently in or not.

So I have a few articles on the blog with talking about embedded Swift. I will post also a few example code in GitHub, and I will continue to write there, and you can contact me if you want to talk about that. Thank you very much for attending the last session.

### Rob
Oh, this one's near and dear to my heart. I love these little systems. Do you have any sense of how small it can go?

I mean, if I want to go to a 866 or maybe an 18 mega, I mean, can it go...

### Eric
Yes, I've seen a few posts about a few kilobytes of code, so three or four. The ATTiny is not yet supported, more because of the instruction sets than the code size. But yeah, that's the goal, that it should go down to 8 bits, really low-power stuff.

### Rob
How about, have you gotten a sense of the overhead? I mean, sometimes it's hard to get C code to fit on these little tiny things. Are you paying a big penalty or not much?

### Eric
No, not much. I think you can get to sizes that are pretty comparable to what you would get from C. Awesome.

### Denis
We asked, can we use Swift embedded in an iOS app, and can the limit of this approach can improve the performance of our app?

### Eric
So the goal of Apple is indeed to use Embedded Swift in more than embedded devices. But they are mainly targeting firmware, bootloaders, kernel code, etc. As I said, it's a subset, and so you can compile with Embedded mode on a Mac.

I've never tried on an iOS, an iPhone, or an iPad or anything. But you can compile code to your Mac host with Embedded.

### Rob
I don't know if you've seen how hard or how complex it is to onboard some new platform. If you had some chip that nobody else has taken care of, is that a huge project, or something you could take on?

### Eric
Yeah, I think it's pretty big. There is, for instance, in the ASP32, there are two main categories. The C, which is using a RISC-V chip, which is supported, and the S series, which is using Extensa core, and it's not supported.

And I've read a few people trying to get there, and it seems to be quite a trip.

### Denis
For the people that are building stuff at home, they are asking, do you have a chip to recommend to start using?

### Eric
So in the examples, it's a bit of a happenstance that I'm using the NRF chip. I think the ASP32 C series, so the C6 in particular, is quite supported. The Raspberry also.

### Rob
The Pico, yes.

### Eric
The Pico, yeah. Because Raspberry Pi is not embedded, it's a computer. It's a small one, but it's a computer.

### Rob
Yes. Wonderful. I'm so excited to see Swift branching out like this.

Thanks for pioneering for us. Thank you very much. Thank you.

Thank you.