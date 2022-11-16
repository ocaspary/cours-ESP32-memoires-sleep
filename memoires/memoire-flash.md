# Mémoire Flash

**Problème de la mémoire FLASH :**

On peut vouloir garder un contexte entre deux redémarrages de l'ESP32. Dans ce cas, on peut utiliser la mémoire flash mais celle-ci à un nombre de cycle d'écriture maximum avant de... mourir. Le nombre cycle max est variable en fonction des circuits mais est de l'ordre de 100 000. Il peut être plus élevé (jusque même 1 000 000) mais vous n’avez aucune garantie que cela soit le cas !

Cela paraît beaucoup mais imaginons que l'on crée un système qui, pour économiser de la batterie, se réveille toutes les 10 min avant de se rendormir. Alors on "tue" la mémoire flash en... 277 heures soit 11 jours. C'est donc impossible.



**Webographie :**

Source de ce tutoriel :

{% embed url="https://randomnerdtutorials.com/install-esp32-filesystem-uploader-arduino-ide/" %}
Pour aller plus loin : serveur Web utilisant SPIFFS :
{% endembed %}

Pour aller plus loin : serveur Web utilisant SPIFFS :

{% embed url="https://randomnerdtutorials.com/esp32-web-server-spiffs-spi-flash-file-system/" %}

**Accès à la mémoire Flash de l’ESP32**

Une autre manière d’accéder à la mémoire Flash avec l’IDE Arduino consiste à utiliser la librairie EEPROM car l’usage de cette librairie avec l’ESP32 est très similaire à celui de l’Arduino.

Cependant, avec cette librairie et l’ESP32, l’accès est limité à seulement 512 bytes. C’est suffisant pour sauvegarder des valeurs ou des états mais bien inférieur à la capacité de la mémoire Flash (16 MB).

A noter que, même en passant SPIFFS, vous n’accèderez pas à la totalité de cette mémoire. Regardez les différentes partitions proposées dans l’IDE Arduino : Outils à Partition Scheme.



**Comprendre et faire le montage du tutorial suivant :**

{% embed url="https://randomnerdtutorials.com/esp32-flash-memory/" %}
