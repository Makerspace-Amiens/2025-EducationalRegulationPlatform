---
layout: default
nav_order: 5
title: Conception et prototypage
---

## Conception et prototypage

Le système a été pensé pour illustrer de manière claire et pédagogique le fonctionnement d’une régulation PID dans un contexte physique concret. Le processus de conception s’est déroulé en plusieurs étapes clés :

### 1. Conception mécanique
- Réalisation d’un support physique stable permettant d’intégrer l’ensemble des composants (capteurs, actionneurs, microcontrôleur).
- Choix de matériaux faciles à usiner (acrylique, PLA imprimé en 3D) pour la structure.
- Conception d’un système mobile (ex. moteur + levier ou bande transporteuse) permettant de visualiser la régulation en action.

### 2. Choix des composants
- **Microcontrôleur** :Carte microbit V2.21 pour sa simplicité et sa large documentation.
- **Capteur** : capteur de position  pour mesurer la variable à réguler.
- **Affichage** : écran OLED I2C pour visualiser en temps réel la valeur de consigne, la mesure, et les paramètres PID.

### 3. Prototypage électronique

- Câblage selon un schéma électrique reproductible.
- Mise en place de potentiomètres pour ajuster manuellement les valeurs de Kp, Ki, Kd.

### 4. Implémentation logicielle
- Développement d’un algorithme PID dans Makecode qui offre plus de fléxibilité et facile à utiliser pour les débutants. 
- Lecture cyclique de la variable de mesure, calcul de l’erreur, et commande du moteur.
- Intégration d’un affichage dynamique de la réponse du système.

### 5. Test et validation
- Simulation de différents scénarios pour observer le comportement du régulateur.
- Réglages des paramètres PID pour obtenir une réponse stable, rapide et sans dépassement excessif.
- Analyse de la stabilité et du temps de réponse à partir de graphiques enregistrés.

