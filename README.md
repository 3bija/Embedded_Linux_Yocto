# Projet Yocto - Distribution Linux Embarquée pour Raspberry Pi 3

Ce projet présente la construction d'une distribution Linux embarquée sur mesure pour une carte Raspberry Pi 3 à l'aide de Yocto Project / OpenEmbedded (branche scarthgap), réalisé en binôme (Mines Saint-Étienne).

## Contenu de la couche personnalisée (`meta-bootlinlabs`)
- **Recettes personnalisées** :
  - `ninvaders` (clone de Space Invaders basé sur ncurses).
  - `ctris` (clone de Tetris pour terminal, intégré via `devtool`).
- **Configuration noyau** : Fragment pour désactiver la compression des modules (`.ko`) afin d'être compatibles avec BusyBox (`uncompressed_modules.cfg`).
- **Scripts et Services** : Script d'initialisation `/etc/init.d/bme680` pour la déclaration automatique du capteur environnemental I2C.
- **Interface Web** : Serveur `lighttpd` avec script CGI (`data.cgi`) pour un tableau de bord de télémétrie en temps réel.

## Instructions rapides
1. Cloner les dépôts nécessaires (`poky`, `meta-raspberrypi`, `meta-openembedded`).
2. Initialiser l'environnement de build :
   ```bash
   source poky/oe-init-build-env builds/rpi3
   ```
3. Ajouter la couche `meta-bootlinlabs` et configurer `local.conf` (`MACHINE = "raspberrypi3"`, activation de l'I2C, ajout des paquets).
4. Lancer la compilation :
   ```bash
   bitbake core-image-minimal
   ```
