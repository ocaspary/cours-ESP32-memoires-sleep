# Découvertes des modes

Lire et comprendre les tutoriels suivants :

{% embed url="https://lastminuteengineers.com/esp32-sleep-modes-power-consumption/" %}

{% embed url="https://diyi0t.com/reduce-the-esp32-power-consumption/" %}

Faire ensuite le tutoriel :

{% embed url="https://letmeknow.fr/blog/2019/08/08/tutoriel-les-sleep-modes-de-lesp32/" %}

Pour le montage, vous pouvez prendre des résistances de 220 Ohms ou 330 Ohms.

Habituellement, les fils noirs sont pour la masse ou GND et les fils rouges pour la tension Vin.

&#x20;

Terminer par cet excellent tutoriel qui approfondit le mode Deep Sleep avec le Touch Pad :

{% embed url="https://lastminuteengineers.com/esp32-deep-sleep-wakeup-sources/" %}

Pour aller plus loin, voir également la fin de la page pour un montage avec ESP32 en mode Deep Sleep et avec une batterie :

{% embed url="http://riton-duino.blogspot.com/2019/02/esp8266-sur-batterie.html" %}



&#x20;

**Exercice : Surveillance**

Utiliser un second ESP32 pour surveiller le bon fonctionnement du premier en instaurant une sorte de redondance. Par exemple, surveiller si le premier ESP32 est toujours alimenté, son nombre de reset pouvant indiquer un dysfonctionnement, etc.

Débranchez le câble d’alimentation du premier ESP32, le second doit afficher des messages d’alerte sur le moniteur série.

**Faire le montage et écrire le code correspondant en s’inspirant des exemples précédents.**

L’ESP32 à droite surveille l’ESP32 qui est à gauche de la figure.

A gauche, un bouton-poussoir est connecté entre la masse et la broche GPIO 18 (mettre cette broche en mode PULL-UP). Quand on appuie dessus pendant plus de 3 secondes, le WatchDog Timer se déclenche et fait un Software Reset (SW) pour redémarrer l’ESP32. Une diode est montée en série avec une résistance de 330 ohms à la sortie de la broche GPIO 4. Cette broche sera à l’état haut en sortie lors d’un Software Reset. La LED s’allumera alors brièvement pour le vérifier.

A droite, l’ESP32 « surveillant » a 2 broches en entrée reliée à l’ESP32 de gauche

\-        La broche GPIO 13 reliée au GPIO 4 pour compter les SW Reset

\-        La broche GPIO 14 reliée à l’alimentation +3,3 V pour un défaut d’alimentation

Ce défaut d’alimentation sera créé en débranchant le ports USB de l’ESP32 de gauche. Le comptage se fait pour chaque action : débrancher et rebrancher comptera pour 2.
