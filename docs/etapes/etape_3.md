---
layout: default
title: Programmation python
parent: Etapes de fabrication
nav_order: 3
---

# Porgrammation
Le contrôle du drone et l'analyse des données sont réalisés en Python. Ce langage est utilisé pour :
- Traiter les données des capteurs IMU (accéléromètre et gyroscope).

(A voir comment copier correctement le code) 
# Code pour le contrôle d'un drone Air:bit 2 avec une carte micro:bit v2 

# Émetteur (Télécommande) et Récepteur (Drone) avec stabilisation PID 

  

from microbit import * 

import math 

import radio 

  

# Configuration radio 

radio.config(group=1, power=7)  # Définit le groupe de communication et la puissance d'émission 

radio.on()  # Active la radio 

  

# Paramètres PID (proportionnel, intégral, dérivé) 

Kp = 1.2  # Gain proportionnel (réagit à l'erreur actuelle) 

Ki = 0.01  # Gain intégral (corrige l'erreur cumulée) 

Kd = 0.5   # Gain dérivé (prédit l'erreur future) 

  

# Variables PID 

prev_error_roll = 0  # Stocke l'erreur précédente pour le roulis 

prev_error_pitch = 0  # Stocke l'erreur précédente pour le tangage 

integral_roll = 0  # Stocke la somme des erreurs pour le roulis 

integral_pitch = 0  # Stocke la somme des erreurs pour le tangage 

  

# Fonction de lecture de l'angle d'inclinaison 

def get_tilt(): 

    ax = accelerometer.get_x() 

    ay = accelerometer.get_y() 

    az = accelerometer.get_z() 

     

    # Calcul du roulis et du tangage en degrés 

    roll = math.atan2(ay, az) * (180 / math.pi) 

    pitch = math.atan2(-ax, math.sqrt(ay ** 2 + az ** 2)) * (180 / math.pi) 

     

    return roll, pitch 

  

# Fonction PID pour ajuster la stabilisation 

def pid_control(setpoint, current_value, prev_error, integral): 

    error = setpoint - current_value  # Calcul de l'erreur actuelle 

    integral += error  # Mise à jour de l'intégrale 

    derivative = error - prev_error  # Calcul du terme dérivé 

    prev_error = error  # Stocke l'erreur actuelle pour la prochaine itération 

     

    # Calcul de la sortie PID 

    output = Kp * error + Ki * integral + Kd * derivative 

    return output, prev_error, integral 

  

# Fonction de mise à jour des moteurs 

def set_motor_power(throttle, roll_output, pitch_output): 

    # Répartition de la puissance des moteurs en fonction du PID et de l'entrée de l'utilisateur 

    motor1 = throttle + roll_output + pitch_output  # Moteur avant-gauche 

    motor2 = throttle - roll_output + pitch_output  # Moteur avant-droit 

    motor3 = throttle + roll_output - pitch_output  # Moteur arrière-gauche 

    motor4 = throttle - roll_output - pitch_output  # Moteur arrière-droit 

     

    display.show(int(throttle / 10))  # Affiche la puissance du moteur sur la LED centrale (simulation) 

    return motor1, motor2, motor3, motor4 

  

# Boucle principale du drone 

throttle = 0  # Puissance des moteurs (initialement à 0) 

while True: 

    roll, pitch = get_tilt()  # Récupère les angles d'inclinaison 

    message = radio.receive()  # Vérifie les messages de la télécommande 

     

    if message: 

        try: 

            cmd, value = message.split(':')  # Sépare la commande et la valeur 

            value = int(value) 

            if cmd == 'throttle': 

                throttle = value  # Met à jour la puissance 

            elif cmd == 'Kp': 

                Kp = value / 10.0  # Ajuste le gain proportionnel 

            elif cmd == 'Ki': 

                Ki = value / 100.0  # Ajuste le gain intégral 

            elif cmd == 'Kd': 

                Kd = value / 10.0  # Ajuste le gain dérivé 

        except: 

            pass  # Ignore les erreurs de réception 

     

    # Calcul des corrections PID 

    roll_output, prev_error_roll, integral_roll = pid_control(0, roll, prev_error_roll, integral_roll) 

    pitch_output, prev_error_pitch, integral_pitch = pid_control(0, pitch, prev_error_pitch, integral_pitch) 

     

    # Mise à jour des moteurs 

    motors = set_motor_power(throttle, roll_output, pitch_output) 

    radio.send('motors:{}:{}:{}:{}'.format(*motors))  # Envoie l'état des moteurs à la télécommande 

    sleep(50)  # Pause pour éviter une surcharge du processeur 

  

# Code de l'émetteur (Télécommande) 

def telecommande(): 

    throttle = 0  # Niveau initial de puissance 

    while True: 

        if button_a.is_pressed(): 

            throttle += 10  # Augmente la puissance 

        if button_b.is_pressed(): 

            throttle -= 10  # Diminue la puissance 

         

        throttle = max(0, min(throttle, 100))  # Contraint la valeur entre 0 et 100 

        radio.send('throttle:{}'.format(throttle))  # Envoie la puissance actuelle au drone 

        display.show(int(throttle / 10))  # Affiche la puissance sur la matrice LED 

        sleep(100)  # Pause pour éviter les envois trop fréquents 

  

# Lancer la télécommande si les deux boutons sont appuyés au démarrage 

if button_a.is_pressed() and button_b.is_pressed(): 

    telecommande() 

 
