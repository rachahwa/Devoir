Ce programme a pour objectif d'analyser les logs CAN capturés, afin d'identifier la commande exacte qui permet d'ouvrir une porte. 
Le programme divise les logs en plusieurs parties et teste chaque partie pour voir si elle contient la commande correcte. 
Si une partie permet d'ouvrir la porte, le programme continue de diviser cette partie jusqu'à trouver la ligne exacte.

Fonctions :

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
