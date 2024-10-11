L'Instrument Cluster Simulator est un outil qui simule un tableau de bord pour les véhicules utilisant le protocole SocketCAN. Cela permet de tester des fonctionnalités de véhicules sans avoir besoin d'un véhicule physique.

Le devoir suivantt porte donc sur l'utilisation de ce un simulateur automobile dont le github est le suivant:

https://github.com/zombieCraig/ICSim


Avant TOUT :
Pour compiler le projet, vous aurez besoin des bibliothèques suivantes :

SDL2 : Une bibliothèque pour la création d'applications multimédia
SDL2_Image : Une extension pour gérer les images
can-utils : Outils pour interagir avec les interfaces CAN

"""sudo apt-get install libsdl2-dev libsdl2-image-dev can-utils"""

Pour compiler le projet : 

""" meson setup builddir && cd builddir
   meson compile """

Pour configurer une interface CAN virtuelle :

"""sudo modprobe can
sudo modprobe vcan
sudo ip link add dev vcan0 type vcan
sudo ip link set up vcan0 """

Pour démarrer le simulateur d'Instrument Cluster :

"""./icsim vcan0"""

Et enfin pour lancer les contrôles les commandes la commande est la suivante : 

"""./controls vcan0 """

Pour ouvrir une porte avec le joystick, il suffit de faire : maj + A ou maj + Y ou maj + X ou maj + B
En fonction de la lettre, une porte différente s'ouvrira.

En exécutant la commande suivante , on commence à écouter et à enregistrer tous les messages CAN reçus sur l'interface vcan0 :

""" candump -l vcan0 """  - Cela crée un fichier nommé candump.log dans le répertoire courant.

Le programme python que vous pourrez retrouver dans ScriptOuverturePorte a pour objectif d'analyser les logs CAN capturés, afin d'identifier la commande exacte qui permet d'ouvrir une porte. Nous allons pouvoir par ce moyen hacker la voiture et ainsi compromettre le système. 
Le programme divise les logs en plusieurs parties et teste chaque partie pour voir si elle contient la commande correcte. 
Si une partie permet d'ouvrir la porte, le programme continue de diviser cette partie jusqu'à trouver la ligne exacte.

Creer un fichier .py, qui va contenir le code de ScriptOuverturePorte : 

""" nano ScriptOuverturePorte.py """

Puis le lancer : """ python3 ScriptOuverturePorte.py """

Il suffira alors de répondre aux questions posées dans le terminal pour pouvoir trouver la bonne ligne de commande.
Attention : il est plus simple de refermer la porte si jamais elle s'ouvre avant de répondre à la question !!!

Si jamais il vous faut plus d'information, voici une petite description des fonctions utilisées:

Modification du nom des fichiers Logs :
-> Le programme cherche un fichier log commençant par candump-2024 et le renomme automatiquement en candump.log juste pour faciliter le traitement. 
   Cette fonction est seulement pour se faciliter la vie

Division du fichier Log :
-> Le fichier est divisé en deux parties égales à chaque itération. Si une partie contient la commande qui ouvre la porte, elle est à nouveau divisée pour affiner la recherche jusqu'à trouver la ligne exacte.
   Au fur et à mesure les lignes du fichier sont comptées pour pouvoir s'arrêter lorsqu'il en reste qu'une.

Rejouer les lignes avec canplayer :
-> Chaque partie du fichier est testée à l'aide de la commande canplayer. En d'autres termes, les commandes sont relancées. Par la suite le programme demande 
à l'utilisateur si la porte s'est ouverte après chaque test.

Écrasement des fichiers temporaires :
-> Le fichier temporaire contient les lignes de commande.Il est écrasé à chaque test pour y mettre la partie à conserver et donc dans laquelle on recherche la bonne ligne d'ouverture de la porte.
Cela sert à ne pas conserver de multiples fichiers inutiles.

Enregistrement de la bonne ligne : 
-> Une fois la ligne exacte trouvée, elle est sauvegardée dans un fichier candump_resultat_final.log.

![image](https://github.com/user-attachments/assets/4cfe91da-bbbd-4c03-9611-c317ce60e5a5)

# Instrument Cluster Simulator

L'Instrument Cluster Simulator est un outil qui simule un tableau de bord pour les véhicules utilisant le protocole SocketCAN. Cela permet de tester des fonctionnalités de véhicules sans avoir besoin d'un véhicule physique.

Le devoir suivant porte donc sur l'utilisation de ce simulateur automobile dont le GitHub est le suivant : [ICSim](https://github.com/zombieCraig/ICSim)

## Avant TOUT

Pour compiler le projet, vous aurez besoin des bibliothèques suivantes :

- **SDL2** : Une bibliothèque pour la création d'applications multimédia.
- **SDL2_Image** : Une extension pour gérer les images.
- **can-utils** : Outils pour interagir avec les interfaces CAN.

Utilisez la commande suivante pour installer ces bibliothèques :

```bash
sudo apt-get install libsdl2-dev libsdl2-image-dev can-utils

# Compilation du Projet

Pour compiler le projet, exécutez les commandes suivantes :

```bash
meson setup builddir && cd builddir
meson compile
