# Installation

* Préparer une base de données codage caratère UTFmb4_unicode_ci

* Téléchager les fichier d'installation sur le [site](https://www.drupal.org/project/drupal/releases/)

* Mettre le fichier dans le répertoire de travail
    * dans le fichier.htacess, trouver la ligne suivante : 
    ```batch
    <IfModule mod_php.c>
        php_value assert.active                   0
    </IfModule>
    ```
    Commenter la ligne ```php_value assert.active                   0```
    ```batch
    <IfModule mod_php.c>
    #   php_value assert.active                   0
    </IfModule>
    ```

* Lancer le site via un navigateur
    * Choisir anglais comme langue d'installation
    * Indiquer les informations base de données et utilisateur bases de données
    * Indiquer les informations dont l'utiisateur (admin) principal
