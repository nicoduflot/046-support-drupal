# Les thèmes enfants

## Créer un thème enfant

Créer un thème enfant permet de s'appuyer sur l'intelligence d'un thème stable et maintenu, et on a la possibilité de modifier les éléments de ce thème.

Pour créer une thème enfant, il suffit d'ajouter un dossier dans le répertoire *\themes*

Les thèmes sont en fait des modules, mais leur fonction est un peu différente

### Création des fichiers nécessaires

De base, deux fichiers sont nécessaire : 

myTheme.info.yml
myTheme.libraries.yml

```
themes
    |_myTheme/
        |_myTheme.info.yml
        |_myTheme.libraries.yml

```

#### Fichier .info.yml

C'est le fichier qui permet de définir, entre autre :
* Le nom du thème / module
* Le type de module : theme
* La description du thème
* la / les versions de base de drupal avec lesquelle le theme est compatible
* le thème parent sur lequel notre thème s'appuie
* Le logo du thème
* les librairies (les fonctionnalité externe comme un datepicker js, jquery, chartjs, etc)
* Les régions du thème (les parties principales du thème comme header, hero, content, sidebar, etc.)

```myTheme.info.yml```

```yml
name: myTheme
type: theme
description: Thème enfant de starterkit_theme
core_version_requirement: ^10 || ^11
base theme: starterkit_theme
logo: images/nicolas-duflot-avatar.svg
libraries:
    - myTheme/general
regions:
    header: 'Header'
    primary_menu: 'Primary menu'
    secondary_menu: 'Secondary menu'
    highlighted: 'Highlighted'
    custom_region: 'Custom region'
    help: 'Help'
    breadcrumb: 'Breadcrumb'
    content: 'Content'
    sidebar_first: 'Left sidebar'
    sidebar_second: 'Right sidebar'
    footer: 'Footer'
```

#### Fichier .libraries.yml

les lirairies correspondent :
* Aux fichiers CSS du thème
* Aux fichiers js du thème
* Aux polices du thème
* Aux widgets js / css comme chartJs
* etc

```myTheme.libraries.yml```

```yml
general: 
    header: true
    css:
        theme:
            # Il est possible de préciser à quel type d'affichage, screen ou print par exemple, sera utilisé la bibliothèque nommé
            css/bootstrap.css: {media: screen}
            css/bootstrap-icon.css: {}
            css/style.css: {media: screen}
            css/print.css: {media: print}
    js:
        js/bootstrap.bundle.js: {}
        js/scripts.js: {}
```
### Activer le débuggage de thème dans drupal

Il faut activer le débug de twigg et arrêter les caches d'affichage afin de voir dans l'inspecteur d'éléments les fichiers twig utilisés dans le thème, connaître le nom des fichiers a créer pour surcharger des parties ciblées du thème et connaîte l'arborescences des fichiers twig dans le thème

```
html.html.twig (<html>)
|   |_page.html.twig (div class layout-container)
|   |   |_region.html.twig (class region region header)
|   |   |   |_block.html.twig (id block-mytheme-page-title)
|   |   |   |   |_page-title.html.twig 
|   |   |   |_block.html.twig (id block-mytheme-syndicate)
|   |   |   |   |_feed-icon.html.twig
|   |   |   |_block--system-branding-block.html.twig (id block-mytheme-site-branding)
|   |   |
|   |   |_(etc)
|   |   |
|   |   |
|   |   |
|   |   |_region.html.twig (class region region-help)
|   |   |   |_ (etc)
|   |
|   |   
|

```

* Accueil > Administration > Configuration > Développement >
**Paramètres de développement**
* Cocher toutes les cases

### Surcharger les fichiers de thème

Les thèmes dans drupal sont gérés par le moteur de thème twig

Un thème enfant s'appuie sur tous les fichiers twig du thème parent, quand il est nécessaire de modifier l'apparence d'un des éléments, il faut reproduire dans le thème enfant l'arborescence des fichiers twig du thème parent et reprendre soit le fichier exact(dans le cas d'une modification générique) soit créer un fichier twig avec le nom suggéré par le débug qui s'affiche en commentaire html dans le code de la page.

#### Les fichiers CSS

Si vous faîte des modifications dans les fichiers CSS, il ne faut pas oublier de vider le cache CSS et Javascript, sinon les modification apportées ne se manifesteront pas.

``` html
<!-- THEME DEBUG -->
<!-- THEME HOOK: 'page' -->
<!-- FILE NAME SUGGESTIONS:
   ▪️ page--front.html.twig
   ▪️ page--node.html.twig
   ✅ page.html.twig
-->
<!-- 💡 BEGIN CUSTOM TEMPLATE OUTPUT from 'themes/myTheme/templates/layout/page.html.twig' -->
```

*page.html.twig* est noté comme étant le fichier utilisé, les nom de fichier possible pour une surcharge particulière sont donc 
* page--front.html.twig
* page--node.html.twig

Comme bootstrap a été intégré dans l'entête, on va s'en servir pour créer le fichier comme si on l'utilisait sur une page normale, mais cela nécessite de parfois découper les parties html dans plusieurs fichiers twig, et dans certains cas, comme pour adapter la navbar de bootstrap, bien comprendre et réinterprêter les macros de twig qui utilisent les données fournies par drupal afin de calibrer les boucles de création d'élément de menu et de sous-menu aux classes et besoin de bootstrap pour que la navbar se comporte correctement.

Quand on surcharge un élément twig par un fichier de notre thème, il ne faut pas oublier de dire à twig de recontruire le registre du thème, sinon les fichiers ne seront pas surchargés tout de suite, ou seulement après un flush de tous les caches (ce qui prends du temps et est un poil agaçant)

#### intégration de la navbar de bootstrap sur starter_kit

##### region--primary-menu.html.twig

On crée une copie du fichier menu.html.twig, on la renomme :

*region--primary-menu.html.twig*
```twig
{#
/**
 * @file
 * Theme override to display a region.
 *
 * Available variables:
 * - content: The content for this region, typically blocks.
 * - attributes: HTML attributes for the region <div>.
 * - region: The name of the region variable as defined in the theme's
 *   .info.yml file.
 *
 * @see template_preprocess_region()
 */
#}
{%
  set classes = [
    'region',
    'region-' ~ region|clean_class,
  ]
%}
{% if content %}
	<div{{attributes.addClass(classes)}}>
		<!-- Intégration de la première partie de l'élément de navigation de bootstrap -->
		<nav class="navbar navbar-expand-lg bg-dark text-white" data-bs-theme="dark">
			<div class="container">
				<a class="navbar-brand" href="#">Navbar</a>
				<button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
					<span class="navbar-toggler-icon"></span>
				</button>
				<div class="collapse navbar-collapse" id="navbarSupportedContent">
					{{ content }}
				</div>
			</div>
		</nav>
	</div>
{% endif %}

```

Ensuite on fait une copie de menu.html.twig qu'on renomme 
*menu--main.html.twig*
```twig
{#
/**
 * @file
 * Theme override to display a menu.
 *
 * Available variables:
 * - menu_name: The machine name of the menu.
 * - items: A nested list of menu items. Each menu item contains:
 *   - attributes: HTML attributes for the menu item.
 *   - below: The menu item child items.
 *   - title: The menu link title.
 *   - url: The menu link URL, instance of \Drupal\Core\Url
 *   - localized_options: Menu link localized options.
 *   - is_expanded: TRUE if the link has visible children within the current
 *     menu tree.
 *   - is_collapsed: TRUE if the link has children within the current menu tree
 *     that are not currently visible.
 *   - in_active_trail: TRUE if the link is in the active trail.
 */
#}
{% import _self as menus %}

{#
  We call a macro which calls itself to render the full tree.
  @see https://twig.symfony.com/doc/3.x/tags/macro.html
#}
{{ menus.menu_links(items, attributes, 0) }}
{% macro menu_links(items, attributes, menu_level) %}
  {% import _self as menus %}
	{% if items %}
		{% if menu_level == 0 %}
			<ul  class="navbar-nav me-auto mb-2 mb-lg-0">
    {% else %}
      <!-- <ul class="menu"> -->
      <ul class="dropdown-menu">
    {% endif %}
    {% for item in items %}
      {%
        set classes = [
          'nav-item',
          item.is_expanded ? 'dropdown',
        ]
      %}
      {% if menu_level == 0 %}
      <li{{item.attributes.addClass(classes)}}>
      {% else %}
      <li>
      {% endif %}
        {%
          set link_classes = [
            'nav-link',
            item.is_expanded ? 'dropdown-toggle',
          ]
        %}
        {% if menu_level == 0 %}
          {% if item.is_expanded %}
              {%
              set dropdown_attr = 'role="button" data-bs-toggle="dropdown" aria-expanded="false"'
              %}
          {% else %}
              {%
              set dropdown_attr = ''
              %}
          {% endif %}
          <a{{ attributes.addClass(link_classes)}} href="{{ item.url }}" {{ dropdown_attr|raw }}>{{ item.title }}</a>
        {% else %}
          <a class="dropdown-item" href="{{ item.url }}">{{ item.title }}</a>
        {% endif %}

        <!-- {{ link(item.title, item.url) }} -->
        {% if item.below %}
          {{ menus.menu_links(item.below, attributes, menu_level + 1) }}
        {% endif %}
      </li>
    {% endfor %}
      </ul>
  {% endif %}
{% endmacro %}

```

**ATTENTION !!!**
> S'il y a une erreur dans la syntaxe des éléments twig, des erreur dans les macro, les boucles ou autre, le site ne s'affichera plus.
> il est donc conseillé de faire les modifications au fur et à mesure
