---
slug: >-
  /talks/frenchkit/swift-connection-2024/natan-rolnik-mastering-swift-for-scripting-and-tooling
date: '2024-09-23'
title: Mastering Swift for Scripting & Tooling
author:
  - Natan Rolnik
video: tbx_T2dwoFI
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/tbx_T2dwoFI.jpg
slides: null
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: false
---
### Natan
Hello, everyone. It's truly an honor to be here. I know after lunch is hard, so I prepared a sentence in French.

All right. So I'm Natan. Let me just set it up here.

So I learned to program in Objective C around 14 years ago. I have a passion for beautiful UI animations and I'm also interested in web server and tooling technologies and I love coding in Swift as I'm sure most of you here are. I'm also a dad of three children and that doesn't leave me too much time, but when I do have a blog, I write about tooling in my website.

I'll leave a link at the end. We're going to talk about tooling, so let's define it. What is tooling?

So it's the use of specialized software for programs that help developers in many ways, in many tasks, and basically their goal is to improve efficiency and collaboration in a team and in the overall process, and how I got into it, that's a little story. So my previous job, I got there and the repo was in quite a bad shape. It had tons of branches.

So not really. So I wrote a bash script and my manager said I wrote a bash script to clean up those branches and merge PRs that didn't need to exist anymore, and my manager said maybe we want to do a team here that the clients of this team are going to be your colleagues and you're going to do some work to help them in the day-to-day, and then I had two options. I had the options to keep drawing JSON as collection views and table views as I was doing for years, or I could go to a new path and learn new areas and basically empower my team and my colleagues, so that's what I did.

Before we move on, I want to set the goals for this talk. The first one is we're going to learn the different approaches when building tools, maybe a script, maybe an executable, maybe with the argument parser. We're going to meet common building blocks and tools that are very popular and useful in this area, and, finally, I want to inspire you all and maybe have some fun along the way.

How we're going to do this, so I wanted to meet my little friend, his Swift bird, and we're going to first discuss why Swift and not other languages. Then we will try a short script, then we will try to make it a bit more complex, and then we will try to do another tool. It's going to be a bit more powerful.

We're going to use stencil which is a template language we're going to talk about it soon, and it's going to be a live coding. The first one is going to be a live coding, and what could go wrong? We're going to do two live codings, and I'm not scared at all.

I prepared some warm-up questions so we can fill the waters a little bit. Take your phones out, and please scan this or just type the address you can see here. I hope my server doesn't crash because the last time I did it, it was with less people.

I see some phones now. I think we're ready. I built a little tool, and we're going to see the results live.

Can you read it? Fine. First question, have you done programming work related to the app to turn iOS up but not the app itself?

That's a good indication. I still see some numbers going up. Next question, have you ever dealt with continuous integration?

I feel you're a good audience. Next, have you felt the need to automate tasks that you or your team were doing again and again and again? It's also good.

Have you played with Swift on the server? Here we can improve. There is more than one option.

Thank you. Last question. Here I expect to be good.

Basically, to sum up this, what we saw here, we saw that we all use Swift, we all need to automate stuff, we help our teams, we do server-side stuff once in a while. So, why use Swift at all, right? There's no shortage of other languages.

There's Ruby, Node, Python, and those languages they even have longer, like, they date longer than Swift, or they have larger ecosystems, but you know what? We are probably here, most of us here are iOS developers in an iOS team, and one person might know better Ruby, the other might know better Python, but if you are in an iOS team, we all know Swift, and that's a huge advantage over the other languages. So, in short, Swift is not the silver bullet, but in this case, it can solve, and anyone can jump in and maintain and help improve or even create a new tool.

So this is an advantage that the other languages, they don't have. So, what are other advantages that Swift has? First of all, it's Swift, right?

We like being the compiler helping us. We like knowing the API and foundation, all property wrappers. They're very helpful in server and also in command-line tools.

Not to mention even plugins and macros which are huge. They're huge helpers in this domain as well. Besides that, it feels at home.

You can use Swift UI from the command line for some specific cases, or if you're doing a macOS app, you know Swift UI, you can just start writing it. And finally, there's an ecosystem that follows a few years, and you can just use packages that are out there. And looking back a little bit, if you compare this with Objective-C, this wasn't so much a reality in its rich history.

Objective-C was mostly, if not only, only for macOS, while Swift, on the other hand, is for macOS, but also for Linux and even Windows, and also embedded hardware, which you're going to hear soon in the next talk. So let's go over what you're going to build now. So the first one, we're going to do a little bit of scripting.

So what are we going to do here? Imagine you have an app for a conference, and you want to give some beta builds for people to try it out, and you want them to know it's a beta feature, it's a beta build, or maybe you're building a feature branch and you want designers in your team to know it's not a regular build or special, you want to differentiate it. Now let's move a little bit to the live demo.

So I prepared here a folder, and you can see it has an icon, and right next to it, we have a script. So I'm going to open the script with XAD. I'm going to open on XCode.

So you can see I prepared here some things. So first I have an extension on NSImage, and it has two things. One is an initialiser that's given an URL, converts it into an NSImage, and finally, I have another property as PNG data, which converts an image to PNG data.

These are going to help us to write less code now, and I have a function here. It's a global function that given a text, an image size, and a colour, it will draw this text in an existing image. So what are we going to do now?

We have this image. We want to load it. I'll explain later how I did this.

So this is currently hard-coded, right? I know where the file is, so I take where I am now, and I append.png. Now I'm going to use the initialiser above. It's optional, so I'm going to handle this case here.

If for some reason it doesn't find it, or can't convert this image to an NSImage, then I want to exit it with a code 1, which is an error, and now I'm going to use an initialiser that AppKit provides me. I give a size, and it provides me a closure, and in this closure, I'm going to do the drawing. So the first thing I want to draw in this canvas, I'm going to actually draw the original image, and then I'm going to write the badge on it.

I'm going to call the function. Let's call it Swift, and now what I have still to do is we're going to create a URL for the output and save it, so first we convert the PNG data, and we also handle the case, create the output URL, and now we perform the save. So let's see if this works.

So I'm going to do Swift, which is going to actually compile the script and perform it. Let's see if it worked. There it is.

So now you notice this is hard-coded. Now I want to add some dynamic components to my script, so what I want now is to actually ask the user, the developer, so I'm going to do, sorry, so this is something else that is also important. I might declare this here, and instead of calling it Swift badger.swift, I can simply do .slash. I don't have permissions because I need to do chmod to make it executable. If I do .slash, it's going to work. As I was saying before, I want to allow the user to add a text, so I'm going to print to the console what should the text badge be, and now I'm going to use the read line function, and this is basically stopped execution, and the script is going to wait until the user returns a string. If this is empty, I'm going to throw an error, and now we need to actually use the badge here, and if we do this now, what should the text be?

I just returned empty, but if I do, let's see, there it is. The last thing I want to do is accept parameters, so in Swift, we have the command line.arguments static property, and this is going to provide me the arguments. The first item in this element is the actual path of the executable, and then these are the rest are the arguments, so I'm looking for the second element.

This is going to be the text, so I'm also handling if there is no text being passed. Here, instead of badge, I'm going to use args1. Finally, I want to add capability that if the user passes dash open, that it opens the image automatically.

So I'm going to use nsworkspace to perform this. If I do this again, it's missing the badge argument, so I'm going to do my favourite one, and I'm going to do dash open, and there it is. All right, so this is the first stage.

Now we're going to go to the second step which is a bit more complex. It's the CLI tool. So what you will build, this is actually these both use cases, they're real-world scenarios.

They're things that I did in my current job, but they're simplified versions. So, usually, for this, there's an input, and most CLI tools, what they do is they receive an input, and they throw an output. In this case, the input is going to be a table of events.

You might have this in a spreadsheet somewhere. In our case, you're going to have this as a markdown file locally, just for the example, and you're going to convert this into typed events, typed structs, and these structs can be used in your codebase. You will notice that, in the previous script, I was messing around with arguments and checking positions, and, although this is possible, this is far from ideal because it's enough the user changes the position of them, and it's a hassle.

You can simply do a better choice, and this choice is the Swift argument parser. It's maintained by Apple, and it has supports all these property wrappers, modern concurrency, subcommands, if you want to chain commands, it can do the heavy lifting for you. Up to a point that it was blessed by Apple and SPM, you can, when creating a new package, you can just do dash dash type two, and it's going to create a package for you, including the argument parser as a dependency.

We're going to use stencil. Stencil is a powerful template language for Swift. Basically, you write a template, and you inject data, and it outputs text.

For an example here, this is a template, a short one, which it expects articles, and, once you pass in some data, and you execute it, it's going to convert it into text. In this case, it's an HTML text. In our case, we're going to do Swift code.

All right, so, on to the second live coding. I'm going to do Z period, which is going to open the current package.swift file. You can see here that we have a package ready.

It already has the argument parser as a dependency, and I added stencil, and I also added mark codable. Why I have this dependency here, you can notice that I have events here. Here I have my source of events that I'm going to generate, so, for example, started playback, stopped playback.

I have a struct. This struct is what those lines are going to be decoded to. They're not the final events.

They're just a struct that my tool is going to use, and I have prepared this, which is it's a command. It's the default command in this case. It's my main type, and the argument parser is going to call the run function.

What this function does, basically, it loads the events, it generates the events based on generates the code based on this parameter here, and, finally, it needs to save it to an output. Currently, I have this output as hard-coded file name, and we have left these two events, these two methods. You can see that I have also this template here.

You might take a look, so you can see this line here. It actually is going to iterate over those events, and for each one, it's going to generate a different struct with a name, and also it's going to iterate over the fields. All right, so what do we need to do here?

We need to load the events. I also prepared a little method here that's going to load a string based on an URL. Before I also load this, we can see that we have no input here, so I'm going to use the argument parser here, and I added an input variable which is using the option property wrapper, and I'm also going to use an output, and the default value is going to be the same I had before.

We're just adding support for the user to override this and pass a custom output path. Now, to load the events, I basically need to load this events.md file. I first check the current directory, where I'm running, and the input.

I append the input. Then I load the string, and then I need to decode to use mark codable to decode these into my struct analytic events. All right, so I initialise a mark decoder, and I decode this into this array.

Now I need to use stencil. That's the second part. I'm going to use stencil, so I need to load the template.

There's this nice bundle.module property which allows me to get the current bundle which is analog to bundle.main on iOS, and you can see that I have the template here, and in the package.swift, I declared it here. I need to explicitly add it as a resource, otherwise, SPM is not going to find it in the run time, and this is going to crash. I should throw here an error.

I'm just throwing a fatal error for the simplicity. Finally, I create a stencil environment, and I do a render template. Now I need two parameters.

One is the template which you already loaded here, so I transform the URL into a string, and finally, remember, we had the injection in that slide, so now it's when I'm going to inject my data. Okay, so if I go over terminal now, you can see that we only have this change here, so if I go to terminal now, and I do a swift run, analytics generator, so it's telling me an error. Basically, it's saying there's an input that's missing.

The output, you can see that there's this square bracket saying that these are optional, but the input I need to pass. The input is this file here, events.md. All right, that was super quick, so if you go back to Xcode, you can see this file here, and that's the file we just generated with the code we wrote. To prove that I'm not inventing things, let's just add a new file here.

Purchase tickets. Yay. And let's add here the tier of the ticket.

It doesn't need to be beautiful, but if I go here and do this, we are going to see what I just added here. All right, so we need to wrap this up. One thing that it's important to mention that better than doing this manually is automating things, and the same way that I ran swift run here in my terminal, you can do this in a GitHub action, so you can create a workflow, once you create this, you give it a name, you set the conditions.

For example, I want this to run whenever there's a push to the main branch, and only when the events file changes, otherwise I don't want to run this all the time. The second thing is I need to give this write permissions, because I want it to push back to the repo, and you can see that it runs on Ubuntu. I can use Linux.

There's no reason to use MacOS here. Finally, I don't need to install Swift, because the Linux images on GitHub nowadays, they already have Swift installed. I check out my repo, and I run the same command we ran there, and finally, you can use an action to push it back to your repo.

And I did this previously, so you can see that update of events.md triggered a workflow. You can see all the steps, and this is the commit, the same thing that we did here manually. If you need to improve times, you can use a cache, the cache action, or you can use precompiled binaries.

You do Swift build release, and you add your binary. So to wrap up, Swift is not the silver bullet, but for your iOS team or even mobile team, it probably is the best choice for tools. Go out and build something.

Your future self and your team, they're going to thank you for saving time and improving your routines. The argument parser is your friend. It's very, very simple to use, and it's better than just writing scripts.

You can try scripts if you're striving for simplicity, but the argument parser is very handy. And leverage the existing ecosystem. You can look for packages in swiftpackageindex.com, and that's it. I left sample code here in this repository. These are some of the projects I used here. Path.swift and pathkit you can use to easier to better handle path. Besides that, this is the website I mentioned about. I try to post weekly. There's also Paul Piela's blog.

There's very good content on tooling. There's some projects you might check out that they are just in this line of tools. Thank you very much.

I hope you enjoyed it.

### Denis
One question from the audience. Is there any hidden code you didn't show us that enabled you to display graphical UI from your script?

### Natan
No. The code was that function. That was all it.

It's actually interesting, because I used here appkit, but I wrote a post not long ago, like two, three weeks ago, that you can use Swift UI from the command line, which in the first moment was like, how? And there's a class that is called image renderer. So you can have your views as long as you're running on Mac OS.

This wouldn't work on Linux. But if you so all this code that I did in appkit, you can just create your view and use hstacks, vstacks for positioning and image renderer and output an image.

### Rob
Something I saw a lot in your first example was when you had trouble, you called exit one. What's the one?

### Natan
Right. So whenever tools or whenever an executable exits, it either exits some terminals, even they have some color that they show, like sometimes they show red, meaning that it was an error. So whenever the code is not zero, it's an error.

There's also an error that Xcode throws a lot is error 65. Probably you've seen this. So it's also a code.

So any code that is not zero is a failure. I think it's also worth mentioning that when you're using the argument parser, you should probably be throwing errors instead of exiting. And the argument parser will be able to catch that and print that there was an error and they will throw an exit code.

### Rob
So the argument parser can kind of take care of all the shell things for you.

### Natan
It's not going to use any stylings and it's not going to be red. Yeah. But it takes care of it.

### Denis
Do you have an opinion about how you can migrate a fastlane implementation that is already on Ruby to use it with Swift?

### Natan
Honestly, I don't. I think that would be a lot of work. And one thing that's worth mentioning is that fastlane as being in Ruby allows plugins much better than Swift.

So I wouldn't recommend to migrate everything. But instead, I would recommend maybe calling scripts. Like if you feel more comfortable writing Swift scripts, maybe you can write your scripts and call them from fastlane.

That's what I would personally do.

### Denis
Yeah. One more. Is there a place where we can get some documentation about the stuff we're not used to use?

For example, I don't know if you want to move from folder to folder. Do you have to get to the function that is provided by the terminal? Or is there like some part of the Swift library somewhere hidden?

You can just have those functions ready to use?

### Natan
If I understand the question correctly, so you can handle the paths. That's what I showed a little bit. There was the filemanager.default.current directory path. It gives you where am I being executed at. And from there, you could launch subprocesses. There's a process API from foundation that you could spin up other processes.

And when you do that, you can specify a path. So for example, if you are in a repository and you have like a subpath, but you are running from the root, what I would do would probably spin up a new process on the subfolders instead. That's what the question meant.

### Denis
Basically, my question was what is the operation we use to do in script? Like changing folder?

### Natan
Changing folders, yeah. Because in bash, you can do CD dot dot. What I said now is the approach that I would follow.

And I think that I'm not sure that there's a way to change in Swift.

### Denis
Thank you. If you don't have any more questions. Thank you so much.

### Natan
Thank you. That was wonderful.