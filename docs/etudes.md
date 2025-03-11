---
layout: default
nav_order: 4
title: Études d'un régulateur PID
---

La commande d’un système consiste à appliquer, via l’entrée de commande, une action sur le système de manière à
obtenir à sa sortie un comportement déterminé. Dans le cadre de notre projet, nous allons démontrer celà avec un régulateur PID qui régulera un drône pour obtenir un équilibre bien défini.

# Qu’est-ce que la régulation PID ? 

Le PID (Proportionnel-Intégral-Dérivé) est un algorithme de contrôle utilisé pour stabiliser un drone en ajustant la vitesse de ses moteurs. Il permet au drone de corriger ses mouvements pour maintenir une attitude stable malgré les perturbations (vent, commandes du pilote...etc).
# Les trois parties du PID : 

- P (Proportionnel) : 

Réagit directement à l’erreur actuelle (différence entre la position souhaitée et la position réelle). 

Plus l’erreur est grande, plus la correction appliquée est forte. 

Problème : Uniquement proportionnel, le drone peut osciller autour de sa position cible. 

 

- I (Intégral) : 

Corrige l’erreur accumulée dans le temps (utile si une petite erreur persiste). 

Permet d’éliminer un décalage constant (exemple : si un moteur tourne légèrement moins vite que les autres). 

Problème : Si la correction est trop forte, le drone devient instable et oscille de plus en plus. 

 

- D (Dérivé) : 

Anticipe l’évolution de l’erreur en regardant sa vitesse de variation. 

Permet de réduire les oscillations en freinant les corrections trop brutales. 

Problème : Trop sensible aux bruits des capteurs. 

# Application du PID sur un drone 
Le PID ajuste la puissance des moteurs en fonction des mesures des capteurs (accéléromètre, gyroscope). Il est utilisé pour : 

Stabilisation (maintenir le drone à l’horizontale). 

Contrôle de l'altitude (garder une hauteur constante). 

Navigation autonome (suivre une trajectoire programmée). 

# Pourquoi bien régler un PID ? 
- Si Kp est trop fort, le drone peut osciller violemment. 

- Si Ki est trop fort, il peut devenir de plus en plus instable. 

- Si Kd est trop fort, il peut réagir trop lentement. 
 
