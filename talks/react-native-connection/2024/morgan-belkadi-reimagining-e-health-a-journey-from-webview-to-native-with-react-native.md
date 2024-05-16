---
slug: >-
  /talks/react-native-connection/2024/morgan-belkadi-reimagining-e-health-a-journey-from-webview-to-native-with-react-native
date: '2024-04-23'
title: 'Reimagining e-health: A Journey from WebView to Native with React Native'
author:
  - Morgan Belkadi
video: 3rMPf4c5DR4
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/3rMPf4c5DR4.jpg
slides: null
tags: []
year: 2024
conference: react-native-connection
edition: '2024'
allow_ads: false
---
### Morgan
Talk to you about something we're doing at Doctolib is changing an application that was a full WebView to React Native. But before I do this, I'm going to introduce myself a little. Mo said it a little.

I'm a staff engineer at Doctolib. I've been working on mobile for like 15 years. So you see I'm wearing skinny jeans, right?

I'm the older generation. I've done Android, iOS, Flutter, React Native, even Windows Mobile back in 2008, actually. Yeah, that was hard.

What have I done? Yeah, ten years of freelancing. And now I'm Doctolib. DrLib was my first permanent contract after ten years of freelancing. So that's a lot of challenge as well. I've done about more than 20, 25 apps.

More of them are in France. But also for Adobe, for Michelin, for Airbus, or L'Equipe for those who know. Publique, some kind of weird newspaper, like Tableau for those who know, yeah.

Sorry. I'm based in the south of France. I'm obviously Mr. Jack, supporter of AS Monaco. Yes, please. Thank you. Yeah, we are two, so half of the supporters.

I like board games and Wish Loren, for those who know about this. And you see this, what you see right now is my corporate picture, right? But you can see me in real life, I look more like this.

So, please, I will introduce, I will not do that face right now. So, I'm working at DrLib as a staff engineer. Who here knows about DrLib?

A lot of French people, right? So, who doesn't know about DrLib? I mean, even before we gave away free socks.

Okay. Okay. So, a few people.

DrLib, in a few words, we are the European leader in health, in the health system. Basically, we help patients with their health management, and we help them book appointments. So, it's all about giving people access to healthcare, for now, in France, in Italy, in Germany, but next in other countries.

So, we have 80 million patient accounts, which is more than the number of French people. 20 million telehealth sessions, 900,000 professional users. It's a big machine rate.

So, for those who are not French, maybe you'll hear about it in the next years. All right. What we're going to talk about today is the WebView.

Everything's going to be centered around the WebView in a React Native app. I'm also not going to talk bad about the WebView, first of all, because I don't have anything bad to say about it, and second of all, because we have the main maintainer of React Native WebView here. Thank you, Thibault.

But, no, this is, you'll see how the WebView was actually super useful for DrLib, and I'll show you, because everyone knows, apparently, about DrLib, I'll show you how big, how present it is in the app that you know right now and have in your hands. Okay. So, that WebView basically was introduced years ago at DrLib, because it was easier, of course.

We had a lot of React developers, because the website of DrLib is in React. So, what we've done is factorize all the manpower that we had, because we couldn't afford to build two apps, of course, in iOS and Android, and we didn't have time nor resources with COVID, etc., to do an actual React Native app. What we did was take a shortcut, in a way, but a shortcut that worked.

So, we embedded the mobile website. So, what you see on your Chrome browser or Safari browser on www.drlib.frdeit is exactly what you see in the application. So, for all the French people, German people, Italian people that use DrLib, what you see or what you used to see in the app is literally the mobile website.

Did people know about this? Did you know that you were using a complete WebView in the app? Can we have a little bit of light, please?

Thank you. Who knew? Who, like, knew?

Okay. Yeah. Wow.

Okay. Who thought they knew? No, you knew.

Okay. Fair enough. So, basically, we ended up doing this, like a croque monsieur of different layers.

So, iOS and Android covered by React Native, covered by a WebView that displaying the mobile website. But it worked. It worked, and we did that because it was a small investment.

We did that because we had a lot of knowledge of React, and we could use a few developers to develop the shell that we used for this. And most of all, it helped us deliver super fast because we could just do the continuous delivery that we were doing on the web, and it would appear in people's phone. So, that was overall a quick win that made a lot of sense.

And we did it, and that's great. Also, we had a secret objective that we never told people, actually. It was to become the biggest WebView in the world.

And we succeeded, actually. I think we succeeded because it's huge. I would not say please don't do that, but, no, we did it, and we are happy we did it, but the WebView is not made for this.

It is not. It is made to display ads, that kind of stuff, to do a few things here and there, but, like, a single-page application is a lot for a WebView. So, why did we change since it was working?

Many reasons. We're not going to cover everything, but as you can see, and this is quite old, actually. This is not the newest numbers, but most of our users are on mobile, especially on the native app.

Like, right now, it's even 70 or 75% on native. So, I think it's 10% on desktop, 10, 15% on the mobile website. So, of course, why would we consider them as second-class citizens, right?

Even though they are, like, three quarters of our users use the native app. But there are also a lot of different reasons why we did this. Mélissa, if we can have a little bit of light again, please.

Thank you. What would you think, like, in the usage friction or anywhere, what would you think, could you give me reasons why we would change, why we would want to go away from a WebView? What comes to mind?

Yes! Thank you! Oh, that's a great question.

This is something I should cover, actually, before this, is that we're already using, even with the WebView, we would already use API features or, like, native features because we use some kind of bridge, it's a JavaScript interface, and that's why we embed the website inside a WebView, and then we have some kind of communication channel that helps us, like, take notification tokens or take geolocation, that kind of stuff.

We were already doing this. Not in the easiest way, but we were doing it. Yes?

Offline. Offline, great question. Of course, this is not something we're going to do right away, but it was a huge pain, because if you don't have native features, if the only thing you do is load a WebView, of course, if you do not have a connection, then you cannot do anything, and this is a huge pain, and it's going to be in the future, like, if you use the app right now, you open it without network, you cannot use it at all.

No appointments, no documents, et cetera, so this will be a huge plus when we have it. One last thing. Yes?

Accessibility, obviously. Thank you. This is very, very important at DrLib.

We are an e-health company, and accessibility is very important for us, and basically it's not that we cannot do it at all, because technically you can do it, but if you want to do it properly, if you want your app to be accessible the right way, to have good voiceovers, to have proper accessibility, you do not want to have a WebView. You simply do not, and so that's why we have many reasons. We did user research, of course, like the marketing teams, communication teams, they had user research to see what people would want to change and why they were complaining about the app, because the app is so used by so many people, and they are happy about it, but they're happy about the service, not technically about the app, and we wanted to change this.

So, very costly, it's slow to start, the offline, we talked about it, the transitions, the transitions, it's really, it feels like a website, and we're all mobile developers here, we like the look and feel of mobile transitions, and we want the best for our users, and so all these reasons, I'm not going to cover them right now, but this is why we decided to change. So, now that we decided to change, great, so how do we, where do we start? Where do we start?

First of all, should we do it iteratively, or should we do it from scratch, like go into a tunnel of seven years, because DrLib is a 10-year-old company, but we could not, of course, stop everything and be in the tunnel, so it's not an actual question, we did it iteratively. But then, when you decide that you want to do it iteratively, where do you start, and what technology do you use, right? Does anyone have an idea of what we used?

I don't. Flutter, exactly. So, yeah, I'm going to talk to you about Flutter today.

We have 30 minutes, yes. Okay, Flutter, how does it work? Now, of course, we use React Native.

React Native, we chose to completely go all in on it, because we had so much manpower on our React developers, and because we also had mobile developers that knew React Native, so for us, it was the best choice. Even for me, as a native developer, I was the one recommending staying on React Native, because it just made sense. We wanted to share some code, we wanted to basically keep what we have and not do things twice, while you know the drill, and React Native was definitely the technology of choice.

So, now, what do we do? So, here is the mobile app, as you know it, as people who know DrLib know. You have everything in one app, that's the web view we load when we load the application, and how would you do it?

I'm not going to force a question again to you, but I remember last time, actually, Thibaut, the maintainer of React Native web view, I asked the question, how would you do it? He said, simple. You just do the navigation.

And, indeed, that's what we did. So, yeah, he knows the drill, also, because he did almost the exact same talk, like, four years ago? Five.

Sorry. Five years ago. And he wrote to his friends and colleagues, okay, we are ahead of DrLib by five years.

He did, actually, he did. So, that's what we decided, and that's what made the most sense, right? You want to extract the navigation first, and then do the screens one by one whenever you can.

The goal is not to do native screens all over the place. We probably won't replace all screens by native screens, but doing the navigation will help us actually display the screens we want to display, and eventually maybe change them to native screens. So, what you see in yellow was the current state of the application.

I forgot to tell you, but after I'm going to show you this, at the end of the talk, we'll see a demo. I should have teased about that. We'll see a big demo, like, of the new DrLib app.

So, for those of you who use the app, you'll see it today for the first time. So, in yellow is the complete app, right? And the navigation, especially the tab bar on the bottom, or bottom navigation, tab bar is included in the web view.

So, the idea was first to remove it from the web view, saying when you are hosted in a React Native app, then do not display the tab bar, et cetera, and eventually, at some point, we will put a native tab bar, and so the web view logically will take less space. Points of attention that we were already thinking about, the authentication-specific behaviors, you know, the links, et cetera, that were being done in the web view, now we had in mind that we would need to be super specific, super careful with the tabs, or the links, et cetera, and the memory, because a web view, as I was saying, is not made to take that much things inside. It's not an SPA, that's not what it's for, and the memory is very scarce, not as much as a tvOS and WearOS.

Mael, I know you know what I'm talking about. But still, the web view is the first thing on the mobile devices, the first thing the system is going to remove, to destroy, if it needs memory. So that's that.

And apart from this, we were like, okay, it's fine, it's going to be fine, let's keep that React Native snow, we're good for a while. But we got the first challenges, right? Someone like a few days after said, hey, what about drawers?

You know, they come from the bottom. But if we put a tab under it, then the drawers are above the tab bar, so it's a very bad UX, right? Because you can have a drawer that's supposed to go in front of everything, but then you can still change tabs that didn't make any sense.

So first hiccups after a few days of thinking, maybe it's not going to go as good as planned. But eventually, it's just a matter of, you know, events and saying, even though you're doing declaratively, you can say, okay, I'm going to show a drawer, and then we decide that we natively, we hide the tab bar. I'm not going to go too much into technical details tonight, but a little bit about the feedback of our experience, I think, is the most valuable thing.

Also challenges, like, well, what about, how do you do when you go from one tab to another? There are many different ways to do this, and maybe we'll talk about it in the Q&A or over a beer. Don't worry, it's soon.

And it's a challenge, because what happens, even for backward compatibility, there are a lot of things. The navigation, for example, if you go to the documents tab in the middle, how would you do this? Because this was our ultimate goal, right?

To go from one web view, one screen, which is a web view, to potentially a native screen. So if we want to do the documents as a native screen, how do we handle this? How do we make it so the tab bar redirects to a native screen on one tab and to web view on another tab?

What we did, basically, to spoil the thing a little, is that the tab bar is, I'm sorry, the web view is always here. It's just hidden. And so when we go on one screen or another, Thibaut and I have a lot of things to talk about again about this, but we hide the web view or we show the web view.

And depending on where you are in the application, that's just how it works. But it is always there. There is one web view for the whole app.

It's always there. You cannot see it, but it's there. So backward compatibility, for example, if we hard code in the app that the second tab is the appointments and it has to go to slash appointments, then our buddies from the web, they have to keep that URL, that path.

Because if they don't, if they don't think about backward compatibility, then when someone, when a user, you know how it is, when users don't update their app, then they're going to try to go on slash appointments and it's not going to exist anymore. Over the challenges that we've faced recently, actually, as we realized, or at least the product realized, that we could not go in production with this without having exactly the same tooling as we had. So real user monitoring that we're doing, that was with Datadog on the web, they absolutely wanted it.

I mean, I say they, but also us, of course, it's super important. We needed logging, we needed A-B testing, because they really want to know how users would behave with the tab bar native and with the web view. So a lot of things that could prevent us from actually going into production as fast as we thought.

But despite all of those challenges, honestly, I've been talking about it with a lot of people today, trying not to spoil too much. But honestly, we have challenges, but it's also super interesting, like really, really interesting, because everything is left to do. We were joking about it within the team, it's like a developer's paradise, because it's a Greenfield project or something, an app that we all know here in France, like 40, 50 million users in France, and everything's left to do.

So basically the app is empty, the code base is very, very small, because there was just the shell, right, to display the web view. Now we are going to focus a lot on native features, on UX, and the company's changing a lot in terms of culture to go mobile first. And this is a big change at DrLib, and we can see investment.

We are able to recruit people, we are able to evangelize the mobile at DrLib, and it's honestly super exciting. We've created a mobile design system, we are trying to put architectural principles in place, like solid principles, trying to do some kind of DDD as much as we can. It's a very, very interesting moment, and it's super nice to do it on a small code base.

And also, yeah, the web already had the previous problems, so we can just ask them what was hard, and they can answer. And if you're wondering, yes, this picture was generated by Chad GPT. And I always wonder how you can tell, but you can tell.

Like, specifically with this waterfall that goes out of this umbrella, what is that about, Chad GPT? Anyway, lessons learned. I have to finish fast.

Lessons learned. I was talking about how the organization changed, right? Because people in the organization, DrLib was a very, very, very, very, very, very, very, very web-centric company.

10 years of web development, and you can imagine that even the app being just a web view encapsulated made a big web culture. So it was hard to change, but now that's what I was saying. It's super exciting because everything is changing towards mobile first, and we love mobile first, right?

And the mobile project is becoming kind of the rising star, and it's super, first of all, it's really gratifying. It's super nice, and we evolve in a good atmosphere, good environment, but it's hard also for the organization to change. When you haven't really thought about all these processes, and when your design team doesn't know about mobile UX, et cetera, it's tough to change.

So I would really talk about the technical challenges that we faced. I've talked about it, but also if you're in the same situation, because the whole point is that I know we know that people usually are in the same situations. If something like that happens, don't overlook the organization issues.

I'm talking to managers mostly because this is a managerial point. Do not underestimate this. So we'll just sum it up with this.

The takeaways are starting with the web view, with the navigation. It seems appropriate. I'm not saying this.

Thibault says this because he did it, and he did it five years ago. Still good? Still good.

So do it. It's fine. Build a design system.

This has nothing to do with going from a web view to native, but here, if you're doing something on a greenfield project, I strongly encourage you to start a design system, even if it's just small components. We have people in our team, great people who've done an amazing job at designing new components very fast and that we can reuse and all, and it's really great to have this with a design system. We have Storybook, etc.

It's the same. Don't underestimate this. It's super important.

The web view itself, do not think it will disappear. Even though we're getting rid of it, it's always going to be there, even if it's for just one screen here or there. For now, it's more than this, but it's always going to be there.

So don't throw it away. Don't think you're going to throw it away. It's going to be there.

Also, you can upscale motivated React developers. That's what we are doing, we've been doing, and we are doing, and also thanks to Bam, who is also helping us with that. It's really good to see people who become super interested.

I don't know if there are... Can I have a little light? We'll finish with this.

Thank you, Melissa. What's the percentage of people who came from web to React Native? Okay.

And from native to React Native? Oh, quite a lot of people, actually. Okay.

Thank you. It's really interesting, and from web to React to React Native, it's really nice because people already know most of what React is, of course, but you all know that it's different. It's still different, so it's good to upscale them.

And finally, please adapt your estimates because the web view is a pain. It's really nice because we have a lot of new things to do, but also it takes a lot more time to go around the web view to work around it and adapt your estimates. And finally, in just 10 seconds, the big demo.

This is the DrLib app as you know it, and it's going to be out in about a few weeks. You're going to see the new application of DrLib. So the tab bar at the bottom looks like this at the moment, and this is the home page, and this is how it's going to look like in a few weeks.

Yes. Big change. Now, of course, no change on the visual thing because the team has done a perfect job at doing it pixel perfect, but this is exactly what we wanted because you're going to feel it at some point because the UX is going to be better, native navigation with React Navigation, etc., but the tab bar itself does not change, and that was what we expected. Thank you.

### Mo
Thank you very much, Morgan. Proceed, please. So a very interesting talk and I think a very relevant talk right now because in an age where a lot of companies are looking to optimize on cost, sometimes decisions are made around how much you can invest in native app development, how much you can invest in React Native when you've already got a web app, and I think you put forth a really good outline of a long-term strategy for companies to be able to adapt native at their own pace for those features that are important. So I think it's really important for us to be familiar with this mindset and this outlook because I see it more and more in my job speaking to companies.

So very, very cool. Awesome. So let's take a look at the audience questions.

So first thing that comes up always with web views in apps is the conversation around App Store, and you mentioned earlier on that the whole app was basically like a web view. Did you have to negotiate with Apple to get an exception for the App Store review?

### Morgan
Well, I was not there when we did it. I've been negotiating with some of the reviewers, like some people like to poke us and some don't, but if you read the guidelines of Apple, you have the 4.2 design that says if your app behaves like a web view, it does not behave like a native app, it has nothing to do on the App Store. And we didn't have any problem per se, but we never know.

And that was one of the big reasons actually to change because legally speaking, they could throw us out.

### Mo
You're at risk at any point. Yeah. Like you say exactly, the restriction is around, it needs to have additional behaviors that are app-like rather than just a wrapper of the web view.

### Morgan
Exactly.

### Mo
So yeah, 100%. Okay, cool. Are you using Expo?

I don't know why I laughed at that.

### Morgan
The question has nothing to do with it.

### Mo
Everyone loves to ask if you use Expo.

### Morgan
Do you use Expo?

### Mo
Who says that? It's anonymous. You can't interrogate our audience, man.

Come on. That's a code of conduct violation.

### Morgan
To answer the question, we are not using Expo right now. We are actually trying it out on our Storybook app to deploy more easily, but we are really thinking about it and the team is having a debate about it, but we might at some point.

### Mo
Cool. So an interesting question in terms of why React Native? When you're having a web view-based application, why would you go with React Native instead of using Cordova?

So Ionic effectively, either in Cordova or Capacitor, take your drug of choice. And why would you use something like React Native that's meant to be for native apps as opposed to a specialized web-based framework?

### Morgan
Yeah, that's a great question. I was not there when the decision was made, but I do think it's because our website is done with React and people knew React, and I think the easiest thing to, the first thing that came to mind was, okay, we know React. We probably can do a little bit of React Native and do that shell.

And I think that was the main criteria.

### Mo
And I think then following on from that, you have a wealth of knowledge now, having gone through this process, and looking back in retrospect, would you take the same approach today with what you guys did, or what would you do differently?

### Morgan
With the same constraints, obviously, if we had to go quickly and to keep the website, maybe something, as you said, like, no, I cannot pronounce Cordova, sorry. I just don't want to.

### Mo
Oh, you don't want to say it. Okay, cool.

### Morgan
No, I'm kidding, but I think it was a good idea. It was the best we could do at the time.

### Mo
Yeah, fair enough. The first DrLib app, somebody knows you guys really well, was released in 2016. Why have you made this decision to migrate to Native now?

### Morgan
Because it works. It was working up, it is still working technically, but you know, DrLib has started, we've started, we've been created in 2013. So I would say the organic moment for a company that size, et cetera, to change, like to change architecture, to invest on quality, and even in that kind of stuff, would have been around 2019, 2020, but COVID happened.

And in France, it was big, we did the vaccine, we had to be able to have a really small time to market still after seven years. And of course, we could not invest on that stuff because all the manpower was taken already.

### Mo
So at the end of the day, business power trumps all, doesn't it?

### Morgan
Yeah, but also it's business, but it's, we helped a lot of people with that. French people would use DrLib on a daily basis to get vaccine and also, it made sense.

### Mo
Cool. Kudos to you. Cathy is asking what your go-live strategy is.

So, you know, are you thinking of keeping the WebView alive forever? So the WebView version of the app, you know, for some backwards compatibility, are you going to force users to upgrade? What's the, or maybe something in between, what's the plan?

### Morgan
The strategy for now, our long-term strategy is to replace screens, WebView, like native screens, do native screens, that makes sense. Not to replace everything just for the sake of it, because I don't think it makes sense either. And in terms of backward compatibility, etc., we've put in place, I don't remember who said it earlier, but I think it was Mikael, something in place to say, hey, a new version is up. And if you cannot, if some users cannot update, then they will keep the WebView.

### Mo
And so for your web teams, that means effectively they need to indefinitely keep those versions of the web.

### Morgan
Maybe at some point we'll sunset it. It's still unclear, because we need to give people access to healthcare, that's very important for DrLib, and we don't want to leave people aside, so we'll keep it as long as we have a decent percentage of users.

### Mo
Yeah, cool. How do you handle the desync between the WebViews that ship continuously from the web team and the native pages? Like, how do you know when to navigate to a native screen?

I'm not sure I understand the question.

### Morgan
If I understand the question, the native screens, this is done on the client side, this is done on the mobile side. We know what screens we want to have as native, is that the question?

### Mo
Yeah, I almost feel like the question is, like, how does, it's probably a question on communication of the native layer with the WebViews.

### Morgan
Yeah, we use that bridge, that native bridge to communicate with one and another on both sides. And now, I was talking about the change of culture, etc. The big change, I would say, for, I should have talked about it, actually, about back-end developers and even front-end developers who are embedded in the app, if you do a product that's embedded in the app, is backward compatibility in general.

Like, you have the actual just knowledge that anything can be called with an app that is a year old or two years old.

### Mo
And I guess just to wrap up, there's a couple of these, so just to wrap them up together, any noticeable UI performance improvements from this migration from a WebView-based approach to a native approach?

### Morgan
For now, we're still in the middle of it. I think we will really see it when we do the home page natively. Because right now, we are still waiting for the WebView to load before hiding the splash screen, to be completely honest.

And for now, we don't see it like that, because the WebView has to load anyway. But as soon as we start doing, actually, native screens, and especially the home screen, then we'll use the magnificent flashlight tool from BEM. Thank you, Alexon.

Thank you, BEM, for that.

### Mo
We refer to it as Holi internally. Holi. The Holi flashlight.

### Morgan
Yeah. Now, this is for sure, and this is one of the reasons we wanted to do this. The startup time, the slowness that we could feel, it's definitely going to be a lot better from now.

### Mo
And we are looking forward to it. Thank you so much, Montgomery, for coming along.