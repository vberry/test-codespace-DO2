# Règles du jeu

Lisez entièrement le sujet avant de commencer.

## Situation initiale
Le joueur / la joueuse représente un.e candidat.e ("DO2") à l'entrée dans la formaiton DO. Pour ça, les épreuves sont délicates (examen de dossier, entretien, ...), mais tout.e DO2 peut faire appel à l'esprit de solidarité avec la promo DO3 actuelle. L'objectif du joueur est d'obtenir ce soutien pour favoriser ses chances d'entrer en DO.

Lors des JPOs, l'aspirant.e DO2 entre à Polytech Montpellier en rêvant des miracles qu'iel va accomplir grâce à la formation DO. Perdu dans ses rêves, iel reprend ses esprits dans une sallle vide et inconnue de l'école. Les salles de l'école sont organisées suivant un damier de 6 x 6 cases. Dans 15 de ses salles, un.e DO3 est en train de travailler sur un projet qu'il doit rendre bientôt. Il est possible de passer de n'importe quelle salle à une salle adjacente orthogonalement, sous condition (voir ci-dessous)

## Objectif
Le but du jeu est de trouver un DO3 et d'obtenir s'on parrainage.
Mais le joueur / la joueuse pas seul.e à parcourir les salles de Polytech et chaque DO3 ne peut parrainer q'une seule personne ! Plus le temps passe, plus les DO3 ont accepté de parrainer d'autres candidats. 
+ la partie est perdue quand plus aucun DO3 n'est dispo. 
+ elle est gagnée si un DO3 accepte le parrainage.

Le jeu est découpé en tours : 
+ à chaque tour de jeu on peut se déplacer dans une pièce 
+ si on arrive dans une pièce où se situe un.e DO3 on peut essayer d'obtenir le parrainage.

Il s'agit d'un jeu de **devinettes** :
+ chaque porte de communication entre salle a été programmée pour ne s'ouvrir qu'en cas de bonne réponse à une question posée par les serveurs de l'école. Cette question est choisie au hasard parmi une liste de questions disponibles
+ Chaque DO3 rencontré peut donner son parrainage (s'il ne l'a pas déjà accordé à un autre candidat) : mais ce parrainage n'est accordé qu'en cas de bonne réponse à une question

#### Web: version simple
---
# Version 1

On ne gère pas explicitement les autres candidats pour le moment, mais on gère individuellement les DO3 : 
+ initialement ils n'ont pas accepté de parrainage et sont tous dans une salle différente
+ à chaque tour de jeu chacun.e des DO3 encore libre a une probabilité `p` d'avoir parrainé un autre candidat que le/la joueur/joueuse.

+ Récupérez les noms des DO3 actuels et simulez leur placement dans le jeu
+ Placez le joueur dans une salle aléatoirement
+ Mettez en place une liste de questions dans un fichier et un module de questions
+ Mettez en place un module partie qui anime les tours de jeu *tant que* la partie n'est pas finie
+ Mettez en place un LAUNCHME.md donnant les instructions pour lancer le jeu (qu'on testera surtout sur CodeSpaces)

# Versions suivantes

En fonction de votre motivation et de votre intérêt vous pourrez participer à la mise en place d'autres fonctionnalités détaillées ci-dessous. Ce choix doit se faire en coordination avec les autres développeurs / ou votre référent *accompagnement DO*.

## Fonctionnalité `B` (DEV) : les bonus

Mettez en place des bonus :

Au fur et à mesure du jeu, la joueuse / le joueur peut gagner des badges lui procurant des avantages :
+ le badge *maître des lieux* peut être gagné en devinant dans quelle pièce iel se situe : coordonnées `x`et `y` : dans ce cas, iel pourra se déplacer deux fois par tour de jeu et ce jusqu'à la fin de la partie.
+ le badge *maître des technos* permet d'obtenir deux chances de franchir une porte : en cas de mauvaise réponse à la question permettant de franchir une porte, une deuxième question est posée. 
+ le badge *maître de l'intégration* permet d'obtenir deux chances qu'un.e DO3 encore libre et rencontré accepte de parrainer : en cas d'échec à la première question, iel accepte de poser une deuxième question. Ce badge s'obtient après avoir rencontré un DO3 **et** une DO3.

## Fonctionnalité `D` (DEVOPS) : utilisation d'une base de données

Mettez en place ce qu'il faut pour que les questions ne soient plus stockées dans un fichier mais soient maintenant dans une base de données. Pour coller au plus près du programme de PeiP suivi par certains d'entre vous, on choisira une base de données relationnelle, et on la manipulera depuis un SGBD `postgres`. Une solution plus simple est d'utiliser SQLite: la base est stockée dans un fichier, il est très simple de faire des backup et de retrouver un état fonctionnel, et tout peut se faire en local.

Si la **fonctionnalité `H`** a été implémentée / ou en prévision de cette fonctionnalité, proposez aussi dans la base ce qui est nécessaire pour enregistrer les meilleurs scores.

### Conception

Vous choisirez conjointement le schéma de la base (tables, champs) et documenterez ce choix dans un fichier `BD.md` 

### OPS
La base de données ne sera pour l'instant pas hébergée en live en permanence sur un site internet dédié, on se limitera à sa génération sur la machine du joueur = l'environnement déployé dans CodeSpaces. 

Explorez les façons de configurer CodeSpaces pour qu'il contienne un serveur de base de données de type `postgres` et que celles-ci puisse être remplie avant le démarrage du jeu. Consultez par exemple [cette page](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-python-project-for-codespaces).

Une fois le fichier de configuration de CodeSpaces mis en place, pour que celui-ci s'active, il vous faudra peut-être supprimer votre CodeSpace actuel (créé sans cette configuration) pour en recréer un disposant de cette capacité de base de données. Ceci ne vous fera pas perdre le contenu de votre projet, stocké indépendamment des CodeSpaces.

Pensez que chaque personne créant un nouveau CodeSpaces depuis ce repo de code aura une BD vide au départ, donc mettez en place ce qui lui permettra d'avoir une BD pleine pour démarrer le jeu.

### DEV
pour le jeu, vous mettrez en place les accès à cette base dans un module `BD` utilisé par le module  `questions`.

### DEVOPS

Un programme spécifique permettra de transférer le contenu du fichier texte des questions de la *Version 1* pour remplir la base de données.


## Fonctionnalité `C` (DEV) : simulation des autres candidats

On va gérer maintenance les candidats en concurrence avec le joueur. 
Paramètres :
+ `n` le nombre de ces autres candidats
+ `p` la probabilité de bonne réponse à une question par un de ces candidats

Chacun de ces candidats (appelons-le `C`) est placé dans une salle différente au départ
A chaque tour de jeu on simule le comportement de chaque autre candidat `C`. 
Celui-ci peut choisir de se déplacer aléatoirement dans toute salle accessible depuis sa salle actuelle.  

## Fonctionnalité `I` (DEV) : individualités des DO3 

+ Chaque DO3 a maintenant une probabilité `d` de se déplacer d'une salle dans une autre à la fin d'un tour. 
+ Certains DO3 sont plus taquins que d'autres et nécessitent deux bonnes réponses à des questions pour accepter le parrainage.

## Fonctionnalité `H` (DEV) : modélisation de high scores

PLutôt que `gagné`et `perdu` maintenant on veut ajouter un score à chaque partie. Ce score sera basé sur le temps mis pour finir le jeu. 

En fait se déplacer d'une pièce à une autre de l'école pendant les JPO prend du temps : cet événement attire beaucoup de monde et parvenir à changer de pièce prend 15mn. Le jeu démarre à 9h du matin et finit forcément à 17h avec une pause de 12h à 14h.
Mettez en place cette nouvelle contrainte et cette façon d'obtenir un `score`. 

Gérez une table des high scores où on enregistre le nom des 10 joueurs ayant mis le moins de temps pour obtenir un parrainage : pour chacun on enregistre à quelle heure il a obtenu son parrainage.

## Fonctionnalité `T`(DEVOPS) : les tests et la CI

En entreprise, quand on écrit des fonctions dans n'importe quel langage de programmation, on mets en place des tests unitaires permettant de tester le comportement de chaque fonction. 

Utilisez le framework `pytest` pour pouvoir implémenter des tests unitaires. Pour cela, il va falloir potentiellement modifier la configuration de votre CodeSpace pour qu'il contienne cet outil. Soit vous trouvez moyen de faire ça automatiquement par les fichiers du dossier `.devcontainer`, soit vous ajoutez ça manuellement dans votre CodeSpace avec l'outil `pip`.

Proposez plusieurs tests pour des fonctions déjà écrites dans le code du projet. Attention, pensez à mettre tous les tests dans un dossiers `tests`.

Une fois que vous pouvez lancer les tests, si certains échouent, cela peut indiquer que le code du projet contient des erreurs, faîtes une issue pour ça. 

Une fois que les premiers tests sont au point, vous avez deux directions vers lesquelles vous orienter : 
1. vous pouvez explore GitHub actions pour les déclencher automatiquement à chaque nouveau commit sur une branche, c'est la façon recommandée de procéder, plutôt que de les lancer à la main comme ci-dessus.
2. Vous devriez regarder aussi la notion de *test coverage* et mettre en place une façon d'obtenir un rapport sur cette mesure, puis d'indiquer dans le projet les parties non couvertes.

## Fonctionnalité `BL` (DEV) : backlog
Ajoutez au stockage ce qui est nécessaire pour enregistrer pour chaque question le nombre de fois qu'elle a été posée et le nombre de fois qu'elle a obtenue une bonne réponse. 

Ajoutez aussi le fait que chaque question appartient à un thème : questions sur Git, questions sur Python, ...

Proposez un programme de *backlog* permettant à l'administrateur du jeu de lister les questions par ordre croissant ou décroissant de difficulté (en s'apuyant sur le taux de bonnes réponse)

Le programme backlog doit permettre aussi d'imposer un thème pour les questions des prochaines parties. Pour ça il modifiera un fichier de configuration. Modifiez aussi le code du jeu pour qu'il lise ce fichier de configuraiton au lancement et ne propose ensuite pendant le jeu que des questions de ce thème.

Note : *si la fonctionnalité `B`* a été implémentée, le stockage des infos nécessaires au bakclog se fera dans la base de données mise en place, dont les tables devont donc être complétées (mettez à jour aussi `BD.md`).*

## Fonctionnalité 'W' (DEV) : version web

En utilisant un framework simple (comme `flask`en Python) proposez une version web de ce jeu, dans un premier temps toujours à un seul joueur. Adoptez un design simple, ce qui compte avant tout c'est que le jeu reste jouable. Vous développerez cette fonctionnalité dans une branche séparée de master que vous appellerez `version-web`.

Ensuite au fur et à mesure des explorations du joueur pendant le jeu, vous pouvez afficher la carte des salles explorées par le joueur, pour l'aider à choisir les prochaines directions dans lesquelles il se rendra. 

Ensuite, on peut profiter que toutes les requêtes des joueurs s'adressent au même serveur pour permettre un jeu à plusieurs joueurs. Pour ça gérez le fait que toutes les 15 minutes le serveur démarre une nouvelle partie et permettent aux joueurs qui se connectent juste avant le début de la partie de participer à la prochaine partie (prenez leur nom, affichez un timeout indiquant le nombre de minutes / secondes avant le début de la prochaine partie). Adaptez la logique du jeu pour qu'il gère la position de tous les joueurs de la partie et leur demande les actions qu'ils veulent faire, informez chaque joueur des actions réussies / ratées par les autres joueurs.


#### Web: version simple

Si vous implémentez un "core" (comme une classe par exemple), sur lequel vous exposez les fonctions (méthodes) du jeu (e.g. def avancer(self, direction): ..), le découpage devient assez simple :
+ Pour votre version en ligne de commande, vous avez un "core" d'initialisé en tant que variable global, et vous bouclez sur des prises d'input et des affichages de grille, en appelant les méthodes du "core" pour effectuer des actions ou récupérer l'état de la grille.
+ Pour votre version web, vous avez un "core" d'initialisé en tant que variable globale ou attribut de l'application web, et ce sont cette fois vos "routes" qui permettent d'interagir avec le core. Pour répondre aux questions, vous pouvez utiliser une route supplémentaire.

Vous pouvez donc utiliser le même core pour ces 2 versions. En termes de software design, votre "core" devient une dépendance. Même pour la version web, vous pouvez très bien avoir une méthode d'affichage sur votre core et n'afficher la grille que dans le terminal. Dans ce cas vous n'avez fait que remplacer les inputs CLI par des requêtes http, mais c'est déjà bien.


#### Web: version moins simple

L'affichage dans le terminal, c'est bien, mais vous avez un navigateur. Pour remplacer l'affichage du terminal (que vous pouvez aussi garder comme logs), ajouter une route pour renvoyer du html permettrait d'afficher une grille sur le navigateur. Vous pouvez générer le html directement sous la déclaration de la route. Mais vous allez devoir changer d'url sur le navigateur pour faire des actions et récupérer le rendu.

#### Web: version complexe

L'idéal serait de renvoyer les données de la grille (e.g. en json), plutôt que directement un rendu en html. Vous pouvez créer des routes permettant de renvoyer directement un fichier html, un fichier css, et un fichier js (attention à ce que vos "src" et "href" des balises "script" et "link" matchent bien les routes définies)

Si le lab de web est bien compris, jouer avec le DOM et utiliser l'api fetch dans votre script.js vous permettra, par requêtes http sur les bonnes routes, à effectuer des actions, et récupérer l'état de la grille sous forme de json (et mettre en place des champs pour répondre aux questions).

#### Web: version encore plus complexe

Dans le lab web avec deno, le front et le back étaient 2 serveurs différents. Vous pouvez séparer front et back, et donc avoir un front avec deno même si le back est en python (attention CORS).

Encore mieux, vous pouvez préparer le cross-platforme multijoueur en réécrivant votre version terminal, plutôt qu'interagir directement avec le "core" auparavant variable global, vous pouvez utiliser le package "requests" pour faire les mêmes requêtes que celles que vous aviez en html/js avec http pour interagir avec le jeu.

Temps réel : passez en mode websocket pour éliminer l'aspect tour par tour.