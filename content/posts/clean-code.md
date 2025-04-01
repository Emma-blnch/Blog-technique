+++
date = '2025-04-01T13:51:02+02:00'
draft = false
title = '🧹 Clean Code : écrire du code propre dès le début'
description = "C’est quoi le clean code ? À quoi ça sert ? Et comment l’appliquer concrètement quand on apprend le C ?"
+++

Quand tu commences à coder, tu cherches souvent à **faire fonctionner ton programme**.  
Mais avec le temps, tu réalises que faire **fonctionner** ne suffit pas : il faut que ton code soit **compréhensible**, **structuré** et **facile à maintenir**.

C’est là qu’intervient le concept de **clean code** ✨

---

## 📖 D’où vient ce terme ?

Le terme "clean code" vient principalement du livre *Clean Code: A Handbook of Agile Software Craftsmanship* écrit par **Robert C. Martin** (alias Uncle Bob).

Dans ce livre devenu culte, il explique que **le code doit être lisible, compréhensible et élégant**.  
Pas besoin d’être expert·e pour appliquer ces principes : tu peux commencer **dès aujourd’hui**.

> Tu peux facilement trouver ce livre en ligne, je te conseille vivement de le lire !  

---

## 🧠 C’est quoi le clean code ?

Un code "clean" c’est un code :
- 📚 **Lisible** : tu comprends ce qu’il fait sans effort
- 👀 **Prévisible** : tu n’as pas de surprise en lisant une fonction
- 🛠️ **Modifiable facilement** : tu peux corriger un bug ou ajouter une fonctionnalité sans tout casser

Et surtout : **tu peux le relire sans souffrir 😅**

---

## 🎯 Pourquoi c’est important ?

- Tu écris du code pour les autres (travail d'équipe)… **et pour ton toi du futur**
- Un code clean est **plus facile à maintenir**
- Il réduit les bugs
- Il est **plus simple à tester**
- Il te fait progresser dans ta façon de penser comme un·e dev

---

## ✨ Principes simples pour débuter

### 🧠 1. Donne des **noms clairs** à tes variables et fonctions
```c
// Pas clean
void f(int a) { ... }

// Clean
void afficher_message(int nombre_essais) { ... }
```

### ✂️ 2. Une fonction = une tâche
Chaque fonction doit faire **une chose**, et bien la faire.
```c
// Pas clean
void fonction(int choix);
int fonction2();

// Clean
void afficher_menu();
int lire_choix_utilisateur();
void traiter_choix(int choix);
```

### 🔁 3. Évite le code dupliqué
Si tu copies-colles du code, c’est souvent qu’il faut créer une fonction dédiée.
```c
// Pas clean
int main() {
    int age = 0;

    printf("Quel est votre age ?\n");
    scanf("%d", &age);
    if (age < 18)
        printf("Vous avez %d ans, vous etes donc mineur\n", age);
    else if (age > 65)
        printf("Vous avez %d ans, vous etes donc majeur\n", age);
    else
        printf("Vous avez %d ans, vous etes donc senior\n", age);
    return 0;
}

// Clean
int main() {
    int age = 0;

    printf("Quel est votre age ?\n");
    scanf("%d\n", age);
    if (age < 18)
        afficher_message(age, "mineur");
    else if (age > 65)
        afficher_message(age, "senior");
    else
        afficher_message(age, "adulte");
    return 0;
}
```

### 🧱 4. Structure ton code
- Utilise des **espaces**, des **indentations** régulières
- Regroupe tes fonctions par rôle
- Organise ton projet (cf. mon article précédent 😉)

### 🗒️ 5. Commente avec intelligence
- Ne commente pas l’évident :
  ```c
  i++; // incrémente i
  ```
- Commente ce qui est **complexe, logique, non intuitif**
  ```c
  // On utilise une boucle while car on ne connaît pas d’avance le nombre d’éléments à traiter
  while (liste != NULL) {
    traiter_element(liste->valeur);
    liste = liste->suivant;
  }
  ```  

> Un bon commentaire ne répète pas le code, il éclaire le pourquoi.

---

## ⚠️ Ce que le clean code n’est pas

- ❌ Ce n’est **pas** écrire un code parfait du premier coup
- ❌ Ce n’est **pas** forcément court ou “stylé”
- ❌ Ce n’est **pas** réservé aux dev seniors

> Le clean code, c’est **penser à la personne qui va lire ton code demain.**

---

## 🧠 Résumé

| Mauvaise pratique | Version clean |
|-------------------|----------------|
| `int f()`         | `int additionner(int a, int b)` |
| Fonction de 50 lignes | Fonctions courtes et claires |
| Code dupliqué     | Fonction réutilisable |
| Trop de commentaires | Juste ce qu’il faut, là où il faut |

---

Tu débutes ? Alors c’est **le meilleur moment** pour prendre de bonnes habitudes 🧼  
Même si ton code est imparfait, pense toujours à une chose : **"Est-ce que je pourrais le relire dans 2 semaines et tout comprendre ?"**

👉 Pour aller plus loin, regarde aussi comment [organiser ton projet](./organisation.md) pour éviter le chaos dès le début 😄
