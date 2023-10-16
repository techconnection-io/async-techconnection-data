---
slug: >-
  /talks/frenchkit/september-2023/benoit-rottembourg-the-case-for-auditing-algorithms-disloyalty-and-bias-mitigation
date: '2023-09-21'
title: 'The Case for Auditing Algorithms: Disloyalty and Bias Mitigation'
author: Benoit Rottembourg
video: rKoBVN6OywE
thumbnail: https://async-assets.s3.eu-west-3.amazonaws.com/thumbnails/rKoBVN6OywE.jpg
slides: >-
  https://async-assets.s3.eu-west-3.amazonaws.com/slides/fae0b93922c949ff916fc6810926b089/slides.pdf
tags: []
year: 2023
conference: frenchkit
edition: september-2023
allow_ads: false
---
So, as you can see, I'm trying to improve the average age of the session.
Thank you.
And maybe some of you don't know INRIA,
INRIA the French National Research Center for Computer Science.
Okay, Cy Kittler, for instance.
And the aim of Regalia is to build algorithms, to audit algorithms.
And I will try to explain why and how.
Most of you were not there, but I was already coding poorly in C++,
I don't remember this kind of language, I imagine.
We were doing workforce management software for call centres.
This is the equivalent of 911 in France.
And at some point, I think it was late in the day, guy called me.
He had an issue with the unions of those guys,aying that guys, agents, at the end of the alphabet,ike Rotenberg, at the end of the alphabet,ad very poor shifts compared to guys at the top of the alphabet,ike Annalisa.
And it was a scandal.
I just bluntly answered,
"It's not possible. I've not the names.
I'm not guilty."
But I dig a little bit into it,nd the agent ID that I was receiving to build my algorithmsas ranked in alphabetical order, that I didn't know.
And I, without knowing it, in the little loops of my algorithm,
I was giving the hardest shift at the end of my loopo the end of the alphabet.
So it was a simple example of an unguilty guy doing very poor stuff.
More seriously,
Deliveroo had the very great idea of using sick leave daysn the evaluation of the ridersnd was sentenced in Italy for discrimination.
They were guilty.
And you have very intermediate situationhere you almost use an almost sensitive variablend build side effects that discriminate between two populations.
And it's massive.
Forty percent of the commercial websites in Europe,ested by the anti-fraud authorities,ave some issues about unfairness, manipulation,ark patterns, and stuff like this.
So probably 40% of you contribute to this situation, statistically.
It might be very small, but it might be super big.
For instance, the European Commission is seriously looking at Amazon buy box.
Are you sure that the best buy box choice that you pick up when you buy is fair?
So they are trying to have the answer.
So the law evolves.
Don't look at that, but just to understand that regulation authorities are trying touscle up, if I can say that, and try to hide data scientists and look into , booking.com, ,nto Spotify, into Google, Amazon, etc.o try to detect bias, disloyalties, sometimes fraud,r anti-competitive practices.
Just to take the last one, in July 2023,he city of New York, so it's not small,ust regulates employers using AI in hiring and evaluation processes.
They have to check their bias,nd they have to say, in average, we are this kind of people,ompared to this kind of people.
So I don't know if we will have more female coders,ut let's try to check what we are doing.
So who is guilty?
Is it just a perception of the society?
Are we getting allergic to Bias?
Or is it something a bit deeper?
Probably A/B testing, I mean, it doesn't help.
In my Boomer days, we were over-specifying algorithms.
HR, unions, etc.
So before the first line of code,here was at least six months of discussion around the table.
And what if the guy arrives at 8, will he lunch at 12 or not?
Etc.
Long discussions.
It's not the case.
Now you have the next sprint.
And that's all.
And probably the chain of subcontractors that goesn the end into India or Pakistan, I don't know,oesn't help.
Someone in Pakistan wouldn't knowhat someone reading Marie Claire,
French newspaper, is probably a female statistically.
So how can he know?
So now that I think, now that the situation is so massive,ow do we put in place auditing mechanisms?
How does it work?
How can we do it?
Can we just open the hood and read the code?
No one of you who has a few lines of code would dare to do that.
Even your own code a few years ago.
There are ways.
There are different approaches, but there are ways
In behavioral testing, so you have a black box,nd you bombard the black box with requests.
And you try to check if female, male, black, white,t cetera, old, young, et cetera,ave an effect on the answers.
But you have many conditions to meeto be able to do it in a proper wayo go in justice at some point.
It's quite delicate.
You have to be frugal.
Suppose you bombard , booking.com,  in Copenhagen next week,ut you don't buy, you just ask questions.
The feeling that , booking.com,  or the algorithm of , booking.com,  will haves that "Oh, the price is too expensive, I have to put down the price."
So you cannot bombard, you are harming the platformf you bombard it in a wrong way.
So there are many conditions, and at some pointou don't want to check everything,ou want to find a prejudice situation, and it's often very local.
Female, 50-ish, black, curvy, etc.
It's always local in the end, for business reasons.
And you try to find a flagrant offense to put into discussion with the platform.
So there are ways to build what we call good surrogate, a clone.e clone the black box in a minimal wayo that there is no way to make a differenceetween the clone and the black box.
And then you try to explain how the surrogate works.
This is a very large philosophy and it's an open topic of research.
Just to give you an idea,s it the same as finding a gold coinith a metal detector and a battery, a limited battery?
Or is it more a battleship game?nowing that probably female, then I can avoid this part of the landscape.
The landscape is 200 variables times the space of the variables, of course.
Well, once, very boomer, I'm sorry.
Once you have detected a bias, what do you do?
Some banks I've met are just plugging out the sensitive data.
Not only it's very rough, but it's not enough.
There might be variables correlated with the sensitive variables.
So you have to put out every guilty-ish variable.
It's not enough.
And by the way, it might be very excessive.
Another way to do that, just take it roughly,ou have a female, and the sensitive variable is female.ake all the males looking like the female,ook at the average decision on the males,nd apply it to the female.
It's another approach.
And you can prove that there are optimal approacheso minimally repair an algorithm.
So that's what I wanted to tell you.
There is some hope.
We can put skin around our algorithms when they are unfair,r in the algorithm,e can regularize with regard to the side effects we have observed.
That will be all for me today.
We are not necessarily, we developers, are not necessarily the guilty ones,ut not taking care with all the skills we have,ith all the data we have, not taking care is being guilty.
Please take care.
[APPLAUSE]
>> Thank you very much.
We can go here on the left part of the screen.
Thank you very much for your talk.
There is something that started to make me thinkbout our role as a developer.
So, as you said, with all the skills we have,e should step up and try to avoid making bad things or evil things in a way.
Very hard question.
How do you think we should act as developershich don't actually own the part of the AR coding?
Sometimes, the business metrics are leading towards a technical choice,ut what we can do as developers to avoid this?
I think it's clearly a product owner constraint that has to be added.
Every time I produce something, I produce like you do quality tests or what we calln the old days regression tests.
It's a form of regression test that we have which is they are the metrics we have, were obsessed with optimizing something and you introduce counter metrics as far as youiscover them.
So that might be official countermetrics, female, age, we have 25 sensitive variablesn France for your information.
So you have 25 countermetrics.
And so typically I think it has to be introduced.
But you need someone else in the company not involved in the product development, a formf auditor or compliance officer, like banks are doing, by the way.
They are not doing it for the pleasure, obliged to do it.
So probably we have to put a kind of external point of view just to challenge a little bit.
Have you thought about this?
Can we see that?
Is there a data drift?
Because the problem might not be at the beginning of the application.
We have interesting questions already from the Q&A.
How do you evaluate the boundary between legitimate user-based segmentation and discrimination?
Well, I've been doing pricing for 20 years.
There is no pricing without discrimination.
No, that's cool.
So saying that at the beginning, on a Friday afternoon, guy who is buying a ticket is more in a hurry.
So you can a little bit increase the pricen a Friday afternoon.
This is some form of discrimination.
What you don't have to do is probably,nd there is bias in the history of the data.
There is bias.
Society is biased.
Probably a definition of what is fair to mes don't do worse than what you findhen you arrive in the data set.
So if your algorithm is increasing the bias compared to the data you receive,robably you're going in the wrong direction.
It's a counterfactual way of not doing dirty stuff.
But it's vicious to know where.
The way I understand it, it's not only...
At some point you might make a mistake where you don't understandow you're integrating some data that shouldn't be there.
And the question that I have is that with the growing usef AI with people, for example, with Apple SDK,e can use AI without being an expert in AI.
Isn't there a risk that people will use technologieshey don't master to the point they are not reliable,ut also in the end they are because they are the only oneorking on it?
- Yeah, I think clearly it's a riskhat if you don't really know the unbalancer some side effects of what you use,ou might go very fast and probably go in the wrong directionut it's speaking about honest peopleut there are guys also who are cheating.
Some, and I can say it, some insurance companiesuring the hiring process for data scientists,
They ask for a way to circumvent female versus male information.
So I think there is also a culture which is no, there are things you cannot do.
A very pragmatic question but interesting.
Can you give us some example of the 24 variables you were mentioning about segmentation?
Yeah, so I think age is obvious, but being pregnant for instance, and it's quite easyo detect fortunately.r let's say monotheism is something super easy to detect.
The way you buy food one week before Ramadan, I think everyone knows, by the way, your neighborsnow, etc.
So religion, you have also some income, I think some situation, etc.
So you can see it, "Défenseurs des droits" in France, and you will see the 25 rules.
So it's not only the variable, it's a situation where you are not allowed to use those variables.
And don't think only about the variables, but correlated variables, like reading Marie
Claire, maybe it's not exactly being a female, but I can tell you it's very close.
And it's good enough, we love the good enough, it's good enough to know the gender, etc.
There's one question that seems really interesting to me.
What as a developer, when you're not in charge of designing the features, when you're askedo do something and you're like, okay, this is going to be a problem, what are your optionsnd who should you talk to?
So in good companies, you have alert, I don't know how they call it, whistleblower, somewhere.
So I had this situation in a very big company where I saw form of fraud.
I went to the guy and we fixed the problem, by the way.
But there are companies that are probably a poor way to look at it.
Here, I think it's a choice you make.
It's like for green washing or for et cetera.
It's your own responsibility in the end.
If you are confronted to a situation like this a lot, and it's at the core of your business,ike building, making cigarettes.
I mean, it's difficult to say to me,ou save humanity making cigarettes, for instance.
I think it's a bit the same.
Some companies are deeply engravednto manipulating customer data.
- Specifically, yeah.
Okay, but if your company is not willingo fix the problem once you've raised it,s there like, I don't know,
NGO or governmental organization?
- Yeah, there are.
You can, there are websites where you can sayhat you have encountered this situation.
La repression des fraudes, DGCCRF in France,ou can anonymously say something.
Kneel, say.
Well, it's not very clean, but this is a way to solve it.
Specifically about our ecosystem, which is mainlyOS apps, Mac OS apps, there is one more actorhan in traditional environments, whichs basically app stores.
So Apple, Play Store.
What role should they play in your opinion in this part?
- I think there are two levels.
The app store itself might favor some kinds of appersus other apps.
So is this neutral?
And I think it has been discussed.
So it's one thing.
The second thing is the data you use in the app.
And I would say on this side,robably Apple is probably better than other GAFAM.
But you have to check your own, the own data.
It might be subtle.
I give an example, face recognition.
You, yes, in face recognition you think, ah, black, white,bese, not obese, et cetera.
There are very subtle stuff like the age of your iPhone.
If you have an old Android or an old iPhone,
The quality of the image is so poor that the face recognition is not easy.
So here poor guys are wrongly detected by the application.
So you really have to imagine what could be the side effects.
And here there are lots of apps now that you can you have to check, you take a kind ofelfie or you say three words and then you can enter the application.
It might not be neutral.
Very interesting.
All right, thank you very much.
Thank you very much indeed.
(audience applauding)