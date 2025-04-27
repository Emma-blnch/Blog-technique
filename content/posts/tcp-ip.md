+++
date = '2025-04-27T13:25:18+02:00'
draft = false
title = '🌐 TCP/IP, ports, sockets... comprendre comment Internet fonctionne'
description = "Une introduction simple aux bases du réseau : TCP/IP, sockets, ports… tout ce que j’aurais aimé comprendre dès le début !"
+++

Quand tu ouvres un site, que tu envoies un message ou que tu ping un serveur… tu utilises **le protocole TCP/IP** sans même t’en rendre compte 🌐  
Mais... c’est quoi exactement ? Et comment tout ça fonctionne en pratique ?

---

## 🧠 C’est quoi TCP/IP ?

TCP/IP est un ensemble de **protocoles de communication** utilisés pour faire transiter des données sur Internet.

- **IP** (Internet Protocol) → gère les adresses
- **TCP** (Transmission Control Protocol) → gère le transport fiable des données

---

## 📦 Adresse IP et port

Une **adresse IP** identifie un appareil sur le réseau.  
Un **port** identifie une application spécifique sur cet appareil.

Exemple :
```
192.168.0.10:80 → adresse d’un serveur web
```

---

## 📡 Le rôle de TCP

TCP permet de :
- découper les données en **paquets**
- assurer qu’ils arrivent tous, dans le bon ordre
- **retransmettre** s’il y a une erreur

C’est comme envoyer une lettre **en recommandé** 📮

---

## 🔌 Les sockets

En C, tu peux manipuler le réseau avec des **sockets** :

```c
int sock = socket(AF_INET, SOCK_STREAM, 0);
```

Tu ouvres une "prise réseau", tu envoies ou reçois des données.

---

## 📍 Zoom sur les adresses IP et les masques de sous-réseau

### 🧠 Une adresse IP, c’est quoi exactement ?

Une adresse IP (en IPv4) est composée de **4 nombres** séparés par des points :  
Exemple : `192.168.1.12`

Chaque nombre peut aller de **0 à 255** car chaque bloc fait **1 octet** (8 bits).  
En tout, une IP fait donc **32 bits**.

Elle permet d’**identifier une machine** sur un réseau.

---

### 🏠 L'adresse IP est divisée en deux parties :

- La **partie réseau** → pour savoir à quel réseau appartient la machine
- La **partie hôte** → pour identifier la machine *dans* ce réseau

C’est là qu’intervient le **masque de sous-réseau**.

---

### 🎭 C’est quoi un masque de sous-réseau ?

Un **masque** permet de dire : "combien de bits sont réservés au réseau ? Et combien pour les machines ?"

Exemple :
```
Adresse IP :      192.168.1.12
Masque :          255.255.255.0
```

→ Ici, les **3 premiers octets** (192.168.1) définissent le réseau  
→ Le **dernier octet** (le 12) identifie la machine sur ce réseau

📌 En binaire :
```
255.255.255.0 = 11111111.11111111.11111111.00000000
```

👉 Chaque `1` = partie réseau  
👉 Chaque `0` = partie hôte

---

### 👀 Et à quoi ça sert ?

- À **organiser** les machines dans plusieurs sous-réseaux (ex : 192.168.1.x, 192.168.2.x…)
- À **limiter la portée** d’un broadcast (message envoyé à tout le réseau)
- À **configurer une IP statique** propre à chaque machine

---

### 🧪 Exemples pratiques

#### Cas 1 : réseau local (chez toi)
```
IP : 192.168.0.23
Masque : 255.255.255.0
```
→ Ton ordi est la machine 23 dans le réseau 192.168.0.0  
→ Tu peux communiquer avec tous les appareils en 192.168.0.x

#### Cas 2 : classe CIDR
On peut aussi écrire le masque sous forme `/x`, ex :
```
192.168.0.23/24 → équivaut à 255.255.255.0 (24 bits pour le réseau)
```

---

## 🛠 Identifier une machine dans un réseau

Une machine est **identifiée de manière unique** par :
- Son **adresse IP**
- Son **adresse MAC** (physique, unique à la carte réseau)

Le protocole **ARP** permet de faire la correspondance entre les deux.  
Exemple en ligne de commande :
```bash
arp -a
```
→ Affiche la table ARP de ta machine (IP <-> MAC)

---

## 🧠 Résumé rapide

| Terme | Rôle |
|-------|------|
| IP    | Adresse d’une machine |
| Port  | Application sur cette machine |
| TCP   | Transfert fiable des données |
| Socket | Point d’entrée/sortie pour la communication |
| Masque | Séparation réseau / hôte |
| ARP | Associe une IP à une adresse MAC |

---

Tu n’as pas besoin d’être expert·e en réseau pour comprendre les bases.  
Mais les connaître t’aidera énormément quand tu feras du C système, des serveurs web… ou simplement pour **debugger une connexion** !  

---

## 🔗 Pour aller plus loin

- [Superbe cours d'OpenClassroom sur ce sujet](https://openclassrooms.com/fr/courses/6944606-concevez-votre-reseau-tcp-ip)
- [Vidéo complète (EN) sur les adresses IP et les masques de sous-réseaux](https://www.youtube.com/watch?app=desktop&v=HQUw0CfQWAM&t=0s&ab_channel=Thuggonaut)
