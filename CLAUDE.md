# iptv-bezo

Nettoyer le boîtier Android TV d'Alban (applis inutiles, pubs, pistage), lui donner un écran d'accueil sobre et y installer un lecteur pour sa liste IPTV.

Projet personnel, sans lien avec Secundo : rien de ce dépôt ne va dans `ab-test-fr/control`, et inversement.

## Règles
- On parle à Alban en français, en le tutoyant. Jamais de tiret long « — » ni « – ».
- Aucun identifiant IPTV, mot de passe ou adresse de liste privée dans le code, les commits ou la conversation. Ils vont dans `prive/` (ignoré par git).
- On **désactive** les applis (`pm disable-user --user 0`), on ne les supprime jamais. Chaque changement est noté dans `annuler.txt` avec la commande inverse.
- On demande à Alban avant **chaque** changement sur le boîtier.
- Ne jamais désactiver : Google Play services (`com.google.android.gms`), Google Play Store, Paramètres, System UI, l'assistant de configuration, le clavier, le Bluetooth, le cadre d'entrées TV (`com.android.tv.*` lié aux entrées et au tuner), ni rien dont le boîtier a besoin pour démarrer. Dans le doute, on laisse.
- Attendre 30 secondes après le dernier changement, redémarrer une fois, vérifier que le boîtier redémarre normalement avant de dire que c'est fait.
- À la fin, rappeler à Alban de couper le débogage USB et réseau sur le boîtier.

## Le matériel
- Boîtier **R69 Plus**, 4 Go / 32 Go, modèle affiché « MBOX ».
- Système **BigdroidOS 3.0.3.010245**, **Android TV 14** (pas Google TV), build 14.0145.250210, noyau 5.15.137.
- Correctif de sécurité du 5 juin 2024 : pas à jour.
- Applis vues à l'écran : AppList, Google Play Store, YouTube, un gestionnaire de fichiers, AirScreen, Twitch, **Aptoide TV** (boutique hors Google, à examiner). L'accueil affiche des pubs Prime Video et des lignes « Tendance sur Google ».
- Ce genre de boîtier sans marque est visé par **BadBox** (logiciel malveillant installé en usine, basé sur Triada). Le R69 Plus ne figure pas dans les listes publiées, mais on vérifie à l'inventaire : paquets aux noms bizarres ou génériques, applis système qui demandent des droits réseau sans raison, services qui tournent en permanence.

## Le plan
1. **Connexion** : trouver le boîtier sur le Wi-Fi (`adb connect <IP>:5555`, ou appairage par code si seul « Débogage sans fil » existe). Alban appuie sur « Autoriser » à l'écran.
2. **Inventaire** : lister toutes les applis (`adb shell pm list packages -f`), les classer en clair : à garder, à désactiver, à surveiller (suspectes). Relever la mémoire libre (`adb shell dumpsys meminfo`, `adb shell cat /proc/meminfo`). Écrire le résultat dans `inventaire.md`.
3. **Tri** : désactiver ce qu'Alban valide, en notant tout dans `annuler.txt`.
4. **Accueil** : écran d'accueil sobre. Point de départ possible : https://github.com/Ansub/tv-detox (licence MIT, `install.sh` et `undo.sh`, scripts shell : sur Windows, les lancer avec Git Bash).
5. **IPTV** : installer un lecteur. Choix par défaut : Kodi + extension « PVR IPTV Simple Client », ou VLC. Une appli maison seulement si Alban la veut.
6. **Réglages** : animations coupées, mise en veille après quelques minutes, puis redémarrage de contrôle et mémoire libre avant / après.

## Questions encore ouvertes
- Format de la liste IPTV : adresse M3U, fichier, ou compte Xtream ? Guide des programmes (EPG) ?
- Lecteur : Kodi, VLC, ou appli maison ?
- Applis à garder : YouTube, Twitch, AirScreen, autres ?
