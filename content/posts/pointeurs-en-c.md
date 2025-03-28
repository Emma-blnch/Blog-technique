+++
date = '2025-03-28T10:52:57+01:00'
draft = false
title = '🔗 Les pointeurs en C : enfin comprendre comment ça marche'
description = "Une introduction claire et accessible aux pointeurs en langage C : à quoi ça sert, comment les utiliser et éviter les erreurs."
+++

Ah, les pointeurs... j'ai mis tellement de temps avant de vraiment les comprendre 😱  
Mais en vrai, c’est **beaucoup plus simple** qu’on le croit une fois qu’on comprend l’idée de base.

---

## 🧭 C’est quoi un pointeur ?

Un pointeur, c’est **une variable qui contient l’adresse d’une autre variable**.

📍 Au lieu de stocker une valeur (comme un `int` ou un `char`), il **pointe vers** un endroit en mémoire.

```c
int age = 30;
int *ptr = &age; // ptr contient l’adresse de la variable age donc il ne contient pas directement 30
```

---

## 🔎 Quelques mots-clés importants

- `&` → l’opérateur **"adresse de"** (donne l’adresse d’une variable)
- `*` → l’opérateur **"valeur pointée"** (déréférencer le pointeur)

Exemple :
```c
int x = 10;
int *p = &x;

printf("%p\n", p);   // affiche une adresse mémoire
printf("%d\n", *p);  // affiche : 10
```

> 💡 `*p` = va à l’adresse stockée dans `p` et lis ce qu’il y a là-bas.  
> Si un pointeur est une porte où il y a derrière une valeur alors le `*` est la poignée qui permet d'ouvrir la porte. Et `&` est l'adresse où se trouve la porte.  

---

## 🧪 À quoi ça sert ?

- 🔁 Partager une variable entre plusieurs fonctions sans la recopier
- 🧱 Manipuler des tableaux et des strings (qui sont des pointeurs cachés)
- 🧠 Gérer la mémoire dynamique (sur la heap avec `malloc`, `free`, etc.)

---

## ⚠️ Les erreurs classiques

- ❌ Utiliser un pointeur sans l’avoir initialisé → `segfault`
- ❌ Oublier de `malloc` pour la heap
- ❌ Oublier de `free` → fuite mémoire
- ❌ Déréférencer un pointeur nul (`NULL`)

---

## 🛠 Exemple concret avec `malloc`

```c
int *n = malloc(sizeof(int)); // alloue de la mémoire sur la heap
*n = 42;
printf("%d\n", *n); // affiche : 42
free(n); // on libère !
```

> 📌 `malloc` retourne un pointeur, donc on le stocke dans un `int *` ici.

---

## 🔗 Et les doubles pointeurs, alors ? (`int **`, `char **`)

Tu les as sûrement vus dans la fonction `main()` ou en passant un tableau de strings :  
```c
int main(int argc, char **argv) {
    // code
}
```

Mais... c’est quoi exactement un **double pointeur** ?

👉 Un `int **pptr` est un **pointeur vers un pointeur vers un int**.

### 🔍 Schéma mental :
- `int x = 10;` → une valeur
- `int *p = &x;` → un pointeur vers x
- `int **pp = &p;` → un pointeur vers le pointeur p

```c
int x = 10;
int *p = &x;
int **pp = &p;

printf("%d", **pp); // affiche 10
```

> 💡 Tu peux voir ça comme une chaîne :  
> `pp` → `p` → `x`

---

## 🧰 À quoi servent les doubles pointeurs ?

### ✅ 1. Modifier un pointeur dans une fonction

En C, tout est **passé par valeur**. Si tu veux **modifier un pointeur depuis une fonction**, tu dois lui passer un double pointeur.

Exemple :
```c
void change_val(int **pp) {
    static int x = 99;
    *pp = &x;
}

int main() {
    int *ptr = NULL;
    change_val(&ptr);
    printf("%d", *ptr); // affiche : 99
}
```

> Ici, `change_val()` modifie l’adresse pointée par `ptr` grâce à `int **`.

---

### ✅ 2. Manipuler un tableau de chaînes

Quand tu vois `char **argv`, c’est exactement ça : **un tableau de `char *`** donc **un `char **`**.

Tu peux aussi l’utiliser dans des fonctions qui reçoivent un tableau de strings par exemple :
```c
void print_all(char **tab) {
    int i = 0;
    while (tab[i]) {
        printf("%s", tab[i]);
        i++;
    }
}
```  

> Imagine un tableau où chaque case contient une phrase. Chaque phrase est elle-même une suite de caractères (une `string` ou `char *`). Ensemble, ce tableau est un `char **`.  

---

Les doubles pointeurs peuvent sembler un peu trop abstraits au début, mais avec un peu de pratique, tu verras que ce sont juste **des pointeurs de niveau supérieur**, utiles dans plein de cas pratiques 💪

👉 Si tu dois retenir juste une chose c'est ça :  
➡️ Les *pointeurs* servent à **modifier une variable dans une fonction** = on envoie l'adresse de la variable.  
➡️ Les *pointeurs sur pointeurs* servent à **modifier un pointeur dans une fonction** = on envoie l'adresse du pointeur.  

---

## 🧠 Résumé rapide

| Symbole | Signification         |
|---------|------------------------|
| `*`     | Accès à la valeur pointée |
| `&`     | Adresse d’une variable     |
| `int *` | Pointeur vers un entier    |
| `int **` | Pointeur vers un pointeur d’entier |
| `char **`| Manipuler un tableau de chaîne de caractères     |

---  

Voilà, t’as survécu aux pointeurs 😄  
Et maintenant tu peux voir à quel point ils sont liés à la **mémoire**, la **stack**, la **heap** et même aux **erreurs** dont on a parlé avant.
