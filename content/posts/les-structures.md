+++
date = '2025-04-16T13:04:14+02:00'
draft = false
title = '📦 Les structures (`struct`) en C : organiser ses données proprement'
description = "Les structures en C te permettent de regrouper plusieurs variables ensemble. Un outil puissant à maîtriser pour structurer ton code."
+++

Quand on commence à avoir plusieurs variables qui vont ensemble, le mieux c’est de **les regrouper dans une structure** (`struct`).  
C’est comme créer un **nouveau type de donnée** personnalisé 📦

---

## 🧠 C’est quoi une `struct` ?

C’est une **collection de variables** (de types différents ou non), regroupées sous un même nom.

Exemple :
```c
struct personne {
    char *nom;
    int age;
};
```  

---

## Pourquoi c’est utile ?

- Tu regroupes **proprement** les données
- Tu passes **moins d’arguments** aux fonctions
- Ton code devient **plus lisible** et **facile à maintenir**

Exemple concret :
Tu écris un shell, et tu veux garder des infos importantes (comme un PID, un statut d’erreur, etc.) accessibles **partout**.  
Plutôt que de jongler avec plusieurs variables, tu crées une `struct` qui centralise tout ça :  
```c
typedef struct s_retour {
    int pid;
    int code_sortie;
} t_retour;
```  
Et ensuite dans ton programme :
```c
int main {
    t_retour retour;

    retour.pid = 1;
    retour.code_sortie = 0;
}
```  

---

## 🛠️ Utiliser une `struct`

```c
struct personne emma;

emma.nom = "Emma";
emma.age = 28;

printf("Nom : %s, âge : %d\n", emma.nom, emma.age);
```

Tu peux aussi créer un **alias** avec `typedef` :
```c
typedef struct personne {
    char *nom;
    int age;
} Personne;

Personne emma;
printf("Nom : %s, âge : %d\n", emma.nom, emma.age);
```

---

## 👉 Accéder à une struct via un pointeur

Si tu passes ta structure à une fonction avec un pointeur, tu utilises `->` au lieu de `.` :
```c
void afficher(t_personne *p) {
    printf("%s a %d ans\n", p->nom, p->age);
}
```

---  

## 📦 Structs dans une `struct` (struct imbriquées)

Tu peux **mettre une struct dans une autre** : pratique pour organiser encore mieux tes données !
```c
typedef struct s_date {
    int jour;
    int mois;
    int annee;
} t_date;

typedef struct s_personne {
    char *nom;
    t_date anniversaire;
} t_personne;
```  
Ici ca te permettra de passer uniquement la struct Personne, pas besoin de passer les deux !
```c
int fonction (t_personne *pers) {
    pers->anniversaire.jour = 01;
    pers->anniversaire.mois = 08;
    pers->anniversaire.annee = 2014;
}
```  

> 💡 Quand tu utilises `->`, c’est que tu manipules un **pointeur** vers une struct. Si tu as une struct "normale", tu utilises `.` !  

---

## 🧠 Résumé  

| Ce que ça permet       | Pourquoi c'est bien |
|------------|--------------------|
| Grouper des variables    | Plus **propre** et logique |
| Passer moins d'arguments | Plus **simple à lire** |
| Struct dans structs    | Organisation++ |
| Utiliser des pointeurs   | Meilleure **performance** |

---

Les `struct`, c’est un pas de plus vers du **code clair et bien organisé** 💡
C'est une base **super puissante** en C, surtout pour commencer à penser en *“objets”*.  

Tu verras, plus tu avances, plus tu les utiliseras 🙌
