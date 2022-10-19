# TD_SauvgardeDonnees_Tuto_Git

README
Le fichier Readme permet de spécifié et d'indiquer des infos sur projet à l'utilisateur qui va utiliser le repository.
Le fichier reame.md (markdown) est codé avec un lagagUe de balisage (comme HTML), c'est utilisé pour réaliser différentes structure de style :

# Titre
## Sous titre

```bash
  git clone https://link-to-project
```

- proposition

![Logo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/th5xamgrr6se0x5ro4g6.png)


- GitHub est un service permettant de stocker (héberger) des repository en ligne (souvent utilisé par les particuliers).

- Git est un service de versionning (VCS version control system) permettant de gérer les version des codes sur un serveur en ligne (souvent utilisé en entreprise).

Le code va être stocké sur un repository qui peut être accéder par plusieurs manière , via ssh ou https.

La manière https est la manière la moins sécurisé car tout le peut peut avoir le lien du repo et le clone si ce dernier est en public.
La manière avec une clé ssh est plus sécurisé car cette dernière agit comme un token, elle garantit une sécutité en plus.

# fonctionnement de Git/GitHub

Git fonctionne en plusieurs étapes entre le code local, l'index et le serveur en ligne.

La première étape (qui peut être facultative si le repo est créé directement en ligne) va être d'initialisé le dossier en tant que repo git :
```
git init
```
On a donc notre code local qui est prêt à indexé ses fichiers (on parle d'indexage pour le fait à transféré ses fichiers vers l'index.

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

puis (Cf branche)

```
git push origin [branche]
```

Voilà le code est bien poussé sur le serveur en ligne !

Si jamais il ne passe pas, cela signifie qu'il y a des erreurs de conflit , pour cela plusieurs manière de faire, directement faire les changements sur l'IDE,
les lignes qui ont été ajouté seront avec un + devant, et celles supprimées avec - .


