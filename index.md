---
layout: single
title: Veille Technologique TP3
toc: true
toc_label: "Table des matières"
toc_sticky: true
---

# Projet Yggdrasil

[Présentation](#présentation) | [Matériel](#matériel) | [Expérimentations](#expérimentations)

---

## Présentation

Le but de notre projet est d’utiliser un **Raspberry Pi** pour surveiller une plante automatiquement. Notre idée principale est de créer un **système intelligent** capable de récupérer des informations sur l’environnement de la plante, d’analyser son état et de réagir s’il y a un problème, afin de l’aider à rester en bonne santé sans avoir besoin d’intervention constante.

Dans un premier temps, on utilise un **capteur de luminosité** pour mesurer la quantité de lumière autour de la plante. Cela permet de vérifier si elle reçoit assez de lumière ou si elle est dans un endroit trop sombre. En fonction des valeurs obtenues, le système peut donner une indication à l’utilisateur pour améliorer la situation, par exemple en déplaçant la plante.

Dans un deuxième temps, on utilise une **caméra** pour prendre des photos de la plante à intervalles réguliers, comme toutes les 15 minutes. Les images sont automatiquement enregistrées dans le système, ce qui permet de suivre l’évolution de la plante sans avoir besoin de la surveiller en permanence.

Dans un troisième temps, toutes ces images sont utilisées pour créer une vidéo <mark>time-lapse</mark> grâce à **ffmpeg**. Cette vidéo permet de voir la croissance de la plante en accéléré, ce qui rend les changements beaucoup plus visibles et faciles à analyser.

Dans un quatrième temps, on utilise **OpenCV** pour analyser les images automatiquement. Par exemple, on peut détecter des changements dans la couleur des feuilles, comme du vert vers du jaune. Cela permet au système de donner des indications sur l’**état de santé de la plante**.

Dans un cinquième temps, les données collectées, comme la **luminosité** et l’**humidité**, sont enregistrées dans des fichiers **CSV** ou **JSON**. Cela permet de garder un historique des données et de pouvoir les consulter plus tard pour analyser l’évolution de la plante.

Dans un sixième temps, on crée une <mark>interface web</mark> avec **Flask** pour afficher toutes les informations du système. L’utilisateur peut voir les données des capteurs, les images capturées et l’état général de la plante directement dans une page web simple et facile à comprendre.

Dans un septième temps, on teste le **capteur d’humidité** en comparant des conditions de sol sec et humide. Cela permet de voir si les valeurs sont cohérentes et de définir un seuil, par exemple en dessous d’une certaine valeur, pour déclencher automatiquement l’**arrosage de la plante**.

Dans un huitième temps, on met en place un <mark>système de notifications</mark> pour avertir l’utilisateur en cas de problème. Par exemple, si la plante manque d’eau ou de lumière, un message peut s’afficher sur l’interface web pour indiquer qu’une action est nécessaire.

Dans un neuvième temps, on effectue des **tests de performance et de stabilité** en laissant le système fonctionner pendant plusieurs heures ou plusieurs jours. Cela permet de vérifier qu’il n’y a pas de bugs, que le programme ne ralentit pas et que tout fonctionne correctement sur le long terme.

Finalement, le projet **Yggdrasil** lie plusieurs technologies comme des capteurs, une caméra, du traitement d’images, du stockage de données, une interface web et de l’automatisation dans le but de créer un <mark>système complet, intelligent et autonome</mark> pour la surveillance des plantes.


---

## Matériel

### Technologie 1 — Raspberry PI

| Champ | Détail |
|-------|--------|
| **Fabricant** | Raspberry Pi Foundation |
| **Modèle** | Raspberry Pi 4 Model B 4GB RAM |
| **Spécifications** | Le Raspberry Pi 4 Model B est équipé d’un processeur quad-core Cortex-A72 64 bits cadencé à 1,5 GHz, de 4 Go de RAM LPDDR4, du Wi-Fi 802.11 b/g/n/ac, du Bluetooth 5.0, de ports USB 3.0 et 2.0, de deux ports micro HDMI qui peut supporter jusqu’à 4K, d’un port Ethernet Gigabit et des broches GPIO pour connecter des capteurs. Voici un lien pour la documentation du Raspberry PI :  |
| **Usage prévu** | On se sert du Raspberry PI comme système principal du projet pour lire les capteurs, contrôler une caméra, traiter les données et héberger sur notre serveur web |
| **Justification du choix** | Le Raspberry Pi a été choisi parce qu’il est simple à utiliser, peu coûteux et très polyvalent. Il permet de connecter facilement différents capteurs et une caméra grâce aux broches GPIO, ce qui est essentiel pour notre projet. De plus, il est assez puissant pour exécuter plusieurs programmes en même temps comme la lecture des capteurs, le traitement d’images avec OpenCV et l’hébergement d’un serveur web. C’est aussi un outil vraiment populaire dans les projets informatiques dont il existe beaucoup de documentation et d’exemples pour nous aider en cas de problème. Finalement, sa petite taille et sa faible consommation en énergie en font une solution pratique pour un petit système qui doit fonctionner en continuellement. |
| **Lien vers la documentation** | [Fiche technique du Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/) |
| **Expérimenté par** | Les 4 membres de notre équipe |

### Technologie 2 — Raspberry PI Camera Module 3

| Champ | Détail |
|-------|--------|
| **Fabricant** | Raspberry Pi Foundation |
| **Modèle** | Raspberry PI Camera Module 3 |
| **Spécifications** | Caméra de 12 mégapixels (Sony IMX708), support de l’autofocus, capture d’images et de vidéos HD, compatibilité avec le Raspberry Pi via le port CSI. Elle a aussi un sensor diagonal large de 7.4mm et une angle de vue de 75 degrès |
| **Usage prévu** | La caméra est utilisée pour prendre des photos de la plante à intervalles réguliers. Ces images permettent de suivre son évolution dans le temps et de créer un time-lapse de sa croissance. On va l'utiliser pour l'expérimentation 2 et 3. |
| **Justification du choix** | Cette caméra de la même compagnie que notre première technologie a été choisie par notre équipe parce qu’elle est compatible directement avec le Raspberry Pi et facile à installer. Elle offre une bonne qualité d’image, ce qui est important pour observer les changements de la plante. En plus de ça, elle supporte l’autofocus, ce qui permet d’avoir des images plus claires sans ajustement manuel et elle est aussi bien documentée. |
| **Lien vers la documentation** | [Caméra Module 3 du Raspberry PI](https://www.raspberrypi.com/products/camera-module-3/) |
| **Expérimenté par** | — |


### Technologie 3 — Capteur de luminosité (LDR)

| Champ | Détail |
|-------|--------|
| **Fabricant** | Générique (C'est un module compatible avec Arduino et Raspberry Pi) |
| **Modèle** | Capteur de luminosité LDR de type KY-018|
| **Spécifications** | C'est un capteur basé sur une photorésistance (LDR) qui varie sa résistance selon la lumière avec une sortie analogique ou numérique, une alimentation 3.3V ou 5V, 3 broches (VCC, GND, Signal) |
| **Usage prévu** | Le capteur de luminosité est utilisé pour mesurer la quantité de lumière autour de la plante. Il permet de déterminer si la plante reçoit assez de lumière ou si elle est dans un environnement trop sombre. On va l'utiliser pour l'expérimentation 1. |
| **Justification du choix** | Ce capteur est simple à utiliser, peu coûteux et efficace pour détecter les variations de luminosité. Il est idéal et parfait pour un projet comme celui-ci puisqu’il permet de prendre des décisions automatiques basées sur la lumière. |
| **Lien vers la documentation** | [Caméra Module 3 du Raspberry PI](https://www.raspberrypi.com/products/camera-module-3/) |
| **Expérimenté par** | — |


---

## Expérimentations

### Expérimentation 1 — Test du capteur de luminosité

| Champ | Détail |
|-------|--------|
| **Réalisée par** | Alexande |
| **Technologie(s)** | Arduino uno r3 et Capteur de luminosité (LDR) |
| **Objectif** | Vérifier si le capteur de luminosité permet de mesurer correctement la quantité de lumière autour d'une plante et de déterminer si elle reçoit suffisamment de lumière pour sa croissance |

#### Contexte de réalisation

Cette expérimentation a été réalisée avec un Arduino Uno R3 à la place d'un Raspberry Pi, puisque le capteur de lumière utilisé est un capteur analogique et que l'Arduino possède des broches analogiques natives

1. J'ai branché le capteur sur l'Arduino Uno R3 : la broche **S** sur **A0**, le **+** sur **5V** et le **–** sur **GND**.
2. Ensuite j'ai coder l'Arduino pour lire les valeurs du capteur et les afficher dans le moniteur série. 
3. J'ai fini par définir des seuils de luminosité pour classifier l'environnement de la plante : trop sombre (< 200), lumière faible (200–500), bonne lumière (500–800) et plein soleil (> 800).

#### Photos / Vidéos

#### Résultat

Le capteur fonctionne correctement et réagit bien aux variations de lumière. En couvrant le capteur avec la doigt, les valeurs chutent significativement, ce qui confirme qu'il détecte bien les changements de luminosité. Le système affiche un message indiquant l'état de la lumière pour la plante, par exemple "Bonne lumière" ou "Trop sombre".


#### Avis sur la technologie

- **Forces** : Le capteur est très simple à brancher, peu coûteux et réagit très bien aux changements de lumière
- **Faiblesses** : Contrairement au Raspberry Pi, l'Arduino ne peut pas envoyer des notifications automatiques pour indiquer si la plante n'a pas asser de lumière
- **Potentiel** : —
- **Limites** : Le capteur mesure uniquement la luminosité ambiante générale

#### Avis final (1 des 2)

> **Validation de l'hypothèse** — L'expérimentation montre que le capteur est capable de mesurer la luminosité autour d'une plante et de donner des indications sur la quantité de lumière

> **Technologie insatisfaisante** — blablablblablalba

---

### Expérimentation 2 — Capture d’images avec la caméra 

| Champ | Détail |
|-------|--------|
| **Réalisée par** | — |
| **Technologie(s)** | — |
| **Objectif** | — |

#### Contexte de réalisation

1. Étape 1
2. Étape 2
3. Étape 3

#### Photos / Vidéos

#### Résultat

#### Avis sur la technologie

- **Forces** : —
- **Faiblesses** : —
- **Potentiel** : —
- **Limites** : —

#### Avis final (1 des 2)

> **Validation de l'hypothèse** — blablablabla

> **Technologie insatisfaisante** — blablablabla

---

### Expérimentation 3 — Génération d’un time-lapse avec ffmpeg 

| Champ | Détail |
|-------|--------|
| **Réalisée par** | Justin Lavigueur |
| **Technologie(s)** | - **ffmpeg** : logiciel en ligne de commande pour traiter des vidéos et images<br>- Images **JPEG** prises avec mon téléphone sur ma plante de jade<br>- Mon ordinateur personnel avec **PowerShell**<br>- Un dossier local pour organiser mes images |
| **Objectif** | Mon objectif pour l'expérimentation est de vérifier s’il est possible de créer une vidéo time-lapse à partir d’une série de photos d’une plante quelconque (dans mon expérimentation, je vais utiliser ma plante de jade que j'ai chez moi. |


#### Contexte de réalisation en étapes
Cette expérimentation a été réalisée sur mon ordinateur après avoir installé ffmpeg. J’ai pris plusieurs photos de ma plante de jade avec mon téléphone dans le même angle pour que ça reste constant. 
Ensuite, j’ai voulu tester deux cas : une vidéo avec 20 photos et une autre avec 30 photos pour voir la différence dans le résultat.

1. J’ai commencé par installer ffmpeg et vérifier qu’il fonctionne correctement dans mon terminal powershell avec une commande simple.
2. Ensuite, j’ai pris plusieurs photos de ma plante de jade en essayant de garder le même cadrage et la même position pour chaque photo. J’ai ensuite placé toutes les images dans un même dossier en nommant chaque photo selon l'ordre de leur prise.
3. Finalement, j’ai utilisé ffmpeg pour transformer les images en vidéo time-lapse de format mp4 en utilisant une commande dans le terminal de mon dossier de photos.

#### Photos / Vidéos
Photos de ma plante de jade prises en série et deux vidéos générées : une avec 20 photos et une autre avec 30 photos.

#### Résultat
Les deux vidéos ont bien été créées. Celle avec 30 photos est plus fluide que celle avec 20 photos. 
Par contre, comme les photos ont été prises sur une courte période, le changement dans la plante n’est pas très visible, donc l’effet time-lapse reste limité.

#### Avis sur la technologie

- **Forces** : Je trouve que ffmpeg est rapide et permet de créer facilement une vidéo à partir d’images. J'ai pas eu beaucoup de complications qaund je l'ai utilisé même si c'était la première fois que je l'utilisais. Une fois qu’on comprend la commande, ça va vraiment vite et en plus de ça, c'est complètement gratuit donc pour moi, c'est un plus.
- **Faiblesses** : Ce n’est pas très intuitif au début parce que tout se fait en ligne de commande. Il faut aussi bien organiser minutieusement ses images dans un ordre parfait comme image1, image2 sinon ça ne fonctionne tout simplement pas.
- **Potentiel** : Cette technologie est très utile pour mon projet parce qu’elle me permettrait de créer automatiquement des vidéos pour montrer l’évolution de ma plante sur plusieurs jours ou semaines.
- **Limites** : Le résultat des vidéos faites par ffmpeg dépend beaucoup du nombre de photos et du temps entre chaque photo. Si les photos sont prises trop rapprochées dans le temps, on ne voit presque pas de changement direct.

#### Avis final (1 des 2)

> **Validation de l'hypothèse** — Cette expérimentation montre que ffmpeg fonctionne bien pour créer un time-lapse. mes deux tests (20 et 30 photos) confirment que plus il y a d’images, plus la vidéo est fluide, ce qui valide l’utilisation de cette technologie pour notre projet Yggdrasil.


---
### Expérimentation 4 — Analyse d’images avec OpenCV

| Champ | Détail |
|-------|--------|
| **Réalisée par** | — |
| **Technologie(s)** | — |
| **Objectif** | — |

#### Contexte de réalisation

1. Étape 1
2. Étape 2
3. Étape 3

#### Photos / Vidéos

#### Résultat

#### Avis sur la technologie

- **Forces** : —
- **Faiblesses** : —
- **Potentiel** : —
- **Limites** : —

#### Avis final (1 des 2)

> **Validation de l'hypothèse** — blablablabla

> **Technologie insatisfaisante** — blablablabla

---
### Expérimentation 5 — Notifications

| Champ | Détail |
|-------|--------|
| **Réalisée par** | — |
| **Technologie(s)** | — |
| **Objectif** | — |

#### Contexte de réalisation

1. Étape 1
2. Étape 2
3. Étape 3

#### Photos / Vidéos

#### Résultat

#### Avis sur la technologie

- **Forces** : —
- **Faiblesses** : —
- **Potentiel** : —
- **Limites** : —

#### Avis final (1 des 2)

> **Validation de l'hypothèse** — blablablabla

> **Technologie insatisfaisante** — blablablabla

---
## Sources

1. [Titre de la source](https://exemple.com) — Description courte
2. [Titre de la source](https://exemple.com) — Description courte
3. [Titre de la source](https://exemple.com) — Description courte
2. [Titre de la source](https://exemple.com) — Description courte
3. [Titre de la source](https://exemple.com) — Description courte
2. [Titre de la source](https://exemple.com) — Description courte
