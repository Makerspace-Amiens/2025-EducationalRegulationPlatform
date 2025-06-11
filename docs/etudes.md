---
layout: default
nav_order: 4
title: Régulateur PID
---

La commande d’un système consiste à appliquer, via l’entrée de commande, une action sur le système de manière à
obtenir à sa sortie un comportement déterminé. Dans le cadre de notre projet, nous allons démontrer celà avec un régulateur PID qui régulera un drône pour obtenir un équilibre bien défini.

# Qu’est-ce que la régulation PID ? 

Comprendre le PID (Proportionnel – Intégral – Dérivé)
Le PID est un système de régulation utilisé pour contrôler des machines, comme un drone, de manière stable et précise. Il ajuste automatiquement les actions à effectuer (par exemple, la puissance des moteurs) pour atteindre un objectif (comme rester à l’horizontale ou suivre une trajectoire).

![image](https://github.com/user-attachments/assets/b518564b-8e75-4bfa-961d-c7a3dde15ed8)

Comprendre le PID (Proportionnel – Intégral – Dérivé)
Le PID est un système de régulation utilisé pour contrôler des machines, comme un drone, de manière stable et précise. Il ajuste automatiquement les actions à effectuer (par exemple, la puissance des moteurs) pour atteindre un objectif (comme rester à l’horizontale ou suivre une trajectoire).

# Les trois composantes du PID
## 1. P comme Proportionnel
Fonction : Réagit à l’erreur actuelle, c’est-à-dire à la différence entre ce qu’on veut et ce qu’on a.

Exemple : Si le drone est penché à droite de 10°, le système applique une correction proportionnelle à cette erreur.

Effet : Plus l’erreur est grande, plus la correction est forte.

Limite :

Si on utilise seulement cette correction, le drone risque d’osciller autour de sa position cible (comme un ressort qui rebondit sans s’arrêter).

## 2. I comme Intégral
Fonction : Corrige l’erreur cumulée dans le temps.

Exemple : Si le drone reste toujours 2° trop incliné malgré la correction proportionnelle, le terme intégral s’accumule et compense ce petit décalage.

Effet : Élimine les erreurs persistantes, dues par exemple à un léger déséquilibre entre les moteurs.

Limite :

Si le réglage est trop fort, le drone peut devenir instable : les erreurs s’accumulent trop rapidement et provoquent des réactions excessives.

## 3. D comme Dérivé
Fonction : Observe la vitesse à laquelle l’erreur change.

Exemple : Si l’erreur augmente rapidement, le terme dérivé s’oppose à cette variation pour la freiner.

Effet : Permet de ralentir les mouvements brusques et de réduire les oscillations.

Limite :

Très sensible aux bruits ou aux petites erreurs de mesure. Cela peut générer de fausses corrections.

# Application du PID sur un drone
Le PID pilote le drone en ajustant la puissance de chaque moteur à partir des informations des capteurs (comme l’accéléromètre et le gyroscope). Il est utilisé pour :

Stabilisation : Garder le drone droit, sans inclinaison.

Contrôle de l’altitude : Maintenir une hauteur constante.

Navigation autonome : Suivre une direction ou une trajectoire programmée.

# Pourquoi bien régler un PID est essentiel ?
Chaque composante a un "gain" (noté Kp, Ki et Kd), qui doit être réglé avec soin :

Terme	Si trop fort…	Si trop faible…
Kp (proportionnel)	Le drone oscille violemment.	Il réagit trop lentement.
Ki (intégral)	Le drone devient de plus en plus instable.	Il garde une petite erreur constante.
Kd (dérivé)	Il ralentit trop les mouvements, ou est perturbé par du bruit.	Les oscillations ne sont pas bien amorties.

# En résumé
Le PID est un équilibre subtil entre réactivité, précision et stabilité.

Mal réglé, un drone peut être trop lent, trop nerveux, ou même injouable.

Bien réglé, il permet un vol fluide, stable et précis.
