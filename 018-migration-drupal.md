# Migration d'un drupal

Il existe des outils extension qui permettraient la migration d'un site Drupal en local (ou d'un hébergeur) vers un autre hébergeur, mais ces outils ne sont pas très adaptés.

Il est possible cependant de le faire "manuellement" en suivant ses étapes :

* Sauvegarder la base de donnée du site a migrer
    * ATTENTION : dans les données enregistrées, l'adresse utilisée par le site a migrer y apparait environ 300 fois, il faut ouvrir le fichier de saugarde dans un éditeur et remplacer l'adresse actuelle par l'adresse de migration :
        * ancienne adresse : http://www.monsite.local => htt://www.monsite.com
* Sur la base de données du nouvel hébergeur, créer une base de données et y importer la sauvegarde modifiée
* Une fois que la BDD est correctement importée il faut transferrer TOUS les fichiers du site vers l'autre hébergeur
* Il faut renommer le fichier ```\sites\default\settings.php``` par exemple en ```\sites\default\-settings.php```
* Ce fichier de configuration n'est pas modifiable dans son contenu
* En le renommant et en créant un nouveau fichier ```\sites\default\settings.php```, il sera possible d'y copier l'intégralité du fichier renommé.
* il faut modifier le nouveau fichier ```\sites\default\settings.php```, au niveau de la variable ```$databases['default']['default']```, le nom de  la base de données, l'utilisateur ayant les droits de modification de la bdd avec le mot de passe
* Normalement une fois tout cela fait le site devrai s'ouvrir avec la nouvelle adresse

**ATTENTION** 

La migration de la BDD utilisera **TOUS** les comptes créés sur le site en local.
Si le compte principal n'utilise pas un mot de passe complexe, il y a de forts risque de tentative de hack