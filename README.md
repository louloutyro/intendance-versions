<img src="icone.svg" width="96" alt="">

# Intendance

Planification des repas et des courses de séjours collectifs : vacances entre amis, maison louée à plusieurs. Planning des repas, présences des convives, listes de courses calculées et réparties par rayon, impression et export PDF. L’interface est en français.

Ce dépôt ne contient que les versions publiées de l’application, pour Windows, macOS et Linux.

## Télécharger

**[Dernière version](../../releases/latest)** : choisir le fichier qui correspond à son système.

Pour savoir quelle puce équipe son Mac : menu Pomme › *À propos de ce Mac*, ligne *Puce* (Apple M1, M2…) ou *Processeur* (Intel).

| Système | Fichier |
|---|---|
| Windows 10 et 11 (64 bits) | `Intendance-…-Windows.exe` (installateur) |
| macOS 14 ou plus récent, Mac Apple Silicon (M1, M2…) | `Intendance-…-macOS-AppleSilicon.dmg` |
| macOS 14 ou plus récent, Mac Intel | `Intendance-…-macOS-Intel.dmg` |
| Linux (64 bits) | `Intendance-…-x86_64.AppImage` |

Au premier lancement, la bibliothèque (séjours, recettes, ingrédients) est créée dans *Documents › Intendance*, avec 25 recettes et 83 ingrédients de départ. Son emplacement se change dans *Réglages › Stockage*, par exemple pour la placer dans un dossier synchronisé.

## Installer

Les paquets ne sont pas signés. Les systèmes affichent donc des avertissements au premier lancement, qui ne signalent pas un défaut de l’application.

**Windows.** Lancer l’installateur. Si Windows affiche « Windows a protégé votre ordinateur », choisir *Informations complémentaires*, puis *Exécuter quand même*. L’installation se fait sans droits d’administrateur ; la désinstallation passe par *Paramètres › Applications*.

**macOS.** Ouvrir le `.dmg` et glisser Intendance dans *Applications*. Au premier lancement, macOS indique que l’application ne peut pas être vérifiée : ouvrir *Réglages Système › Confidentialité et sécurité*, puis choisir *Ouvrir quand même* en regard d’Intendance.

**Linux (Ubuntu, Linux Mint…).** L’AppImage demande FUSE 2 : `sudo apt install libfuse2t64` (Ubuntu 24.04, Mint 22) ou `sudo apt install libfuse2` (Ubuntu 22.04, Mint 21). Rendre ensuite le fichier exécutable (`chmod +x Intendance-…-x86_64.AppImage`, ou *Propriétés › Permissions › Autoriser l’exécution*) et le lancer d’un double-clic. Pour l’ajouter au menu des applications et le désinstaller proprement, [Gear Lever](https://flathub.org/apps/it.mijorus.gearlever) s’en charge.

## Ligne de commande

À partir de la version 0.2.0, chaque paquet contient aussi `clintendance`, la ligne de commande d’Intendance : elle lit, exporte, importe et modifie la bibliothèque avec les mêmes règles que l’application, depuis un terminal, un script ou un agent (assistant d’intelligence artificielle).

| Système | Emplacement |
|---|---|
| macOS | `/Applications/Intendance.app/Contents/MacOS/clintendance` |
| Windows | `clintendance.exe`, dans le dossier d’installation (par défaut `%LOCALAPPDATA%\Programs\Intendance`) |
| Linux | l’AppImage, lancée sous le nom `clintendance` : `ln -s ~/Applications/Intendance-…-x86_64.AppImage ~/.local/bin/clintendance` |

```
clintendance --help                 # objets et verbes
clintendance guide                  # guide d’emploi pour les agents
clintendance guide --commandes      # tableau complet des commandes
clintendance courses liste          # liste de courses du séjour
clintendance recette lister --json  # sortie lisible par une machine
```

Pour un agent, `clintendance guide` dit l’essentiel : toujours `--json`, lire le code de sortie, désigner les éléments par leur identifiant, `--simulation` avant d’écrire, un point de retour avant une longue séance (`bibliotheque sauvegardes creer NOM`), et les lots (`lot FICHIER`) pour écrire plusieurs modifications en une fois.

Sans `--bibliotheque CHEMIN`, la commande agit sur la bibliothèque de l’application. Les modifications sont refusées tant qu’Intendance est ouverte sur cette bibliothèque ; chacune est précédée d’une sauvegarde (`clintendance bibliotheque sauvegardes`).

## Désinstaller sans perdre ses données

Désinstaller l’application ne touche pas à la bibliothèque, qui reste dans *Documents › Intendance* (ou dans le dossier choisi dans les réglages).
