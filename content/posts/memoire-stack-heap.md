+++
date = '2025-03-28T10:52:16+01:00'
draft = false
title = '🧠 Stack, Heap et mémoire en C : comprendre où vont tes variables'
description = "Un article simple pour comprendre comment fonctionne la mémoire en C, la différence entre la stack (pile) et la heap (tas), et pourquoi ça compte pour ton code."
+++

Quand tu codes en C, tu entends souvent parler de **stack** (pile) et de **heap** (tas).  
Mais qu’est-ce que ça veut dire concrètement ? Et pourquoi c’est important ?

---

## 🧱 Qu’est-ce que la mémoire en C ?

Quand tu exécutes un programme, ton ordinateur lui réserve de la **mémoire**. Cette mémoire est divisée en différentes zones, et **les deux principales** que tu manipules en C sont :

- la **stack** (ou pile)
- la **heap** (ou tas)

Chacune a un fonctionnement et un usage différents.

---

## 📦 La stack (pile)

> La stack, c’est comme une pile d’assiettes : on empile des trucs, et on les enlève dans l’ordre inverse.

### ✅ Ce qu’on y trouve :
- les **variables locales**
- les **paramètres des fonctions**
- les appels de fonctions eux-mêmes

### ⚡ Caractéristiques :
- Allouée **automatiquement**
- Très rapide
- Taille limitée
- Se vide toute seule quand la fonction se termine

### Exemple :
```c
void ma_fonction() {
    int a = 42; // stocké sur la stack
}
```

> 💡 Tu ne gères rien, tout est pris en charge automatiquement.

---

## 🧺 La heap (tas)

> La heap, c’est un peu comme un grand entrepôt où tu ranges les données dont tu ne sais pas combien de temps tu vas les garder.

### ✅ Ce qu’on y trouve :
- les **données dynamiques**, allouées avec `malloc`, `calloc`, `realloc`

### ⚡ Caractéristiques :
- Allouée **manuellement**
- Plus lente que la stack
- Capacité plus grande
- Tu dois **libérer** la mémoire toi-même (`free()`)

### Exemple :
```c
int *ptr = malloc(sizeof(int));
*ptr = 42;
free(ptr); // bien penser à free sinon ➡️ fuite mémoire !
```

> ⚠️ Oublier de libérer la mémoire = **fuite mémoire** = pas bon !

---

## 🧠 Résumé rapide

| Zone  | Allouée comment ? | Ce qu’on y stocke             | Durée de vie |
|-------|-------------------|-------------------------------|--------------|
| Stack | Automatiquement   | Variables locales, appels     | Temporaire (fonction) |
| Heap  | Manuellement      | Données dynamiques (`malloc`) | Manuelle (jusqu’à `free`) |

---

## 📌 Pourquoi c’est important ?

- Pour comprendre **d’où viennent les erreurs** (ex : "segfault", "memory leak"…)
- Pour bien utiliser les **pointeurs** (qu’on verra dans l’article suivant 😉)
- Pour éviter les bugs liés à la mémoire (comme utiliser une variable déjà libérée)

---

Voilà, maintenant tu sais où vont tes variables quand tu les déclares ✨  
Prochaine étape : les [pointeurs](./pointeurs-en-c.md) 🔗 (et tu vas voir, avec ce qu’on vient de voir, c’est beaucoup plus clair 😉)

---

## 🔗 Pour aller plus loin

- [Explication approfondie de la différence entre stack et heap](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/)
