# Objectif

Aider les candidats à la [formation DO de Polytech Montpellier](https://www.polytech.umontpellier.fr/formation/cycle-ingenieur/devops) à comprendre de quoi il retourne a propose de   
+ certains concepts DEVOPS
+ les bases de la techno `git`
+ les commandes shell (CLI)
+ les bases de données
+ une application web

Les familiariser à la gestion de projet en équipe :
+ coordination
+ documentation
+ gestion des tâches
+ review de code
+ cycle de vie du repo

Le tout **par la pratique** comme le plus souvent dans la formation DO

---
# Comment démarrer le projet

## Enseignants 
Il est probable que ce projet serve pendant plusieurs années.  Chaque année on veut démarrer d'un projet propre : le présent dépôt ne doit donc contenir que l'énoncé et les instructions. 

Donc chaque année : 
1. les enseignants font un fork spécifique de ce dépôt de code
2. modifie le `README` pour ne laisser que les instructions pour les étudiants ci-dessous 
3. invitent sur ce fork les étudiants participants au projet

## Etudiants : 
3. créent un compte sur github pour ceux qui n'en ont pas déjà un
4. indiquent leur identifiant github aux enseignant qui les ajouteront comme collaborateur au dépôt de code, aussi appelé *repo(sitory)*
5. travaillent directement sur le dépôt de code auquel ils ont été ajouté
6. se répartissent le travail en concertation (serveur Discord ou autre moyen de communication) 
7. ajoutent du code sur une *branche* (une version du code) dédiée : tout le monde ne travaille pas sur la même branche, et on ne travaille pas directement sur la branche principale (`main`). Par exemple l'ajout d'une fonctionnalité (*feature*)  XXX se fait sur une branche nommée `feat-XXX`
8. demandent à ce que la feature qu'ils ont développé une fois prête soit ajoutée à la version principale du code : pour ça, ils font une *Pull Request* 
9. relisent les PR effectuées par les autres collaborateurs et leur font des remarques sur des modifs nécessaires / souhaitables et/ou acceptent la PR.
10. itèrent en repartant à l'étape 6. 

---
# Codespaces : 

## Qu'est-ce que c'est
+ une VM dans le cloud avec votre projet automatiquement copié dessus
+ un éditeur web des fichiers de votre projet 
+ un environnement de développement dans lequel vous pouvez installer des outils pour le projet
+ un endroit où est déployée votre application, vous permettant de la tester 

[Cette vidéo](https://youtu.be/Ce7A_7bXLDQ?si=dR4M7Rs_MKt4I-p1) par exemple vous explique ça plus en détail et vous montre un exemple d'application

## Combien ça coûte 
En 2025 tout compte gratuit sur GitHub a droit à 120h / mois. 
Soit largement assez *si vous respectez les consignes ci-dessous*. 

## Attention à ne pas dépasser la limite qui vous est allouée gratuitement : 
+ Reflexe à prendre : `Stop codespace` (menu CodeSpaces dans le bouton vert `code`) quand vous avez fini votre session 
+ Fermer le navigateur ne suffit pas pour arrêter la VM dans le cloud qui tourne et donc la consommation !
+ où voir la consommation actuelle ?

## Où le trouver / le lancer
Dans le bouton vert `code` en haut à droite quand regarde le contenu du repo

