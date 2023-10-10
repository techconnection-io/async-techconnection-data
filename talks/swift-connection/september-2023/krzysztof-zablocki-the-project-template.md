slug: >-
  /talks/${editionInfo.conferenceSlug}/${editionInfo.editionSlug}/${slugifiedSpeaker}-${slugifiedTalkTitle}
date: '2023-09-21'
title: The Project Template
author: Krzysztof Zabłocki
video: 9KOnO77msU8
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/9KOnO77msU8.jpg
slides: ''
tags: []
year: 2023
conference: swift-connection
edition: september-2023
transcript: >-
  Hello, so yeah, I do a lot of open source.

  Over the years, I did over 20 open source projects that are available on my
  GitHub, and they're used by over 80,000 teams, including those at Apple,
  Airbnb, Disney.

  I hope a lot of you use it as well.

  The thing I'm most known for is Sorcery, but it's actually not the most
  popular project I have.

  There are a couple of projects that are cloned way more than Sorcery, like
  Difference, for example, which I'm gonna mention.

  And I have led the New York Times for over six years.

  So today, it's gonna be interesting because in May, I decided to stop doing
  full-time gigs for a while and just focus on consulting only.

  And as I moved into that transition of having more free space and exploring
  indie work again, outside of consulting, trying to find the right balance,

  I've been working on a lot of different projects, my own projects, but also a
  lot of client projects, and I started to look at the kind of frameworks,
  techniques and workflows that are the same across all of the projects that I
  work on, regardless of what architecture they're using, whether it's DCA,
  SwiftUI, MVVM, it doesn't really matter.

  I try to find the common points.

  I'm actually building a video course about this stuff, so today is going to be
  very dense, only have half an hour, so I'm going to talk about my favourite
  things from the whole community of Coco.

  So we'll see some of the tools that you probably use, but some of them I hope
  will be new to you and you can explore and learn and hopefully make your life
  a little easier as we go.

  So what we're going to cover is project organisation, the standard build,
  well, not standard, but build tools, the work flows around bugs and debugging
  our application, improving iteration speed, better testing and a couple of
  tools that I want to mention that I find useful in day-to-day development.

  So let's start with project organisation.

  So we have a lot of options.

  The three most common ones, we can use Swift package manager, we can use
  CocoaPods or Cartage.

  It's surprising but if you look at the statistics, CocoaPods have not
  dwindled, actually since

  Since SPM was released, Cocoapods has been growing and growing, but my
  recommendation is to use Swift package manager whenever possible, first off
  it's a default that Apple gives us which isn't necessarily a bad thing, but it
  doesn't have to be the right thing, as you will see in this talk, there's a
  lot of things we could do different, I think SPM is very useful, for a couple
  of reasons, my favourites are the fact that it forces you to modularise your
  application, and that means it will force you to have better boundaries
  between different features and different APIs.

  And I think it's really valuable because it's easy, very easy to write code
  without thinking about data modeling.

  But when you have to be explicit about what's public, what's internal and
  what's private, that forces you to make the right choices and spend a little
  bit more time thinking about what makes sense and what doesn't.

  It also will lead to better API for testing because the less public interface
  we have, the less tests we have to write and the tests will be more
  maintainable in the long run.

  And I would push it to the limit, so if I use SPM for organisation, I won't
  have almost no -- like I basically won't have PBX project files other than the
  root file, and I will do that by creating a module called app feature in my
  SPM definition and I will just embed everything into that.

  So then the PBX project file is simply just a host for that one thing.

  That means that every merge conflict that you had to deal with in the past,
  it's pretty much gone and that's really nice.

  It also forces you to modularise by feature, which is something I have been a
  fan of for over a decade.

  I know some people like to organise code by role, so like view models
  together, views together, models together, especially in Java world, that's
  also apparently something that's popular.

  I think that's a mistake, because when I have to change view, I usually have
  to change the model as well, so I would have to jump across the whole file
  system.

  So the SPM approach is really nice, it will also make it more possible to use
  Swift previews and preview apps which I'm going to mention.

  If you don't modularise your Swift previews it probably won't work, so
  definitely SPM is my default.

  And the thing that people forget often times is that package Swift is a normal
  Swift file outside of the fact that it's sandboxed so you cannot access
  external things.

  But because it's normal Swift we can add conveniences for ourselves.

  So if you don't like some of the API like myself, I don't like repeating
  myself, I have this extension, for example, single target library, and I just
  write the name once rather than the default with Swift is have to duplicate it
  every time, and the same with the dependencies,

  I have a set of common dependencies that pretty much all my frameworks use, I
  automate it,

  I don't write it for every definition, it just makes no sense, so definitely
  leverage that fact.

  With build tools, there are really three standard ones, which most of you
  probably use, like

  Swift and Swift format by JP and Nick Lockwood, and the reason for those tools
  is simple,

  If I'm sending a PR for code review, the last thing I want to know is this
  doesn't follow our style, this is a waste of time for the reviewer and for
  myself, if there's a style,

  I don't really care, I could not care less, make the tools automated for me,
  just make it match whatever the team decided because consistency is key.

  Sorcery is something I wrote, I just hate repeating my code over and over
  again, that's why I would use it.

  The thing with Swift Lint that I don't see utilised as much as I would like to
  in some of the projects that I worked on is it supports custom rules.

  And I see people sometimes have two or three rules, things like don't use
  HTTP, use HTTPS, but I really like to push it, so if I'm using a project with
  TCA, one of the common issues that a lot of developers do is when they use
  view stars, the view star implementation in

  TCA internally removes duplicates, but people forget about it, so they chain,
  remove duplicates at the end, that's just performance cost.

  I write custom rules for everything. I have projects that have over 30 custom
  SwiftLint rules and I would highly encourage you to write your own. Because if
  something comes up in code review over and over again, it should be automated.
  It should not be something that humans have to write. So definitely would
  leverage that. With sorcery, it's the same story. A lot of people that
  actually use sorcery use the bundle template that I provide with it. But
  that's not really where the power comes in. That's useful for mocking and
  stuff.

  But write your own templates.

  There's a lot of templates that companies use for their own architecture.

  For example, Airbnb scans all their frameworks, which is in thousands, and
  finds classes conforming to a specific protocol and then auto registers us in
  the system.

  Macros cannot do it, sorcery can.

  The same with example here, when I have enum with associated values, I cannot
  use that to case iterable for the UI, but I can use sorcery to generate a kind
  enum, which is basically a sibling of my original Enum that I can use for
  building custom UI.

  So definitely leverage that, Sorcery has automatic demon mode, so it's really
  easy to write it, and there's Sorcery Pro you can use to get an easier
  workflow.

  The way we integrate those build tools matter a lot, so some people would
  integrate Sorcery as a build phase, and even though it's my tool and I like
  when it's running in projects,

  I would highly discourage that, because the third party tools that we
  integrate, they

  So, I don't actually have to run every time, and especially if you do
  incremental builds, you'll pay the same cost.

  So Apple optimises your incremental build, but the external tools will not
  know that cache and it will have to rerun the same.

  So for example, running a couple of tools at the New York Times took six
  seconds per run, including incrementals, and I would run two to 400 times per
  day, that's my iteration change.

  90% of the time, I did not need to run those tools, and it added to hours over
  time.

  I actually added for the company, when we had 30 engineers, we added to nine
  hours wasted every single day just running third-party tools we didn't need to
  run.

  So my recommendation is to do it as a pre-commit script.

  I have an article where I show you exactly how you could script it.

  And this is much more convenient, and it's going to save you a lot of time.

  When we look at bugs and debugging, there's a couple of areas.

  So the bug reporting, avoiding leaks preemptively, creating debug settings so
  that your QA and your engineers can put yourself in a specific scenarios that
  are not production, and then doing pixel perfection because our designers love
  to point out that this is five pixels off from the edge.

  So first of bug reporting, there are two tools that I use most of the
  projects.

  It's either Instabug or Sentry.

  Instabug is really nice.

  The one beef I have with Instabug team is they said they're not planning to
  support Catalyst.

  So if you're using Catalyst, you cannot use Instabug.

  It's very easy to replace Instabug, because what you can do is you can use
  SwiftUI to build your custom reporting for Sentry.

  The reason why you want to be able to provide users ability to report bugs and
  suggest improvements is because it will prevent bad word of mouth.

  You don't want to have situation where someone writes a tweet about how your
  app is slow or it's hanging and it gets 500,000 impressions, which is what
  happened with the browser company at some point.

  So you want to avoid that.

  You want to give the user ability to easily contact you without hitting the
  app store reviews.

  And also, it gives you more context to figure out why the book happened in the
  first place outside of the metadata that you're already tracking.

  Another thing that you should be doing is avoiding memory leaks.

  And the problem is with the tools that Apple gives us, they're not preemptive.

  So the tools like MemoryGraph Debugger, you have to think about running them.

  And then, let's be honest, we don't run them with every release.

  We don't run them very often.

  So what happens is I didn't have memory leaks, user crashed, or I had many
  users crash because memory ran out, and I decided I'm going to use memory
  graph debugger, and now my diff is massive and finding those leaks is actually
  very hard.

  So rather than doing that postactively, the lifetime tracker, which is an open
  source project I built many, many years ago, it uses very simple principle for
  most applications, you are able to define how many classes or how many
  instances of a given class or an an object can live at the maximum, for
  example, at the times we had caching for articles, articles were web views, so
  very expensive, but we only pre-cached up to three articles, so if there was a
  fourth article in memory, we knew we leaked one of the previous ones.

  So this tool is very simple, we just define three is the maximum, and then if
  ever in memory there is four, okay, we had a leak.

  And it works as you develop, it's constantly available in your application,
  you are working on something else, you're just navigating through your
  application, boom, there's a leak, you get information and you can find it in
  a much smaller diff.

  So very useful for custom applications, the open source version just uses
  numbers, but for a lot of clients what I did is I bound it to the data model,
  so I can write rules against the data model, so if in the database I had ten
  websites and in memory I had 12 website controllers, it means something was
  leaking, so I would recommend either doing a custom one or you can reach out
  to me and I'll build it for you.

  Another tool that I built a while ago that most people don't realise because I
  release too much stuff is automatic settings.

  So every single app I have worked on over the years needed some kind of way to
  have debug settings.

  So being able to override my authentication so that I don't have to log in or
  change the paywall counter so at the times we only could read five articles
  before logging in, but

  As a tester, as an engineer, I want to test up to 20, I just don't want to log
  in, or

  I want to change animation speed, stuff like that.

  We all have apps that do this stuff.

  I don't want to write that UI, I don't care about the beauty of that UI, it's
  not something that users actually use, it's something that's only used
  internally.

  So I wrote this simple framework, automatic settings, and the code you see on
  the left is basically the code you get to execute, and then all the UI on the
  right is fully automated. There's zero code that you had to write to get the
  UI for it. So, Sourcery will generate a property grid implementation that lets
  you mutate all the data, which means when I integrated that at the times, it
  removed 5,000 lines of custom UI code, and it made it so that if the product
  team or engineers want to expose extra controls, they simply define the data
  and they're done with it, they build the project, the UI is already there.

  So massive amount of code being saved and you don't have to maintain this, you
  don't have to test it, it's all done for you, very conveniently.

  Another thing that often happens is I personally work in simulator a lot,
  probably like 90% of the time I work in the simulator, I only use device if
  I'm using specific APIs, like

  If I'm working with ARKit or I need some graphics stuff, then I would use the
  device.

  Most of the time I try to avoid it because of the iteration cycle.

  I don't want to wait for my device to launch and do all this stuff.

  So I only run on device every now and then to check performance and things
  like that.

  So simulator that Apple gives us is great, but there is a rocket sim written
  by Antoine.

  It's a premium tool, but it's not very expensive.

  And it gives you a lot of control.

  It gives you overrides for the standard system stuff, so you can change the
  dynamic type, you can reduce motion, all this stuff.

  But it also shares a couple of other apps that existed in the past.

  For example, there was this thing called Uber Layer, where you could compare
  your designs against the actual designer mock.

  So this does really well, because it integrates it at the simulator level, so
  you can copy the image from Figma, and then you can compose it on top of your
  simulator, perfectly aligned, and then you can just see if it matches or not.

  It also does something that is so trivial and used to be available in the
  system, which is network link conditioner that for some reason is no longer
  the default.

  You can simulate airplane mode without having to turn off network on your Mac,
  which is the Stack Overflow answer when people ask how do I test airplane
  mode, just disconnect your Mac.

  That's not very convenient when I want to read Stack Overflow as I develop.

  So consider buying this.

  It also supports screen recordings, but unlike the standard quick time or
  simulator one, you can add a lot of conveniences, like you can add the device
  bezel, so it looks much nicer.

  I highly recommend it, it's really nice.

  And when we talk about iteration speed, we're talking about time it takes from
  the moment

  I change my code to the moment I can verify if my code actually makes sense or
  it didn't fix what I thought it did.

  So I want to shorten that loop.

  I want as quick loop as possible because it makes me connected to my code,
  especially if I'm working on UI, UX, this is really something I don't want to
  wait and wait and wait.

  This used to be much faster in Objective C, it's getting better in Swift
  nowadays, but you probably remember how slow it is, or how slow it was until
  recently, it's getting better.

  But there are three things that I use to make it even faster for my own
  projects and client projects. is building playbook style interfaces, and
  playbook is basically this idea that you take all your screens in your
  application in different permutations, so if I have an authentication screen I
  can be logged in, I can be logged out, I can have errors because my password
  is different, and I generate this one single app that hosts all of those
  variants.

  So I can very quickly review if the design makes sense, if I didn't break
  something, if I'm changing something fundamental in my design system, I want
  to quickly verify that actually works very well.

  And so there's two frameworks that are very useful for that.

  One is Playbook iOS and the other is Prefire.

  The same idea, the biggest difference is Prefire uses sorcery and also uses
  your existing SwiftUI previews.

  So if you already use SwiftUI previews, it will take it and generate all the
  snapshots that's for you fully automated using sorcery and it will generate
  this view also without having to register anything.

  This playbook, it's a little more mature, there's more contributors to
  playbook, but it requires you to create your own scenarios, so it's a little
  more work on your side to integrate it.

  But definitely worth checking out, it also makes your designers a lot happier,
  because you can just send them this playbook application and they run it and
  they can quickly verify that everything matches.

  The same with QA.

  Another thing that I often do is because I organise with SPM, this enables the
  idea of preview apps.

  And a preview app is basically a target that only has a single file, which is
  my host, and what I do is I import the module that I care about to test or
  iterate over, and

  I just launch it.

  And that means that I only have to rebuild that target and its chilled
  targets, but I no longer have to rebuild my whole application.

  So if I'm in a focus mode working on one piece of the application, like, for
  example, with the browser company, there is this idea of home, which is like
  your downloads, your archive, all that stuff.

  I had a preview app and I could launch immediately into home view without
  having to build my sidebar, without having to build a bunch of other features
  we had because the code base was really big.

  So it's a very quick way of actually jumping straight into a feature.

  You can also set yourself up with a custom version of that feature.

  What I often do is when I'm hosting my module, I will add a top bar and each
  item in the top bar will be a different variant.

  So I'll be logged in, I'll be logged out, I'll be on a different profile, and
  that makes it much faster to develop.

  But it's still not as fast as it could be, because anyone with experience with
  Flutter or React or any kind of web stack, to be honest, uses hot reloading.

  This is like a standard, has been a standard for years.

  It was even available back in iOS, not iOS, back in Coco development many
  years ago when

  Xcode had edit and run button, Xcode 3 or something, very old, probably older
  than most of us.

  The idea of hot reloading is very simple.

  I save, I do changes in my file, I save it, it should just update.

  Very simple, apparently something

  Apple have never heard of.

  I have no idea why.

  So in 2014, after Apple released Playgrounds,

  I built Objective-C Playgrounds.

  And that was already supporting hot reloading in Objective-C and Swift using
  Dicey, which was a framework that was used back then.

  Nowadays, I use this thing called Injection for Xcode.

  And two years ago, I think it was two years ago,

  I open sourced this thing called Inject, which is a very simple framework that
  enables hot reloading across all of Apple's stacks.

  So you can do SwiftUI, UIKit, AppKit, you name it.

  And what's really cool about it, the integration is really simple because it
  becomes a no-op in production.

  So as you develop, you get hot reloading capabilities.

  And it works with value types and everything else.

  So it's much more stable than it used to in the past.

  And you don't have to remove that integration code, because in release mode,
  it's a no-op.

  So what you can do is you work on your application, just do normal stuff.

  And you realize something is wrong, like the title is wrong or the layout
  seems off.

  Rather than having to restart your application or go and find a preview or go
  and find a snapshot, you just change your code and you save the file.

  And this is an example of it.

  You just save the file, and it's updated.

  Regardless where you were, even if you got one date-- you know how hard it is
  to reproduce bugs related to data.

  Sometimes you just get weird data, and you can never reproduce it again.

  So as long as you're working on simulator and you're developing, you can
  always modify the code.

  You never have to remove it.

  It's extremely useful.

  And once you start using code reloading, it's really hard to go back.

  I've been using this technology for 10 years, so it is very stable. it saved
  me a lot of money and a lot of time.

  Let's talk about testing.

  Testing is something I'm a big proponent on.

  I think we don't do enough testing in mobile yet.

  On a lot of other stocks, it's more mature.

  I think a lot of people think that testing is not worth it.

  I think that the reason a lot of people think testing is not worth it is
  because they use empty patterns and they create tests that are not
  maintainable.

  And I think that if you do testing when you have a small team, you will
  actually benefit more than a big team does.

  Because with big companies, when I work with Fortune 500, they have dedicated
  QA teams.

  So they have people that will make sure that before we release this
  application to App

  Store, it's actually solid.

  If I'm working alone or I only have a few people, it falls on to me and other
  engineers to make sure that we didn't screw up and we are all humans and we
  will screw up.

  So I want to avoid having to have that burden on me to make sure I didn't
  break something

  10 levels down the road in the hierarchy when I was working on the first
  screen.

  So there are three main things that I use.

  First off, snapshot testing, which is a point free library that I really like.

  It replaces Facebook snapshot tests that were popular a few years ago and
  Facebook as usual archived and didn't support.

  It's multi platform including Linux, it supports all the frameworks you can
  use at Apple, but

  It also supports testing not just screenshots, which is really nice.

  What you can do, for example, if you use GRDB, which is SQLite wrapper, one of
  the best open source libraries out there, by the way, if you want to deal with
  SQLite, it has support for snapshotting migrations.

  So you can write very easily, write tests that verify that your database
  migration worked correctly.

  So highly encourage that you use it.

  It's really easy to use.

  The tests themselves are really readable, really there's nothing bad about it
  other than your repo size will grow because a lot of images in repo just means
  larger repository, fortunately it shouldn't be a problem for most of us.

  I mean I'm biased because I have a good network, but I hope you guys do too.

  Another tool which is actually my I think most popular project is called
  difference,

  I wrote this when I was creating sorcery, because I hated how when you have
  complex objects in your XCT assert equal and you try to ask Xcode to verify
  that this object matches this object, it will just do what it does here on the
  screen shot.

  Throw me a wall of text printing all the variables for each object and hope
  that I somehow have a scanner in my eyes and I can figure out what's wrong
  between those two walls.

  That's not really how I work, I might be getting older, it's really just not
  the way TDD should work, TDD should have very quick iteration cycles, if my
  test fails, I immediately want to know what's wrong, so I can go and fix the
  implementation.

  So I created this, this is just using mirror, and what it displays is at the
  bottom, which even with a very complex object, dictionaries, arrays, all that
  stuff, it will find the exact property that's different.

  And here it says that the stomach carcinoma value is different.

  And I don't need to scan anything, I just look at the bottom of the stack,
  okay, this is wrong, I need to go and change my implementation.

  So it's really convenient.

  There is another library that you might explore which does a similar thing,
  it's newer, which is point free log dump, and that does something similar,
  different presentation.

  I like this because I wrote it, I've been using it for a long time.

  I'm biased, sorry.

  For testing, if you do UI testing, that's the hardest testing you can do, in
  theory at least.

  I highly encourage that you use page object pattern, if you want to learn
  more, just search for page object pattern, there's plenty of resources for it.

  In short, rather than doing your UI tests, like when you write UI tests, you
  don't want to look at the elements and search for labels and all this stuff,
  you want to write a higher order abstraction on top of each screen you have.

  For example, if I have authentication screen, I will define my object first, I
  will hide all the implementation detail, how that is actually designed in that
  screen, and then

  I would create chainable interface, so when I write my test, my test read like
  this.

  So I can read, okay, so what I wanted to test here is the login has valid
  credentials, I highly recommend using snake case for XCTest, because when you
  have a lot of tests, it just read much more -- it's much easier to read. I
  know it's not standard Apple way, but I have to mention that. It just works
  better. I have thousands of tests in my apps.

  So I can read my tests, and it's like, okay, so I create authentication
  screen, I type in my email, my password, tablogin, and I expect it to succeed.
  Very readable. Do I know how the design looks? I don't. The benefit of that is
  I have hundreds of those tests.

  If I ever change the authentication screen layout, I don't have to touch any
  of my tests.

  I just go to my page object pattern implementation and I change those details
  there, all my tests still pass, and that's the key, because with TDD you go
  red, green refactor, but every time you change implementation detail, if your
  user stories didn't change, they should never go red, so that's why you want
  to do this, you don't want to modify your test.

  If you have to modify your test every time you change implementation, that's
  an anti-pattern and that's why you probably don't like writing tests, so
  highly discourage getting to that point.

  And there are three other libraries that I really like, which is Pulse,
  Proximan and

  SwiftUI introspect.

  So Pulse is a framework and there's also a Mac application, which is like a
  premium, it's still in beta, so you can still access it for free, but it's
  basically a logging system.

  And it was designed for networking, but it's actually a general purpose.

  So you can integrate it with your own models, with your own logs, and it looks
  amazing,

  It's one of the better looking community things I have seen.

  Much better than most of my tools because I'm absolutely terrible at design.

  And it's multi-platform, supports Aura, Apple platforms, doesn't support
  Linux, but it doesn't really matter.

  It's built with SwiftUI as well.

  And you can use it for free, so basically when you integrate Pulse, you can
  always pop in the console in your application and then you can get the premium
  app for Mac, so you can connect remotely.

  It's very convenient, very powerful. is much better for networking, and it's
  kind of amazing, I used Charles in the past, but

  Proximan is really good.

  When I was researching my video course, I was looking at the different tools
  and what they can do, and everything can do SSL proxying, Charles and Proximan
  do that, but with Proximan you can do stuff like filtering, you can do GraphQL
  debugging, I can break point on a a specific GraphQL request and react to
  different params, I can write JavaScript logic to reply with different fake
  files, and what you can do, because it's in the middle, you can do that, most
  of your requests hit real server, you get real data, but if you want to
  simulate a specific scenario, you can say, if this argument was passed, I want
  to fail or provide this weird data that's malformed, just to verify my
  application handles it, it's really really powerful, it also looks very nice.
  So I highly recommend trying this tool if you do any networking in your
  application, even if it's offline first.

  And the last tool that I framework really that I always use in the last, I
  think, three years is SwiftUI introspect. As much as I like SwiftUI, and for
  me SwiftUI is the default for most things I do, the API is just very limited.
  There's a lot of things missing.

  If anyone tried to use video player in SwiftUI, you know that people at Apple
  don't often think about what you want to use.

  So there's almost no API you can use.

  So the thing here is you can use the view representable, but if you use view
  representable you have to replace the whole implementation.

  So it's not like you can use view representable and just tweak one thing, you
  have to rewrite the whole video player.

  Whereas if you use introspect, it gives you access to underlying components.

  So the way SwiftUI works is the SwiftUI definitions get changed into labels,
  AV video player controllers, all those different things.

  And rather than having to rewrite everything from scratch, you can just do,
  okay, well, for this iOS version, because it changes across versions, which is
  always a pain for us to maintain, but for this thing, if I have a navigation
  view, I actually want to change the background colour for my bar.

  And you can do it with two lines of code rather than having to replicate
  everything and maintain everything.

  I found it extremely useful when I was developing Sorcery Pro, because I
  needed API that Apple just didn't give me, even though it was available in
  UIKit.

  So I would use that in every project for now.

  It also doesn't use private API, so you don't have to worry about being
  rejected.

  And recently they added ability to specify iOS versions, so you can be more
  explicit, because there might be a difference in how the Swift UI definition
  is represented on iOS 15 versus iOS 16. So this deals with that. And the thing
  is, the Swift UI version is bound to the system, so if you test it on that
  version of the system and it works, it's not going to break. You don't have to
  worry about that. So there's a lot of risk in using something like this. So in
  summary, I always say, don't count on Apple, don't count on defaults. We have
  an amazing community, there have been a ton of tools and frameworks created
  over the last 12, 14 years, actually 16 years, 2008 when

  I started with the private Apple SDK and SIGWIN.

  So 16 years almost, and there's just so much good stuff you can use.

  If you want to search for more tools, there's this repo called awesome iOS, at
  least hundreds of different things you could be using, different variants of
  the same tools, completely different approaches.

  I would highly encourage you to try new approaches.

  I know we are often stuck in the rut and we have a workflow that we feel works
  for us and we don't really want to get out of comfort zone.

  Some tools might not work for you, some tools might not be maintainable in the
  long run.

  I have rules that I follow for my tools that they never cancerous, you can
  always easily remove them, stuff like that.

  But even if one tool works, it could save you hours per week.

  Hours of time is a lot of time you could be spending with your family, you
  could be enjoying your other passions and not stuck in front of your Mac and
  being annoyed that things don't work. I write about this stuff on my blog and
  Twitter, sometimes, mostly blog, and I'm going to launch a video course soon,
  so you can follow me there. And I'm available for consulting, that's pretty
  much all I do right now, which is help teams be more efficient.

  And those are my contact information, and I'm open to questions. Thank you.

  Thank you, Christophe.

  >> So we got some questions.

  The most specific one is about your rules.

  Are they open source?

  People can grab them and get inspired or use them?

  >> They are not open source because they are project specific.

  They are pretty simple.

  I might share some after when I get my laptop.

  Didn't take it with me here.

  Yeah, I try to-- the thing is, people use defaults for source tree, for
  SwiftLint, stuff like that.

  But those tools really shine when you take your project needs.

  And the way I build those rules is really simple.

  If I see the same comment in my PRs, it means it should be automated.

  If it's the same pattern over and over again,

  If you have to point out, oh, this is not how we do things, you might not
  deprecate the API, because for some reason, it might still be needed.

  But you can write a Swift linter role so that the next time it happens, you
  don't have to be the bad guy.

  That's the thing.

  The linters become the bad guy.

  I don't need to be the one saying, well, this doesn't follow our best
  practices.

  I can just make it-- as a team, we decided this is best practice, and the bot
  is the bad, bad thing, not me.

  We have a question from Woody.

  And what's the future of Sorcery with Swift macros?

  >> I'm not worried.

  Sorcery just enabled Linux support.

  There's a lot of workflows that Sorcery offered that macros simply cannot do.

  Like the example I mentioned with Airbnb, when they use Sorcery to discover
  types conforming to a protocol across the whole code base, you cannot do that
  with macros.

  There's also a bunch of limitations and bugs with macros right now.

  One of the limitations is due to the fact that macros use visitor pattern,
  which is how Swift syntax parses your code.

  And you have to be really careful, because with visitor pattern, what that
  means is if you have your type definition and you're building a macro that's
  supposed to know all the variables or all the functions, and you do any
  extension outside of that definition, that will not be available to your
  macro.

  And there will be no compile warnings or errors.

  You simply won't have the code.

  So be very careful.

  That's not the story with Sorcery, because source tree, before it runs, it
  builds the whole project AST, so if I have a file with 20 different file
  extensions, it will concatenate everything and when you run your template you
  have access to everything at once, which with macros it forces you to have
  this massive file, which is something like in the browser company we had TCA
  architecture and some of our state objects were actually using 10, 20
  extension files, so with macros that would be problematic.

  A bit of topic question is about the tools you make.

  There is many issues in many open source ecosystems, like libraries made for
  JavaScript that actually are the basics for most of all JavaScript packages.

  And those maintainers are not getting paid at all, or just a few. and they
  actually create the modern web.

  How do you relate to those issues as a maintainer?

  Oh, yeah.

  This is a real problem.

  So maintaining projects, it's work-- like, it's a full-time job in itself.

  I have over 20 projects.

  I rely on community.

  A lot of people contributed to those tools, which is also something that's
  really important, because I don't want projects to go under.

  If I ever get hit by a bus, or so you will live.

  There is now, I think, around 100 people that contributed.

  There's probably like 15 people having maintainer access so they can release
  new versions.

  The guy that's working on it right now, the Linux support, amazing.

  He's doing an amazing job working on it.

  Free sponsorship from people doesn't really work in my experience.

  When I had GitHub sponsors, in the 10 years

  I was open sourcing, I got like total $500.

  So that's very far from the amount of hours

  I spent for community staff.

  When I did Sorcery Pro, it's a paid application which costs $20, and it adds
  custom editor for Sourcery.

  It also adds Xcode extension, which lets you do a lot of really cool stuff.

  You can watch it on my website.

  I made around $30,000 from that.

  So that's not bad.

  I worked on it a month over time, but obviously, Sourcery, I worked for years.

  Pulse is doing something similar, where you have the default open source thing
  free, and you can buy an application that's empowering you to do even more.

  So that's one model of doing it.

  I recently got sponsored by Bumble.

  So they gave me $1,000 per month.

  Airbnb sponsors, I think, $100 per month.

  Airbnb has been doing this for a long time.

  It's not a massive amount of money, but it's decent.

  I started blogging doing premium articles as a way to monetize some of that
  and also have more time for doing this.

  So if anyone wants to support the kind of open source work I'm doing, my blog
  has premium articles for people that pay, I think it's $10 per month or $9 or
  something like that if you subscribe for a year and you get access to premium
  content, you can understand how to write your own tools, stuff like that.

  But yeah, in my experience, you have to give something if you want to get
  something from people.

  Unfortunately, even though when the tools save you, like Sorcery saves a lot
  of time for people.

  But I understand not everyone can support it.

  So yeah, I generally give incentive.

  Like with my blog, people that pay premium get access to a lot of interesting
  stuff, especially around TCA.

  I got a lot of people interested in my writing because I chained, like I
  affected how TCA works now.

  So yeah, try to find ways to monetize your writing or ideas without
  restricting the main content as well.

  It's important for me, I want this stuff to be free.

  - Okay, nice.

  Very specific question as well.

  How does Pulse compare to the OS log feature?

  - US what, sorry?

  - OS log.

  - Oh yeah, I mean, it's much more nicer.

  The other thing is it's designed for networking, so you get a lot of custom UI
  with a lot of details.

  It's just better designed for those kind of stuff.

  OS log is too general purpose, so that's obviously just gonna be very raw logs
  instead of having this nice and polished experience.

  - Performance wise?

  - I mean OS lock is gonna be faster because it's using static strings and
  stuff.

  - Thank you Christophe.

  - Thank you.

  (audience applauding)
allow_ads: false
