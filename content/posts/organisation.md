+++
date = '2025-04-01T13:40:04+02:00'
draft = false
title = '📁 Organiser un projet C : fichiers, dossiers, .h et Makefile'
description = "Pourquoi et comment structurer proprement un projet en C : header, multi-fichiers, dossiers, Makefile... tout ce que j’aurais aimé comprendre plus tôt !"
+++

Quand on commence à coder en C, on met souvent **tout dans un seul fichier `.c`**.  
Et au début… ça fonctionne ! Mais plus ton projet grandit, plus **tu risques de te perdre** si tu ne l’organises pas un minimum 😵‍💫

Dans cet article, je t’explique **comment structurer ton code proprement** : header (`.h`), fichiers séparés, Makefile… et pourquoi c’est une bonne idée !

---

## 🧠 Pourquoi organiser son projet ?

- Pour **se relire plus facilement**
- Pour **travailler à plusieurs**
- Pour **rester zen quand ton projet passe de 100 lignes à 2000**
- Pour **réutiliser ton code plus facilement**

---

## 🔖 Les fichiers `.h` (header)

Un **header** sert à **déclarer ce que tu vas utiliser dans d’autres fichiers** :
- Les prototypes de fonctions
- Les constantes
- Les structures

Exemple :
```c
// nom du fichier : utils.h
#ifndef UTILS_H
#define UTILS_H

#include <stdio.h>

void afficher_message(void);

#endif
```

> 💡 Le `#ifndef` évite que le fichier soit inclus plusieurs fois dans un même projet (sinon erreur à la compilation). C'est une protection importante à ne pas oublier !

Dans ton fichier `.c`, tu inclues ce `.h` :
```c
#include "utils.h"

void afficher_message(void) {
    printf("Hello !\n");
}
```

---

## 📦 Plusieurs fichiers `.c` = plusieurs responsabilités

Tu peux séparer ton code en **plusieurs fichiers selon leur rôle** :
- `main.c` → point d’entrée
- `utils.c` → fonctions d’aide
- `affichage.c` → fonctions pour afficher quelque chose à l'écran
- `parsing.c` → lecture de fichier

Ça t’évite un **fichier de 2000 lignes** impossible à débuguer où tu passes plus de temps à chercher tes fonctions qu'à vraiment travailler dessus !

---

## 🗂️ Créer des dossiers

Quand le projet grandit, tu peux ranger tout ça :
```
📁 includes/   → tous tes `.h`
📁 src/        → tous tes `.c`
📁 obj/        → fichiers temporaires
📁 libft/      → ta librairie perso
```

Ca te permet de t'y retrouver plus clairement !  

> Si tu dois retenir une chose c'est : toujours penser à ton *toi du futur* (ou à une personne future) qui devra débugger et repasser sur ton projet, tu veux lui **faciliter la tâche** !

---

## ⚙️ Le Makefile : ton meilleur allié

Tu pourrais compiler ton projet à la main :
```bash
gcc main.c utils.c affichage.c -o prog
```

Mais… dès que tu changes un seul fichier, tu dois tout retaper 😵

Un **Makefile** te permet d’automatiser ça :
```Makefile
CC = gcc
SRC = main.c utils.c affichage.c
OBJ = $(SRC:.c=.o)
NAME = mon_programme

all: $(NAME)

$(NAME): $(OBJ)
	$(CC) $(OBJ) -o $(NAME)

clean:
	rm -f *.o

fclean: clean
	rm -f $(NAME)

re: fclean all
```

Et là, pour compiler, il te suffit de taper :
```bash
make
```

> N'oublie de rajouter dans ton Makefile tes nouveaux fichiers `.c` si tu en crée d'autres.

---

## 🧠 Résumé

| Élément    | Rôle |
|------------|------|
| `.h`       | Déclarer les fonctions/structs |
| `utils.c`  | Implémenter les fonctions |
| `main.c`   | Lancer le programme |
| `Makefile` | Automatiser la compilation |
| `dossiers` | Ranger, structurer, respirer 😄 |

---

Organiser ton projet, c’est pas de la flemme ou du "trop pro".  
C’est juste une **bonne habitude** pour t’aider à avancer plus vite, plus loin 🚀

👉 Et si tu veux rendre ton code encore plus lisible, va lire [mon article](./clean-code.md) sur le **clean code** 🧹
