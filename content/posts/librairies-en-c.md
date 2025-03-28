+++
date = '2025-03-28T10:48:57+01:00'
draft = false
title = '📚 Les librairies en C : à quoi elles servent ?'
description = "Une petite intro simple aux librairies les plus utiles en langage C avec leurs fonctions principales."
tags = ["C", "librairies", "programmation", "débutant"]
+++

Quand tu codes en C, tu vas souvent utiliser des **librairies**.  
Mais c’est quoi exactement une librairie ❓

---

## 📖 Définition rapide

Une **librairie** (ou bibliothèque) en C, c’est un fichier qui **contient des fonctions toutes prêtes**, qu’on peut utiliser sans les réécrire soi-même.  

📕 En gros, c'est comme un dictionnaire où l'ordinateur peut chercher les définitions des fonctions que tu veux utiliser.

Tu les ajoutes en début de fichier avec `#include <nom.h>`

Par exemple :
```c
#include <stdio.h>
```
te permet d'utiliser `printf`. Donc :
```c
#include <stdio.h>

printf("bonjour\n");
```
✅ fonctionnera parfaitement mais :
```c
printf("bonjour\n");
```
❌ ne marchera pas, ta machine te dira sûrement `"implicitly declaring library function 'printf'"`.

> 💡 Astuce : pour savoir si tu dois inclure une librairie, pense à regarder le message d'erreur. S’il parle d’une fonction "non déclarée", c’est souvent qu’il manque son #include en haut du fichier !  
> Plus d'infos sur les messages d'erreur dans mon article dédié !

---

## 🧰 Les librairies utiles à connaître

### `stdio.h` → affichage et lecture (standard)

- `printf()` → afficher dans le terminal
- `scanf()` → lire une entrée clavier
- `perror()` → afficher une erreur système

### `stdlib.h` → outils utiles (standard)

- `malloc()` / `free()` → allouer / libérer de la mémoire
- `exit()` → quitter un programme
- `atoi()` → convertir une string en entier
- `rand()` → générer un nombre aléatoire

### `string.h` → manipuler des chaînes de caractères (standard)
- `strlen()` → longueur d’une string
- `strcpy()`, `strncpy()` → copier une string
- `strcmp()` → comparer deux strings
- `strcat()` → concaténer des strings (les "coller" ensemble)

### `stdbool.h` → utiliser `bool`, `true`, `false` (standard)

- Fournit le type `bool` et les valeurs `true` / `false`
- Nécessaire pour faire des conditions plus lisibles

### `unistd.h` → fonctions système (système)

- `write()` / `read()` → écrire/lire des fichiers ou terminal
- `sleep()` → pause du programme
- `close()` → fermer un fichier

### `fcntl.h` → manipuler les fichiers (système)

- `open()` / `close()` / `read()` / `write()` → ouvrir, lire, écrire, fermer un fichier  
- `fcntl()` → modifier les propriétés du descripteur de fichier  

### `limits.h` → connaître les limites (standard)

- Définit les **valeurs max/min** pour les types (`INT_MAX`, `CHAR_MIN`, etc.)
- Utile pour éviter les dépassements

### `stdint.h` → types précis (standard)

- Donne des types comme `int8_t`, `uint32_t`, etc.
- Très pratique pour écrire du code portable et clair


> Les librairies `standard` du C font partie de la norme **officielle** du langage C donc *peu importe ton système d'exploitation* elles seront incluses par ton compilateur.
> Par contre les librairies `système` font partie du standard **POSIX** et sont disponibles uniquement sur *Linux* ou *Unix* (ou bien sur un environnement compatible POSIX type Cygwin).

---

## 🔗 Pour aller plus loin

- [Cours sur les librairies système (stdlib, etc.) – IRIF](https://www.irif.fr/~yunes/cours/systemes/stdlib.html)
- [Article Wikipédia sur la bibliothèque standard du C](https://fr.wikipedia.org/wiki/Biblioth%C3%A8que_standard_du_C)

---

N’hésite pas à venir piocher ici quand tu ne sais plus quelle librairie utiliser 😄  
Et tu peux venir voir mon article sur les **types** si tu veux comprendre pourquoi `stdbool.h` ou `stdint.h` peuvent te sauver la mise !
