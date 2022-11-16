# Exercice machine à états finis avec le mode Deep Sleep

**Reprendre l’exercice machines à états finis avec Touch (gestion de la LED bleue), voir ESP32 – Cours 3) en mettant l’ESP32 en mode Deep Sleep.**

Utiliser trois broches « Touch sensitive » de l’ESP32 pour gérer la LED bleue.

Cette fois, Il faudra pincer le fil associé au Touch 1 pour réveiller l’ESP32 et exécuter le programme. On peut ensuite, pincer Touch 2 et Touch 3, tout en maintenant Touch 1 pincé. Si on le relâche, l’ESP32 se remet en mode Deep Sleep et garde l’état en mémoire.

Le réveil se fait uniquement par Touch 1.

Tester d’abord le mode Deep Sleep avec juste Touch 1. Les fonctions utiles sont données par le fabriquant (Espressif) : esp\_sleep\_enable\_touchpad\_wakeup() , esp\_deep\_sleep\_start(), sans oublier : touchAttachInterrupt(touch1, gotTouch1, threshold).

{% embed url="https://docs.espressif.com/projects/espidf/en/latest/apireference/system/sleep_modes.html" %}

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Trois fils pour le montage : touch1 --> GPIO13, touch2 --> GPIO12, touch3 --> GPIO14

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
