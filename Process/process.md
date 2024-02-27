# Let's try to recap what I have for now (2024-02-27)

## Game overview

A game third person 3D exploration game about a world plunged into a never-ending winter. The player is an explorer from a village/tribe who goes on an adventure to find a new source of energy for the survival of his people. The player will explore the world, find ancient and mysterious structures, and meet other explorers and eventually learn what happened to the world and the ancient civilization throught a fragmented narrative.

## Story, setting and characters

Le jeu prend place dans un monde fictif plongé dans un hiver continu. Le joueur joue un explorateur provenant d’un village/tribu qui part à l'aventure. Par le passé une autre espèce, aujourd’hui disparue, était sur cette planète. Cette ancienne civilisation était bien plus avancée technologiquement que celle du joueur. La civilisation du joueur a, au fil du temps, récupéré des objets et des technologies de l'ancienne civilisation pour les intégrer à leurs usages. Au centre du village du joueur se trouve un noyau énergétique (une source d’énergie provenant de l’ancienne civilisation) qui permet de maintenir une température acceptable dans le village. Cependant, le noyau est défaillant et le joueur doit partir à l’aventure pour en récupérer un nouveau. Le joueur a à sa disposition une technologie de propulsion nouvellement créée par son village qui lui permet de se déplacer plus rapidement et plus facilement dans le monde, lui permettant d'explorer des lieux où son espèce n'a jamais mis les pieds auparavent.

À terme, le joueur apprend que, il y a des centaines de milliers d'années, l'ancienne civilisation était elle aussi à la recherche d'une puissante source d'énergie. Dans ce but, elle a construit une machine qui pompe la chaleur du coeur de la planète, ce qui a mené au refroidissement progressif de la planète et à sa disparition. Le joueur apprend alors que la source d'énergie qu'il recherche et qui lui permet de survivre dans l'environnement est la cause des conditions de vie actuelles.

Environnement :
- L'environnement est recouvert de neige et de glace et comprend montagnes, vallons et falaises (idées de structures naturelles : caynon de glace, tempête de neige, lac gelé, grottes).
- Des structures gigantesques de l'ancienne civilisation sont éparpillées dans le monde.
- Le joueur peut rencontrer d'autres explorateurs qui lui partagent leurs histoires/rumeurs.

Comment est racontée l'histoire ?
- Narration environnementale
- Dialogues avec les autres explorateurs

**Plot holes**
- Pourquoi le joueur part à l’aventure ?
- Comment l'ancienne civilisation a disparu ? Déclin lent ou disparition soudaine ?
- Qu'est-ce que l'ancienne civilisation cherchait à faire? Pourquoi cherchaient-ils une source d'énergie puissante ?
- Contradiction entre manque d'énergie au village et présence de stations de recharge dans l'environnement

**Environment Moodboard**
<image src="./images/24-02-27_env-moodboard-v2.png">

**Ancient Civilization Moodboard**
<image src="./images/24-02-27_civ-moodboard-v2.png">

**Player's Civilization Moodboard**
<image src="./images/24-02-27_player-civ-moodboard-v2.png">

**Visual research**


https://github.com/fly04/diploma-project/assets/46554723/1cb64461-7780-4c29-912a-568d6f7b0e0c



## Gameplay
Le gameplay est centré autour du mouvement.
Le joueur peut :
- **Marcher/Courir**
- **Sauter**
- **Glisser** : le joueur peut glisser naturellement sur la neige pour se déplacer plus rapidement et dévaller les pentes pour accumuler du momentum.
- **Se propulser horizontalement** : le joueur peut se propulser horizontalement pour remonter les pentes ou parcourir de larges distances plus rapidement
- **Se propulser verticalement** : le joueur peut se propulser verticalement pour atteindre des hauteurs inaccessibles autrement

La propulstion est limitée et doit être rechargée en se tenant près d'une station de recharge. Ainsi, il est possible de limiter les déplacements du joueur et le guider vers les lieux importants. Elle permet également de créer des phases de plateforme.

### Storyboards
- Glisse
<image style="width: 800px;" src="./images/24-02-27_storyboard-slide.png">
- Propulsion horizontale
<image style="width: 800px;" src="./images/24-02-27_storyboard-propel-horiz.png">
- Propulsion verticale
<image style="width: 800px;" src="./images/24-02-27_storyboard-propel-vert.png">

### Prototyping


https://github.com/fly04/diploma-project/assets/46554723/7f88cc49-fd57-468c-aa7b-c1084fea2889


https://github.com/fly04/diploma-project/assets/46554723/97dae183-bba9-4159-88fd-8ddfc144b4a7



## Game Structure

- Le jeu est structuré en zones ouvertes reliées entre elles.
- Chaque zone comprend des points d'intérêts et des lieux à explorer (stations de recharge, structures de l'ancienne civilisation, landmarks, autres explorateurs).
- Certains points d'intérêts sont des lieux clés permettant de donner des éléments clés de la narration, accéder à un nouveau lieu, explication d'une mécanique, découvrir un raccourci.
- Les autres points d'intérêt mènent le jouers vers les points clés.

Exemple de circulation chart *(comment modérer le nombre de poi que le joueur va ajouter à sa liste interne en une seule fois =/= comment le joueur doit explorer)*

<image style="width: 500px;" src="./images/24-02-27_circulation-chart-v2.png">

Le jeu altèrne entre :
- phase d'exploration dans l'environnement ouvert : cherche de points d'intérêt, rencontre d'autres explorateurs, recherche de stations de recharge
- phase d'exploration dans les structures de l'ancienne civilisation : plateforming, découverte de la narration environnementale

## Interface
L'interface est minimaliste. Idéalement, le maximum d'information est présentée de manière intradiégétique. Par exemple, la barre de propulsion est représentée par un objet sur le personnage.

- Exemples (Astroneer, Deadspace) :
<image style="width:500px" src="./images/24-02-27_interface-example-v2.png">

## Intentions
- Sense of freedom while exploring (fluid movements, rythm)
- Awe and wonder (gigantic structures from the ancient civilization)
- Tense of unknown (inside of the structures, the unknown, the cold)

## Scale

- Demo : ~1 zone, about 15min of gameplay (?)
- Full game : 6-7 zones, about 5 hours of gameplay

## Games

To play/finish :
- [Kairo](https://store.steampowered.com/app/233230/Kairo/)
- [NaissanceE](https://store.steampowered.com/app/265690/NaissanceE/)
- [A Short Hike](https://store.steampowered.com/app/1055540/A_Short_Hike/)
- [Valley](https://store.steampowered.com/app/378610/Valley/)

Other inspirations :
- [Journey](https://store.steampowered.com/app/638230/Journey/)
- [Outer Wilds](https://store.steampowered.com/app/753640/Outer_Wilds/)
- [Sable](https://store.steampowered.com/app/757310/Sable/)
