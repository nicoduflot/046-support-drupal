# Les vues

Une vue est ce qui sert à afficher le contenu du site Drupal

Une vue consite à créer, par défaut une page, qui fait une requête sur le contenu. Il est possible d'ajouter des critères de filtrage à cette requête

Une fois que la requête est correctement faîte, il faut choisir un modèle d'affichage des données dans la vue.

## 1. Modification d'une vue existante

### La vue "Page d'accueil"

* Accueil > Administration > Structure > Vues
* Trouver la vue "Page d'accueil" dans la liste
* Cliquer sur "Modifier"

On va se concentrer uniquement sur l'affichage des résultats

La page "modification d'une vue" possède trois parties :
* La requête dans le contenu et l'affichage des données
* Les paramètres de la page (chemin, pagination, etc.)
* Les réglages avancés

Pour changer seulement l'affichage de la requête de la page d'accueil, il faut agir sur la première partie.

* Ajouter un titre à la page, attention, à chaque modification d'un élément, il faut bien vérifier en haut de la modal si c'est seulement cet affichage (ici la page) ou tous les affichage (toute les forme rendue par la vue : flux RSS, bloc, etc). Dans ce cas particulier on précise bien qu'on ne modifie que la page.
* Format : on change le format d'affichage, on choisi, par exemple, grille réactive (responsive), sur les champs (champs du contenu récupérés par la requête de la vue)
    * Nombre de colonnes max : 3
    * Largeur minimale des colonnes : 220px
    * Nombre d'éléments a afficher : 9 (sert pour la pagination)
* Champs : on sélectionne les champs pour alimenter chaque élément de la grille, ici par exemple le titre, la galerie ou le média contenu (on regroupe tous les contenus promus en page d'accueil, certains possèdent un galerie, d'autres un média contenu) et le corps
    * Pour le titre, dans les "paramètres d'affichage", on coche la case "Personnaliser le code html du **champ**" et on choisi, par exemple, H2
    * Pour la galerie, on précise qu'on n'affiche qu'un élément à partir de 0 dans l'option "Paramètre de champ multiple" afin de n'avoir qu'un média sur les X enregistrés pour le contenu
    * Pour le corps, on choisi l'option "Résumé ou coupé" pour l'option "outils de mise en forme" et on change la troncature de 600 à 300
    * Pour l'affichage de la galerie et du média contenu, "outil de mise en forme" : "vignette" et "style d'image" : "Vignette de la médiathèque (220x220)"

## 2. Création d'une vue

* Accueil > Administration > Structure > Vues > Ajouter une vue 
* Inscrire le nom de la vue
* Paramètres de la vue : permet de préconfigurer la requête des données (le contenu) qui alimentera la vue.
* Cocher créer une page
* Indiquer le titre de la page
* Le chemin de la page (équivalent à son alias d'url)
* Paramètres d'affichage de la page permet de préconfigurer l'affichage final des éléments de la requête dans la vue
* remplir les autres champs
* enregistrer

On arrive ensuite sur la configuration finale de la vue ou on pourra 
* Changer le titre de la page
* préciser le foramt d'affichage des résultats
* Préciser les champs de sortie ou la forme du contenu
* préciser la requête sur le contenu en ajoutant des filtres
* préciser la requête sur le contenu en caractérisant le tri

## 3. Création d'un bloc sur une vue existante

* Sur la page de modification d'une vue, il faut cliquer sur "Ajouter" dans la partie "Affichages" et choisir "bloc"
* Attention, si l'affichage des champs et des données est différent de la page, ne pas oublier de supplanter l'affichage et de ne l'appliquer qu'au bloc
* Gérer les champs comme pour la page
* Enregistrer
* Placer le bloc créé dans une région


## 4. Création conjointe vue et bloc

* Accueil > Administration > Structure > Vues > Ajouter une vue 
* Inscrire le nom de la vue
* Paramètres de la vue : permet de préconfigurer la requête des données (le contenu) qui alimentera la vue.
* Cocher "créer une page"
    * Voir création d'une vue (#2)
* Cocher "Créer un bloc"
    * Préciser le titre
    * Préconfigurer l'affichage des résultats
    * Le nombre d'éléments par bloc
    * Une fois enresitrer, voir la création d'un bloc sur une vue existante (#3)