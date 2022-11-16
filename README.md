---
description: description
---

# SPIFFS (sous Arduino)

**Installation du téléchargeur SPIFFS pour l’ESP32 sur l’IDE Arduino**

**Présentation**

L’ESP32 contient un SPIFFS (Serial Peripheral Interface Flash File System). SPIFFS est un système de fichiers léger créé pour les microcontrôleurs qui ont une puce flash, et qui y sont connectés par bus SPI, comme la mémoire flash de l’ESP32.

<figure><img src=".gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

**Introduction à SPIFFS**

SPIFFS nous permet d’accéder à la mémoire flash (Flash Memory) comme nous aimerions le faire avec n’importe quel système de fichiers sur l’ordinateur. Nous pouvons écrire, fermer et supprimer des fichiers. Actuellement, SPIFFS ne supporte pas les répertoires, aussi les fichiers sont sauvegardés dans une structure au même niveau.

Les principaux usages de SPIFFS sont :

* Créer des fichiers de configuration avec des installations
* Sauvegarder des données de manière permanente
* Créer des fichiers pour enregistrer des petites quantités de données plutôt que d’utiliser une microcarte SD
* Sauvegarder des fichiers HTML et CSS pour construire un serveur Web
* Etc.

**Installation**

Plutôt que de coder à la main l’accès à la mémoire flash, nous allons utiliser un plugin de l’IDE Arduino qui nous facilitera la tâche.

Tout d’abord, assurez-vous que la dernière version de l’IDE Arduino a bien été installée.

Ensuite, télécharger le fichier **ESP32FS-1.0.zip** disponible à l’adresse suivante :

[https://github.com/me-no-dev/arduino-esp32fs-plugin/releases/](https://github.com/me-no-dev/arduino-esp32fs-plugin/releases/)

Allez dans le répertoire de l’IDE Arduino, ouvrez le répertoire **tools** (arduino 1.8.10 > tools).

Décompressez le répertoire .zip et assurez-vous d’avoir une structure de fichiers similaire à :

\<home\_dir>/Arduino-\<version>/**tools/ESP32FS/tool/esp32fs.jar**

Redémarrez l’IDE Arduino.

(Remarque : vous trouverez les dernières instructions à l’adresse suivante : [https://github.com/me-no-dev/arduino-esp32fs-plugin](https://github.com/me-no-dev/arduino-esp32fs-plugin))

**Téléchargement de fichiers dans la mémoire flash**

1\.     Créer un croquis (sketch) Arduino et sauvegardez-le.

2\.     Ouvrez le répertoire de ce croquis (Ctrl K ou Croquisà Afficher le dossier des croquis)

3\.     A l’intérieur de ce répertoire, créer un nouveau répertoire appelé **data**

4\.     A l’intérieur du répertoire data, vous mettrez les fichiers que vous voulez sauver dans le système de fichiersESP32. Par exemple, créez un fichier **test.txt** qui contient le texte suivant : _**Exemple pour tester le filesystem ESP32**_

5\.     Pour télécharger les fichiers, dans l’Ide Arduino, allez à **Outilsà ESP32 Sketch Data Upload** (ne pas oublier de fermer le moniteur série s’il est ouvert)

<figure><img src=".gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Remarque : pour certaines cartes de développement ESP32, quand on voit le message « Connecting ……\_\_\_\_\_\_\_...... », vous devez appuyer sur le bouton BOOT et rester appuyé jusqu’à la fin du téléchargement des fichiers.

Quand vous voyez le message **SPIFFS Image Uploaded**, c’est que l’opération a réussi.

<figure><img src=".gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

**Vérification du téléchargement**

Le code ci-après a pour objectif de lire le contenu du fichier **test.txt** sauvegardé en mémoire flash via SPIFFS. On inclura la bibliothèque SPIFFS.h.

```arduino
/*********
Complete project details at https://randomnerdtutorials.com 
*********/
#include "SPIFFS.h"
void setup() {
  Serial.begin(115200);
  if(!SPIFFS.begin(true)){
    Serial.println("An Error has occurred while mounting SPIFFS");
    return;
  }
  File file = SPIFFS.open("/test.txt");
  if(!file){
    Serial.println("Failed to open file for reading");
    return;
  }
  Serial.println("File Content:");
  while(file.available()){
    Serial.write(file.read());
  }
  file.close();
}
void loop() {
}
```

Après téléversement du fichier Test.ino, ouvrez le moniteur série au taux de 115200 bauds.

Sur l’ESP32, appuyez sur le bouton « ENABLE » (ou « RST »). Le contenu du fichier **test.txt** s’affiche sur le moniteur série :

<figure><img src=".gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
