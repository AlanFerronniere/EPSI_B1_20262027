# Projet IOT

## Contexte
Le but du projet est de créer des objets connectés capables de mesurer l'attrait de tableaux exposés dans des galeries d'art. Ces objets permettront de collecter des données sur l'intérêt des visiteurs pour chaque œuvre, en utilisant des capteurs et des technologies IoT.

### Premier type de mesure : j'aime / j'aime pas
2 boutons sur l'objet connecté permettront aux visiteurs d'indiquer leur intérêt pour le tableau. Le premier bouton sera utilisé pour exprimer un intérêt positif, tandis que le second bouton sera utilisé pour exprimer un intérêt négatif. Chaque pression sur un bouton sera enregistrée et envoyée à un serveur central pour analyse.

### Second type de mesure : temps passé devant le tableau
Un capteur de proximité sera intégré à l'objet connecté pour mesurer le temps que chaque visiteur passe devant le tableau. Le capteur détectera la présence d'une personne et enregistrera la durée de son passage devant l'œuvre. Ces données seront également envoyées au serveur central pour être analysées.

### Sécurité de l'oeuvre : température et humidité
Un capteur de température et d'humidité sera intégré à l'objet connecté pour surveiller les conditions environnementales autour du tableau. Ces mesures permettront de s'assurer que l'œuvre est conservée dans des conditions optimales, et toute variation significative pourra déclencher une alerte pour le personnel de la galerie.

## ESP32 et capteurs

L'ESP32 est un microcontrôleur puissant et polyvalent qui sera utilisé comme base pour notre objet connecté. Il dispose de capacités Wi-Fi et Bluetooth, ce qui permettra de transmettre les données collectées par les capteurs vers un serveur central.
Vous utiliserez différents capteurs pour mesurer l'intérêt des visiteurs et les conditions environnementales autour des tableaux. 
- 2 boutons
- 1 capteur de proximité ultresonique
- 1 capteur de température et d'humidité (DHT11)

## Pour commencer

Commencez par découvrir le fonctionnement de l'ESP32 et comment programmer ce microcontrôleur. Vous pouvez utiliser l'environnement de développement Arduino IDE pour écrire et téléverser votre code sur l'ESP32.
Des tutos sont disponibles sur https://esp32io.com/

> https://esp32io.com/tutorials/esp32-software-installation

## Etape 1
Essayez les capteurs en utilisant le moniteur série pour afficher les données collectées. Vous pouvez commencer par tester chaque capteur individuellement pour vous familiariser avec leur fonctionnement.

> https://esp32io.com/tutorials/esp32-serial-monitor
> https://esp32io.com/tutorials/esp32-ultrasonic-sensor
> https://esp32io.com/tutorials/esp32-dht22

