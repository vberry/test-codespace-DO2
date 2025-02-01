
# Objectif

Il s'agit de mettre en place un jeu à un joueur. Le joueur représente un candidat ("DO2") à l'entrée dans la formaiton DO. Pour ça, les épreuves sont délicates (examen de dossier, entretien, ...), mais tout.e DO2 peut faire appel à l'esprit de solidarité avec la promo DO3 actuelle. L'objectif du joueur est d'obtenir ce soutien pour favoriser ses chances d'entrer en DO.

## Situation initiale
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



# Version 1

On ne gère pas explicitement les autres candidats pour le moment, mais on gère individuellement les DO3 : 
+ initialement ils n'ont pas accepté de parrainage et sont tous dans une salle différente
+ à chaque tour de jeu chacun.e des DO3 encore libre a une probabilité `p` d'avoir parrainé un autre candidat que le/la joueur/joueuse.

+ Récupérez les noms des DO3 actuels et simulez leur placement dans le jeu
+ Placez le joueur dans une salle aléatoirement
+ Mettez en place un module de questions
+ Mettez en place un module partie qui anime les tours de jeu *tant que* la partie n'est pas finie


# Version 2 : les bonus

Mettez en place des bonus :

Au fur et à mesure du jeu, la joueuse / le joueur peut gagner des badges lui procurant des avantages :
+ le badge *maître des lieux* peut être gagné en devinant dans quelle pièce iel se situe : coordonnées `x`et `y` : dans ce cas, iel pourra se déplacer deux fois par tour de jeu et ce jusqu'à la fin de la partie.
+ le badge *maître des technos* permet d'obtenir deux chances de franchir une porte : en cas de mauvaise réponse à la question permettant de franchir une porte, une deuxième question est posée. 
+ le badge *maître de l'intégration* permet d'obtenir deux chances qu'un.e DO3 encore libre et rencontré accepte de parrainer : en cas d'échec à la première question, iel accepte de poser une deuxième question. Ce badge s'obtient après avoir rencontré un DO3 **et** une DO3.

# Version 3 : simulation des autres candidats

On va gérer maintenance les candidats en concurrence avec le joueur. 
Paramètres :
+ `n` le nombre de ces autres candidats
+ `p` la probabilité de bonne réponse à une question par un de ces candidats

Chacun de ces candidats (appelons-le `C`) est placé dans une salle différente au départ
A chaque tour de jeu on simule le comportement de chaque autre candidat `C`. 
Celui-ci peut choisir de se déplacer aléatoirement dans toute salle accessible depuis sa salle actuelle.  

# Version 4 : individualités des DO3 

+ Chaque DO3 a maintenant une probabilité `d` de se déplacer d'une salle dans une autre à la fin d'un tour. 
+ Certains DO3 sont plus taquins que d'autres et nécessitent deux bonnes réponses à des questions pour accepter le parrainage.

# Version 5 : modélisation du temps et high scores

En fait se déplacer d'une pièce à une autre prend du temps : les JPO attirent beaucoup de monde et parvenir à changer de pièce prend 15mn. Le jeu démarre à 9h du matin et finit forcément à 17h avec une pause de 12h à 14h.
Mettez en place cette nouvelle contrainte. 

Gérez une table des high scores où on enregistre le nom des 10 joueurs ayant mis le moins de temps pour obtenir un parrainage : pour chacun on enregistre à quelle heure il a obtenu son parrainage.

# Version 5 : backlog

Ajoutez au code la possibilité de stocker pour chaque question le nombre de fois qu'elle a été posée et le nombre de fois qu'elle a obtenue une bonne réponse. 

Ajoutez un programme de *backlog* permettant à l'administrateur du jeu de lister les questions par ordre croissant ou décroissant de difficulté (en s'apuyant sur le taux de bonnes réponse)

