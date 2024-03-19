# Character controller et esthétique
## Retour sur les retours
En travaillant sur l'implémentation du slide jump, je me suis rendu compte de tout un tas de problèmes avec mon character controller. Je pense par exemple à : le fait que le personnage fasse des *bumps* vers le haut lorsqu'il passe d'un plan plat à une pente qui casse la vitesse et annule le slide, le fait que lorsque tous les boutons sont appuyés en même temps le controller se casse et le personnage s'envole à toute vitesse, le fait que je n'ai pas trouvé de solution pour gérer les impulsions et transitions entre différentes vitesse de manière smooth. En bref, pour la 3?ème et (j'espère) dernière fois, j'ai complètement changé la manière de gérer les mouvements. J'ai décidé d'utiliser un asset trouvé sur l'asset store de Unity : [Kinematic Character Controller](https://assetstore.unity.com/packages/tools/physics/kinematic-character-controller-99131). Ce dernier ne donne pas un character controller fonctionnel out of the box, mais offre une interface qui permet d'utiliser de nombreux callbacks d'une classe où la logique cinématique est complètement réécrite (n'utilisant donc pas le rigidbody de Unity). Ainsi, je peux me focaliser sur la logique des mouvements avec une fondation solide. Après avoir passé beaucoup de temps sur les autres méthodes d'implémentation, j'ai fini par bien comprendre la logique dont j'avais besoin pour les mouvements et ai pu intégrer les déplacements, gestion des pentes, saut, glisse et slide jump très rapidement, et le résultat est bien meilleur que les précédentes itérations. J'espère que cette fois c'est la bonne !

# More on character controller and level design process (2024-03-13)
## Retours sur les tutoriels
J'ai terminé la série de tutoriel mentionnée précédemment. Toutefois, j'ai rencontré certains problèmes avec le fonctionnement proposé. J'ai donc décidé de faire des tests personnels avec toutes les manières que j'ai pu voir passer jusqu'ici, à savoir utiliser un character controller, utiliser un rigidbody en fixant manuellement la vélocité et utiliser un rigidbody en lui appliquant des forces. Finalement, j'ai choisi de travailler avec cette dernière solution car, si elle ne me permet pas d'être aussi précis que en défissant la vélocité, elle me permet plus facilement de gérer les différents cas de figures.

## Considérations sur la glisse
Activer l'état de glisse automatiquement semble finalement ne pas être la bonne solution. Le joueur est moins en contrôle ce qui rend la mécanique moins intéressante. La solution retenue jusqu'ici est que si le joueur dépasse une certaine vitesse et appuie sur un bouton, il se met à glisser. Concernant le problème de mélanger la glisse en tant que mécanique et le fait de glisser sur une pente trop raide, il me semble qu'il suffirait de les considérer différemment et que cela se soit visuellement pour ne pas créer de confusion.

## Level design
Ayant une idée plus claire de mes mécaniques, j'ai commencé à réflechir au level design en m'inspirant [du process de Steve Lee](https://www.youtube.com/watch?v=0FSssDWEFLc) consistant à penser son niveau avec du texte, mes premières itérations sont [ici](./leveldesign.md).

## Ancienne civilisation
Je réflechissais à quoi ressembleraient 'les interfaces' de l'ancienne civilisation avec lesquelles le joueur pourrait interagir pour débloquer de nouveaux passages. En gros, à quoi ressemblent les boutons et leviers de cette civilisation ? J'aimerais m'éloigner de l'aspect mécanique d'un levier ou d'un bouton pour quelque chose de plus mystérieux, plus proche du fantastique. 

En brainstormant, l'idée de "maquettes" que les anciens manipulaient pour modifier la réalité m'a plu, des sortes de "poupées vaudous" dont les effets seraient répliqués sur le monde réel. En jeu, cela se tradurait par une simple interaction avec la maquette (genre appuyer sur X pour interagir), par exemple face à un pont détruit, le joueur pourrait interagir avec sa maquette dans un autre lieu pour le "reconstruire". Cela pourrait peut-être également me permettre de créer des puzzles basés sur cette mécanique (activer des trucs selon une bonne séquence?). 

Maintenant à voir comment je peux rattacher ça aux éléments de lore que j'avais établi pour l'ancienne civilisation et si je peux l'étendre à d'autres situations.

# Character controller stuff (2024-02-28)
## Tutoriels
Mon plan est de me baser sur un character controller provenant de tutoriels et de construire sur cette base pour mécaniques et interactions spécifiques à mon projet. J'ai commencé par suivre cette [série de vidéos](https://www.youtube.com/playlist?list=PLh9SS5jRVLAleXEcDTWxBF39UjyrFc6Nb), toutefois je me rend compte que la manière dont ce dernier est conçu ne répond pas à mes attentes. Notamment le fait que beaucoup de hacks sont utilisés pour la gestion des slopes ce qui rend le fait de construire par dessus très compliqué.

Sur la base des problèmes rencontrés, j'ai cherché d'autres séries de vidéos davantage adaptées à mes besoins. Pour les deux prochains jours, je prévois de travailler sur [cette approche](https://www.youtube.com/playlist?list=PLxAJ_iP7Q93v70WAqtPoA8MYNLJeIKvPU) qui d'après les passages que j'ai regardé me paraît beaucoup plus détaillée (en termes d'explications et de fonctionnalités) et solide.

## Considérations sur la glisse
En travaillant sur mon character controller, certains questions ont émergé concernant la mécanique de glisse :
- Dans beaucoup de jeux, il y a deux cas de figure par rapport aux slopes : soit la pente a un angle plus grand que la pente maximale que le joueur peut monter alors lorsqu'il est dessus il glisse doucement vers le bas et lorsque il est en bas et qu'il essaie de monter il ne peut pas, soit la pente a un angle plus petit et le joueur peut monter et descendre dessus (parfois avec un multiplicateur de vitesse en fonction de l'angle).
- Comment intégrer le fait de pouvoir glisser pour traverser de grandes étendues (composées à la fois de dénivellés ayant de grandes et petites pentes) ? Pour le cas de la descente d'une pente ayant un angle plus grand que le treshold, il joueur doit simplement se diriger vers la pente ce qui le fera passer en mode glisse. Pour le cas où l'angle de la pente est plus petit que le threshold, comment est-ce que le joueur fait pour passer en mode glisse ?
    - Une possibilité serait de faire passer en "mode glisse" sur un input, toutefois si c'est le cas je trouverais ça bizarre que lorsque le joueur descend une pente qui dépasse le treshold, il passe en mode glisse automatiquement et que d'autres fois il doive appuyer sur un bouton.
    - L'approche que je vais essayer est de faire en sorte que le joueur passe en mode glisse lorsqu'il dépasse une certaine vitesse (en prenant en compte que selon l'angle de la pente, il se déplace plus ou moins vite). Un éventuel problème serait que le joueur puisse passer en mode glisse lorsqu'il ne le souhaite pas, mais à priori cela devrait pouvoir être gérable avec une inclinaison plus ou moins grande du joystick (à vérifer avec des playtest).

# Let's try to recap what I have for now (2024-02-27)

## Game overview

A third person 3D exploration game about a world plunged into a never-ending winter. The player is an explorer from a village/tribe who goes on an adventure to find a new source of energy for the survival of his people. Revolving around movement, the player will explore the world, find ancient and mysterious structures, and meet other explorers and eventually learn what happened to the world and the ancient civilization throught a fragmented narrative.

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

**Plot holes/Trucs à définir**
- Pourquoi le joueur part à l’aventure ?
- Comment l'ancienne civilisation a disparu ? Déclin lent ou disparition soudaine ?
- Qu'est-ce que l'ancienne civilisation cherchait à faire? Pourquoi cherchaient-ils une source d'énergie puissante ?
- Contradiction entre manque d'énergie au village et présence de stations de recharge dans l'environnement
- Expliquer la présence des structures de l'ancienne civilisation dans l'environnement
- Quelles sont les attentes du village vis-à-vis de leur propulseur? Est-ce qu'ils ont fait exprès qu'il soit rechargeable avec les anciennes stations de recharge?

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
