# Paramètres xDrip+

S'il n'est pas déjà configuré, téléchargez [xDrip+](https://jamorham.github.io/#xdrip-plus).

**Cette documentation est pour xDrip+ pour Android.** Il y a une application "xDrip pour iOS" qui n'a rien à voir avec l'original xDrip+ pour Android.

Pour les émetteurs G6 fabriqués après l’automne/fin 2018 (c.a.d. N° de série commençant par 80 ou 81) veuillez vous assurer d'utiliser au minimum la version [release du 2019/05/18](https://jamorham.github.io/#xdrip-plus).

Si le numéro de série de votre émetteur Dexcom G6 commence par 8G... ou 8H... utilisez l'une des [dernières "Nightly build"](https://github.com/NightscoutFoundation/xDrip/releases).

Si votre téléphone tourne Android 10 et que vous avez des difficultés avec la version master de xDrip+ essayez la[ build 2019/12/31 ou plus récente ](https://github.com/NightscoutFoundation/xDrip/releases).

## Paramètres de base pour tous les systèmes MGC & MGF

* Assurez-vous de définir correctement l'URL de base incluant **S** à la fin de http**s**:// (et non http://)
   
   par ex. https://API_SECRET@your-app-name.herokuapp.com/api/v1/
   
   -> Menu Hamburger (en haut à gauche de l'écran d'accueil) -> Paramètres-> Cloud Upload -> Syncchronisation Nightscout (REST-API) -> URL de base

* Désactivez `Automatic Calibration` Si la case `Automatic Calibration` est cochée, Activez `Download data` une fois, ensuite décochez la case pour `Automatic Calibration` et désactivez `Download data` à nouveau, sinon les traitements (insuline & glucides) seront ajoutés deux fois dans Nightscout.

* Appuyez sur `Extra Options`

* Désactivez `Upload treatments` et `Back-fill data`.
   
   **Avertissement de sécurité : Vous devez désactiver "Upload treatments" dans xDrip, sinon les traitements peuvent être doublés dans les AAPS conduisant à de faux GA et IA.**

* L'option `Alert on failures` doit également être désactivée. Sinon, vous aurez une alarme toutes les 5 minutes dans le cas ou le wifi / réseau mobile est trop mauvais, ou si le serveur n'est pas disponible.
   
   ![xDrip+ Basic Settings 1](../images/xDrip_Basic1.png)
   
   ![xDrip+ Basic Settings 2](../images/xDrip_Basic2.png)

* ** Inter App-Settings ** (Diffusion locale) Si vous voulez utiliser AndroidAPS et que les données doivent être transmises à AndroidAPS, vous devez activer la Diffusion locale dans xDrip + dans les paramètres Inter-app.

* Pour que les valeurs soient les mêmes, vous devez activer `Send Display Glucose`.

* Si vous avez aussi activé `Accept Treatments` et la diffusion dans AndroidAPS, alors xDrip+ recevra l'insuline, les glucides et les informations sur les débits de basal d'AndroidAPS et peut estimer la prédiction des hypo, etc. avec plus de précision.
   
   ![xDrip+ Basic Settings 3](../images/xDrip_Basic3.png)

### Identifier le récepteur

* Si vous avez des problèmes de diffusion locale (AAPS ne recevant pas les valeurs Gly de xDrip +) allez dans Paramètres > Inter-app settings > Identify receiver et entrez `info.nightscout.androidaps`.
* Attention: La correction automatique a parfois tendance à changer la lettre i en majuscules. Vous **ne devez utiliser que des minuscules** pour taper `info.nightscout.androidaps`. Un I majuscule empêcherait AAPS de recevoir les valeurs de Gly de xDrip+.
   
   ![xDrip+ Paramètres interapp basiques Identifier le récepteur](../images/xDrip_InterApp_NS.png)

## xDrip+ & Dexcom G6

* L'émetteur Dexcom G6 peut être connecté simultanément au récepteur Dexcom (ou alternativement à la pompe t:slim) et à une application sur votre téléphone.
* Lorsque vous utilisez xDrip+ comme récepteur, désinstallez d'abord l'application Dexcom. **Vous ne pouvez pas connecter xDrip + et l'application Dexcom avec l'émetteur en même temps !**
* Si vous avez besoin d'éclaircissements et voulez profiter des alarmes xDrip+, utilisez l'applications [Dexcom patchée](../Hardware/DexcomG6#if-using-g6-with-patched-dexcom-app) avec la diffusion locale vers xDrip+.

### Version de XDrip+ en fonction du numéro de série de l'émetteur G6.

* Pour les émetteurs G6 fabriqués après l’automne/fin 2018 (c.a.d. N° de série commençant par 80 ou 81) veuillez vous assurer d'utiliser au minimum la version [release du 2019/05/18](https://jamorham.github.io/#xdrip-plus). 
* Si le numéro de série de votre émetteur Dexcom G6 commence par 8G ou 8H essayez [Nightly build 2019/07/28 ou ultérieure](https://github.com/NightscoutFoundation/xDrip/releases).

### Paramètres spécifiques à Dexcom

* Ouvez les paramètres de débogage G5/G6 -> Menu Hamburger (en haut à gauche de l'écran d'accueil) -> Paramètres -> G5/G6 Debug Settings ![Open xDrip+ Settings](../images/xDrip_Dexcom_SettingsCall.png)

* Activez les paramètres suivants
   
   * `Use the OB1 Collector`
   * `Native Algorithm` (important if you want to use SMB)
   * `G6 support`
   * `Allow OB1 unbonding`
   * `Allow OB1 initiate bonding`
* Toutes les autres options doivent être désactivées
* Ajuster le niveau d'alerte batterie à 280 (en bas des paramètres de débogage G5/G6)
   
   ![xDrip+ G5/G6 Debug Settings](../images/xDrip_Dexcom_DebugSettings.png)

### Redémarrages préventifs non recommandés

**Avec Dexcom les émetteurs dont le numéro de série commence par 8G ou 8H le redémarrage préventif ne fonctionnent pas et pourrait tuer complètement le capteur !**

L'extension automatique des détecteurs Dexcom (`preemptive restarts`) n'est pas recommandée car cela peut entraîner des "sauts" dans les valeurs Gly le 9ème jour après le redémarrage.

![xDrip+ Jump after Preemptive Restart](../images/xDrip_Dexcom_PreemptiveJump.png)

Ce qui est clair, c’est que l’utilisation du G6 est peut-être un peu plus complexe qu’on pourrait le penser au premier abord. Pour l'utiliser en toute sécurité, il y a quelques points à prendre en compte :

* Si vous utilisez les données natives avec le code d'étalonnage dans xDrip+ ou Spike, la chose la plus sûre à faire est de ne pas autoriser les redémarrages préventifs du capteur.
* Si vous devez faire un redémarrage préventif, assurez-vous de le faire à un moment de la journée où vous pouvez observer le changement et faire la calibration si nécessaire. 
* Si vous redémarrez des capteurs, fais-le sans l'étalonnage de l'usine pour obtenir les résultats les plus sûrs les jours 11 et 12, ou assurez-vous que vous êtes prêt à le calibrer et à garder un oeil sur la variation.
* La pré-installation du G6 avec un étalonnage d'usine peut entraîner des variations dans les résultats. Si vous faites une pré-installation, alors pour obtenir les meilleurs résultats, vous devrez probablement calibrer le capteur.
* Si vous n'êtes pas attentif aux changements qui peuvent avoir lieu, il peut être préférable de revenir dans un mode "non calibré en usine" et d'utiliser le système comme un G5.

Pour en savoir plus sur les détails et les raisons de ces recommandations, consultez [l'article complet](http://www.diabettech.com/artificial-pancreas/diy-looping-and-cgm/) publié par Tim Street sur [www.diabettech.com](http://www.diabettech.com).

### Connecter l'émetteur G6 pour la première fois

**Pour le deuxième transmetteur et les suivants, voir [Étendre la durée de vie de l'émetteur](../Configuration/xdrip#extend-transmitter-life) ci-dessous.**

Pour les émetteurs G6 fabriqués après l’automne/fin 2018 (c.a.d. N° de série commençant par 80 ou 81) veuillez vous assurer d'utiliser au minimum la version [release du 2019/05/18](https://jamorham.github.io/#xdrip-plus).

Si le numéro de série de votre émetteur Dexcom G6 commence par 8G ou 8H essayez [Nightly build 2019/07/28 ou ultérieure](https://github.com/NightscoutFoundation/xDrip/releases).

* Désactivez le récepteur Dexcom d'origine (s'il est utilisé).
* Faites un appui long sur l'icône rouge xDrip+ sur l'écran principal pour activer `Source Wizard Button`.
* Utilisez le Source Wizard Button qui assure les paramétrages par défaut incluant OB1 & Native Mode 
   * Ce guide vous aidera lors du paramétrage initial.
   * Vous aurez besoin de votre numéro de série de l'émetteur si c'est la première fois que vous l'avez utilisé.

* Mettre le numéro de série du nouveau transmetteur (présent sur l'emballage du transmetteur ou à l'arrière de celui-ci). Veillez à ne pas confondre 0 (zéro) et O (o majuscule).
   
   ![xDrip+ Dexcom Transmitter Serial No](../images/xDrip_Dexcom_TransmitterSN.png)

* Insérer un nouveau capteur (uniquement en cas de remplacement)

* Placer l'émetteur dans le capteur
* Ne démarrez pas le nouveau capteur avant que l'information suivante soit présente dans la page Etat du système -> Classic Status Page -> G5/G6 status -> PhoneServiceState :
   
   * Numéro de série du transmetteur commençant par 80 ou 81 : "Got data hh:mm" (par ex. "Got data 19:04")
   * Numéro de série du transmetteur commençant par 8G ou 8H : "Got glucose hh:mm" (par ex. "Got glucose 19:04") ou "Got now raw hh:mm" (par ex. "Got now raw 19:04")
   
   ![xDrip+ PhoneServiceState](../images/xDrip_Dexcom_PhoneServiceState.png)

* Insérer un nouveau capteur (uniquement en cas de remplacement)
   
   -> En bas de l'écran, `Warm Up x,x hours left` doit être affiché après quelques minutes.

-> Si le numéro de série de l'émetteur ne commence pas par 8G ou 8H et qu'il n'y a pas de temps renseigné après plusieurs minutes, arrêtez et redémarrez le capteur.

* Redémarrer le transmetteur (état du système - si pas de remplacement du capteur)
* Ne rallumez pas le récepteur Dexcom d'origine (si utilisé) avant que xDrip+ affiche les premières lectures.
* Faites un appui long sur l'icône rouge xDrip+ sur l'écran principal pour désactiver `Source Wizard Button`.
   
   ![xDrip+ Dexcom Transmitter 1](../images/xDrip_Dexcom_Transmitter01.png)
   
   ![xDrip+ Dexcom Transmitter 2](../images/xDrip_Dexcom_Transmitter02.png)
   
   ![xDrip+ Dexcom Transmitter 3](../images/xDrip_Dexcom_Transmitter03.png)
   
   ![xDrip+ Dexcom Transmitter 4](../images/xDrip_Dexcom_Transmitter04.png)

### Etat de la batterie de l'émetteur

* L'état de la batterie peut être contrôlé dans l'état du système (menu Hamburger en haut à gauche sur l'écran d'accueil)
* Balayez vers la gauche une fois pour voir le deuxième écran. ![xDrip+ First Transmitter 4](../images/xDrip_Dexcom_Battery.png)

* Les valeurs exactes lorsque l'émetteur "meurt" à cause d'une batterie vide ne sont pas connues. Les renseignements suivants ont été affichés après la mort de l'émetteur :
   
   * Affichage 1 : Transmitter days: 151 / Voltage A: 297 / Voltage B: 260 / Resistance: 2391
   * Affichage 2 : Transmitter days: 249 / Voltage A: 275 (at time of failure)

### Étendre la durée de vie de l'émetteur

* Jusqu'à présent la durée de vie des émetteurs dont le numéro de série commence par 8G ou 8H ne peut pas être prolongée.
* Pour éviter les difficultés de démarrage de capteurs il est fortement recommandé d'étendre la durée de vie de l'émetteur avant le jour 100 de la première utilisation.
* La session en cours du capteur sera stoppée lors de l'extension de la durée de vie de l'émetteur. Donc étendre la durée de vie avant un changement de capteur, ou soyez conscient qu'il y aura une nouvelle phase de démarrage du capteur d'une durée de 2h.
* Arrêtez le capteur manuellement via le menu hamburger.
* Basculez dans le mode `engineering` : 
   * appuyez sur le caractère à droite de l'écran de démarrage xDrip+ qui représente une seringue
   * puis appuyez sur l'icône du microphone dans le coin inférieur droit
   * dans le champs de texte qui s'ouvre, tapez "enable engineering mode" 
   * cliquez sur "Done"
   * si le moteur de reconnaissance vocal Google est activé, vous pouvez aussi dire la commande vocale : "enable engineering mode". 
* Accédez aux paramètres de débogage G5 et vérifiez que `Use the OB1 collector` est activé.
* Utilisez la commande vocale : “hard reset transmitter”
* La commande vocale sera exécutée lors de la prochaine réception de données du transmetteur
* Regardez l'état du système (menu Hamburger -> état du système) et voyez ce qui se passe
* Si vous voyez un message "Phone Service State: Hard Reset maybe failed" sur le 2ème écran d'état du système, il suffit de démarrer le capteur et ce message devrait disparaitre.
   
   ![xDrip+ Hard Reset maybe failed](../images/xDrip_HardResetMaybeFailed.png)

* Le nombre de jours du transmetteur doit être à 0 après l'extension réussie de l'émetteur et le démarrage du capteur.

### Remplacement de l'émetteur

Pour les émetteurs G6 fabriqués après l’automne/fin 2018 (c.a.d. N° de série commençant par 80 ou 81) veuillez vous assurer d'utiliser au minimum la version [release du 2019/05/18](https://jamorham.github.io/#xdrip-plus).

Si le numéro de série de votre émetteur Dexcom G6 commence par 8G ou 8H, utilisez une des dernière [nightly builds](https://github.com/NightscoutFoundation/xDrip/releases) de xDrip+.

* Désactivez le récepteur Dexcom d'origine (s'il est utilisé).
* Arrêtez le capteur (uniquement en cas de remplacement)
   
   Vérifiez qu'il est vraiment arrêté :
   
   Sur le 2ème écran d'état "G5/G6 Status", regardez `Queue Items` à peu prèt au milieu - cela devrait afficher quelque chose comme `(1) Stop Sensor`
   
   Attendez jusqu'à ce que cela arrive - en général en quelques minutes. L'état du capteur doit être "Stopped" (voir la capture d'écran).
   
   -> Pour retirer le transmetteur sans arrêter le capteur, voir cette vidéo <https://youtu.be/AAhBVsc6NZo>.
   
   ![xDrip+ Stop Dexcom Sensor 1](../images/xDrip_Dexcom_StopSensor.png)
   
   ![xDrip+ Stop Dexcom Sensor 2](../images/xDrip_Dexcom_StopSensor2.png)

* Forget device in xDrip+ system status AND in smartphone’s BT settings (Will be shown as Dexcom?? whereas ?? are the last two digits of the transmitter serial no.)
   
   ![xDrip+ Forget Device](../images/xDrip_Dexcom_ForgetDevice.png)

* Remove transmitter (and sensor if replacing sensor)

* Put the old transmitter far away to prevent reconnection. A microwave is a perfect Faraday shield for this - but unplug power cord to be 100% no one is turning the microwave on.
* Faites un appui long sur l'icône rouge xDrip+ sur l'écran principal pour activer `Source Wizard Button`.
* Utilisez le Source Wizard Button qui assure les paramétrages par défaut incluant OB1 & Native Mode 
   * Ce guide vous aidera lors du paramétrage initial.
   * You will need your transmitter serial number if this is the first time you've used it.
* Put in serial number of new transmitter. Veillez à ne pas confondre 0 (zéro) et O (o majuscule).
* Insert new sensor (only if replacing).
* Put transmitter into sensor - **Do not start sensor immediately!**
* New "Firefly Transmitters" (serial no. starting with 8G or 8H) can only be used in native mode.
* The following options must not be activated for new "Firefly Transmitters" (serial no. starting with 8G or 8H):
   
   * Preemptive Restart (disable!)
   * Restart sensor (disable!)
   * Fallback to xDrip+ (disable!)
   
   ![Settings for Firefly transmitters](../images/xDrip_Dexcom_FireflySettings.png)

* Check in Classic Status Page -> G5/G6 status -> PhoneServiceState if one of the following informations is displayed:
   
   * Numéro de série du transmetteur commençant par 80 ou 81 : "Got data hh:mm" (par ex. "Got data 19:04")
   * Numéro de série du transmetteur commençant par 8G ou 8H : "Got glucose hh:mm" (par ex. "Got glucose 19:04") ou "Got now raw hh:mm" (par ex. "Got now raw 19:04")
   
   ![xDrip+ PhoneServiceState](../images/xDrip_Dexcom_PhoneServiceState.png)

* Wait 15 minutes as the transmitter should communicate several times with xDrip before new sensor is started. Battery data will be shown below Firmware information.
   
   ![Firefly transmitter battery data](../images/xDrip_Dexcom_FireflyBattery.png)

* Start sensor and DO NOT BACKDATE! Always select "Yes, today"!

* Restart collector (system status - if not replacing sensor)
* Ne rallumez pas le récepteur Dexcom d'origine (si utilisé) avant que xDrip+ affiche les premières lectures.
* Faites un appui long sur l'icône rouge xDrip+ sur l'écran principal pour désactiver `Source Wizard Button`.
   
   ![xDrip+ Dexcom Transmitter 1](../images/xDrip_Dexcom_Transmitter01.png)
   
   ![xDrip+ Dexcom Transmitter 2](../images/xDrip_Dexcom_Transmitter02.png)
   
   ![xDrip+ Dexcom Transmitter 3](../images/xDrip_Dexcom_Transmitter03.png)
   
   ![xDrip+ Dexcom Transmitter 4](../images/xDrip_Dexcom_Transmitter04.png)

### Nouveau capteur

* Désactivez le récepteur Dexcom d'origine (s'il est utilisé).
* Stop sensor if necessary
   
   Vérifiez qu'il est vraiment arrêté :
   
   Sur le 2ème écran d'état "G5/G6 Status", regardez `Queue Items` à peu prèt au milieu - cela devrait afficher quelque chose comme `(1) Stop Sensor`
   
   Attendez jusqu'à ce que cela arrive - en général en quelques minutes.
   
   ![xDrip+ Stop Dexcom Sensor 1](../images/xDrip_Dexcom_StopSensor.png)
   
   ![xDrip+ Stop Dexcom Sensor 2](../images/xDrip_Dexcom_StopSensor2.png)

* Clean contacts (transmitter backside) with alcohol and let air-dry.

* In case you use this function disable `Restart Sensor` and `Preemptive restarts` (Hamburger menu -> Settings -> G5/G6 Debug Settings). If you miss this step and have these functions enabled the new sensor will not start properly.
   
   ![xDrip+ Preemptive Restart](../images/xDrip_Dexcom_Restart.png)

* Start Sensor
   
   **For new Firefly transmitters** (serial no. starting with 8G or 8H) **it is mandatory, for all other transmitters it is recommended to wait approx. 15 minutes between stopping and starting the new sensor (until `Sensor Status: Stopped` is shown on second system status screen). DO NOT BACKDATE!**

* Set time inserted
   
   * To use G6 Native mode you must wait for the 2 hour warm up (i.e insertion time is now).
   * If you are using the xDrip+ algorithm then you can set a time more than 2 hours ago to avoid warm up. Readings may be very erratic. Therefore, this is not recommended.
* Enter Sensor code (on the peel-off foil of the sensor) 
   * Keep code for further reference (i.e. new start after transmitter had to be removed)
   * Code can also be found in [xDrip+ logs](../Configuration/xdrip#retrieve-sensor-code): Click 3-dots-menu on xDrip+ homescreen and choose `View Event Logs`.
* No calibration is needed if you use G6 in "native mode". xDrip+ will show readings automatically after 2 hour warm-up.
* Do not turn original Dexcom Receiver (if used) back on before xDrip+ shows first readings.
   
   ![xDrip+ Start Dexcom Sensor 1](../images/xDrip_Dexcom_SensorStart01.png)
   
   ![xDrip+ Start Dexcom Sensor 2](../images/xDrip_Dexcom_SensorStart02.png)

### Retrieve sensor code

* In master dated 2019/05/18 and the latest nightly builds the sensor code is shown in system status (Hamburger menu top left on homescreen).
* Swipe left once to see second screen.
   
   ![xDrip+ Retrieve Dexcom Sensor Code2](../images/xDrip_Dexcom_SensorCode2.png)

* Dexcom sensor code can also be found in xDrip+ logs.

* Tap 3 dot menu (top right side on homescreen)
* Select `View Event Logs` and search for "code"
   
   ![xDrip+ Retrieve Dexcom Sensor Code](../images/xDrip_Dexcom_SensorCode.png)

## Troubleshooting Dexcom G5/G6 and xDrip+

### Problem connecting transmitter

* Transmitter must be shown in your smartphone's bluetooth settings.
* Transmitter will be shown as Dexcom?? whereas ?? represent the last two digits of your transmitter serial no. (i.e. DexcomHY).
* Open system status in xDrip+ (hamburger menu on top left side of home screen).
* Check if your transmitter is shown on first status page ('classic status page').
* If not: Delete device from your smartphone's bluetooth settings and restart collector.
* Wait about 5 min. until Dexcom transmitter reconnects automatically.

### Problem when starting new sensor

Please note that the following method might likely not work if your Dexcom G6 transmitter's serial no. is starting with 8G or 8H.

* Native sensor is marked as "FAILED: Sensor Failed Start"
* Arrêter le capteur
* Redémarrez votre téléphone
* Start sensor with code 0000 (four times zero)
* Wait 15 minutes
* Arrêter le capteur
* Start sensor with "real" code (printed on the adhesive protector)

Check in xDrip+ logs if xDrip+ starts counting "Duration: 1 minute" (and so on). Only in the xDrip+ logs you can detect at an early stage whether xdrip+ has stopped a sensor. Latest status is not always shown correctly on bottom of startscreen.

## xDrip+ & Freestyle Libre

### Paramètres spécifiques au Freestyle Libre

* Ouvrir les paramètres Bluetooth -> Menu Hamburger (en haut à gauche de l'homescreen) -> Paramètres -> défilement vers le bas -> Paramètres moins courants -> Bluetooth Settings
   
   ![xDrip+ Libre Bluetooth Settings 1](../images/xDrip_Libre_BTSettings1.png)

* Activez les paramètres suivants
   
   * `Turn Bluetooth on` 
   * `Use scanning`
   * `Always discover services`

* Toutes les autres options doivent être désactivées
   
   ![xDrip+ Libre Bluetooth Settings 2](../images/xDrip_Libre_BTSettings2.png)

### Connectez l'émetteur du Freestyle Libre & démarrez le capteur

![xDrip+ Start Libre Transmitter & Sensor 1](../images/xDrip_Libre_Transmitter01.png)

![xDrip+ Start Libre Transmitter & Sensor 2](../images/xDrip_Libre_Transmitter02.png)

![xDrip+ Start Libre Transmitter & Sensor 3](../images/xDrip_Libre_Transmitter03.png)