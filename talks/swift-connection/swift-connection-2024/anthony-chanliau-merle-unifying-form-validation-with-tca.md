---
slug: >-
  /talks/swift-connection/swift-connection-2024/anthony-chanliau-merle-unifying-form-validation-with-tca
date: "2024-09-23"
title: Unifying form validation with TCA
author:
  - Anthony Chanliau Merle
video: RrBxRX_SEsQ
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/RrBxRX_SEsQ.jpg
slides: https://storage.googleapis.com/async-techconnection-downloads-events/swift-connection/swift-connection-24/Swift%20Connection%20ACM%20V3.pdf.zip
tags: []
year: 2024
conference: frenchkit
edition: swift-connection-2024
allow_ads: true
---

### Anthony

Hello everyone, just a little check about the slides and the clicker, right? Let's go to the next. Okay.

Okay, so bottom is next. So my name is Anthony, and I'm an iOS lead developer at Aviv Group, and this company holds applications like European real estate applications, like Sologée in France, Imoweb in Belgium, and Immonet and Imowelt in Germany. Today I would like to share with you the issue we faced with working with form validation in our applications, and what solution we came up with, and how it works under the hood.

So let's say you have a form which requires the user to enter its username, and optionally its phone number. So that can be a contact form, for example. And the user can submit the form through the validate button.

And one key question that we have to ask for this kind of form is when to validate the fields. And one answer that we came up with to most of us is obviously when the validate the submit button is tapped. When we want to validate the form, we want to ensure that all fields are right, and so we can work with it.

But there are some other cases that we can validate each field to be more reactive to the user. So it can be when the user enters and exits the field, or when the value changes, for example. This is fine when you have one form to answer this question, but when you have multiple forms like that, you cannot just answer this question every single time, because you end up with inconsistent behavior on the UI.

Some form will validate the field when the user enters and exits the field, and so on, and some other will validate in other cases. And you will end up, as we did, with code duplication, because every form will have to validate every field and so on. So basically that was duplicated.

So we ended up reinventing the wheel with every new form that we created. But what if we had something that can enforce these rules to be answered every time, and you can just use it, and the validation would be automatically handled by this tool? And it will take care of validating the whole form upon the user validation, and each time, for instance, a value changes, and you will just plug it into your screen and into your tool feature, and it will handle everything.

And even better, what if we, to create this thing, we would only need a few things, like to let it know when the user taps the submit button, which field to validate with the rules according for each field, and let it have a way to notify us back that the validation has been succeeded. That would be great. And in other words, what if we had a unified form validation system?

And that's what we came up with, and we worked on in our applications. But just before I present you this solution we came up with, I want to open a small parenthesis about the architecture we used, because it helped us actually build that tool. So the composable architecture, also known as TCA, really basically it's just like you view all the store, and it can send actions when you have UI interactions from the user, and these actions are handled by what's called a reducer that will hold all your business logic, and it will update the state so that your view will be updated for the user.

I won't go into more detail about it, but I want to emphasize a key feature in TCA, which is how they handle bindings with this architecture. Every time a binding has a new value, it will send a binding action, and this action will encode the key path to the value that is being validated. So for now it's pretty abstract, but bear with me, it will be really handy just afterwards.

If you want to know more about TCA, there was a great introduction talk at Swift Connection last year, so you can watch it if you want on the Technic Connection website. I will close the parenthesis and get back to our ideal tool that we want to make. As I said, we made it and we called it form validation, basic naming for now, and I will show you in code what it looks like, but for now it takes a lot of space in the screen, so let me just rotate it, make it less space and put it aside.

And now we have some code. Actually some reducer code, but we don't care about anything about it, but just know that there is a form validation, which is convenient, and if we expand it, we can see that we only have a few things that it needs to be created. Actually we need a user action to let it know when the user wants to submit the form, a onSucceed action to let it know back the system that the validation succeeded, and then the list of fields that needs to be validated, so for instance there are two fields and one is the user name, for example.

And how does it work under the hood? So for the form validation, every time it receives an action, it will match against two possible cases, either it is the user action that we pass to it, so it knows that it has to validate every field, so it will go through each field, and if the validation succeeds, it will send back to us the validation succeed action so that we can send the form to the API or do anything we want. And the other case is this famous binding action, and actually thanks to the fact that it encodes the key path to the value, we are able to get this specific field that needs to be validated and run the validation for this field in particular so that the user knows that something went well or wrong when he inputs the field.

Talking about the field validation, what it looks like, it's basically just a function which takes as input the state of the screen, of the form, and it will extract the value that needs to be validated from the state, and it will run each rule for it, and at the first rule that fails, it will just grab the error from the rule and just display it, update the state to be able to be displayed to the user, and it will return false. And if no rule fails, it will just send back the error to nil so that we remove the error to the user and just return that everything went well.

And talking about rules, we saw two rules before, which is the non-empty and length, and they look like pretty much the same API than the field validation, but first I want to emphasize that it needs error message and a check closure that will implement the validation, and the error message is pretty important to be here because with that we are able to display a specific error for the specific validation so that we can really specifically clue the user what it needs to be changed to the input.

And then it has a validation, a validate function that will take as input the value to validate and will check with the check closure and return the error message if something went wrong. And we will focus on the length function, how to create it, so that we can have an idea of how to create multiple rules and so on. So basically it's just an extension to the rule struct, and we will have a static function which will be specified to the bare minimum requirement for the value that we want to check.

So here, for example, the value has to be conformed to the collection protocol so that we can access its current value and check whether it's at least the character that we want to, the element that we want to make. And with these components, we can basically validate any kind of forms, even a form in which you just have to select a picture after all, like there is no picture, that's optional, we can just check that. And some other forms like the user profile, for example.

And these screens thankfully don't come from our applications, because the UI is pretty simple, but specifically for this conference, we made a small project to showcase how to use the validation system and how it was implemented, and it is available on GitHub. So you can go to it, get the code, how the validation form is actually implemented, and maybe inspire yourself to get it and modify it as you need or update it to use it on your applications. And lastly, you can contact me if you want to share any thoughts, if you have any questions about this topic on Gmail, LinkedIn, and GitHub.

And thank you for your attention. I was pleased to share this with you guys. Thank you.

### Zino

No questions from the audience.

### Anthony

That's okay. But we do have questions.

### Zino

Okay.

### Audrey

Very declarative.

### Zino

Yeah.

### Audrey

So thank you, Anthony. My question will be about when you work with products, they want sometimes to get the product being, you know, available for every country. So my question will be about localization.

Where does localization strings, string key, or string resources fit in our model?

### Anthony

So as you saw, like, for now, they are pretty close to the reducer part, because we declare all the validation rules on the reducer side, and we keep the error string with that. So that will be on that side. On the other side, obviously, can lead to some issues when you want to test them, because you have, in that case, ensure to test on the right language, because you want to assert that the error string value is actually, like, for example, in English and so on.

So these are some, like, difficulties that we didn't manage to face yet, but indeed, we are aware of that.

### Zino

And the second obvious question is about accessibility, right? So in the same vein that when your error messages or your validation rules can differ from language to language, they can also differ from, let's say, user preference, because of accessibility, somebody who has bigger font or whatever. So I know it's kind of a generic question, and it's a hard problem to solve, right?

But do you think that with work, this particular system can adapt to a dynamic problem?

### Anthony

I believe it can adapt to some problem from accessibility, because, like, actually, it only works on the logical part, and you can, as long as you work with bindings, because that's how we implemented it, you can basically fit any UI you want. So the accessibility for the font size and so on is closer to the UI part, so you will define it on the UI, and it will have, like, no impact on the logic. But on the other side, maybe for the accessibility, I don't have any insure for that yet.

### Audrey

I have a last question about the point three, the fact that you're using TCA. Do you encounter to try to contact or maybe try to improve or maybe do some more requests about your way of doing things, like, which is really declarative and which is really nice and clear for people to adapt?

### Anthony

Yeah. Well, first, thank you, because, like, it was really important to make it declarative, at least to us, because we wanted to be really easy for the developers to use it and to have less friction as possible to have, like, configurations or, like, specific logics and so on. We really just wanted to have it plug and play, and we believe this API is at least good enough for that, and we didn't take the opportunity yet to talk about with the point three guys, and actually, that's, like, the first time we shared this to an audience, like, we did it, and in the company, a colleague of mine that's in the crowd coming from Belgium just told me, like, there is this connection happening, and you helped us build this thing on the validation form, and that would be great, like, to make it, to open it to people so that they can get inspiration from it.

So, yeah, I start by this, sharing it here, but I still feel, like, a bit, not imposter, but something like that, like, not legitimate enough to, like, say to the point three guys, like, hey, we came up with that, like, would it be nice to maybe work with that, or I don't know.

### Audrey

Apparently not, because there was no question, so I think everyone understood.

### Zino

Just for, just to reassure the problem with the imposter syndrome here, who is thinking about doing something like that for their form validation in the room? Yeah, see? Yeah, great.

Quite a few people, actually.

### Anthony

I'm happy with that, and, yeah, and actually, when I was working, when I was creating this talk, and I tried to make this solution, like, pretty, not abstract, but, like, the global image of this, I came up with the graph with, like, a way to notify the user, to notify the system that the user tapped the button, a way to send this thing, and I was writing it, and I was, like, that's actually not TCR at all, it can just be, like, SwiftUI bindings or publishers for people who work on, like, React or things like that, so they can really, like, take this picture and adapt the thing to their own needs.

### Zino

Definitely. Thank you very much. Thank you.

### Anthony

Thank you. Thank you, everyone.
