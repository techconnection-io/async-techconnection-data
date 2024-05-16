---
slug: >-
  /talks/flutter-connection/2024/maxime-eglem-michael-ohayon-bringing-your-flutter-app-to-the-web
date: '2024-04-24'
title: Bringing Your Flutter App to the Web
author:
  - Maxime Eglem
  - Michaël Ohayon
video: dIo7QYcm6lg
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/dIo7QYcm6lg.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: '2024'
allow_ads: false
---
### Maxime
I'm thrilled to be here today to share our journey of transitioning our clients' Adenoid mobile application into the web and prod. Welcome everyone. My name is Maxime Eglem, I'm a consultant at Selenza and I am with Michaël Ohayon, a consultant at Publicis Sapiens. Let's start with a quick introduction of the mobile application and Adenoid. Adenoid is a worldwide company that provides prepared services like mail vouchers and gift cards to millions of employees. We are going to give you the reasons why we shifted to the web, how we approached it and all the lessons we've learned along the way.

Basically, our mobile application uses very solid, clean architectures. We have golden tests, we use a dedicated module design system with atomic design and so on. I'm not going to go very deeply into it, I'm sure you're all familiar with all the famous pop that we use.

However, if you have any questions, don't hesitate to reach out to us.

### Michaël
The quick question to have in mind is, OK, we now have a mobile application, maybe like the one you have, and the question is, OK, why going web and why going web with Flutter? So three main things to have in mind. We think that depending on the country, on the kind of people that will use the application, some users that they will prefer to have desktop applications for many different reasons.

Sometimes it's easier to type on a keyboard than maybe using your phone, and we feel like maybe for them it's going to be a better experience. But having that in mind, we plan to provide the same user experience. When I mean that, I mean like we have journeys that we've tested them, we have a lot of QA, a lot of design behind those, and we want to provide them with the same stuff that we've been doing for the mobile applications.

And the last point is you know about the limitation about Flutter web, and we are going to talk about them. But the approach to do web with Flutter is actually to have application, and because we start from a mobile app, it seems to fit very well. So we had to take a decision here.

We have another team in the company using Angular, and we were using Flutter. So either we would decide to go with Angular and like get the top-notch web experience, but that would mean to have a new code base, new repositories, new continuous integration, delivery, et cetera, and maybe new developers as well. And so the balance here is, okay, should we go with that or go in deep unknown Flutter web things?

That seems to be fitted for the web experience with some limitation, but for the one we want to have that may fit, keep the same team, reuse the UI, UX, each one is everything I've been telling you about, and the win would be to have a good time to market, because we could use the flows that we already have, put them to web, and hopefully win some really good time to the market. The thing that we did was to try to experiment and use the current code base. We didn't want to go too much into starting from a new app, because we knew that the biggest issues would not have been visible using a new application.

So that's what we've done. So we just switched the web builder target, so it's as easy as saying, okay, Flutter build web. We have new options, for sure, source maps and other things that you don't really need to care about at the first build web things.

Regarding the build time, you know, I guess all the room knows the build times for Android and iOS application. On web, we have something that is around two minutes, three minutes sometimes, including Pubcat build runner stuff, so it's very good. In terms of UI UX, by default, to be honest, it was a bit non-optimized, but it worked, and when I say it worked, it means that you could run the application, you could navigate between screens, you could type, you could click as well, without any code modification, and that's really a big win, to be honest.

Most packages that we use were almost working. I mean, like, no big crash out of the box or build issues, but more like small issues from place to place. And the last thing, because we went web, we had all the issues that you have using a classic web application, so that means that we needed to host, actually, the application, we needed to do some stuff regarding the APIs to do the correct configuration to auto-communication, but it was expected.

To give you a few numbers, the first build we've done in less than one day, for sure, but the first navigation working okay, it was in days, and as a side topic, in less than two months, we moved to production.

### Maxime
And now, this is what it looks like, a wonderful web application that is exactly the same as the mobile application, except that we have less features. So basically, like Michael said, we wanted to be very fast to know if it was possible, and it was a solid start, but clearly not enough for Edenide, a big company. So we had to iterate a little bit more, but we had the main most wanted features like onboarding, logging, and card ordering for our clients, and what we did is focus a little bit more on dedicated pages, and after a couple of weeks, this is what we succeeded to have, like a very dedicated web-stylish mobile application that had specific web header and footer that you can see to manage properly the navigation. We have as well the burger menu that appears responsively on the support screen, and so on and so on. So starting like that, we were very happy about the improvement.

So now, let's get to the exciting part, all the issues that we had. Basically, three main issues. The first one is the runtime error when you arrive to a page, so we had to manage most of all the flow again and again.

We are using for our clients, our vendors, SDKs for mostly analytic and so on. Those was not floater ready, floater web ready, and sometimes even worse, it wasn't even ready for the web. And the other thing is sometimes we don't have the same sensors, but you already know.

So we have to do some wrappers and manual binding to make it work, so it's an extra work, and yeah, I think we're good.

### Michaël
Yeah, let's go into other issues that we have or things that we discovered that are nice to share, we hope, with you. We talked in the talk before regarding secrets in applications. I guess most of you, you may use .env files on the web when you use an asset file containing keys and values, they are directly visible into the browser on network traces. So on the bottom right, you can see that mysecret.env is clearly visible to anyone just opening the network inspector, and everything by default is just readable, human readable. So to fix this kind of stuff, even if it's not perfect, because someone that really wants to get the values will find a way to get them, we found in the community we use the invite package that allows to obfuscate a bit. So if you look at the top right, this is floater web code minified, there is no obfuscation by default, and once you have the invite package to do some code generation on top of that, you will end up with something like on the bottom right, which is surely less readable by humans.

So again, it's not perfect, but surely, I guess in production, that's what you want to achieve instead of the things that we had before. Again, in the security environment, when you use some SDKs, most of the time, especially if you come from the native world, you know that you can restrict the API calls using a signature or package name or stuff like that. We found out that some packages available on both web and mobile, sometimes they take some shortcuts.

So really, it tends to you to really check how the web implementation is done, because we figured out that some packages were not using at all any security or any restrictions, and that means that anyone with a key could actually just call the web service, and you would have to pay for them to use them. So surely you need to double check the implementation, and again, floater web is pretty new, okay, it compiles and runs, but it's up to you to double check.

### Maxime
Another thing that we had to take care of, this one is very easy, but still need to take into consideration, the CDN is something different on a mobile application, so we need to manage it on the CI-CD, and all the facing domain, the public facing domain that need to be managed. Another thing that we had to improve as well is during the CI-CD, during deployment, make sure that we remove the cache, otherwise you need to wait like two hours or even more to get the update, so it's a little bit frustrating. Another thing to take into consideration, if you use hash switching like us, like we are actually, you need to use the URL rewriting to make sure it works, also...

### Michaël
For universal link, if you want universal link, like if you want to have the same link without any hash on mobile and web, and you use hash, you need URL rewrite at some point. Thank you, good point.

### Maxime
Another thing is, we might forget, but on mobile application, we know exactly the routes that the user is going to use. On mobile, on web sites, the user can go directly to a specific page without doing the previous flow or the flow that you wanted, so you need to make sure that you guard them all, and also you need to make sure that you manage the states, because refreshing the web page is not the same as a pull to refresh, so if you don't want a white page, make sure you manage your state correctly. And the last thing that we need to add, that is, according to your needs and use cases, you might think about two different flows or multiple flows according to the platforms.

In our case, during the onboarding, the flow on the onboarding for the web application wasn't the same as the mobile application, Android and iOS, for multiple reasons.

### Michaël
Two last slides. So a few concerns that we are not covering too much, but still you may know them and you need to have them in mind. Performance.

For sure, Flutter web is a bit behind the other frameworks, and depending on what you are going to do, maybe a bit or maybe even more. For this case, what we noticed is that the very, very first page load takes something like five, six seconds, because there is like a big chunk of JS coming up and many resources, but it's cached, and when the user come back or reload the page or anything, it's very acceptable, and when I say acceptable, it's like .3, less than .2 or .3 seconds, so the user won't notice, and everything else in terms of, like, navigation, clicking, anything else, HTTP calls, rendering of images, not visible by the user, so good, but still to have in mind. SEO, to keep things simple, don't do, you cannot do SEO, and you should split your SEO content from the web applications for now.

You may have to, as we did, to create some wrappers around some JS SDK to make them work in the Flutter world, and a good thing to have in mind, if you don't have any design system or widget book or anything, you should really have it, because going web without that is going to be really difficult. To sum up, the application is live in multiple countries on the web, and that was not, we didn't know if it was going to work, to be honest, when we started, and so it's good, and because it's the same application, we didn't split the code base, every new feature is available on both web and mobile, and it's been the case for months now, so we really like to go on the web using Flutter, and if you have any ideas of going web, maybe you should do it. If everything here makes you, like, want to try it, you should definitely continue to try. Thank you.

### Maxime
Thank you.

### Guillaume
Thank you, guys. Join me to the Q&A table.

### Simone
So, how many of you are actively considering to have a web app from the Flutter one? Can you have some lights in the public? Yeah, many.

The vast majority. All right. Awesome.

I think you interested some people. So, yeah, please sit down.

### Guillaume
Okay, so we have, like, many questions. The first one is did you manage to export easily accessibility features to the web app?

### Michaël
Surprisingly, yes. We used semantics, like the way you would be doing it in your application, and to, like, if you enable accessibility to modern web, basically, if you correctly tagged all the stuff that you want to expose correctly, we didn't have any big issues, so it should work for you.

### Maxime
If you use the base widget correctly, it's not going to be an issue.

### Guillaume
Okay. Good to know.

### Maxime
So, yeah.

### Guillaume
Do you when you show the application on a mobile device, do you show a hint to actually use the web app?

### Maxime
It's both, actually.

### Michaël
On iOS. But go on. Go on.

Okay. So, by default, because we have universal links, when you open the website on your iPhone, you will have a prompt, like, okay, you can install the application, and on the web, we have specific flows, because depending on the country, sometime maybe you will want to have more users on the web or on mobile, et cetera. It may depend.

In our case, we allow the user to do both. So, but it's really, like, product vision, to be honest, more than a technical thing.

### Guillaume
Yeah, definitely. So that's a good transition with the next question is how many of the users are using the web app compared to the mobile app now that you've migrated?

### Maxime
Way more than we thought. So, at the beginning, we created the web, or we wanted to do that just for the people that didn't have any mobile application, and trust me, that exists in certain countries. And so this is the main reason why we shift.

However, we discovered that it's sometimes easier to go to the web for the onboarding and so on. So we tried to trick in somehow to make sure they are using more of the mobile app than the web.

### Simone
A question that we were, I think, kind of expecting, how do you handle state management? Like, especially when the page reloads, how do you make sure that the state is preserved?

### Maxime
So we have to iterate. So at the beginning, we did not. And then what we did is on some cases, we made dedicated endpoints to make sure that we can call a dedicated, like, let's go, you go to, in our case, transaction details.

You cannot go to the transaction details directly on the mobile app. You need to go through all the lists of your transactions. However, on the web, you can.

And what we did, we created a dedicated endpoint to call it and to be transparent for the user. And the other way that we use is to find, to manage the cache differently as well. But the cache is destroyed somehow when you refresh the page.

So you need to make sure of that.

### Michaël
Just one thing with that. It's really very similar to when you are going to implement deep nested navigation based on, I don't know, maybe you receive a push notification and you want the user to be able to see a specific transaction. If for some reason the token is expired, that can happen.

It's exactly the same stuff. And you know how to do that in mobile. It's just that the web will make it more visible for you.

### Guillaume
Okay. And then you have to handle it where you probably don't have on the mobile.

### Michaël
Yeah, sure. And it was a discovery for us at first.

### Guillaume
I guess. Do you need to, well, yeah, do you need to rewrite your navigation logic?

### Maxime
No, not a lot.

### Michaël
Not that much.

### Maxime
Yeah, not that much.

### Michaël
No, we, the fact is, because like it's something new and products shifted some stuff. So we have some endpoints, but like let's say emailing, you receive a new email going to the platform. Before that, you needed to have the application.

And because we went web, now it's possible. So navigation logic, quite similar, except, yeah, the root guards or any logic that prevents you to actually do bad stuff and makes the application fail.

### Maxime
And we use famous probe that you already, that you are using as well. It's AppRouter or even GoRouter. Both are managing it well.

So it helped us a lot.

### Guillaume
Okay. Thanks. Maybe one last one.

There are many questions, guys.

### Simone
Yeah, lots of them. I mean, almost the last talk of the day. I mean, there is a second last talk of the day and so many questions.

Not in a rush to drink, so that's good. It's sober people who are asking questions.

### Guillaume
Okay, maybe. How do you handle CICD with having both web and app inside your project? Two different pipelines.

### Michaël
Yeah, so the code base is the same, but for the pipeline, maybe you already have like a specific task to build Android and iOS, and we just added a third one to build the web version.

### Maxime
So basically the build are the same and some part is different. So it's not really a big deal when you know how to manage it properly.

### Simone
Right. I think many people would like to go and take the details if you stick to the bar, I think. Sure.

And myself, I have so many questions.

### Guillaume
Thank you so much, guys.

### Simone
You're welcome. Thank you. Round of applause.