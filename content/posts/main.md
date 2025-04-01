+++
date = '2025-03-28T16:59:14+01:00'
draft = false
title = '📍 La fonction main : explication et utilité'
description = "Pourquoi la fonction main est obligatoire en C, comment elle fonctionne, et ce que signifient int argc et char **argv."
+++

Quand tu codes en C, **tout commence par une seule fonction** : `main()`  
C’est elle que le système appelle **en premier** quand il lance ton programme.

Mais pourquoi est-elle si spéciale ? Et que veulent dire ses arguments `int argc` et `char **argv` ?  
Je t’explique tout 👇

---

## 🚪 `main()` : la porte d’entrée

Quand tu exécutes un programme C, **le système cherche automatiquement une fonction appelée `main()`**.  
Sans elle, ton programme ne sait pas **par où commencer** → tu auras une erreur à la compilation.

```c
int main(void) {
    // code principal ici
    return 0;
}
```

> 💡 `return 0;` signifie "le programme s’est bien terminé".  
> Un `return 1;` ou tout autre valeur indique une erreur.

---

## 🧠 Pourquoi `int main()` et pas `void main()` ?

En C, la norme veut que `main()` **retourne un int**, pour que le système sache **si tout s’est bien passé ou pas**.

Donc toujours :
```c
int main(void) { ... }
```

Et **pas** :
```c
void main() { ... } // ⚠️ non standard, à éviter
```

---

## 💬 Et `int argc`, `char **argv`, c’est quoi ?

Parfois, tu verras `main` écrit comme ça :
```c
int main() {
    // code
    return 0;
}
```  
ou même comme ça :
```c
int main(void) {
    // code
    return 0;
}
```  
Les deux signifient que tu n’as pas besoin d’utiliser les arguments argc et argv dans ton programme.  

Et parfois, tu verras `main` écrit comme ça :
```c
int main(int argc, char **argv)
```

### ✅ C’est pour récupérer ce que tu tapes dans le terminal quand tu exécutes ton programme :

Exemple :
```bash
./mon_programme salut toi
```

- `argc` = le **nombre d’arguments** passés au programme (ici 3 : `./mon_programme`, `salut`, `toi`)
- `argv` = un **tableau de chaînes de caractères** contenant ces arguments

Tu peux afficher ce qu’il y a dans `argv` :
```c
#include <stdio.h>

int main(int argc, char **argv) {
    for (int i = 0; i < argc; i++) {
        printf("Argument %d : %s\n", i, argv[i]);
    }
    return 0;
}
```

Souvent `argc` est utilisé en "protection" d'un programme. Tu peux dire à l'ordinateur que tu attends un nombre spécifique d'arguments à l'éxecution (quand on lance le programme dans le terminal) et s'ils ne sont pas présents alors ton programme peut renvoyer une erreur.  
Exemple :
```c
int main(int argc, char **argv) {
    if (argc < 2)
        return 1;
    else
        return 0;
}
```  
Ici, cela veut dire : si le nombre d'arguments n'est pas 2 (donc ./mon_programme + 1 seule autre chose) alors je renvoie 1 pour signaler une erreur.

`**argv` quant à lui, sera souvent utilisé pour spécifier que tu attends quelque chose de précis à tel ou tel argument.  
Exemple :
```c
int main(int argc, char **argv) {
    char *nom_du_fichier = argv[1];
    return 0;
}
```  
Ici, on récupère le premier argument utilisateur (après le nom du programme) pour le stocker dans une variable.  

Si tu ne veux utiliser que `argc` ou que `argv` tu peux ! Mais tu vas tout de même devoir mettre les **deux** en arguments de la fonction.
```c
int main(int argc, char **argv) {
    (void)argv;
    if (argc < 2)
        return 1;
    else
        return 0;
}
``` 
Ici j'ai mis `(void)` devant argv pour spécifier que je ne lui préciserai rien. Si jamais je ne le faisais pas, le compilateur me renverrai une erreur de type *"variable non utilisée"*.  
> 💡 C’est une petite astuce propre et recommandée pour éviter les warnings quand une variable d’argument est inutilisée dans une fonction.

---

## 🧵 Et ça a quoi à voir avec les pointeurs ?

Regarde bien la signature :
```c
char **argv
```

Ça veut dire : **"pointeur vers un pointeur de char"** → autrement dit, **un tableau de chaînes**.

C’est pour ça qu’on peut écrire `argv[i]` :  
- `argv` est un pointeur vers un tableau de `char *`
- chaque `char *` est une string (chaîne de caractères)

---

## 🧠 Résumé

| Élément | Signification |
|--------|----------------|
| `main()` | Fonction principale, appelée au lancement |
| `int`   | Type de retour standard (0 = succès) |
| `argc`  | Nombre d’arguments passés en ligne de commande |
| `argv`  | Tableau contenant ces arguments (strings) |
| `return` | Sert à dire si tout s’est bien passé (ou non) |

---

Sans `main()`, ton programme n’a **pas de point d’entrée**.  
C’est la **colonne vertébrale** de chaque code en C 🧠

👉 Si tu veux mieux comprendre ce `char **argv`, va jeter un œil à [mon article](./pointeurs-en-c.md) sur les **pointeurs** et les **chaînes de caractères** !
