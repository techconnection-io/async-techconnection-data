---
slug: "/talks/flutter-connection-23/francois-nollen-mind-your-app-footprint-🐾⚡🌱"
date: 2023-06-02
title: "Mind Your App Footprint! 🐾⚡🌱"
author: "François Nollen"
video: JQFp2vXTtgQ
thumbnail: thumbnails/triosncf.png
slides:
tags: []
year: 2023
conference: flutter-connection
edition: 2023
allow_ads: false
---

Bonjour et bienvenue dans cette session sur la réduction de la footprint d'une application en utilisant Flutter et mobile.

Pour préparer cette conversation, nous avons appris de nouvelles techniques et conseils.

Certains d'entre eux, nous les utilisons maintenant en production.

Nous sommes donc très heureux d'y être, de partager cela avec vous.

Merci à tous d'être là, et beaucoup de merci au Flutter Connection Team.

Merci.

Je m'appelle François, je suis avec Jocelyn et Adrien.

Nous travaillons sur l'application SNCF Connect.

C'est une application utilisée par des millions de personnes en France pour trouver et utiliser non seulement des trains, mais aussi des solutions durables pour le voyage et les mobilités du jour au jour.

Mais ce talk n'est pas sur notre application, c'est sur vous et nous, ce que nous pouvons faire pour optimiser et rendre nos applications plus efficaces.

Donc, il y aura une petite introduction, puis nous allons rapidement nous concentrer sur les techniques de développement.

Nous parlerons des components défauts, de la tree-shaking, même d'implémenter notre propre mode Eco-Friendly.

Nous reviendrons sur des outils et des techniques pour tester et moniter cela.

Et c'est tout.

Mais commençons par le pourquoi.

Vous savez, l'industrie numérique, l'économie numérique,

Il s'agit en fait de ressources réelles, d'infrastructures et de matériaux rares, comme par exemple les minéraux rares pour construire des batteries et des téléphones.

A l'origine de l'agence française L'ADEME, pour la transition écologique, en France, les technologies numériques causent 2,5% de la footprint carbone de toute l'industrie, et 4% de la production de gaz à effet de serre mondial.

Si on regarde le plus récent rapport publié en mars, on voit que près de 40% de la footprint vient du dispositif utilisateur.

Ce n'est pas la réseau, les centres de données et le cloud. et la plupart de la pollution vient de la production du dispositif.

Les téléphones et les smartphones sont les pires, car leur durée de vie est d'environ deux ans et demi.

Et si on ne fait rien, cela augmente dramatiquement les prochaines années.

Pour le reste de la discussion, je dirais "footprint" ou "carbon footprint" mais ce n'est pas seulement sur le carbone, mais aussi sur l'énergie consommée et les rares minéraux utilisés par exemple.

Donc vous devez avoir tout cela en tête.

Et en ce qui concerne cela, qu'est-ce que nous pouvons faire pour améliorer nos applications et réduire le footprint ?

Nous allons donc rapidement nous concentrer sur les techniques de développement.

Mais avant cela, un mot sur le produit et le design.

Cela peut être évident, mais c'est notre responsabilité et notre choix de travailler sur des produits bons, utiles, pour offrir des fonctionnalités utiles.

Nous devons essayer d'implémenter un design simple et efficace et de rendre nos services plus inclusifs, plus accessibles. on a déjà parlé de l'accessibilité aujourd'hui.

La bonne nouvelle est que chaque fois que vous essayez d'améliorer votre produit, d'améliorer votre design, en général, cela améliore aussi l'implémentation technique, cela améliore le point de départ du carbone, cela améliore l'accessibilité, parce que cela devient plus simple, et cela améliore l'expérience d'utilisateur.

Donc, dans certains cas, vous pouvez même améliorer le business, parce que vous avez plus d'utilisateurs et des utilisateurs plus heureux.

Nous sommes à Flutter Connection, nous sommes tous des développeurs, donc d'ici à présent, nous nous concentrons sur les techniques de développement.

Et Jocelyn, nous avons vu que la plupart de la pollution et le footprint viennent du dispositif utilisateur.

Alors, qu'est-ce que nous pouvons faire si nous voulons des applications meilleures, plus rapides, plus petites, plus efficaces ?

Il y a déjà des techniques et des conseils que nous connaissons, que nous avons entendu parler.

Exactement.

Voici quelques principes.

La première chose à regarder est l'utilisation CPU pour vérifier la reconception de la batterie.

Et ensuite, le FPS, pour que lorsque vous opérez sur un ordinateur basse ou un ordinateur vieux, tout soit lisse pour vos utilisateurs.

Chaque technique de flutter est très bien documentée, et nous ne reviendrons pas sur ces points. nous pouvons vérifier votre hardware consommé, comme GPS, Bluetooth, caméra, senseur, et vérifier que vous l'utilisez quand vous ne l'avez pas besoin.

Vous devez aussi vérifier votre utilisation de réseau, par exemple, l'implémentation de cache sur votre mobile.

Si vous utilisez un diode, par exemple, il ne vient pas par défaut, donc vous devez le faire vous-même et vérifier que vous utilisez du cache.

Assurez-vous d'adapter le tailleur de vos actes, payload et storage à vos besoins.

Ce que je veux parler d'abord est le mode sombre.

Donc, les principes ici, LCD, qui est un peu un modèle de technologie de vie, et complètement indépendant du couleur montré.

Donc le mode noir ne s'ajoute pas ici.

Amoled peut couper certaines parties de son écran si le display de couleur est noir.

Donc un thème noir complet est vraiment bien.

Mais il consomme aussi beaucoup moins d'énergie avec des couleurs noires.

Par exemple, avec notre app, nous avons un thème bleu noir.

Nous avons fait des tests avec notre partenaire Greenspector pour montrer que nous avions une réduction de 25% sur notre même flux d'achat.

Estimant que ce flux sera montré environ 30 millions de fois sur les téléphones, nous avons un échec de 7 tonnes de CO2 par an.

Donc, que ce soit en mode noir ou en mode sombre, n'hésitez pas à l'utiliser.

Vous pouvez aussi regarder les threads dans votre application.

Vous devriez utiliser une bonne stratégie de threads, car lorsque vous gagnez le pouvoir de l'arrayage Flutter, le sub-système peut optimiser les traitements sur l'hardware, et vous pouvez utiliser un CPU Core optimisé pour sauver la vie de la batterie et pour optimiser le UX, car vous ne voulez pas déchargez le main thread.

Des conseils sur le thread, vous pouvez utiliser compute ou isolate.run, la version latente de Flutter, pour déserialiser les grandes payloads.

Vous pouvez utiliser isolate pour plusieurs requêtes en parallèle.

Regardez aussi le schedule microtask, si vous voulez prioriser un futur pour votre écran, et aussi utiliser WorkManager si vous avez besoin de faire quelque chose en arrière-plan.

Par exemple, si vous avez besoin d'annoncer une notification pour votre serveur.

Repaint Boundary.

Craig a expliqué mon slide.

Il l'a très bien expliqué, donc je ne vais pas y revenir.

Nous l'utilisons dans notre app avec de bons résultats.

Comme vous pouvez le voir à gauche, avec notre écran de maison sans repaint Boundaries, et à droite avec repaint Boundaries, avec votre belle performance Overlay Flutter, vous pouvez voir une conception de CPU beaucoup moins large quand vous utilisez Repaint Bondary, c'est la bonne façon, comme l'a expliqué Craig.

Un autre bon conseil, c'est de rester à l'abri, simplement.

Bien sûr, certaines choses viennent presque gratuitement.

Rester à l'abri avec vos libraires, SDK, les frameworks, etc., peut gérer de nombreux futurs presque gratuitement.

Par exemple, dans Flutter 3.10, vous avez l'impeller qui arrive à l'iOS par défaut.

Nous avons réalisé quelques tests sur notre app.

C'est notre écran de maison avec KIA en haut et avec l'impeller en bas.

Donc vous avez un FPS beaucoup meilleur mais aussi une conception de CPU beaucoup meilleure juste en vous enregistrant Flutter.

Et si vous vous demandez ce que vous voyez maintenant,

Ces résultats viennent de la présentation de Emmanuel, un de nos collègues, il est quelque part dans la salle.

C'est une présentation qu'il a faite, il a proposé à Flutter Paris en janvier, il y a un replay disponible si vous voulez en savoir plus.

Et maintenant, c'est le moment un peu bizarre, où je dois parler de l'arrière-plan

à une conférence Flutter.

C'est juste pour le dire, it's possible to move some logic from the presentation, from the frontend to the backend, and it can be quite interesting for you Flutter developers.

So for instance, most or part of the logic presentation, mapping things, formatting strings, applying the user local to a string, these types of things, we can do that on the backend.

And there's this pattern we use, the back-for-front pattern.

Le Back4Front serveur est aussi votre meilleur ami pour toujours, clairement, quand vous êtes un développeur Flutter, parce que de cette façon, vous avez une certaine logique, vous pouvez juste vous déplacer vers le backend.

Si vous avez plusieurs canaux et peut-être plusieurs technologies sur le frontend, cela vous donne plus de consistance, vous écrivez moins de code, c'est facile de redéployer sur le backend, et parfois vous avez un meilleur temps de marché.

Sur la front-end, ce qui est vraiment intéressant, c'est que vous obtenez une application plus petite, c'est plus rapide et potentiellement vous obtenez moins de crashs parce que de toute la logique, vous avez démarré.

Avec Green Spectre, nous avons déjà mentionné, nous pouvons mesurer le résultat de cette approche, de cette architecture, entre notre précédente application en jaune, en orange, et SNCF Connect qui a un serveur de front-end. et nous avons clairement un plus petit déploiement et moins de données sur la réseau entre l'application Flutter et le serveur et le backend.

Nous voulions partager avec vous un cas d'utilisation pour cela, comme exemple, c'est le tracking du business.

Je ne sais pas combien de vous avez à implémenter le tracking du business dans votre application, mais même le tracking du business et le management de consentement,

You have to remind the GDPR

"règlement".

Even that can be done from server to server and you can move that outside of the Flutter application.

It means most of the events for instance if you want to track transactions, booking and stuff, you can do that on the server directly.

No impact, nothing to do on the frontend.

And when you have to collect something, to do something on the frontend for tracking.

You just have to instrument your frontend for instance.

If you don't want to integrate too many third-party SDKs, you can, that's what we do, you can implement a root observer for instance, get know where we are, get the consents, get what you have to collect on the frontend and send it to the BFF.

But the mapping, the data layer, all of that is c'est que la plupart du magique de la gestion de la traçabilité et du management de l'accès est fait sur le serveur.

De cette façon, vous pouvez enlever de vos applications front-end beaucoup de SDKs de 3e partie, ce qui signifie moins de usage de CPU, moins de storage.

Et moins de malheur pour les développeurs.

Oui, parce que parfois nous avons des conflits de versions intégrant les librairies de 3e partie et aussi moins de appels aux domaines de 3e partie.

C'est vraiment intéressant pour les développeurs de front-end.

Une autre façon de limiter le footprint de votre app est de réduire la taille du bundle downloadé pour vos utilisateurs.

Nous allons voir rapidement deux techniques concernant les bundles d'app et le tree-shaking.

Flutter est compatible avec les bundles d'app Android. nous avons gagné en moyenne 48% du poids de l'application totale et vous pouvez attendre un gagnement significatif aussi qui vous permettra de retirer tous les codes inutiles pour une architecture spécifique dans votre bundle final et sachez aussi que Flutter est compatible avec les components déferlés je parlerai de ça plus tard

Sur l'IOS

Récemment, Apple a enlevé la option de bytecode dans Xcode 14

Nous ne savons pas pourquoi, mais nous avons remarqué que certaines applications célèbres ont beaucoup augmenté leur taille

Il est donc possible de faire des travaux pour enlever et obtenir un résultat similaire à celui d'avant avec l'option de bytecode

Mais nous pensons que l'Apple prévient que les parcs de dispositifs seront plus homogénés et qu'ils seront automatiquement retirés dans le futur.

Sur le tree-shaking, c'est plus à propos de retirer des codes inutiles pour les autres plateformes Flutter de votre app, pour qu'elles puissent retirer les fonctions, les fields, etc.

Le tree shaking est fait à la fois du compilé quand vous construisez votre application.

Vous pouvez en apprendre plus dans le talk d'Alexander à Flutter Heroes.

Il décrit cela très bien.

Je vais vous donner quelques conseils rapides sur comment observer le tree shaking rapidement dans votre application et comment l'optimiser.

La bonne pratique principale est de utiliser const, car const est la seule chose que le compilateur sait à ce stade.

Si vous utilisez "platform.is_android", votre code ne sera pas triché.

Si vous voulez vérifier si votre code est triché, vous pouvez utiliser l'option "analyse" dans la ligne de commande quand vous construisez votre bouton final.

Avec la taille analysée, vous obtenez un rapport.

Et vous pouvez voir si le code a été enlevé.

Je vais vous montrer une démo rapide d'un flutter Google Wallet, un plugin que nous avons open-sourcé pour mettre les trains de tickets dans le flutter Google Wallet.

Vous pouvez donc utiliser les outils dev, vous pouvez les utiliser de votre idée préférée, je les utilise juste de la ligne de commande.

Il y a une section div dans l'outil où vous pouvez importer deux analyses.

Il y en a une que j'ai déjà faite sans les consts, avec la plateforme basique .is, et une avec les consts et le tree-shaking.

Si je fais une analyse, on voit le diminution.

C'est une analyse de la partie iOS de l'installation iOS.

On peut voir que Flutter Google Wallet est enlevé, et aussi quelques localisations Flutter, et d'autres codes, parce que nous avons inclus des codes d'accessibilité dans le plugin Flutter Google Wallet.

Ce sont des techniques assez simples à mettre en pratique.

Et maintenant, voyons si nous pouvons créer nos propres fonctionnalités éco-friandes.

Oui, Adrien a déplacé les choses à l'heure statique, nous pouvons également déclencher les choses à l'heure de la course.

Vous pouvez donc implémenter votre propre mode d'éco.

En général, il s'agit de négocier avec votre équipe, avec votre expérience utilisateur, avec votre développeur, avec votre P.O.

Un compromis qui est très bon, c'est de targuer quand vous avez besoin d'un mode d'éco.

Quand en avez-vous besoin ?

Vous en avez besoin quand votre utilisateur est en mode de vieillissement quand il a une batterie faible ou quand il est sur un ordinateur vieux ou vieux

Toutes ces choses, vous les avez avec les librairies classiques comme Battery+ ou Device+

Vous pouvez détecter ordinateurs vieux ou vieux par l'SDK de l'Android ou par la mémoire ou par le nombre de mots mais il y a beaucoup de solutions.

On a vu ce matin que Flutter est une bonne choix pour les appareils bas-fin.

Oui.

Mais si on veut aller plus loin, qu'est-ce que nous pouvons désactiver ?

Oui.

Donc, une fois que vous avez un objectif, quand vous avez besoin d'un mode Eco, c'est beaucoup plus facile de couper un peu de code pour ces situations spécifiques.

Donc, vous pouvez objectifier la chaîne UI ou la chaîne des plateformes, avoir plus de déchets dans votre app, ou plus de temps pour vivre.

Vous pouvez désactiver les SDK secondaires qui ne sont pas mandatoires.

Vous pouvez éviter ou réduire la précision de géolocalisation ou d'autres précisions si vous ne les avez pas vraiment besoin pour votre utilisateur.

Mais vous pouvez aussi targuer le thread de rastre ou les animations de transition sur les effets de mélange, l'opacité, les clips et les ombres.

Ces choses sont vraiment difficiles sur un appareil de base, alors vous pouvez améliorer la performance en la faisant plus simple.

Nous l'avons essayé sur notre flux d'embarquement, une série de 4 ou 5 écrans avec de belles animations, transitions, accueillant les utilisateurs.

Nous l'avons essayé sur un ordinateur bas-fin.

Nous avons coupé tout ce que j'ai parlé avant, la géolocalisation, l'animation, etc.

Le résultat est que le FPS sur un ordinateur bas-fin est vraiment bien, jusqu'à 60 FPS.

Et l'utilisation du CPU descend de 79% à 36% d'utilisation moyenne.

Donc en coulant quelque chose, vous améliorez vraiment votre performance sur votre flux.

La chose vraiment bien, c'est que vous n'avez pas à être un développeur de Flutter ninja hardcore.

Tout le monde peut l'utiliser, il n'y a pas de compétence hardcore.

C'est tout un sujet de choix et de balance.

Retournons à la compétence de défaut que nous avons mentionné.

Oui, c'est une autre façon de retirer certaines de vos fonctions de votre hub, mais c'est la façon hardcore ninja.

L'idée est de faire un sideload asynchronos et en mode on-demand, une fonction qui ne peut pas être utilisée si souvent par les utilisateurs.

Il n'y a pas de disturbance, ça se déroule sans problème.

Si vous avez un réseau disponible et que vous sauvez des banes de réseau, vous pouvez sauver de la storage de téléphone.

C'est assez facile à implémenter.

Prenons un exemple.

Nous parlerons de la fonction Public Transportation pour Paris dans notre app.

Utilisable pour les tickets métro.

C'est uniquement utile pour Paris, alors pourquoi ne pas le déclencher ?

Déclencher ?

Le premier pas est de déclencher votre dépendance comme dépendance déclenchée.

Ensuite, vous avez CallLoadLibrary.

C'est un futur classique de Flutter. donc vous devez gérer le chargement, le chargement de votre choix pour l'utilisateur.

Et puis, quand vous allez faire le bundle FlutterBuild, vous verrez quelques pas nouveaux, un pas qui s'appelle la validation de JensSnapShot.

C'est l'un des derniers pas dans le FlutterBuild.

Cette fonction vous donnera des conseils sur ce qui manque pour l'utilisation, et les plombings que vous devez faire pour y arriver.

Donc vous devez modifier votre perspective.yaml, ajouter des fichiers pour votre fonctionnement, des modifications dans le manifeste, des gradus de magie sombre.

Et puis ?

Et puis, chaque fois que vous vous ré-courrez, la étape de validation de la snapshot de gens vous dira chaque fois ce qui manque, vous donnera des exemples de fichiers de ce qui manque ou vous pouvez l'implémenter.

Et enfin, dans votre bundle final, vous verrez un nouveau fichier avec un .so avec le code de votre fonctionnement.

Si vous le déclenchez, vous verrez le .par.so.

Et aussi, si vous ouvrez votre application et que vous cliquez sur votre fonctionnement, vous verrez que le SplitCompat va logger certaines choses quand il est en train de vérifier le download de votre fonctionnement, etc. et en fin de compte, lancer le projet.

Jusqu'ici, nous avons vu de nombreuses techniques pour optimiser l'application, pour la rendre plus rapide, plus petite.

Et avant de passer au test et au monitoring, un mot sur la façon dont nous construisons, comment nous déployons nos factories pour construire des produits et pour construire du code.

Je pense que c'est ce qu'on appelle le troisième scope pour les gens qui étudient les émissions de gaz à eau.

C'est la pollution quand on crée le produit, pas le produit en soi, mais comment on le fait.

Je vais être rapide sur ça, mais c'est aussi une bonne idée de penser à comment on travaille.

Donc, nous, les développeurs, nos workstations, combien de moniteurs vous utilisez, vous vous déconnectez parfois ou c'est toujours en fonction ?

Et combien d'environnements vous avez, combien d'infrastructures vous déployez, en particulier si vous travaillez avec de nombreux autres développeurs et de nombreux équipes, vous pourriez avoir de nombreux environnements en marche et tout cela a un impact aussi sur l'environnement.

Certains ont.

Même chose si vous avez des branches de features longues vies,

Si vous êtes habitué à développer des fonctionnalités et les garder pendant des jours, des semaines, des mois avant de les tester ou de les envoyer en production surtout si vous avez des environnements en cours, juste en attendant c'est probablement un mauvais habit et vous devriez regarder ce qu'on appelle les 7 déchets de Lean vous pouvez faire quelque chose, vous pouvez essayer de délivrer en petits increments et faire plus de délivrage continu et de déploiement continu

Je disais qu'il faut avoir moins d'environnements de marche mais peut-être qu'il y a une exception à la question de la compatibilité des backwards.

C'est vrai que pour rester compatible et soutenir tous les outils

ça peut être nécessaire de faire plus de tests, peut-être des environnements dédiés pour tester les outils.

Mais si on ne fait pas ça, on aura des utilisateurs qui seront forcés à changer leur outil et comme nous l'avons vu, c'est très polluant.

Nous devions donc aussi avoir cela en tête.

Nous allons maintenant rapidement vérifier les solutions et outils que nous utilisons et que nous connaissons pour tester et monitorer la performance au long de l'heure.

Nous devons donc mentionner Greenspector.

Nous avons partagé avec cette compagnie française depuis des années.

They provide audits on the performance and the carbon footprint.

Last year we reached the silver level, which is not quite a good result for an application of this size.

Typically, the insights you'll get with Green Spector is the elapsed times, the energy, the payload, et le ranking de vos scénarios et flux, en particulier les pires, pour pouvoir les concentrer et travailler sur eux.

Actuellement, nous examinons d'autres outils, comme Frogger, une autre compagnie française, qui propose de mesurer le carbone sur la front-end, mais aussi sur la back-end et sur l'infrastructure cloud.

En tant que développeurs mobile, vous devriez regarder le projet EcoCode Community.

Il y a aussi un Android et un iOS plug-ins pour SonarQube qui sont disponibles depuis plusieurs mois.

Et nous pouvons aussi utiliser les outils de monitoring traditionnels.

Oui, nous avons testé quelques outils de monitoring différents.

Le plus célèbre est Firebase, qui est gratuit, et vous pouvez obtenir des données sur les latencies HTTP, sur le temps d'application.

Un outil qui propose une métrique très intéressante est Sentry qui est un outil de misère d'utilisateur qui donne des sujets sur la partie de votre application qui prend le plus d'énergie ou le plus de temps pour vous montrer à vos utilisateurs.

Cela peut être du réseau, des assets, et vous donner les sujets.

Jocelyn, vous vouliez nous parler de Maestro.

Si vous voulez écrire vos propres scénarios, une façon facile de le faire est d'utiliser le outil Maestro par mobile.dev.

Ce outil est vraiment agréable pour écrire et gérer des flux.

Tout ce que vous devez faire est d'écrire un fil YAML et décrire l'action que vous voulez prendre, comme cliquer sur un bouton, scroller ou des choses comme ça.

Maestro va donc gérer votre file YAML et votre scénario.

Comment ça vous aide ?

Ça vous aide quand vous l'intégrez avec Flashlight.

Parce que vous m'avez dit que parfois c'est un peu flou et c'est là que Flashlight apporte de la magie.

Maestro peut être un peu flou sur certains scénarios comme WebView ou PlatformView.

Flashlight est un outil qui répand le flux.

C'est créé par BAM, sponsorisé ici.

Une chose vraiment cool, c'est qu'il peut gérer vos commandes de test.

Maestro, myonboarding.yml

Vous pouvez lui dire de faire le flux autant de fois que vous voulez.

Vous voulez 10 fois, parce que parfois les résultats ne sont pas les mêmes.

Donc, il est en moyenne tout, pour que le résultat soit plus précis.

Vous pouvez y ajouter le retry, à cause du temps de flou.

Et vous pouvez également enregistrer la vidéo de ce que Maestro fait.

Il s'intègre vraiment bien avec votre CI, mais c'est seulement pour Android.

Ce que vous pouvez avoir avec Flashlight,

Avec mon mode Eco de d'avant, j'ai généré un rapport.

Normal Result est l'application que nous utilisons tous.

Eco Result est l'application qui targete tous les appareils.

Je peux les comparer avec Flashlight.

Je reçois un rapport sur la gauche, le mode normal, et sur la droite, le mode Eco.

La chose à vérifier est l'utilisation de CPU, ici 86% en descendant jusqu'à 38%.

L'utilisation de CPU haute en descendant jusqu'à...

Vous pouvez voir le CPU usage pendant le flux et le CPU usage avec votre fil.

Je n'ai pas beaucoup gagné sur le fil UI, mais quand je vérifie le fil Raster, en targetant toutes les animations de trucs de fous, j'ai droppé la conception du fil Raster.

Et c'est tout pour ma propre flashlight.

Merci pour le rapport de flashlights.

Je pense que vous avez terminé.

Retournons aux slides.

Et, puisque nous étions sur les tests...

Oui, un mot sur les tests d'intégration et le plus ninja analysé.

Vous pouvez donc gérer des tests d'intégration avec un moteur de performance custom.

Par exemple, un code d'un driver de performance avec un timeline, etc.

Le but est de tracer l'action de votre test d'intégration Flutter.

Et vous obtiendrez un Summary de JSON et un Timeline de JSON.

Ce timeline peut être ouvert en tracing Chrome ou dans le nouveau outil Perfetto de Google, qui est un autre défilé de défaut dans les outils Flutter Debugger.

Vous pouvez donc analyser vos threads dans le profond.

Avec le summary, vous avez de la bonne information, par exemple, les builds d'un cadre d'échantillons, et beaucoup d'indicatifs intéressants.

Je pense que nous avons un peu de temps, donc nous ne passons pas de temps sur les Goldens que nous utilisons pour tester l'accessibilité et vérifier que notre application rende bien nicely on all devices with very small screens.

But that might be an interesting idea if you don't do that.

And also there are assessment models and questions to try to evaluate your footprint just by answering questions, but we'll skip that.

As we've seen, there are many tools, solutions, tips to try to measure the carbon footprint and monitor the performance.

Comme nous l'avons dit au début, nous avons appris de nombreuses techniques que nous ne savions pas il y a 6 mois.

Je suis sûr que certaines d'entre elles, nous ne les connaissons pas encore, alors partagez-les.

L'idée, ce que nous voudrions que vous souveniez au bout du jour, c'est qu'il y a de nombreuses façons de réduire votre imprimé, en particulier sur les appareils utilisateurs, et en particulier sur les appareils plus vieux.

Et il y a des solutions que nous savons tous, et d'autres que quelques-uns de nous connaissent, comme peut-être les 3D contents.

Donc apprenez-les et utilisez-les.

N'oubliez pas de tester et de monitorer votre app.

Il y a beaucoup d'outils disponibles, et chacun peut répondre à vos besoins.

Et ce n'est pas toujours facile d'atteindre un impact et d'avoir des résultats en un seul coup.

Vous devez être convaincu, vous devez essayer.

N'hésitez pas à partager vos découvertes, partager ce qui vous marche.

C'est une autre façon d'optimiser l'effort et les résultats de tout ce que nous faisons.

L'année dernière, nous avons eu l'opportunité de partager sur plusieurs sujets sur Flutter.

N'hésitez pas.

Si vous avez des questions, si vous avez des choses à partager, s'il vous plaît, contactez-nous.

Peut-être que certains d'entre vous seraient intéressés à travailler avec nous.

Nous avons des ouvrages ouvert, bien sûr, donc n'hésitez pas à regarder notre site web.

N'hésitez pas à nous poser des questions, à nous contacter, vous trouverez nous facilement sur LinkedIn.

Et merci, merci beaucoup pour votre attention.

Merci !

[Applaudissements]

Merci beaucoup pour tous ces conseils et techniques.

D'accord, donc, y a-t-il des questions sur le thread ?

D'accord, d'abord, j'ai une question moi-même.

Savez-vous si Flutter consomme plus que une application native ?

Nous avons des résultats comparés avec notre application précédente, qui était native. mais il y a trop de paramètres pour vraiment comparer.

Pour le moment, l'app Flutter consomme moins que l'app native.

Je dirais que ce n'est pas un problème.

Je pourrais ajouter que l'utilisation de Flutter nous a permis de écrire moins de code, de factoriser et de travailler plus que comme un seul équipe sur une seule monorepo.

Donc nous avons clairement amélioré le temps de marché et nous écrivons moins de code.

Donc il devrait y avoir un bas point de départ en termes de construction.

D'accord, merci. J'ai une autre question de Mathieu.

Est-ce que vous allez open source un package Flutter pour savoir si un appareil est low end ?

C'est un de nos idées. C'est notre plan. et nous pensons que ce serait génial d'avoir un module comme celui-ci.

Génial, oui.

Ça peut certainement aider à tous à imprimer ces techniques que vous avez mentionnées.

Comment pouvez-vous automatiser les vérifications dont vous parlez de performance, de footprint, dans votre CI et dans toute votre expérience de développeur de Flutter 40 ?

Nous avons déjà vérifié la taille du bundle, c'est quelque chose de très facile à faire.

Juste assurez-vous de vérifier la taille du bundle et aussi la taille du final APK.

La taille du bundle ne représente pas la taille du final APK de l'expo.

Si vous avez déjà fait des tests d'intégration sur votre CI, vous pouvez aussi ajouter une option de trace, un opérateur custom, pour obtenir des résultats que vous pouvez comparer d'un logiciel à l'autre.

Il y a de plus en plus d'outils disponibles.

J'ai mentionné le plugin SonarCube d'EchoCode, qui est gratuit.

C'est assez récent et peut-être que nous pouvons l'aider à le rendre encore plus fort.

C'est quelque chose que nous n'avons pas mentionné.

Le outil est SourceLabs.

Par exemple, si vous utilisez SourceLabs pour obtenir des appareils virtuels, il y a beaucoup de métriques sur l'utilisation de CPU, l'utilisation de mémoire.

Donc si vous faites vos tests sur SourceLabs, vous obtiendrez des métriques aussi.

C'est bien de le savoir, merci.

Avec toutes ces techniques que vous avez présentées, si je suis nouveau à l'application Flutter, où commencerais-je ?

Je pense que si vous commencez de zéro, la chose Maestro + Flashlight est vraiment facile pour vous monter, vous marcher et aller à un CI.

Je commencerais ici, et puis au fur et à mesure que votre équipe grandit, ou que vous voulez mettre plus d'énergie dans ce bundle, vous allez aller plus profond que ça.

Et peut-être que vous pourriez faire un peu d'analyse de votre bundle, et tester quelques trucs, un nouveau code,

à un certain coût, et essayer de penser quelles fonctionnalités ne devraient pas être dans votre dernier bundle pour la dernière architecture.

C'est assez facile à implémenter.

C'est un bon début.

And even if you are not on your laptop and you have nothing to code and just your mobile to browse on the internet, you can have a look at the, for instance, the Référentiel d'éco-conception provided by the French government.

And I think it's being adapted currently for the whole Europe.

So it's just answering questions about your digital service.

So even when you can't code, you can just have a look at these questions and wonder what could I improve.

D'accord, merci.

Une dernière question.

Avez-vous eu des moments où vous avez dû faire des échanges difficiles ?

Je suppose que toutes ces implémentations, quand vous targez des appareils de base ou des comportements spécifiques,

ça peut rendre le code plus difficile à maintenir, et causer des bug éventuellement. et finalement avez-vous rencontré ce genre de problème, ou avez-vous eu des problèmes un mois plus tard ?

Pas vraiment. Il y a eu une phase où nous avons commencé à travailler avec AppBundle.

Nous avons, sur certains appareils, des problèmes d'architecture quand ils ont été téléchargés des magasins. et nous avons dû ajuster des fichiers gradés pour obtenir des bons résultats pour certaines architectures de dispositifs customisés.

Oui, et pas tout ce que nous parlons est encore en production.

Nous sommes vraiment heureux de préparer cette conversation car nous avons appris tellement et comme je l'ai dit, certaines des techniques nous les avons mises en production.

Nous ne savions pas de ces 6 mois.

Pas tout est en production, mais c'est une bonne façon d'innover, je pense.

Préparer des discussions.

Génial, merci beaucoup les gars.

Et, oui, c'est tout.

Merci.
