---
slug: >-
  /talks/flutter-connection/2024/masahiro-aoki-enabling-instant-updates-in-flutter-apps-with-shorebird-my-journey-with-code-push
date: '2024-04-24'
title: >-
  Enabling Instant Updates in Flutter Apps with Shorebird: My Journey with Code
  Push
author:
  - Masahiro Aoki
video: pRoKzWbMcNA
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/pRoKzWbMcNA.jpg
slides: null
tags: []
year: 2024
conference: flutter-connection
edition: '2024'
allow_ads: false
---
### Masahiro
Enabling Instant Updates in Flutter Apps with Shobo, my journey with CodePush. I'm Masahiro Aoki, founder of OpenCI, a free CI-CD service for Flutter. If you have some interest about OpenCI, you can go to OpenCI.io. And because it is closed beta, you can join our Discord channel if you are interested. I was a former software engineer at IBM, startup co-founder, CDO, and as I mentioned to you, I just became an organizer of Flutter Tokyo a few hours ago. So, if you have a chance to come to Japan, let's do some Flutter meetups. Of course, I have loved Flutter and Dart for five years.

And I'm based in Tokyo, Japan. So, disclaimer, all demos are run by MacBook Pro, I have a Mac, 64GB, XR, iPhone 12, Pixel 8 Pro, and I'm not a member of the Shobo team, nor have I received any money, just a user. And today's goal is to understand what CodePush is, how Shobo works, and how to use Shobo even in a production environment, and the pricing of Shobo.

So, I have some questions about Shobo, so answer them and wind dash. So, first, what is Flutter? As you know, Flutter is an open source framework by Google for building beautiful natively compiled multi-platform applications from a single code base.

And Flutter is written in Dart, and you can distribute the Flutter app to many platforms like iOS, Android, web, Linux, macOS, Windows, and even tvOS. Yes, Flutter runs everywhere and with one code base. Great, isn't it?

And what is CodePush? So, the Shobo team explained CodePush as follows. CodePush is a tool that allows you to update your Flutter app instantly over the air without going through the store update process.

And this allows you to directly deploy fixes and new features to your end-user devices. And please raise your hand if you have experience updating apps to Apple or Google. Okay, most of them have the experience.

So, in the normal process of reviewing for fixing bugs, first you find a bug and fix them, and upload the build to the stores, Apple and Google stores, and submit the review to them and wait for the store approval. And if you are lucky or request an expected review, the store approves your build in a few hours. However, in most cases, as you know, this will take a few days.

And if you are so unlucky, you have to wait days, weeks, or even months. And after the store approval, you can release the build to the store. Finally, the users get an update.

The problem is that you must wait for the store review and can't know when the store approves your app. And sometimes your app will be rejected for other reasons. Overall, I think no one likes this review process.

On the other hand, if you use CodePush, you don't have to care about the stores. After fixing bugs, all you have to do is send the code to the users. I think you can wait up to 10 minutes to debug the update to the users.

CodePush demo. First, I'll show you how CodePush works. The first screen is the original Flutter counter.

After killing the app, CodePush was made. So the screen became black. This doesn't use Firebase Remote Config or Launch Lockly or similar services.

I'll show you the Showable team. The only CodePush service for Flutter is developed by Flutter Heroes. As you know, Eric is a founder of Flutter and the former director of engineering for Flutter and Dart at Google.

And Felix is very popular for the block library, which is one of the most famous state management packages in Flutter. And Brian is a former Flutter team member. And another Eric is the Flutter and Dart GDE and the Frame Core member.

The first case, where the app on the Google Store views become unnecessary with CodePush. Please raise your hand if you think A is the answer. A few?

OK. How about B? OK, most of us.

The answer is no. I'll explain the reasons. So with CodePush, you can change any Dart code.

This is an example of the default counter app. The blue line is original. And the red line was deleted.

And the green line was added. In other words, you can change Flutter widgets code. For example, you can change Flutter widgets like color, text, size, and business logic within Dart.

However, you have to care about the number of changes. The more the code you change, the larger the part size will be. However, you cannot change the native code.

For iOS, it is Swift or Kotlin. For Android, it is Kotlin or Java due to the Apple and Google Store requirements. And these are the Flutter packages.

And if you upgrade Cloud Firestore or your launcher, you cannot use CodePush because they have native code changes. This means that if you upgrade those packages with no native code change, you have to submit a build to the store and wait for the store approval. But you can upgrade the provider or block which are pure Dart packages and use CodePush.

If you change assets, for example, adding a new image widget and a JPEG or PNG image to Flutter, technically, you can use CodePush. However, Java doesn't support assets right now. Unfortunately, the asset support has no idea at the moment since after Java's iOS stable release, the team has been too busy meeting the new customer's requirements.

This is not directly related to the quiz, but because it is very important, I will explain. With CodePush, technically, you can change any Dart code. This means that you can change app features without submitting app store reviews.

For example, you submitted a to-do app and the store accepted it. Then you can send the CodePush. The main functionality is a to-do.

Then you modify the code to change the app features to like the dating app. Then you can send the CodePush to reflect these changes. In this case, you deceive the stores.

This is not allowed for Apple and Google. If you do this, your app will be banned from stores and showbiz. Another example is changing in-app purchase providers.

If your app has IAP providers and the contents are digital, the transaction fee is up to 30%, 3-0. However, with CodePush, after the store review approval, you can change IAP providers to like Stripe to reduce the fees to 3%. This is also technically achievable, but it's not allowed.

Okay, showbiz architecture. I'll explain how showbiz works. The first showbiz is a fork of Flutter.

The reason showbiz forked Flutter is to implement CodePush functionality. As you know, Flutter itself doesn't have CodePush. For your information, Eric, the founder of Flutter and showbiz, had attempted to implement CodePush for Flutter, but the PR wasn't much.

The next question is to check your understanding of how CodePush works. So, can you use CodePush to update the contents of an existing app built by Flutter? If your app is listed in the stores, can you use CodePush to update the app?

What do you think? So, A, yes. Okay, okay.

How about B? Okay. The answer is no.

You can use CodePush, but I'll explain the details. You can use CodePush for existing apps built by Flutter. The app listed in App Store and Play Store was built by Flutter.

As I said, it doesn't have the functionality to update the app contents. In other words, the app in the store doesn't have the CodePush functionality. The app cannot get updates from the showbiz server nor reflect changes to the app.

So, I think you can get an overview of how showbiz works, so I'll dive deep into it. So, showbiz consists of three parts. The first component is the showbiz CLI, a command-line interface that empowers you to create, build, perform CodePush, and more.

The interface is the primary tool you use when working with showbiz, offering a streamlined and efficient way to manage your CodePush operations. The modified Flutter engine, the heart of showbiz, is where the magic happens. The showbiz team, with their ingenious use of C++ and Rust, have enabled CodePush in the Flutter engine.

Understanding the modification may be challenging, but it's a journey that's sure to inspire. The last part is the cloud infrastructure. This manages your CodePush data and usage over the showbiz.

The showbiz CLI. This wraps the original Flutter command and adds a few showbiz commands. So, showbiz creating IPF5 command is very similar to the Flutter build IPF.

And the code of the CLI is open source for transparency, so you can go to the showbiz repository and check the code. And as I said, the CLI is just a wrapper of the Flutter command, so you can use the Flutter command with the showbiz CLI, and I'll explain this later. This is the most challenging and fun part.

I'll explain this as much as possible, but if you need more details, please head over to the showbiz dev or docs in Discord. And there isn't an issue to add more explanation. So, ShowBot takes a unique approach by forking Flutter slash engine, also known as the Flutter engine, and adding a ShowBot updater.

In other words, to enable CodePush, they forked the Flutter engine, then added ShowBot updater. And they also modified Flutter slash Flutter, the Flutter framework and the Flutter slash build root, known as the build root for CodePush to work. The Cloud infrastructure is divided into three key components.

Release binary, storage, patch binary storage, and check requests. These components are designed to ensure seamless operation of their services. They store release artifacts, such as IPA for iOS, and app bundle for Android in private storage.

And the forward patch, which is diffs from the release, they are stored in the storage and the sub via global CDN. This section will provide instruction to how to use ShowBot. So, before using ShowBot, you have to create a ShowBot account.

It's free, so don't worry. Then install ShowBot CLI using the command line above. And once you've installed ShowBot, you can use it to log in.

The CLI will generate a login link for you, which you can then use to log in through the browser. When you log into ShowBot, and navigate to the project root directory, run showbot init. This will create showbot.yaml file at the root of your project, which contains ShowBot's app ID. This app ID is what connects your app to ShowBot. So, if your app has multiple flavors, such as staging and production, a corresponding number of app ID will be created. And you can check the status of these apps on the ShowBot web dashboard.

And it is important to note that for Android, using ShowBot requires internet permission. So, if your Android manifest.xml doesn't allow the permission, ShowBot init will automatically modify the code to ensure the necessary access is granted. This step is crucial for the seamless operation of ShowBot in your app.

And the next command is showbot release. For Android, run showbot release android. For iOS, showbot release iOS.

And for iOS, it creates IPA. For Android, it creates app bundle. After creating these artifacts, you can upload it to App Store Connect, Play Store, or Firebase App Distribution.

To use the original Flutter command, you can use double hyphens, like the showbot release iOS hyphen hyphen space dot define. Blah, blah, blah. And please be careful that these release commands produce only a release build, not a debug or not a profile build.

So, if you forget, I will explain the build modes of Flutter. In Flutter, there are three build modes, debug, profile, and release. Debug mode is for debugging the app.

So, you can use hot reload to check the app. But the performance is worse than the release. And the profile mode is for checking the app performance.

And the release mode is for distribution. So, the performance is the best for the release mode. And since the release command of the showbot is only for release, you cannot check the build on your iOS simulator or Android emulator.

And successfully running the showbot register the release to the showbot server so that it can be used for code push. At the console, you can see the message indicating that your build is registered on the showbot server. To check the build, you can use the showbot preview command.

The advantage of using this command is that it is super fast. As you see, after running showbot preview, you can choose which build to preview on your phone. Then, the CLI downloads the artifact from the showbot server and installs it to your phone.

And since the CLI only downloads and installs, not builds, if your internet speed is fast enough, the preview is fast. But you can use showbot preview only on your machine. So, if you want to test a build across your team, use test file, test track, or Firebase app distribution.

And there is a staging argument. And with this argument, you can check the staging patch. So, when you want to enable update to the end user's app, in other words, you want to push your code, you can use showbot patch Android for Android, showbot iOS for iOS.

And showbot patch has one argument, which is staging. As mentioned earlier, you can patch with a staging argument. Why is this so important?

The answer is straightforward. When you run showbot patch, the update is registered on showbot server. This means that when an existing user opens the app, it will automatically update.

However, if the patch has bugs, the user will also encounter these bugs. This is where the staging argument comes in. By using it, you can avoid this potential problematic situation in a production environment when patching, using staging, and checking the preview comment are much safer than patching directly.

After using the staging argument, confirming that your patch works fine, head to the showbot console, where you find the go live button, and press it to send the update to the users. And I will dive deep into the patching. One of the key steps in the patching process is running the showbot patch comment.

This comment generates an artifact and sends it to the showbot's Google Cloud Storage. The app, built by showbot release, not further built, checks patch updates every time the app starts with a GET request to showbot server, which runs Google Cloud Run. And if the response indicates an update is available, the app downloads the artifact using the showbot's response download URL.

Then, the update reflects the change to the app. And the updating process is done in an isolated thread, not a main thread, so as not to block the Flutter UI. As you know, Flutter is single-threaded, so if you run heavy processing in main thread, like downloaded artifacts, you are freezing, so this approach is necessary.

So the pricing of the showbot is very generous. You get 5,000 patches every month for free, and after that, it's pay-as-you-go. The hobby plan includes one developer, so if you want to invite other developers to your showbot account, you must use the team plan, which includes unlimited developers.

The last question is about pricing. So how many patches will be made if you code push one update to 10,000 users? Okay.

Please raise your hand if the answer is A. Okay, maybe half of them. How about B?

Yes. It's a good question. Okay, the answer is 10,000 patches.

So you cannot use a hobby plan for this situation. You have to pay some. And if your existing app has many users, I think the cost can be huge.

But maybe the showbot team can discount the price, so feel free to discuss the cost with them. Yes. And the showbot supports GitHub Actions and Codematch for CI-CD.

Of course, you can use other CI-CD services, though it may be challenging, like Xcode, Cloud, Bitwise, SakuCI. At OpenCI, we support showbot. And as mentioned earlier, you can implement showbot into the CI-CD workflow using showbot in GitHub Action.

It's really easy and simple since the showbot team has already developed the GitHub Actions. However, the most difficult part is how to use showbot in CI-CD and how to make the showbot release and patches in the CI-CD pipeline. So, I will show you three examples.

And the first is the showbot team's recommendation. The default branch is main. This workflow is triggered when the release branch is created or patched, or pushed.

And in this demo, there is an environment variable, showbot token. This is retrieved from running showbot login. And when creating a new release branch, this workflow runs showbot release.

For pushing an existing release branch, showbot patch runs. This workflow is only for Android. So, you need to prepare for the iOS workflow.

However, as you may know, the macOS instance of the GitHub Actions is really expensive. So, you can consider using CodeMagick or OpenCI. They are much cheaper.

Yes, OpenCI is free. And the next showcase is from one of my clients. They use OpenCI as their CI-CD.

They are a pre-CSS startup. The default branch is develop. When creating PR to develop, CI triggers and runs showbot release iOS and Android with internal flavor.

Then, deploy the build to the Firebase app distribution for testing. When QA, they merge develop into the main branch. And for publishing a build to the stores, when creating a release branch from main, the CI triggers and it runs showbot release with stable flavor.

And then, deploy the build to app store and play store. For patching, pushing the release branch is a CI trigger. When the trigger fires, showbot patch is run.

As you may notice, they no longer use original Flutter build command, only showbot release. So, if you want to compare showbot and Flutter build, you can also set up the original Flutter workflow. And this example comes from one of my other clients, and they have only two Flutter devs, and C runs startup.

Their default branch is main. And when available, they use showbot patch to update app. For PR, they release showbot build with staging and production flavor and distribute them to the Firebase app distribution.

Future roadmap. So, showbot team is now really working hard to improve iOS performance and fixing bugs. So, unfortunately, desktop support, asset support, and faster integration support are planned, but no ETA.

And frequent FAQ. So, any performance difference between native Flutter and showbot? I have not seen any issues with our performance for Android.

However, there are slight difference between native Flutter build and showbot build for iOS. The showbot team insists that showbot for iOS is production ready, and I agree with their opinion. So, for more details, see issue 1825.

And for the app size, iOS doesn't have a problem. However, for the Android APK, the size can be bigger than the Flutter. So, be sure to check the size before releasing the build to your users.

So, I have to say is showbot is production ready, and I agree with this. But, honestly speaking, it's not much in a service like Flutter. So, they need more jobs, and maybe you will encounter a failure bug.

So, be careful and do enough testing before using showbot in production. Fortunately, the showbot team is very kind, helpful, and quick to respond to. Yes, that's it.

And I have some souvenirs from Japan. So, they are chocolate and cookies. And this is a prize time.

So, please raise your hand if you correct all the questions. Please. Who correct all the answers?

Okay, okay. Thank you, thank you. So, I will throw the dash.

Please raise your hand. Okay. Oh!

And, yes. And one more dashes. Okay.

Yes. Congratulations. And I have some T-shirts and Japanese chocolate cookies.

So, yes. And I have some more surprises. Even if you cannot get the prize, I have one more surprise for you.

I asked the showbot team to create a coupon for you. And, of course, you can start using showbot for free. But, as I mentioned, it is limited to one developer.

So, you can try showbot in your team. But, be careful. This gift expires on May 1st.

And, again, I'm just a showbot user. And I'm not getting any money from them. And a special thanks to them.

I'm deeply grateful to my esteemed clients, for their invaluable insights into showbot production. The showbot team support has been instrumental in my deeper understanding of showbots. And I am immensely grateful to the connection team for the opportunity to speak at this prestigious conference.

It is an honor I still find hard to believe. And, Raul, your encouragement to serving the CFP for this conference and your invaluable insights have been transformative for me. I'm really grateful for your support.

And Maru always helps me organize my slides, talks, and supports me. So, feel free to connect with me. If you come to Japan, let's grab some tea.

Thank you so much.

### Guillaume
Thank you very much. We have time for a couple of questions. There's a bunch of questions on the Slido.

Thanks a lot. There are a lot of questions. We will send them all to you and probably to the showbot team too so they can help you answer.

The first one is how Apple and Google managed the 3.2.2 paragraph? Are they watching your app?

### Masahiro
I think they don't know. Yeah. So, that is the reason I talk about do not deceive the stores.

Yeah. Maybe some of your competitors will report that you changed the app features. Maybe this is one possible way they know to deceive the stores.

### Guillaume
Well, you can try and play but if you lose, then you lose big. Maybe it's too big a bet. The second one is have you encountered any unexpected limitations like incompatibility with native Flutter tooling while developing using Shorebird?

### Masahiro
I'm guessing because it's fork and shouldn't be any but for now I haven't experienced the difference between the native Flutter. But the Shorebird team sometimes said that the native Flutter to output is not useful for the Shorebird so they have to add some modification for the output of the Flutter command.

### Simone
Is Shorebird for updates of your app no matter the update or just for pushing crucial fixes in case you have some major bug?

### Masahiro
Okay. I think you should try updating the app if your app doesn't have the native code changes and if you run the Shorebird patch sometimes the warning and for my advice don't ignore the warning because if you ignore the warning maybe your app will crash and one of my clients experienced the crashing so don't ignore the warning.

### Simone
By the way, do you have a way to limit the users that you push the patch to? Let's assume you have 20,000 users but you want just 100 users or 1,000 users to receive the patch.

### Masahiro
I think there is no way but I think there is an issue so maybe it's better to ask the Shorebird team about that because if your app has 300,000 users maybe the cost can be huge.

### Simone
You can use Shorebird I think for A-B testing if you want to test a small feature to a small number of users.

### Masahiro
Maybe in that case using the flavor is a good option. For all the plans you can make unlimited number of apps so you can use the flavors.

### Guillaume
Another practical question can you combine Shorebird CLI with Flutter management version system like FBM?

### Masahiro
That's a good question. I haven't seen this kind of comments in the Shorebird Discord. I think you cannot use the FBM with Shorebird CLI but there is the argument of setting the Flutter version of the Shorebird so you can use the argument.

Like Shorebird version 3.19 5 something like that.

### Guillaume
I'm guessing if it's a fork of Flutter it's using version defined by the CLI of Shorebird so you can pass a tag to the version but it wouldn't make sense to be able to choose from the version that you have locally. I guess. Thanks.

### Simone
There are 20 questions.

### Masahiro
You can ask me any time when I'm free.

### Guillaume
Maybe one last one that had many votes. Would you recommend to always after pushing a patch would you recommend to always push a new release with that same patch? We've heard of some performance issue impact on a patch so is it a best practice to push a patch to make sure that user the bug is fixed and then afterwards when the bug is actually fixed push a release.

### Masahiro
Fixing bugs of Shorebird? No, no. Or bugs of the app?

### Guillaume
No. You're fixing a bug in your application and using Shorebird patch and afterwards should you push a new release to make sure that you have a new stable version that is not patched but actual new release?

### Masahiro
I think it's better to if you can you have to submit a new version of the build with Shorebird release not patching because maybe they have the native code changes.

### Guillaume
But is it considered a best practice to do this every time you do a patch a few days later to have a new release or not necessarily and you can push some patches in a batch?

### Masahiro
I see it depends but for I think it's better to patch every time because it reduces the development time and it reduces the chance of the rejecting from the stores. Yeah. So for the business and for the customers I think it's better option to use patch every time.

### Guillaume
Yeah. Definitely seems safer that way.

### Masahiro
Yeah.

### Guillaume
Thank you very much Masahiro and let's have lunch.

### Masahiro
Yeah. Thank you so much.