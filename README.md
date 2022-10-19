# TD_SauvgardeDonnees_Tuto_Git

# REAME
Le fichier Readme permet de spécifié et d'indiquer des infos sur projet à l'utilisateur qui va utiliser le repository.
Le fichier reame.md (markdown) est codé avec un lagagUe de balisage (comme HTML), c'est utilisé pour réaliser différentes structure de style :

# Titre
## Sous titre

```bash
  git clone https://link-to-project
```

- proposition

![Logo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/th5xamgrr6se0x5ro4g6.png)

# Présentation GitHub/Git
- GitHub est un service permettant de stocker (héberger) des repository en ligne (souvent utilisé par les particuliers).

- Git est un service de versionning (VCS version control system) permettant de gérer les version des codes sur un serveur en ligne (souvent utilisé en entreprise).

Le code va être stocké sur un repository qui peut être accéder par plusieurs manière , via ssh ou https.

La manière https est la manière la moins sécurisé car tout le peut peut avoir le lien du repo et le clone si ce dernier est en public.
La manière avec une clé ssh est plus sécurisé car cette dernière agit comme un token, elle garantit une sécutité en plus.

Plusieurs outils permettent d'accéder aux services de git :

-Git CMD (outil en ligne de commande)
-GitHub desktop (outil de visualisation et contrôle sur une application)



# Fonctionnement de Git/GitHub

Git fonctionne en plusieurs étapes entre le code local, l'index et le serveur en ligne.

## Config initiale (depuis source local)

La première étape va être d'initialisé le dossier en tant que repo git :
```
git init
```
## Config initiale (depuis source en ligne)

Git/GitHub nous laissent la possiblité de créer nos repository en ligne directement depuis son site, pour cela on va 
- créer un repo 
- lui donner un nom
- ajouter un README ( facultatif)
- ajouter des fichiers en plus (comme la license, gitignore (cf gitignore) ect.. (facultatif)
 
 on aura donc par defaut un lien de repo git qui va nous servir de connexion vers le repo.
 
 on peut alors initaliser le repo vide et lui envoyer nos fichiers on peut faire :
 ``` 
 echo "# tt" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Akkuun/tt.git
git push -u origin main
```

si jamais, on veut importer un projet, on peut lui associer une origine ( son point de connexion avec git/gitHub)
```
git remote add origin git@github.com:user/nomrepo.git
git branch -M main
git push -u origin main
```


On a donc notre code local qui est prêt à indexé ses fichiers (on parle d'indexage pour le fait à transféré ses fichiers vers l'index).

L'index est la zone intermédiaire entre le code local et le code en ligne, on peut le représenter de cette manière : 

![git_workflow_001](https://user-images.githubusercontent.com/90316879/196621879-a3470e86-29d4-4618-9851-654fce8cbf0c.png)

La prochaine étape va être de signifié à git les fichiers qu'on veut transféré : 
```
git add fichier1.txt
```

généralement on ajoutera tout les fichiers ( certains fichiers pourront être filtré dans un fichier .gitignore qui contiendra les fichiers à ignorer) avec :

```
git add .
```

Les fichiers vont être transportés vers l'index, la prochaine étape est de pousser vers le serveur en ligne. Pour cela on va tout d'abord indiquer un message permettant de repérer l'utilité du transfert ( /!\ ces messages doit bien être clairs et précis afin de ne pas être ambigüe!)

```
git commit -m "rectification condition boucle pour eviter cas overflow"
```


Si jamais il ne passe pas, cela signifie qu'il y a des erreurs de conflit (Cf Erreur de conflit)

puis (Cf branche)

```
git push origin [branche]
```

Voilà le code est bien poussé sur le serveur en ligne !


# Erreur de conflit 
Une erreur de conflit signifie que du code à été dupliqué sur les deux version du code (local et celle en ligne), pour cela plusieurs manière de faire, directement faire les changements sur l'IDE, les lignes qui ont été ajouté seront avec un + devant, et celles supprimées avec - , il n'y a plus qu'à garder les lignes voulues.

Généralement on utilise une autre manière de faire, en utilisant des branches on va éviter au maximum ce genre de problèmes (cf Branches).


# Branche

Les branches sont des espaces parrallèle qui provienent de la même source (le main sur GitHub ou master sur Git).

Le but des branches est de structurer et organiser les membres sur le projet.

/!\/!\/!\/!\/!\/!\ NE JAMAIS TRAVAILLER SUR LE MASTER /!\/!\/!\/!\/!\/!\/!\/!\ Toujours travailler sur une branche!

Les branches vont être très utiles pour réaliser des pull request. Je m'explique, admettons SamSam travaille  sur une nouvelle fonctionnalité et veut 
la push sur le master (on suppose qu'elle travaille bien et à bien compris le principe de branche car elle se situe déjà sur la branche SamSam ou une branche décrivant sa fonctionnalité (le plus couraement fait)).

