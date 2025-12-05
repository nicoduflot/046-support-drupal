# Thèmes de base

Il est possible de télécharger de d'installer de nouveaux thème, en revanche, la customisation de base d'un thème dépend entièrement de comment est fait le thème

## Thème livré avec Drupal 11 : Olivero

Olivero permet des modifications simples
* Couleur générale (lien, entête, couleur "call-to-action")
* Logo du site
    * Si le logo est en SVG, il faut auparavent installer une extension qui permet le svg (svg image) et une extension qui va "assainnir" le svg (svg sanitizer)
    * il faut ensuite indiquer à drupal que le svg est autorisé dans les type de fichier de la médiathèque
        * Accueil > Administration > Structure > Types de média > Modifier Image > Gérer les champs > Paramètres du champ Image pour Image
        * Ajouter "svg" à la liste suivante "Extensions de fichier autorisées"
    * le logo devra être mis "manuelement" dans le répertoire suivant : \<répertoire du site\>\\sites\\default\\files
    * dans les paramètres du thème :
        * décocher Image du logo > Utiliser le logo fourni par le thème
        * Mettre le nom du fichier dans : Image du logo > Chemin vers le logo personnalisé
* favicône du site
    * même répertoire que pour le logo
    * dans les paramètres du thème :
        * Décocher Favicon > Utiliser la favicon fournie par le thème
        * Mettre le nom du fichier dans : Favicon > Chemin vers l'icône personnalisée

### Modifications avancées

Il est possible ensuite de customiser le CSS, mais pour cela il faut installer l'extension CSS Editor, qui ajoutera une case à cocher dans les paramètres du thème : 
* Custom CSS > Enable or disable custom CSS:

Une fois que l'extension est utilisée, un encart CSS apparaît et il est possible d'avoir une vue des modifications en direct en cochant la case :
* Custom CSS > Enable auto preview

Parfois il faudra enregistrer les changements pour recharger et voir certaines modifications faîtes dans le Custom CSS

#### Modifications possible avec Custom CSS

#### Ajouter ses polices de caractère

Il suffit de créer un répertoire dans ```<répertoire du site>\sites\default\files```, nommé par exemple "fonts", à l'intérieur y mettre les fichiers nécessaire pour écrire dans le Custom CSS un 
```css
@font-face {
    /* le nom CSS qu'on appliquera à la police dans le fichier pour l'utiliser */
    font-family: 'Starborn';
    /* ici le CSS est considéré comme chargé depuis le répertoire <répertoire du site>\sites\default\files donc pour accéder au r&pertoire des fonts on utilise un chemin relatif*/
    src: url('fonts/Starborn.eot');
    src: url('fonts/Starborn.eot') format('embedded-opentype'),
         url('fonts/Starborn.woff2') format('woff2'),
         url('fonts/Starborn.woff') format('woff'),
         url('fonts/Starborn.ttf') format('truetype'),
         url('fonts/Starborn.svg#Starborn') format('svg');
}

/* on l'utilise par exemple en surcherge de la classe du thème olivero qui désigne l'élément contenant le nom du site */

.site-branding__text{
  font-family: 'Starborn';
  text-shadow: 3px 3px black, -1px -1px black;
}
```