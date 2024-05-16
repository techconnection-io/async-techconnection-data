---
slug: /talks/frenchkit-2022/thomas-ricouard-swiftui-at-scale
date: "2022-09-29"
title: SwiftUI at Scale
author:
  - Thomas Ricouard
video: tsZBLvdcoTw
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/tsZBLvdcoTw.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/talks/frenchkit-2022/thomas-ricouard-swiftui-at-scale/slides.pdf
tags:
  - SwiftUI
year: 2022
conference: frenchkit
edition: "2022"
allow_ads: true
---

0:00:21.4 Thomas: Hi, everyone. Today, I will talk to you about SwiftUI obviously, and how we use it at scale in the [Medium](https://medium.com) application. So, I will be like your SwiftUI salesman today. So why would you want to use SwiftUI? I have a very boring list of bullet points here, simply because, well, it's less code. Right? And more fun. So...

[laughter]

0:00:46.1 Thomas: That's really why you want to use SwiftUI. And if you didn't get it, I got one more slide full of bullet points, and yeah, it's

- Because
- It's
- Less
- Code
- And
- More
- Fun

But now that you get it, and of course, you got it because it was very explicit, I will get to some other very boring example. So exhibit A: "design and product, they come to you with a perfect application and the most beautiful list they've ever designed, and I tell you, yeah, please implement that, we want that. It's an app for FrenchKit and you do your best SwiftUI table you ever did. It's the best app you ever did. You use the most up-to-date UIKit API and I come to you a bit later on and tell you, "We might need some scrollable carousel at the top." And you're like, "Oh, I might do a `UICllectionView`." It happened to me for 10 years and... Actually that's not true since SwiftUI it didn't happen to me.

0:01:45.5 Thomas: But yeah, you're like, "Yeah, maybe I should have used `UICollectionView`." So with UIKit what you do, for doing that, you're setting up your nice `UITableView` using the flavour of the day. Maybe it's Delegate/Datasource pattern, maybe it's Diffable Datasource, maybe this new Cell configuration. You are making `UITableViewCell` with nice autolayout or xib if you're still like dinosaurs. You place everything by hand like drag and drop if you're really still using this or attributes, stuff like that. And you realize that the new design might be nice with the `UICollectionView` instead. So you write everything to fight your UI collection view, which not that much, but it's still a lot. And so not really like raising sheep somewhere else than in the iOS world. So like a good idea. With SwiftUI you can do this list in five lines and if you want to add this new section on top, you do five more lines and you're done. Just I left out the UI for the cell, but it's three more lines of code.

0:02:51.5 Thomas: Well, I have one more boring example for you. You want to do this awesome like Tinder for movies where you can swipe left or right. And it's very custom, you know that with autolayout it would be like headache: tt's not a list, it's not a... Yeah it's stack. Anyway, with UIKit you do that, you insert it to configure all your views. Add views like a hundred of lines of code of that. You add your autolayout constraint: same, you can use like something like autograph, maybe your own helpers, you wrote like many of them I'm sure, and or you can use this ASCII format. I have no idea how to use that. I just know that it exists and some people are very proud that they know how to use it. I never got around of using it. You have to run your app on multiple devices and you could, yeah, use `UIStackView`: it's actually very nice. It looks like SwiftUI, it's not SwiftUI. You can stack them different type of view within stack view or stuff like that. But it's still a lot of code. And with SwiftUI you can describe this view very simply. It's more than five lines of code, but it's still you can understand that it uses some `VStack` and `HStack` and some `Spacer` and you got this. And I have a screenshot of it running so I'm not lying to you.

0:03:58.3 Thomas: And you can add more preview, if you want you can preview it in dark mode, in light mode. You can preview it on an iPad, on a lot of different devices at the same time. Preview is working okay right now. So you got this.

0:04:12.3 Thomas: So this was nice, but why at scale then? Well, what I demonstrated with simple list and stuff like that it's what we use in the Medium application, it's full of SwiftUI and used by millions of people and we actually like write a lot of SwiftUI these days. We have ton of new features on SwiftUI. When Glose got acquired by by Medium, we made a new list feature and it's full in SwiftUI. So it's... You can make list of stories, you can create a list. So there is some text input and you can add stories inside, you can share it and all of that in SwiftUI. And it's really great because it was really fast to iterate and to make this. The recommendation screen: we wrote that very recently also, it's the list of entities.

0:05:12.6 Thomas: So we have some general SwiftUI code we can use with any entities, like topics, users, publications and well, it's only SwiftUI also, and a lot more. We wrote different parts of the app, the ID profiles in SwiftUI, your highlights... also recently we wrote activities, so all your notification, also in SwiftUI and basically it's some list, it's some input. And we also have responses which are in SwiftUI, which we actually have to work around the cable a lot but yeah, it's also like fully in SwiftUI for the responses.

0:05:37.6 Thomas: But it's not about SwiftUI, just for SwiftUI. So with SwiftUI we can take full advantages of SwiftUI packages. So when doing this new features in SwiftUI we move that to feature packages, and with that we get like much faster compile time. You can work on your feature isolated, have your preview running without compiling your whole application. We can just compile the activity features and without compiling the whole app. And we are happy, we're trying it on the whole application of course - or we can use SwiftUI previews when it works. It's much better in the latest version of Xcode. As I said before, less code, much less code: basically you can focus more of your time into like polishing and other parts of the code than just wiring up the UI together.

0:06:24.9 Thomas: It's much faster to make new feature because making change for previewing them like is saving a bunch of time we can use for other things. So of course, what I'm seeing here, not all screens and features are made for SwiftUI. So,

0:06:44.9 Thomas: Was it a mistake to have SwiftUI into Medium? Well [chuckle] 99% of the time, no. Sure, it's a little bit hard to test the framework. I am not there yet, we have to make some compromise some time on what to test and how to test it. SwiftUI is linked on the version shipped in iOS device. So once you have the simulator you also have to test on device. And sometime you have to test on iOS 14, iOS 14.1, 15 or 16, and you could get a little bit different behavior and you could have to use some work on, but it is getting much better and it's not that time consuming. [...] And I had to make this slide with a lot of mistakes, because if there was no mistakes, you would not believe me. And high-level components, like `NavigationStack` and `List` have a lot of _"free"_ behaviors. Like, if you make a `List` it'll have separator, it'll have dividers set on. It's okay, you can customize it now. It got much better in iOS 16. But yeah, it was harder to customize in some cases.

0:07:54.9 Thomas: So all in all, we're really happy with of course with using SwiftUI. And well that was a quick talk to tell you what we do at Medium with SwiftUI. Thank you.

[applause]
