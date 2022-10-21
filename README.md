# TD_SauvgardeDonnees_Tuto_Git

Ce document est un résumé exhaustif qui reprend les principaux principes et commandes de Git/GitHub. le but de ce document est d'avoir compris les principaux fondamentaux de ces outils et de commencer à avoir de bonnes pratique vis à vis de ce dernier (Cf Workflow).


# Historique de Git

Git est un logiciel de gestion de versions décentralisé. C'est un logiciel libre et gratuit, créé en 2005 par Linus Torvalds, auteur du noyau Linux, et distribué selon les termes de la licence publique générale GNU version 2. Le principal contributeur actuel de Git, et ce depuis plus de 16 ans, est Junio C Hamano.

Depuis les années 2010, il s’agit du logiciel de gestion de versions le plus populaire dans le développement logiciel et web, qui est utilisé par des dizaines de millions de personnes, sur tous les environnements (Windows, Mac, Linux)3. Git est aussi le système à la base du célèbre site web GitHub, le plus important hébergeur de code informatique.

Git à été racheté par Microsoft le 4 juin 2018 pour une somme de 7,8 Millliard.



# Présentation GitHub/Git
- GitHub est un service permettant de stocker (héberger) des repositories en ligne (souvent utilisé par les particuliers).

- Git est un service de versionning (VCS version control system) permettant de gérer les versions des codes sur un serveur en ligne (souvent utilisé en entreprise).

Pour résumé :Git est un logiciel de gestion de version tandis que GitHub est un service en ligne d’hébergement de dépôts Git qui fait office de serveur central pour ces dépôts.

# Repository

Un repository est un emplacement où est stocké le code en ligne, il se comporte dans leurs structure comme des dossiers en arborescence et plusieurs dossiers peuvent exister dans un repo. On pourra retrouver nos fichiers à travers nos chemins de dossier comme sur une machine classique :

- exemple de chemin : Maths/algo/fichierTest

## Clone 
Le code qui va être stocké sur un repository peut être récupéré par plusieurs manières, via ssh ou https.

La manière https est la moins sécurisée car tout le monde peut avoir le lien du repository si ce dernier est en public.

La manière avec une clé ssh est plus sécurisée car cette dernière agit comme un token: elle garantit une sécurité en plus.

Plusieurs outils permettent d'accéder aux services de git  (Cf installation pour plus de details concernant l'installation):

-Git CMD (outil en ligne de commande)
-GitHub desktop (outil de visualisation et de contrôle sur une application)


# Fonctionnement de Git/GitHub

Git fonctionne en plusieurs étapes. Chaque étapes va intéférer avec un ou plsieurs blocs présent dans les outils Git/GitHub.

Le premier bloc est le bloc local ==> la machine de l'utilisateur

Le deuxième bloc est consacré à l'index, une source de sauvgarde temporaire situé entre le code local et le serveur Git/GitHub en ligne

Le dernier bloc lui est consacré aux serveurs Git/GitHub qui sont en ligne.

A travers ce document nous verrons les différentes étapes pour transferer son code sur un serveur en ligne ( points importants, commandes important à savoir, fichiers externe ect...).

## Config initiale (depuis source local)

La première étape va être d'initialiser le dossier sur la machine local en tant que repo git :

```
git init
```
## Config initiale (depuis source en ligne)


### Création de dépôt en ligne 
Git/GitHub nous laisse la possiblité de créer nos repositories en ligne directement depuis son site. Pour cela, on va 
- créer un repo 
- lui donner un nom
- ajouter un README ( facultatif)
- ajouter des fichiers facultatif en plus comme la license, gitignore (cf fichier généré par Git)
 <img width="581" alt="image" src="https://user-images.githubusercontent.com/90316879/197238657-f008f75c-fe59-4ece-b949-37d11cbfcdb0.png">

 On aura donc par defaut un lien de repo git qui va nous servir de connexion vers le repo.
 
 On peut alors initaliser le repo vide et lui envoyer nos fichiers. On peut faire :
 ``` 
 echo "# tt" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Akkuun/tt.git
```

Si jamais, on veut importer un projet, on peut lui associer une origine ( son point de connexion avec un repo git/gitHub existant)
```
git remote add origin git@github.com:user/nomrepo.git
git branch -M main
```

### Tranfert de fichiers vers les serveurs Git (git add, git commit) 

On a donc notre code local qui est prêt à indexer ses fichiers (on parle d'indexage pour le fait de transférer ses fichiers vers l'index).

L'index est la zone intermédiaire entre le code local et le code en ligne. On peut le représenter de cette manière : 

![git_workflow_001](https://user-images.githubusercontent.com/90316879/196621879-a3470e86-29d4-4618-9851-654fce8cbf0c.png)

La prochaine étape va être de signifier à git les fichiers qu'on veut transférer : 
```
git add fichier1.txt
```

Généralement, on ajoutera tout les fichiers en même (certains fichiers pourront être filtrés dans un fichier .gitignore qui contiendra les fichiers à ignorer Cf Fichier Externes) avec :

```
git add .
```

Les fichiers vont être transportés vers l'index (une zone de stockage temporaire avant le transfert vers le serveur en ligne). La prochaine étape est de pousser vers le serveur en ligne. 
Pour cela on va tout d'abord indiquer un message permettant de repérer l'utilité du transfert ( /!\ ces messages doivent bien être clairs et précis afin de ne pas être ambigües!)

```
git commit -m "rectification condition boucle pour eviter cas overflow"
```


Si jamais il ne passe pas, cela signifie qu'il y a des erreurs de conflit (Cf Erreur de conflit).

Puis on va pousser vers une origine (ici notre branche) (Cf branche)

```
git push origin [branche]
```
Bien sûr, si on travaille seul sur une branche main, on peut push sur le master directement mais c'est une mauvaise habitude de travail à avoir (Cf branche)

```
git push
```

Voilà le code est bien poussé sur le serveur en ligne !



# Erreur de conflit 

Les conflits surviennent généralement lorsque deux personnes ont modifié les mêmes lignes dans un fichier, ou si un développeur a supprimé un fichier alors qu'un autre développeur le modifiait. Dans ces cas, Git ne peut pas déterminer automatiquement la version correcte. Les conflits n'affectent que le développeur qui effectue le merge, les autres membres de l'équipe ne sont pas conscients du conflit. Git marquera le fichier comme étant en conflit et arrêtera le processus de merge. Il incombe alors aux développeurs de résoudre le conflit.

pour régler cela, il y a plusieurs manière de faire:
- Directement faire les changements sur l'IDE, les lignes qui ont été ajouté seront avec un + devant, et celles supprimées avec - , il n'y a plus qu'à garder les lignes voulues.
- Supprimer les erreurs depuis l'application (GitDesktop)
- Utiliser différentes commandes pour réglers les problèmes( Cf git diff, status)

Généralement on utilise une autre manière de faire, en utilisant des branches on va éviter au maximum ce genre de problèmes en contrôlant au maximum les erreurs avant qu'elle n'agissent sur la branche main (cf Branches) .


# Branches

Les branches sont des espaces parrallèle qui provienent de l'origine et permettent de travailler sur le même projet à plusieurs. Lors de la création du projet la seule branche présente est la branche main.

Le but des branches est de structurer et organiser les membres sur le projet afin d'éviter que des erreurs de code soit transféré sur le repo en ligne.


Pour créer une branche, il y a deux manières de faire : 

- depuis l'interface en ligne  (on parlera de GUI Git User Interface)
- ou depuis l'interface de ligne de commande (on parlera de CLI Command-line interface)

```
git checkout -b <branch-name>
```

Un message expliquant que vous avez bien changé de branche devrait apparaitre et lors de votre prochain push, votre code sera sur la nouvelle branche créée.

Attention la commande suivante permet de créer une branche sans changé de branche, le prochain push sera alors toujours sur le main

```
git branch <branch_name>
```
Il est possible également de créer une branche à travers un commit

Pour voir les différentes branches :

```
git branch -a
```


Il est aussi possible de réaliser une fusion entre une branche secondaire sur la branche actuelle (Cf pull request et Merge request).


/!\/!\/!\/!\/!\/!\ NE JAMAIS TRAVAILLER SUR LE MASTER/MAIN /!\/!\/!\/!\/!\/!\/!\/!\ Toujours travailler sur une branche!

Les branches vont être très utiles pour réaliser des opérations pour mettre à jour le code par rapport au main/master sans l'interférer.
Je m'explique, admettons SamSam travaille sur une nouvelle fonctionnalité et veut 
la push sur le master (on suppose qu'elle travaille bien et à bien compris le principe de branche car elle se situe déjà sur la branche SamSam ou une branche décrivant sa fonctionnalité (le plus couraement fait)). Elle va donc fusionner son travail avec le main mais sur sa branche, pour cela elle doit récupérer le master/main en local en faisant :

```
git pull origin [branche]
```
Elle va régler les erreurs de conflits s'il y en a. Son code sera donc compatible avec le main car elle sera assurée qu'il y a pas d'erreurs.

```
git add .
git commit -m "message expliquant clairement ce qu'elle a fait"
git push origin main
```

# Fonctionnalité en plus importante

## Pull request et Merge request (mise à jour de branche participative à Mise à jour de branche originelle)

Il est possible de demander une récupération de code de la branche main au propriétaire directement via un pull request grace à l'interface en ligne /application ou avec la commande git merge :

```
git merge origin [branchName]
```

### Exemple pull request 
Reprenons notre exemple précédent, dans notre projet la branche main à été mise à jour par SamSam auparavant et Corentin vient de revenir de vacances et veut travailler sur une fonctionnalité, pour cela il doit récupérer la dernière version à jour du main, il pour cela il peut aller sur Git/GitHub et voir une option qui indique qu'il a du retard par rapport à la version du code du main :
<img width="660" alt="image" src="https://user-images.githubusercontent.com/90316879/196640143-f886ad6b-457e-4083-94f7-3c4497b3ad1d.png">

Pour rattraper ce retard il va faire une demande de pull request (toujours avec un message scpécifiant cette demande.
<img width="903" alt="image" src="https://user-images.githubusercontent.com/90316879/196640510-f6a36d63-2608-4d4d-8acd-de8645d95ef4.png">

Le propriétaitre va alors accepter ou non cette requête s'il acccepte la request sera fermée et la branche de Corentin aura bien récupéré le contenu du main. 

### Exemple merge request
Le Merge request permet de fusionner toutes les ressource nécéssaire pour que la branche actuelle recoive tout le contenu de la branche passé en paramètre.

Par exemple, je suis dans la branche A. Je fais

```
git merge origin B
```

Le contenu de B va être fusionné avec A sur la branche A.  /!\ Bien vérifier d'être sur la bonne branche pour réaliser le merge!

Il est possible de faire uniquement cette commande avec git merge, ce qui va merge le contenu de la branche actuelle avec la branche spécifié par défaut du répo.

```
git merge
```




## Log

Pour voir l'historique des commits sur la branche actuelle, on peut utiliser la commande git log, qui nous donnera la description du dernier commmit qui est composé de cette manière : 
Commit : xxxxxxx (identifiant du commit)
Author : xxxx
Date : 

```
git log
```


## Fork

Au sein de GitHub, un « fork » constitue une simple copie d'un projet au sein de votre espace de nom personnel,ce qui permet de récupérer en plus des codes, historique des commits, des ressources utilisées ect ...

/!\ à différentier avec un simple clone, le clone va lui copier un projet en local qui sera syncronisé avec le serveur tandis que le fork est une duplication indépedante du repo originelle qui pourra faire son cycle de vie à part sans être synchrnonisé au repo du main.

Une fois le fork réalisé, cela permet aussi d'accéder à tout l'historique du projet( version du code, message des commits....).

Je pense que si on utilise un projet dans un cadre d'une réalisation à but d'évolution, il faut réaliser un fork pour pouvoir avoir tout l'hsitorique du projet et repecter le travail réalisé auparavant par les créateur du repo d'origine afin de travailler de notre côté avec toutes les ressources dupliquées.


# Fichier Externes géré par Git

## README
Le fichier Readme permet de spécifier et d'indiquer des informations sur projet à l'utilisateur qui va utiliser le repository.
Le fichier reame.md (markdown) est codé avec un langage de balisage (comme HTML). C'est utilisé pour réaliser différentes structure de style :

   # Titre
   ## Sous titre

```bash
  des commandes sur différents langages possible
```

- proposition

![Logo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/th5xamgrr6se0x5ro4g6.png)

## git ignore

Un fichier git .ignore est un fichier qui permet de ne pas prendre en compte certains fichier en fonction de leur extension.
voici un exmple d'un fichier .ignore

<img width="901" alt="image" src="https://user-images.githubusercontent.com/90316879/197197009-c0d03690-e568-4a9c-a6b3-75cd08920f47.png">

# tag
 à faire
Git proposes un service sur  Les tags sont des réfs qui pointent vers des points spécifiques de l'historique Git. Les tags sont généralement utilisés pour capturer un point de l'historique utilisé pour une version marquée (c. -à-d., v1. 0.1).

# WorkFlow (Git flow/GitHub flow)
Git flow est une méthode de travaille (on parle de workFlow) expliquant comment travailler de manière optimisé sur son projet à travers les différentes branches.
Cette méthode à été proposé par Vincent Driessen en 2010.

Avec cette méthode, le projet doit utiliser seuelement 5 branches : 

Main ==> Represente la branche utilisé en production
Develop ==> Represente la branche avec les derniers déplacement
Feature
Release
Hotfix
 
 
A noté que deux manières de travailler avec cette méthode est possible :

-GitHub Flow qui est plus simple que Git flow destinée pour des teams de dev web et d'application, elle est surtout utiliser pour les opérations DevOPS. Mais cette méthode n'utilise pas toutes les branches de git flow ce qui peut généré des problèmes dans le futur.

-GitLab flow est une alternative à Git flow qui est resemblant dans sa composition 




diff,roolback,

gestion de projet   ( tag dans commit), ticket
git confign git 


reverte

clone

