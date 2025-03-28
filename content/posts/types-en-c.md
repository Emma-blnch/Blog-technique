+++
date = '2025-03-28T10:46:46+01:00'
draft = false
title = '🗒️ Comprendre les types en C simplement'
description = "Petite intro claire et illustrée aux types de base en langage C"
tags = ["C", "programmation", "débutant", "types"]
+++

Quand on commence à coder en C, on peut vite tomber sur la notion de "types" et être perdu sur les différences et rôles de chacun. Bien les comprendre c'est gagner **en clarté** et **en précision** dans ton code 💡

Voici un petit tour d’horizon des types de base que j'utilise tout le temps en C 🧵

---

## 🔢 Les nombres : `int`, `float`, `double`, etc...

En C, on a plusieurs types pour représenter des nombres, selon **le type de nombre** (entier, à virgule…) et **l’espace mémoire** que ça prend.

| Type        | Description |
|-------------|-------------|
| `int`       | Nombre entier (positif ou négatif) |
| `float`     | Nombre à virgule (précision ~6 chiffres) |
| `double`    | Nombre à virgule avec plus de précision (~15 chiffres) |
| `unsigned`  | Empêche les valeurs négatives |
| `short`, `long`, `long long` | Changent la taille mémoire (et donc la plage de valeurs) |

Exemples :
```c
int age = 30;
float note = 18.5;
unsigned int points = 150;
long big_number = 1234567890;
```

> ⚠️ En C, une virgule s’écrit avec un point : `3.14`, pas `3,14`

Pour afficher un nombre tu vas devoir utiliser `%d` pour un int, `%u` pour un unsigned, `%ld` pour un long int par exemple.
```c
int negatif = -54;
unsigned int positif = 4;
long big_number = 1234567890;  
printf("%d\n", negatif);  // affiche : -54
printf("%u\n", positif);  // affiche : 4
printf("%ld\n", big_number);  // affiche : 1234567890
```

Tu utiliseras les différents types de nombre selon la situation et ce que tu veux en faire !  

Si tu veux un nombre forcement positif, tu te tourneras vers le *unsigned int* par exemple.
Si tu veux faire un calcul de decimal, tu choisiras surement un float ou un double.

💭 A toi d'adapter et de choisir selon ton programme et ce que tu attends.

---  

## 🔤 `char` : une lettre, un symbole, un caractère

Un `char` (pour *character*) permet de stocker **un seul caractère** : une lettre, un chiffre, un symbole...

Il faut le mettre entre **guillemets simples** `'A'`, `'3'`, `'!'`.

Exemple :
```c
char lettre = 'E';
```
est correct.  
Mais :
```c
char lettres = 'ABC';
```
est faux ! Tu ne peux mettre qu'une seule lettre parce que le type char n'a de place en mémoire que pour un seul caractere.

> ✅ 1 `char` = 1 octet  

Pour afficher avec printf un char tu vas devoir utiliser `%c`.
```c
char lettre = 'A';
printf("%c\n", lettre);  // affiche : A
```

Mais tu peux aussi utiliser `%d`, comme pour les nombres ! 😮
```c
char lettre = 'A';
printf("%d\n", lettre); // affiche : 65
```  

> ✅ Chaque caractère correspond à un code (un chiffre) dans la table ASCII (cette table sera votre meilleur ami)

---

## 🧵 `char *` ou "string" : une suite de caractères

Il n’existe pas de `string` en C comme en Python ou JS. En réalité, une chaîne de caractères est juste un **tableau de `char`** terminé par un **caractère nul `\0`**.

On la met entre **guillemets doubles** `"Bonjour"`.  

Pour afficher une string avec printf tu vas devoir utiliser `%s`.
```c
char *phrase = "Hello world!";
printf("%s\n", phrase);  // affiche : Hello world!
```

> 💡 En mémoire, `"Hello"` c’est en réalité séparé caractère par caractère (avec 1 octet par caractère) : `'H'`, `'e'`, `'l'`, `'l'`, `'o'`, `'\0'`


---

## 🚫 `void` : le vide

`void` signifie que **la fonction ne retourne rien** :

```c
void dire_bonjour(void) {
    printf("Salut !\n");
}
```

Contrairement par exemple à :  
```c
char *dire_bonjour(char *str) {
    str = "bonjour !\n";
    return (str);
    // ça n'affichera pas "bonjour !" mais si on appelle cette fonction ailleurs on pourra l'afficher
}
```

On peut aussi s’en servir pour déclarer un **pointeur sans type précis** :
```c
void *ptr = NULL;
```

---

## 🔁 `bool` : vrai ou faux ?

Un booléen permet de représenter une **condition vraie ou fausse**.

Il faut inclure une librairie spéciale (plus de détails dans mon article sur les librairies !) :
```c
#include <stdbool.h>
```

Ensuite, on peut utiliser `true` ou `false` :
```c
bool est_allume = true;

if (est_allume) {
    printf("La lumière est allumée !\n");
}
```

> `false` vaut 0, `true` vaut 1

---

## 🔒 `const` : on ne touche plus !

Le mot-clé `const` empêche de **modifier une variable après sa déclaration**.

Exemple :
```c
const int jours_semaine = 7;
jours_semaine = 8; // ❌ Erreur : variable constante
```

> 🧠 Tu peux aussi avoir des pointeurs `const`, mais ça c’est pour plus tard 😉

---

## 🧠 Résumé rapide

| Type     | À quoi ça sert ? |
|----------|------------------|
| `char`   | Un seul caractère |
| `char *` | Une chaîne (string) |
| `int` / `float` / `double` | Des nombres |
| `void`   | Rien du tout 😄 |
| `bool`   | Vrai ou faux |
| `const`  | Valeur figée, non modifiable |

---

J’espère que ce petit tour t’a éclairé 🔦  
Tu veux aller plus loin ? Un article sur les **pointeurs** est déjà disponible ! 🔗
