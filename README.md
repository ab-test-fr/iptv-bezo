# iptv-bezo

Nettoyer le boîtier R69 Plus et y lire la liste IPTV. Le contexte complet est dans `CLAUDE.md`.

## Préparer un PC Windows (une seule fois)

Le PC doit être sur **le même Wi-Fi que le boîtier**.

1. Ouvre **PowerShell** (menu Démarrer, tape « PowerShell »).
2. Installe Git :

   ```powershell
   winget install --id Git.Git -e
   ```

3. Installe Claude Code :

   ```powershell
   irm https://claude.ai/install.ps1 | iex
   ```

4. Ferme PowerShell et rouvre-le, puis récupère le projet (une fenêtre de connexion GitHub peut s'ouvrir) :

   ```powershell
   git clone https://github.com/ab-test-fr/iptv-bezo.git
   cd iptv-bezo
   claude
   ```

5. Connecte-toi avec ton compte Claude, puis écris : « Lis le CLAUDE.md et on commence par la connexion au boîtier ». Claude installera lui-même `adb` s'il manque.

Sur le PC de quelqu'un d'autre : à la fin, tape `/logout` dans Claude Code et déconnecte GitHub (Gestionnaire d'identification Windows, entrée `git:https://github.com`).

## Préparer le boîtier

1. **Paramètres > Préférences de l'appareil > À propos**, puis appuie 7 fois sur **Build Android TV** jusqu'au message « Vous êtes développeur ».
2. Reviens en arrière, ouvre **Options pour les développeurs** et active **Débogage USB**, plus **Débogage réseau** ou **Débogage sans fil** s'ils existent.
3. Note l'adresse IP du boîtier : **Paramètres > Réseau et Internet**, puis ton Wi-Fi.
4. À la première connexion, le boîtier demande « Autoriser le débogage ? » : coche « Toujours autoriser » et valide.

Quand tout est fini, coupe ces options de débogage.
