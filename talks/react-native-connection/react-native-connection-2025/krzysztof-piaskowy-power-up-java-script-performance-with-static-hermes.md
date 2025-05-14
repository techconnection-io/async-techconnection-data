---
slug: >-
  /talks/react-native-connection/react-native-connection-2025/krzysztof-piaskowy-power-up-java-script-performance-with-static-hermes
date: '2025-04-02'
title: Power-up Java Script performance with Static Hermes
author:
  - Krzysztof Piaskowy
video: vlj_ZWaCjvA
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/vlj_ZWaCjvA.jpg
slides: null
tags: []
year: 2025
conference: react-native-connection
edition: react-native-connection-2025
allow_ads: false
---
[Krzysztof]  
When I started programming, I wanted my program to be as fast as possible, even the simple one. So I decided to write everything in C++ because it is really fast. I was disgusted with JavaScript because everyone said to me that this is slow and bad. And I believed them. At the same time, whenever I need to combine a string with a number in C++, I feel jealous of how easy it is in JavaScript. So I had kind of love-hate relationship with C++. As I gained more experience, I started to wonder: Why JavaScript is slow? You can find many benchmarks that show how much JavaScript is slower compared to C++, but what if it isn't true? What if JavaScript isn't actually slow? And we are just asking a wrong question. What if the real question should be: is JavaScript actually slow? Hello, I'm Krzysztof Piaskowy, the maintainer of reanimated and React Native open source developer at Software Mansion. But today I have a question for you. Do you like getting things for free? I hope you do, because we can get free performance boost with static Hermes. There is a lot of confusion about what Static Hermes is, and it's simply the next version of Hermes engine that comes with a bunch of smart optimizations. Static Hermes offers different modes with different performance levels. It can interpret plain JavaScript or TypeScript, but also can generate bytecode from them. Moreover, you can enable JIT compilation in the runtime or even compile your code to native binary. Let's focus on the difference between interpreting plain code and bytecode. Okay. When your app is running in debug mode, Metro serves the entire JavaScript bundle as a long string. At runtime, Hermes has to parse the whole bundle into tokens and next to AR, which is intermediate representation. You can think about it as a kind of assembler language, but for virtual machine. Then, Hermes applies some optimization, and finally, it can start interpreting the code. And it's happened, all of this happened in runtime. Passing the entire bundle in runtime can take a lot of time, especially if your app is quite big. And this is where the bytecode appears. Bytecode is produced by a Hermes compiler on your local machine when you build your release app. The compiler parses the code, applies more advanced optimisation and generates the bytecode. And the bytecode is a binary format so you can run it by a virtual machine without any additional overhead. But what is actually Hermes compiler? So it's time for first demo. This is Hermes repository where I have already built the Hermes binaries. I mean Hermes VM and Hermes compiler. I have add simple JavaScript codes that adds two numbers. Okay, I'm going to compile this code into bytecode using Hermes compiler and run it in VM. Like I said, bytecode is binary format and that is built in compile time instead of runtime. And you can just run it. We can see that we have result. As I mentioned, Hermes comes with a bunch of smart optimizations. But to really understand how those optimizations work, it's crucial to dive deeper into how CPU and assembly works. But don't worry, we will handle that. Let's imagine a simple CPU model. Let's call it Intel -1. The CPU has basic components. For example, in this case arithmetic operation unit that can access and perform operation over data stored in registers. Registers are processor internal memory, since the processor doesn't have as fast access to external RAM memory. What we want to execute is this C++ code that adds two properties of object A and B and assign the result to field C. Simple, yeah? After the compilation, let's execute our program on this tiny CPU. First, the operation system needs to load the program from the disk into RAM memory. The compiler knows the types and the sizes of the variables, so it can compute the exact location in the memory. The previous part of the program just described the layout of the things in memory. Now let's start executing the assembly. First, we need to load value from address A into register R1. In native words, each operation is described by a single assembly instruction, like we can see here. Yeah, and we loaded this value to register. We need to load the value from address B. Yeah. Once we have all values in register, the arithmetic unit can perform operation on register 1 and 2. Yeah. And finally, we can move the result from register R3 back to RAM memory. And that's how it works in native code. All code is transferred into assembly instructions that the processor can understand. In JavaScript it's quite different because JS is dynamic language and it doesn't know information about types. So the virtual machine has to do a lot of extra work. The interpreter can't simply compute the memory addresses for each variable like in the previous example. Let's consider the same code but in JavaScript. This time, instead of focusing on assembly, we will be dealing with more high-level virtual machine instruction, which under the hood, those VM instructions are mapped to more than just one native assembly instruction. We need to check if the variable is defined and if it's an object. We need to check if property A exists. Once we know that it exists, now we can load this property into a virtual machine stack memory. We need to check the type of this variable. We check if B exists, load to stack memory, check type, check if it's possible to perform operation on given types, perform this operation, check if property C exists because we want to save something, and finally, we can save value to property C. And that was a lot. Can you imagine how many Acelder instructions it would require? Don't worry, I will show you. With static Hermes you can generate the assembler code needed to execute your actual JS. It shows how much work VM has to do because it hasn't typed information. You can see that simple program requires almost 900 of instructions. But thanks to the Hermes team, there is a hope for us. Now Hermes uses type information, for example, from TypeScript to optimize the bytecode. But what do you mean? It's easy to say that compiler uses type information, but how it actually works under the hood? Let's consider our last example again, but this time let's add type information to code. When you have enough type information, you can get rid of some unnecessary instructions. You don't need to check if the variable is an object or if the property exists. You don't need to check the type of variables in execution time anymore. Basically, you need to do this. This. And that's why using type information is a game changer. But does it remind you of anything? Now you can see clear relation between assembly and virtual machine instruction. So let's check how adding types to our previous example can affect the amount of required assembly instruction. Now we need almost three times less assembly instruction than before, and that's a pretty huge difference. As you may see, it's all about types. The key to optimalisation is to figure out how to avoid unnecessary checks and recognise cases when you can do less. Because when you do less, you are faster. There is a trade-off. Someone needs to do more. And you choose. It's you or the interpreter. So, I will ask you again. Is JavaScript slow? No, it isn't. It just do a lot of for you. No matter what language it is, assembly, C++ or JavaScript, the only number of instruction matters. Let's get back to the rest of the optimization. When you write your app, you probably create a lot of small functions. But calling functions is expensive. To optimize it, compiler replaces the function call with the body of function itself. Take a look at the example. We want to compute the area of square with a size of 5. So we call computeArea, which calls computeSquare, which multiplies two numbers. You can see the chain of function calls. The compiler, to optimize it, replaces the call computeSquare with its body. Then it will replace the call of computeArea. And we ended up with a trivial operation that compiler also can just simply solve. As a result at runtime, we have just a value instead of additional function call. When you create, we often also create many small objects, but allocations are expensive too. To reduce the amount of allocation, the compiler tries to decompose the object into primitive types. In effect, the code that uses object syntax will be transformed into local variables that don't require complex allocation. If you want to learn more about optimization in Hermes engine, I can really recommend great Neil's talk from the Hermes engine team. JIT is another cool feature in Hermes. a just-in-time compiler collects information about method invocation. For example, if you have a function that you call it multiple time, passing a number as an argument, JIT will recompile the function, assuming that this argument will be always a number. However, if the type changes in the future, the compiler will fall back to previous slower implementation. And this part is a good one. With new Hermes compiler called Shermes, if I pronounce it correctly. You can compile JavaScript or TypeScript code into standalone native binary. You can run this binary directly on your CPU without virtual machine. Is it awesome? Yeah? Okay, with the new Hermes compiler, you can generate C code that represent your JavaScript instructions. Here is the section that implements the actual logic of your program. Yeah, that's the section. And the rest of the code is responsible for implementing the virtual machine behavior. You also can generate the assembly version of your code. And it's quite long, but don't worry, we will not read it. And finally, you can compile your code into real binary. You can... Yeah, let's wait, okay. You can see that it has regular executable binary format. And it can be run as a standalone binary. And for me, this is mind-blowing that we can just run JavaScript as a binary, but I'm not sure how you feel about it. Okay, so what kind of performance we can achieve with binary format? I will use the nbody simulation, which is a common benchmark. I am compiling the TypeScript version to binary with static Hermes compiler. Now I'm compiling the C++ version of the benchmark. And now let's run the C++ version and see how much time it takes to compute the simulation. Okay, we have a result and now let's compute it with Hermes binary. OK, I need to run it again. So it's pre-recorded, like you can see. OK, run the C++ version and run JS version. Okay, why it doesn't work? No matter. Can I just simply switch it? Let's wait again, but believe me, it's worth it. Just once again. It's good to repeat something to remember, yes? So we can feel like in school. And, wow. Our JavaScript binary is faster than C++1. For me, this is a real game changer. I was so surprised that I ran it multiple times, you can clearly see, thinking that I may have done something wrong. Of course, if you compile C++ with more aggressive optimization, like O3 or something like that, the results will change. But still, JavaScript can be faster than C++. Doesn't sound good enough. In the previous implementation of Hermes, the execution of nbody benchmark is almost 8 seconds. With static Hermes, there is a huge performance boost. Bytecode produced from JavaScript or TypeScript can run almost 2 times faster. The binary with static Hermes is almost 13 times faster. And the ultimate question is how to use it. So you will need to wait a bit. The PR that adds support to static Hermes to React Native is already open, but it requires a bit more work. But after the conference, when I will go back to Poland, I will get back to it and I will try to do my best to deliver it in cooperation with Metafolks. Thank you all and I hope that you will not mad at me about this assembler stuff. And I also want to thank the entire Hermes team for the great job they did for static Hermes. There are also round of applause for them. And the last thing, remember JavaScript isn't slow.

[Mo]  
Very cool stuff. I didn't know you were so actively involved in the static Hermes things. Yeah, a bit. Humble. Cool. So while we let audience questions come in, a few things that were interesting for me was the first thing was when you went from untyped code to typed code, one of the things you crossed out was checking type compatibility. Does that still not need to happen even though the types are defined to make sure that you can actually do the arithmetic operation? Or is that also excluded from it? How does that work?

[Krzysztof]  
So if you want to execute plain JavaScript without any types, Hermes can also try to figure it out what type are you using. So if you don't use explicit type, Hermes also will try to figure it out. But sometimes the code is more complicated. That is not obvious how to-- what actually you want to do in your code. And in this situation, the explicit types comes from TypeScript, is really useful and Hermes can optimize your code more. So, does it mean Hermes can do less?

[Mo]  
But is there a, do you also need to still, on like the assembler instruction level, do you still need to check for, even if you know the types ahead of time from TypeScript, do you need to assess whether or not object.a and object.b are both integers from the TypeScript types before you can add them? Or is that step also removed from the assembler instructions?

[Krzysztof]  
OK, so if you are in interpreting mode, you still need to check what is the type. Because if it matches the expectation, you will fall into fast path. But if you don't meet expectation, you will fall back to slower implementation. But in assembly, on the native binary, you can't dynamically check the types. CPU will understand just, this is just a number, and I will pull it to my register, do something with it, and I don't care about what is the type. This is your problem that your program will break.

[Mo]  
Makes a lot of sense. One of the things that was interesting to me was the 900 lines of assembler instructions that you showed. Is that largely due to the fact that we're dealing with a stack in terms of the memory and you need to cycle through the stack? What's the majority of that instruction that's cut out when you go into typed instructions?

[Krzysztof]  
Okay, so I used static Hermes to generate those instructions, and I disabled all optimalization from the code. So it's because with current implementation of Hermes, this is not possible to generate assembly instructions. So I do... to generate something that is really close to previous implementation. So I decided to use the new Hermes implementation, disable all optimalization, and then we can just realize how much work Hermes needs to do. And yeah, all of this, the actual logic of this program doesn't take whole 9,000... of instructions, but because it also contains the logic of the VM, also dealing with stack memory, checking the types, and basically run loop.

[Mo]  
OK, we're going to move on to audience questions. Pierre has asked, if we use the types to do optimizations, what happens if our types are wrong on the TypeScript level? Is it-- like if you just put a bunch of ts ignores or any types, could we end up having runtime crashes? Or is it just going to be slower?

[Krzysztof]  
OK, so it depends on which mode are you using. If you're using interpreting mode or plain code interpreting or bytecode interpreting, you can still-- you have still some additional checks. Hermes assumed that this will be this type and okay, let's do fast path for this specific type. But if you are in native binary, there is high probability that you can receive the crash. But there is also in native code, you can also use any type, but it's still generates you much slower code. But if you explicit tell that something is number, but you will pass here string, this should crash.

[Mo]  
Okay, makes a lot of sense. Will, I think you've coined a term here, shermis be integrated into React Native, or will it be a separate library?

[Krzysztof]  
Hmm, so I think this is more question to Ricardo, for example. I don't know the plan for the method. Integrating Shermis with React Native, I think this is much longer time. Can you give us a timeline? No, I'm joking. So if you told me that this is impossible to do tomorrow... Don't answer that. Don't answer that. That was a joke. That was a joke.

[Mo]  
Ricardo is very angry at me right now. Cool. Have you tried comparing static Hermes against Bun?

[Krzysztof]  
against-- but ban, I think it's a different concept. It's a different concept, yes. Because ban, this is environment and different runtime. And Hermes, this is also different runtime. And ban, this is more CLI tool. The first man isn't for standalone executing JavaScript in environment like mobile development on device. This is different tools, it's hard to compare.

[Mo]  
How boring does it feel to read JavaScript code now that you know how to read assembly?

[Krzysztof]  
So I like both of them. Like I said, this is no matter what language it is, this is just the way how you express your thoughts. This is just it.

[Mo]  
What does it mean in practice? We've talked about benchmarks, and oftentimes benchmarks are different to how things end up in reality. But what do you think this will mean in practice for performance boosts that are noticeable inside of actual apps? What places do you think in reality it could actually have a positive impact on?

[Krzysztof]  
Okay, I also placed some benchmarks in my PR to React Native, and I tested it in... in the Errant Tester app, which is an example app in, a playground app in a React Native repository, and I, in a runtime, I saw almost 30% of performance boost. Of course, it depends on which kind of operation do you use, but in average, I think you can reach up to 30%.

[Mo]  
And is that like 30% improvement in FPS, or is that 30% in CPU usage?

[Krzysztof]  
Time of execution.

[Mo]  
Time of execution, okay, cool. Yeah. One of the other questions that's being asked is: Does static Hermes need typescript? Which I think is no, but like, will you have any performance advantages without typescript?

[Krzysztof]  
Yeah, you have. You don't need to have fully typescript in your code. Hermes can... try to figure it out from just simple JavaScript. And it's, as I showed on the graph on the last slide, the JavaScript, bytecode generated from the JavaScript and TypeScript, the result was similar. Of course, the TypeScript was slightly faster, but in some cases when Hermes can enough information, because if you have a lot of hard-coded values, this is easy for a compilator to find out what you actually want to do. But if you have a lot of random inputs from the user, it's hard to assess what it could be.

[Mo]  
Makes a lot of sense. And lastly, I've left this, even though it has a crap ton of upvotes, but I've left this because it's totally unrelated to your talk. But obviously, you maintain a library, so good luck to you. When are shared element transitions coming?

[Krzysztof]  
That's a great question. So I have a dream. that one day I will have enough time...

[Mo]  
Can you stand up and do your speech, please? I have a dream. Okay, go ahead.

[Krzysztof]  
That with Bartek we will have enough time to do it. This is literally our dream.

[Mo]  
Okay, well, I hope you see your dream. I've been told it's impossible to get shared on the transitions.

[Krzysztof]  
Okay, it will be tomorrow.

[Mo]  
Awesome. Give him a massive round of applause. Thank you so much, Krzysztof.

[Krzysztof]  
Thank you.