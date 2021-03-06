---
layout: post
title: "Recueil de commandes / scripts utilitaires"
modified: 2017-08-16
tags: [outils, powershell, productivité, terminal]
categories: [code]
author: gabrielrobert
---


Voici une liste plutôt personelle de différentes commandes pouvant être utiles et qui permettent d'améliorer la productivité dans la vie de tout les jours. C'est plus une cheat sheet qu'un cas typique d'article.


### Supprimer les dossiers `/bin` et `/obj` d'une solution

Attention, cela va aussi affecter les dossiers `node_modules`, veuillez donc effectuer cette commande avec précaution.

```powershell
Get-ChildItem .\ -include bin,obj -Recurse | foreach ($_) { remove-item $_.fullname -Force -Recurse }
```

[Voir les sources](https://stackoverflow.com/questions/755382/i-want-to-delete-all-bin-and-obj-folders-to-force-all-projects-to-rebuild-everyt)


### Lire un fichier en continue (tail)

```powershell
Get-Content "<path>" -Wait
```

[Voir les sources](https://stackoverflow.com/questions/4426442/unix-tail-equivalent-command-in-windows-powershell)

### Supprimer des fichiers existants suite à la mise en place d'un `.gitignore`

```bash
git rm -r --cached . 
git add .
git commit -am "Remove ignored files"
```

[Voir les sources](https://stackoverflow.com/questions/1274057/how-to-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore)

### Supprimer tous les packages d'un projet (nuget / Package manager)

```powershell
Get-Package -ProjectName "PROJECT_NAME" | Uninstall-Package -ProjectName "PROJECT_NAME" -RemoveDependencies
```

[Voir les sources](https://stackoverflow.com/questions/28596666/how-do-i-uninstall-all-nuget-packages-from-a-solution-in-visual-studio-2013)

### Supprimer un packages de tous les projets (nuget / Package manager)

```powershell
Get-Project -All | Uninstall-Package "PACKAGE_NAME" -RemoveDependencies
```

[Voir les sources](http://www.eidias.com/blog/2012/10/11/nuget-command-line-uninstall-package-from-all-projects)

### Supprimer les fichiers d'un projet Xamarin pour charger les dépendences de nouveau

```bash
rimraf "C:\Users\YOUR_USER\AppData\Local\Xamarin"
```

### Place l'environnement courrant en mode "Development" lors de l'utilisation d'une application ASP .NET Core.

```powershell
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

[Voir les sources](https://stackoverflow.com/questions/39944489/startup-cs-returns-wrong-environment)


### Supprimer les branches locales et remote d'un répertoire git

```bash
#!/bin/sh
# Deletes all local and remote tags.
# `git delete-tag` comes from git-extras:
# https://github.com/visionmedia/git-extras
# Is very slow but will get there in the end.
git ls-remote --tags \
| awk '!/\^{}/' \
| awk -F tags\/ '{ print $2}' \
| xargs -L 1 git delete-tag
```