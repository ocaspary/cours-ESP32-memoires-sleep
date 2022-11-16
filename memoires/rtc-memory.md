# RTC memory

Le meilleur moyen de sauvegarder un contexte en évitant le problème de la mémoire Flash ! Pour cela pas besoin de librairie ou d'includes spéciaux... il suffit de déclarer la variable avec le préfixe : RTC\_DATA\_ATTR.

**RTC\_DATA\_ATTR int bootCount=0;**

Après un reset HARD ou SOFT la valeur de bootCount est remise à zéro mais après un "deep sleep" non. Voici un exemple pour comprendre : lancez le programme tel quel, avec ESP.restart(), avec abort().

**Comprendre le code en recherchant les fonctions : rtc\_get\_ … , esp\_sleep\_ … , esp\_deep\_ …**

Pour vous aider : [http://esp32.info/docs/esp\_idf/html/db/dc1/group\_\_rtc\_\_apis.html](http://esp32.info/docs/esp\_idf/html/db/dc1/group\_\_rtc\_\_apis.html)

Autre info : il y a deux cœurs dans l’ESP32 : core 0 – PRO et core 1 – APP. Le CPU0 lance tout le code de gestion de **PRO**tocole, tandis que le CPU1 s’occupe de l’**APP**lication. Cela explique le fait que le code dans la boucle loop() s’exécute sur le cœur 1. Le fonctionnement des cœurs est symétrique et les tâches interchangeables via des mécanismes de queues et sémaphores (thread).

**Fichier Boot\_Count.ino :**

```arduino
    #include <rom/rtc.h>

    RTC_DATA_ATTR int rtcBootCount = 0;
    int bootCount=0;

    void setup(){
      Serial.begin(115200);
      delay(500);
      Serial.printf("\n\n%d\n%d  %d\n",rtc_get_reset_reason(0),rtcBootCount,bootCount);
      bootCount = bootCount+1;
      rtcBootCount = rtcBootCount+1;  
      delay(3000);

      //ESP.restart();
      // abort();
      esp_sleep_enable_timer_wakeup(0); 
      esp_deep_sleep_start();
    }

    void loop(){
    }
```

Tel quel, on voit bien que la valeur de bootCount est remise à zéro à chaque boot alors que rtcBootCount continue à être incrémenté. (les lignes 16 et 17 sont un deep sleep de.. zéro micro secondes)

En revanche, avec un Hard reset, les deux valeurs restent à zéro. De même si on fait un Soft reset (Ligne 14) ou un abort (ligne 15).

Cet exemple nous amène aux modes Sleep de l’ESP32 ci-dessous.
