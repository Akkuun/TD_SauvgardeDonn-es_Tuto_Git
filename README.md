# TD_SauvgardeDonnees_Tuto_Git

Ce document est un résumé exhaustif qui reprend les principaux aspects et commandes de Git/GitHub. le but de ce document est d'avoir compris les principaux fondamentaux de ces outils et de commencer à avoir de bonnes pratiques vis-à-vis de ce dernier (Cf Workflow).


# Historique de Git

Git est un logiciel de gestion de versions décentralisé. C'est un logiciel libre et gratuit, créé en 2005 par Linus Torvalds, auteur du noyau Linux, et distribué selon les termes de la licence publique générale GNU version 2. Le principal contributeur actuel de Git, et ce depuis plus de 16 ans, est Junio C Hamano.

Depuis les années 2010, il s’agit du logiciel de gestion de versions le plus populaire dans le développement logiciel et web, qui est utilisé par des dizaines de millions de personnes, sur tous les environnements (Windows, Mac, Linux)3. Git est aussi le système à la base du célèbre site web GitHub, le plus important hébergeur de code informatique.

Git à été racheté par Microsoft le 4 juin 2018 pour une somme de 7,8 Milliards de dollars.



# Présentation GitHub/Git
- GitHub est un service permettant d'héberger des repositories en ligne (souvent utilisé par les particuliers).

- Git est un service de versionning (VCS version control system) permettant de gérer les versions des codes sur un serveur en ligne (souvent utilisé en entreprise).

Pour résumé, Git est un logiciel de gestion de version tandis que GitHub est un service en ligne d’hébergement de dépôts Git qui fait office de serveur central pour ces dépôts.

# Repository

Un repository est un emplacement où est stocké le code en ligne, il se comporte dans sa structure comme un dossier en arborescence, plusieurs dossiers peuvent exister dans un repository. On pourra retrouver nos fichiers à travers le chemin de dossier comme sur une machine classique :

- exemple de chemin : Maths/algo/fichierTest

## Récupération d'un repository
Le code qui va être stocké sur un repository peut être récupéré de plusieurs manières, via ssh ou https.

- La manière https est la moins sécurisée car tout le monde peut avoir le lien du repository si ce dernier est en public.

- La manière avec une clé ssh est plus sécurisée car cette dernière agit comme un token: elle garantit une sécurité en plus.

Plusieurs outils permettent d'accéder aux services de git (Cf installation pour plus de details concernant l'installation):

-Git CMD (outil en ligne de commande)
-GitHub desktop (outil de visualisation et de contrôle sur une application)

on peut aussi faire une copie d'un répo directement avec la commande git clone 

````
git clone ssh://john@example.com/path/to/my-project.git 

````

Plusieurs options de clone existe aussi :

Clonage dans un dossier spécifique
````
git clone <repo> <directory>
````

Lors de la première commande git, ce dernier va nous demander de nous identifier via git config: 
````
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
````

# Fonctionnement de Git/GitHub

Git fonctionne en plusieurs étapes. Chaque étape va interférer avec un ou plusieurs blocs présent dans les outils Git/GitHub.

Le premier bloc est le bloc local qui correspond la machine de l'utilisateur.

Le deuxième bloc est consacré à l'index, une source de sauvegarde temporaire située entre le code local et le serveur Git/GitHub en ligne.

Le dernier bloc est consacré aux serveurs Git/GitHub qui sont en ligne.

A travers ce document nous verrons les différentes étapes pour transferer son code sur un serveur en ligne ( points importants, commandes importantes à savoir, fichiers externes, ect...).

## Config initiale (depuis source local)

La première étape va être d'initialiser le dossier sur la machine locale en tant que repo git :

```
git init
```
## Config initiale (depuis source en ligne)

### Création de dépôt en ligne 
Git/GitHub nous laisse la possiblité de créer nos repositories en ligne directement depuis son site. Pour cela, on va 
- créer un repository
- lui donner un nom
- ajouter un README ( facultatif)
- ajouter des fichiers facultatifs en plus comme la licence, gitignore (cf fichier généré par Git)
 <img width="581" alt="image" src="https://user-images.githubusercontent.com/90316879/197238657-f008f75c-fe59-4ece-b949-37d11cbfcdb0.png">

 On aura donc par defaut un lien de repo git qui va nous servir de connexion vers le repo.
 
 On peut alors initaliser le repo vide et lui envoyer nos fichiers. On peut faire :
 ``` 
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Name/repoName.git
```

Si jamais, on veut importer un projet, on peut lui associer une origine ( son point de connexion avec un repo git/gitHub existant)
```
git remote add origin git@github.com:user/nomrepo.git
git branch -M main
```

# Tranfert de fichiers vers les serveurs Git (git add, git commit) 

On a donc notre code local qui est prêt à indexer ses fichiers (on parle d'indexage pour le fait de transférer ses fichiers vers l'index).

L'index est la zone intermédiaire entre le code local et le code en ligne. On peut le représenter de cette manière : 

![git_workflow_001](https://user-images.githubusercontent.com/90316879/196621879-a3470e86-29d4-4618-9851-654fce8cbf0c.png)

La prochaine étape va être de signifier à git les fichiers qu'on veut transférer : 
```
git add fichier1.txt
```

Généralement, on ajoutera tous les fichiers en même temps (certains fichiers pourront être filtrés dans un fichier .gitignore qui contiendra les fichiers à ignorer (Cf Fichier Externes) avec :

```
git add .
```

Les fichiers vont être transportés vers l'index (une zone de stockage temporaire avant le transfert vers le serveur en ligne). La prochaine étape est de pousser vers le serveur en ligne. 
Pour cela on va tout d'abord indiquer un message permettant de repérer l'utilité du transfert ( /!\ ces messages doivent bien être clairs et précis afin de ne pas être ambigus!)

```
git commit -m "rectification condition boucle pour eviter cas overflow"
```


Si jamais il ne passe pas, cela signifie qu'il y a des erreurs de conflit (Cf Erreur de conflit).

Puis on va pousser vers une origine (ici notre branche) (Cf branche)

```
git push origin [branche]
```
Bien sûr, si on travaille seul sur une branche main, on peut push sur le master directement mais c'est une mauvaise habitude de travail à avoir (Cf branche).

```
git push
```

Voilà le code est bien poussé sur le serveur en ligne !



# Erreur de conflit 

Les conflits surviennent généralement lorsque deux personnes ont modifié les mêmes lignes dans un fichier, ou si un développeur a supprimé un fichier alors qu'un autre développeur le modifiait. Dans ces cas, Git ne peut pas déterminer automatiquement la version correcte. Les conflits n'affectent que le développeur qui effectue le merge, les autres membres de l'équipe ne sont pas conscients du conflit. Git marquera le fichier comme étant en conflit et arrêtera le processus de merge. Il incombe alors aux développeurs de résoudre le conflit.

Pour régler cela, il y a plusieurs manière de faire:
- Directement faire les changements sur l'IDE, les lignes qui ont été ajouté seront avec un + devant, et celles supprimées avec - , il n'y a plus qu'à garder les lignes voulues.
- Supprimer les erreurs depuis l'application (GitDesktop)
- Utiliser différentes commandes pour réglers les problèmes( Cf git diff, status,git revert)

Généralement on utilise une autre manière de faire, en utilisant des branches on va éviter au maximum ce genre de problèmes en contrôlant au maximum les erreurs avant qu'elle n'agissent sur la branche main (cf Branches).

## git diff
Si jamais il y a des erreurs, la commande git diff est très utile pour trouver ce qui a changé entre 2 points dans l'historique de votre projet, ou pour voir quelle personne a essayé d'introduire une nouvelle branche, etc.

Git diff sans paramètre donne les différences entre le dernier commit, votre index, et votre répertoire : 
````
git diff 
````
ou alors entre 2 branches avec :

````
git diff [branchName]

````
## git revert

Git revert permet de réaliser un commit pour annuler un commit précédent qui aurait ajouté des erreurs dans le projet, cette commande est très utile pour revenir à un état stable du projet: 

````
git revert [Commit ID]
````

pour voir l'ensembe les ID des commits précédent utiliser faire :

````
git log
````
# Branches

Les branches sont des espaces parallèles qui proviennent de l'origine et permettent de travailler sur le même projet à plusieurs. Lors de la création du projet la seule branche présente est la branche main (GitHub) ou master (GitLab).

Le but des branches est de structurer et organiser les membres sur le projet afin d'éviter que des erreurs de code soit transférées sur le repo en ligne.

Pour créer une branche, il y a deux manières de faire : 

- depuis l'interface en ligne  (on parlera de GUI Git User Interface)
- ou depuis l'interface de ligne de commande (on parlera de CLI Command-line interface)

```
git checkout -b <branch-name>
```

Un message expliquant que vous avez bien changé de branche devrait apparaitre et lors de votre prochain push, votre code sera sur la nouvelle branche créée.

Attention la commande suivante permet de créer une branche sans changer de branche, le prochain push sera alors toujours sur la branche actuelle car on ne se sera pas déplacé.

```
git branch <branch_name>
```
Il est possible également de créer une branche à travers un commit.

Pour voir les différentes branches :

```
git branch -a
```


Il est aussi possible de réaliser une fusion entre une branche secondaire sur la branche actuelle (Cf Pull request et Merge request).


/!\/!\/!\/!\/!\/!\ NE JAMAIS TRAVAILLER SUR LE MASTER/MAIN /!\/!\/!\/!\/!\/!\/!\/!\ Toujours travailler sur une branche!

Les branches vont être très utiles pour réaliser des opérations pour mettre à jour le code par rapport au main/master sans l'interférer.
Je m'explique, admettons SamSam travaille sur une nouvelle fonctionnalité et veut 
la push sur le master (on suppose qu'elle travaille bien et à bien compris le principe de branche car elle se situe déjà sur la branche SamSam ou une branche décrivant sa fonctionnalité (le plus couramment fait)). Elle va donc fusionner son travail avec le main mais sur sa branche (Cf Pull request), pour cela elle doit récupérer le master/main en local en faisant :

```
git pull origin [branche]
```
Elle va régler les erreurs de conflits s'il y en a. Son code sera donc compatible avec le main car elle sera assurée qu'il y a pas d'erreurs.

```
git add .
git commit -m "ajout fonctionnalité"
git push origin main
```

# Fonctionnalités en plus importante

## Pull request et Merge request (mise à jour de branche participative à Mise à jour de branche originelle)
 Les pull et pull request permettent de recupérer l'ensemble des fichiers non présents sur la branche active depuis une cible cité en paramètre :
 
 ```
 git pull origin [branchName]
 ```

### Exemple pull request 
Reprenons notre exemple précédent, dans notre projet la branche main à été mise à jour par SamSam auparavant et Corentin vient de revenir de vacances et veut travailler sur une fonctionnalité, pour cela il doit récupérer la dernière version à jour du main, pour cela il peut aller sur Git/GitHub et voir une option qui indique qu'il a du retard par rapport à la version du code du main :
<img width="660" alt="image" src="https://user-images.githubusercontent.com/90316879/196640143-f886ad6b-457e-4083-94f7-3c4497b3ad1d.png">

Pour rattraper ce retard il va faire une demande de pull request (toujours avec un message scpécifiant cette demande).
<img width="903" alt="image" src="https://user-images.githubusercontent.com/90316879/196640510-f6a36d63-2608-4d4d-8acd-de8645d95ef4.png">

Le propriétaire va alors accepter ou non cette requête. S'il acccepte, la request sera fermée et la branche de Corentin aura bien récupéré le contenu du main. 

 On peut aussi faire la commmande :
 ````
 git pull origin [main]     ou master si GitLab
 ````

### Exemple merge request

Le Merge request permet de fusionner toutes les ressources nécéssaires pour que la branche actuelle reçoivent tout le contenu de la branche passée en paramètre.
```
git merge origin [branchName]
```

Par exemple, je suis dans la branche A. Je fais :

```
git merge origin B
```

Le contenu de B va être fusionné avec A sur la branche A.  /!\ Bien vérifier d'être sur la bonne branche pour réaliser le merge!

Il est aussi possible de faire cette commande avec git merge, ce qui va merge le contenu de la branche actuelle avec la branche spécifié par défaut du répo (généralement main/master).

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

/!\ à différentier avec un simple clone, le clone va lui copier un projet en local qui sera synchronisé avec le serveur tandis que le fork est une duplication indépendante du repo originel qui pourra faire son cycle de vie à part sans être synchronisé au repo originel.

Une fois le fork réalisé, cela permet aussi d'accéder à tout l'historique du projet(version du code, message des commits....).

Je pense que si on utilise un projet dans un cadre d'une réalisation à but d'évolution, il faut réaliser un fork pour pouvoir avoir tout l'historique du projet et repecter le travail réalisé auparavant par les créateurs du repo d'origine afin de travailler de notre côté avec toutes les ressources dupliquées.


# Fichier Externes géré par Git

## README
Le fichier Readme permet de spécifier et d'indiquer des informations sur le projet à l'utilisateur qui va utiliser le repository.
Le fichier readme.md (markdown) est codé avec un langage de balisage (comme HTML). C'est utilisé pour réaliser différentes structure de style :

   # Titre
   ## Sous titre

```bash
  des commandes sur différents langages possible
```

- proposition

![Logo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/th5xamgrr6se0x5ro4g6.png)

## git ignore

Un fichier git .ignore est un fichier qui permet de ne pas prendre en compte certains fichiers en fonction de leur extension.
voici un exemple d'un fichier .ignore :

<img width="901" alt="image" src="https://user-images.githubusercontent.com/90316879/197197009-c0d03690-e568-4a9c-a6b3-75cd08920f47.png">

# tag
 Les tags sont des références qui pointent vers des points spécifiques de l'historique Git. Les tags sont généralement utilisés pour capturer un point de l'historique utilisé pour une version marquée (c. -à-d., v1. 0.1).
 
Afficher la liste des tags:
````
git tag [nomTag]
````
Création d'un tag:
````
 git tag -a v`[version] -m "my version 1.4"
````
# Outils de gestion de projet

Git/GitHub donne l'accès aux repo à des fonctionnalité permettant d'ajouter des opération possible au répo.
<img width="666" alt="image" src="https://user-images.githubusercontent.com/90316879/197245571-dc3969a2-eba3-413a-8395-c0c0df58c7f8.png">

## Issue

Cet onglet est dédié aux tickets de gestion de projet permettant de visualiser les tâches en cours pour les différents collaborateurs.

Un ticket est composé d'un titre, une description, un auteur, un identifiant et un statut (fermé ou ouvert).Un ticket peut être créé depuis l'interface de Git/GitHub en ligne : 
<img width="695" alt="image" src="https://user-images.githubusercontent.com/90316879/197246701-124974c9-8af6-4d89-99f0-a46e428fe836.png">

Les tickets sont très pratique pour voir l'avancé du projet, Git/GitHub sont très puissant car ils permettent de fermer des tickets directement depuis un commit qui à été un push.

Pour cela il suffit de faire :

```
git commit -m "close #IDTickets"
```

Plusieurs autres valeurs peuvent être utilisées pour fermer plusieurs tickets en même temps, mais le message doit OBLIGATOIREMENT contenir l'instuction close. Voici la liste des paramètres possibles : 

close, closes, closed, fix, fixes, fixed, resolve, resolves, resolved

Par exemple :

````
git commit -m "closes #1, closes #2, closes #3; Message du commit"
````


## Pull Request

Cette page est dédiée au pull request ouvertes.

## Action

Cette page est dédié aux différents work flow notamment Git flow.

Git flow est une méthode de travail (on parle de workFlow) expliquant comment travailler de manière optimisée sur son projet à travers les différentes branches.
Cette méthode à été proposée par Vincent Driessen en 2010.

Avec cette méthode, le projet doit utiliser seulement 5 branches : 

Main ==> Représente la branche utilisée en production
Develop ==> Représente la branche avec les derniers codes en développements
Feature
Release
Hotfix
 
 
A noté que deux manières de travailler avec cette méthode est possible :

-GitHub Flow qui est plus simple que Git flow est destiné pour des teams de dev web et d'applications, elle est surtout utilisée pour les opérations DevOPS. Mais cette méthode n'utilise pas toutes les branches de git flow ce qui peut générer des problèmes dans le futur.

-GitLab flow est une alternative à Git flow qui lui ressemble dans sa composition

L'action principale utilisée par cette page sont les outils d'intégration continue (CI/CD Sur GitLab), ces outils permettent de faire des tests supplémentaires sur différents critères suivant les outils installés. Par exemple la pipeline la plus basique s'occupe de vérifier si le code complile bien, si ce n'est pas le cas la pipeline indiquera une erreur et ne réalisera pas le merge. Ces outils sont très pratiques pour des codes déployés au public pour vérifier si les derniers changements ont affectés les performances de l'existant, notamment avec des pipelines de test unitaire, test de vitesse de requêtes ou test de sécurité.

Une fois les actions définie, on peut voir leur état sur la page : 

![image](https://user-images.githubusercontent.com/90316879/197268789-85f2f85e-f7fa-494f-ac4b-374fb176c5ff.png)

## Wiki

Cette page est similaire à un fichier README.

## Insights

Cette page permet de visualiser des statistiques sur le repo :
![image](https://user-images.githubusercontent.com/90316879/197269082-729e2aa1-ef20-4fb1-ae2f-d59d236aebac.png)
![image](https://user-images.githubusercontent.com/90316879/197286031-31c005b5-2992-4f5d-a4c6-d498412cfe0a.png)



# Installation Git/GitHub

Pour installer Git il suffit de suivre les instructions sur ce lien : https://git-scm.com/downloads
ou alors aller sur la version en ligne avec un navigateur et se connecter à son compte.

