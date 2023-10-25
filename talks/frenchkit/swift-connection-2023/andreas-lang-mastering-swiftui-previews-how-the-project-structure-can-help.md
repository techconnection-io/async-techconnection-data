---
slug: >-
  /talks/frenchkit/swift-connection-2023/andreas-lang-mastering-swiftui-previews-how-the-project-structure-can-help
date: '2023-09-21'
title: 'Mastering SwiftUI Previews: How the Project Structure can help'
author: Andreas Lang
video: 0yUdC_PawYo
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/0yUdC_PawYo.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/3cc1b32396b74cc7aa27ddc1fc74ddea/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: swift-connection-2023
allow_ads: false
---
Hello, my name is Andreas Lang and I'm a senior software architect working at
NVW. So let's start first, what is NVW? We are one of the biggest German energy producer and supply company but we are not only working in Germany maybe it's more interesting for you we have also subsidiaries in whole Europe or some countries in Europe and even in Turkey. If you have an electric car you might know our app Mobility Plus in which you can find more than 100 more than half a million of charge points in 17 countries in Europe and you can then charge electric vehicle there and pay with it.
With that app we have more than 100,000 monthly active users.
Where do we build all those apps?
Well this one and others, in the NBW Centre of Excellence mobile.
It exists since 2009 and in the last 14 years we have built over 100 apps. for the public app store as well as company apps in the custom app store.
Obviously we started back then with UIKit and our architecture that we then took over after some years was Viper. I'm not sure if you're still familiar with that architecture. Here I have on the right side a little architecture sketch that you have there, the view, the router, the presenter, the interactor and the entity.
So it's a...
Therefore the name comes from.
And we also always saw that we have a clean architecture approach in our app so that the domain and data layer is divided from the application or UI layer.
When SwiftUI was introduced four years ago, we directly start or tried to start to adopt it in our apps, and the first thing, because we knew it already, was to do it with Viper.
But as you see with the bump there, it didn't really work out, because the views and the navigation and the view models in SwiftUI work a bit differently than in UIKit, and we also have something else in the app, in SwiftUI, we have previews. when you open a new file and say you want to have a SwiftUI view, Xcode gives this template where you already have the preview inside.
Now in my projects I hear from the developers there are a lot of prejudice regarding to previews.
They say, ah, previews break easily because, for instance, in this example when you put
There are now some parameters in the view.
You also need to put the parameters in the preview, and so on.
They say, ah, it's so slow.
They always reload, and they don't show really the results, because there are many instances of the app.
And depending how you do the preview, they even make an APA calls or database access.
And if you have errors in the preview, it's also hard to trace.
But I must say, at least in my experience, in Xcode 15, they improved that.
You have now a better error code, or you can better see where the error comes from.
So because of those prejudices, I see in a lot of projects that the developers just do that with the preview.
So they comment it out, or even remove it at all. which is sad, I would say, because previews give a lot of advantages.
You can see the view in all variants, like in the different colors came, dark and light mode, the orientation, and also even more important in the dynamic types that the system offers.
I think there are 12 different variants of dynamic type, so all the text sizes that you can have.
All these three variants you can directly select, even since last year in Xcode.
You do not need to change something in your preview, it is just in the bottom, in the configuration of the preview that you want to have a different variant of your screen.
At least in my experience, previews are also faster than building the app, running the app, navigating to the screen that you just want to see, and maybe even change some states that you have the screen in the way you want to see.
Let us come also to the super goal for the previews that I see.
It is easy to have all possible states and X traces, and also the impossible ones, because I also see in the code this comment, this should never happen, and therefore you do not really check it anymore, but probably it can happen, and maybe you should want then also a preview or that the screen handles this state in a good way, and therefore you should also check it in the preview.
How can we achieve this goal?
The first point is reducing the complexity that makes,
Make the view small and therefore also the preview small, and then they build also faster.
You can do that also by separation of data and logic.
It is also good to make the data easily mockable, and the logic preferably optional, so that you have in your preview that you don't need to make this API calls or this database accesses.
And also one point that I always like is to only use primitive types in views so that you can in the preview easily use string, bool, integer, doubles.
Let's see on a simple view, I called it, how that would work out, because I like to have simple views that are combined together, like Lego blocks, to a bigger view or to the screen then.
Let's start with a simple view.
Here I have the preview of it, like let's say an app where you want to check in the places that you are, the cities that you have been.
You see here you have been in Paris,
The first one is that you have been there, the second one that you have not been there.
And the code of it would be like that.
You have some parameters, name, country and visited.
And then a closure, what happens when you tap on the button.
And the button is this map pin there on the right side.
So for that, to do the preview, it is relatively easy. you have those primitive types, you can just write the strings and the only difference between those previews is the visited, so you can also just have both variants of this screen with visited true and false.
And for the preview you don't need to have some action on the button, so you just set it to nil.
You can even improve that preview, this view, and then also the preview, because when you have several parameters of the view, now we have only three, but when it gets more, maybe it would be better to move those to a specific model.
Let's do it.
Now, on the right side, you see now we have the city model, and that we use also in the view and we can even make an extension on this model, kind of for preview where we have a static function with standard parameters.
And then in the preview, as you see in the bottom, we just need to change now this one standard parameter visited true or false.
True is already the default, so we can set it just to false and it also reduces the code on the previews.
What do we do now with all the simple views when we would want to put them in a screen with real logic?
Let's see what Apple says about it.
Because Apple says the best way to build an app is with Swift and SwiftUI.
But then when you check their example apps or the videos, they don't really say more than that.
At least I never found an example in the last four years that really says how you should to do the architecture, that you have good previews.
There was only one video, I think it was three years ago, where they say a bit of structuring the app and to use the previews, but it only worked in a simple example.
I tried it with a bigger app and it did not really work out anymore.
And I think also now SwiftUI advanced in the last years and this example does not work at all.
We had to come up with our own approach.
So, with the architecture, one thing that I also mentioned before is to split up the app into different...
With clean architecture, we have the data separated from the domain, so the data has the repositories and DTOs and entities that we have as a Swift package, and then the domain layer we also have in the Swift package as the model and the service.
And then it comes to app layer or the UI layer.
And obviously this is just...
We don't have only one domain package or data package, but for each feature another one.
And in the app UI layer we have now...
It was our approach.
We have the logic that can be optional.
So with dependency injection we can say for the previous we don't want to inject it and in the production app we want to inject it or we can even mock it because we can say with a dependency injection for the preview we want to have a mocked logic so maybe we don't have to have the API calls there but just directly static data.
Then the logic changed the state.
The state updates then the view, and the state is also in the view implemented that way that you can easily mock it.
The view gives an action to the logic again.
This is kind of Redux, or similar also what we saw before with the TCA architecture.
But we only do that for each view separately, we do not have one state for the whole app.
Because that seemed a bit too complex in our use cases.
So let's already come to an end.
What are the takeaways that you should take?
How did I proceed?
Previews play an important role in development, at least in my development.
It is important that you use Swift packages, that you split up your code in Swift packages, that the build times are reduced, mainly also the build times for the previews.
That you have small and reusable views, and that you build larger views via the composition of smaller ones.
And also an important point is to separate the logic from the data, that you can mock the data and also mock the logic, or maybe in most of the previews you don't even need to have the logic.
And you should build the data flow from the app from bottom to top.
So SwiftUI previews with the right architecture makes development more efficient and, at least for me, makes fun.
[APPLAUSE]
Thank you very much.
Here you have my contact data with the email address and LinkedIn and Masterdont.
You can also find that when you scan this QR code.
It's also embedded there.
And if you have a question, please contact me.
About previews, you said that Xcode 15 runs notably better on SwissPreview.
Did you have any examples for that?
>> This is my experience, the error codes that it puts.
Before, I always had, or most of the time, when there was an error in the preview,
I had to go somewhere in the log folders inside the library folder to see the log of the preview.
Now in the last days I saw it when I had an error or directly in Xcode what was the problem.
For instance, when you have an environment set in your view but you do not set it in the preview, then you get an error because it is not there.
I think, if I remember correctly, now in Xcode it says that it is missing and before I had to check all these build or runtime logs to find what the error was.
Yes, SwiftUI is bringing obviously lots of questions regarding architecture.
Do you think at some point we will have some kind of main architecture that will rise where everybody will use this one with SwiftUI?
It is difficult because I think, let us see the TCA,
I think that is very complex, the architecture,
And it's good.
I think it's a nice architecture, but probably too complex for most of the apps.
So I think it depends a bit what is the use case of your app.
If it's a simple view where you maybe don't need really an architecture, I support it.
You always have to think about the architecture.
But you have the TCA, which is very complex, and maybe for some developers, or when you have bigger teams, or when your developers change also regularly because you have maybe external resources, then maybe it is also not the correct architecture.
I think it is depending on what you want to achieve.
>> We could call it MVC UI, which would be quite a good name, or MVVM UI.
>> I mean, also in your iKit you had, for instance,
Viper or other things.
Speaking about Viper, do you actually try it or even manage to keep a Viper architecture with SwiftUI?
>> I tried in a mixed app. There it was more possible, but in only SwiftUI app, I do not see it really, because then what do you do with the router or with the view model and what is the interactor in the SwiftUI?
There I do not see it.
All right, okay, thank you very much indeed.
- Thank you Andres.
(audience applauding)