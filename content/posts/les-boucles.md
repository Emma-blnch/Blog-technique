+++
date = '2025-04-09T12:47:14+02:00'
draft = false
title = '🔁 Les boucles en C : while, for, do... et comment les utiliser'
description = "Découvre les différentes boucles disponibles en langage C, quand les utiliser et comment éviter les pièges classiques."
+++

Quand on apprend à coder, on se rend vite compte qu'on a souvent besoin de **répéter une action plusieurs fois**. C’est là qu’entrent en jeu les **boucles** 🔁

---

## 🧠 C’est quoi une boucle ?

Une boucle permet d’exécuter **plusieurs fois** un bloc de code, tant qu’une **condition** est vraie.

Il existe **plusieurs types** de boucles en C :

---

## 🧵 La boucle `while`

```c
int i = 0;
while (i < 5) {
    printf("%d\n", i);
    i++;
}
```

✅ Tant que la condition est vraie (`i < 5`), on répète le bloc.  

> Ici, la boucle va donc afficher la valeur de i du départ `i = 0` jusqu'à ce que la condition ne soit plus vraie donc `i >= 5`. Donc la sortie sera :
```c
0
1
2
3
4
```

> Fais bien attention à initialiser `i = 0` **en dehors de la boucle**, il sera réinitialisé à chaque tour et ta boucle deviendra infinie !  

---

## 🔂 La boucle `do...while`

```c
int i = 0;
do {
    printf("%d\n", i);
    i++;
} while (i < 5);
```

✅ Elle s’exécute **au moins une fois**, même si la condition est fausse dès le début.

---

## ➿ La boucle `for`

```c
for (int i = 0; i < 5; i++) {
    printf("%d\n", i);
}
```

✅ Parfait quand tu sais combien de fois tu veux répéter.

> Tu n'es pas limité dans le nombre de conditions. `for (int i = 0, j = 2; i < 10 && j < 12; i++, j += 2)` est totalement valable !

---

## ⚠️ Attention aux boucles infinies !

```c
while (1) {
    // Cette boucle ne s’arrête jamais
}
```

Pense toujours à modifier ta variable pour **sortir de la boucle** à un moment.

Reprenons notre exemple pour afficher la valeur de `i`.  
```c
int i = 0;
while (i < 5) {
    printf("%d\n", i);
    // je n'incrémente pas i
}
```

Ici la boucle est infinie car je n'ai pas `i++` donc `i` vaut **toujours** `0` !  

# Quel intérêt d'une boucle infinie ?
Mais alors, il y a t-il **un intérêt** à faire une boucle infinie ou bien est-ce juste une **erreur à éviter** ?  
Et bien une boucle infinie peut être utile pour un programme graphique par exemple. 🔄 Ce sera la “boucle de vie” du programme. 

```c
while (1) {
    gérer_evenements();
    mettre_a_jour();
    afficher();
}
```

> Mais tu pourrais aussi l'utiliser dans le cas d'un serveur client qui attend des connexions, un système embarqué, une interface en ligne de commande, etc...  

# Astuce !
Même dans une boucle infinie, on met une condition de sortie quelque part :
- Un break quand une variable change
- Un return
- Un signal d’interruption externe
- Une condition sur input ou exit()  

---

## ✅ Résumé rapide

| Type       | Quand l’utiliser ? |
|------------|--------------------|
| `while`    | Quand tu veux boucler **tant qu’une condition est vraie** |
| `do while` | Quand tu veux **faire au moins une fois** |
| `for`      | Quand tu sais **combien de fois tu veux boucler** |

---

Les boucles sont incontournables en C et dans tous les langages. Apprends à bien les maîtriser, et tu éviteras des bugs bien relous 😅

👉 Prochaine étape ? Manipuler des données plus complexes avec les `struct` !
