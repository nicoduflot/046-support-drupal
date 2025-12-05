# Nouvelles taxonomies

## Création d'une taxonomie

1. Créer le nouveau vocabulaire
2. Créer l'alias d'url du vocabulaire
3. Ajouter les termes 

Voilà l'arborescence actuelle retenue

| type de contenu       | Taxonomie(s)      |Réalisé Contenu    | Réalisé taxonomie |
|-----------------------|-------------------|-------------------|-------------------|
|Page                   |                   |                   |                   |
|Article                | Étiquettes        |    OK             |      OK           |
|Article                | Catégories        |    OK             |      OK           |
|Créateur - Créatrice   |                   |                   |                   |
|Lire                   |Support littéraire |                   |      OK           |
|Lire                   |Genre littéraire   |                   |      OK           |
|Voir                   | Support vidéo     |                   |      OK           |
|Voir                   | Genres vidéo      |                   |      OK           |
|Écouter                |Support audio      |                   |      OK           |
|Écouter                |Genre audio        |                   |      OK           |

```batch
Article (Par défaut mais il faut ajouter une taxonomie)
	Les taxonomies d'Article :
		Étiquettes (par défaut)
		Catégories
			- News

Créateur / Créatrice
    - Pas de taxonomie pour ce type de contenu
    - Il servira en champ de référence sur les contenus audio - vidéo - lecture
    
Lecture
	Les taxonomies de lecture :
	Support Littéraire
		- Roman
		- Magazine
		- Comics
		- BD
		- Manga
		- Audiobook
	Genre littéraire
		- Horreur
		- Aventure
		- Comédie
		- Essai

Voir
	Les taxonomies de Voir :
	Support vidéo
		- Film
		- Série
		- Création
	
	Genre vidéo
		- Horreur
		- Aventure
		- Streaming
		- Comédie

Écouter
	Les taxonomies d'Écouter :
	Support audio
		- Podcast
		- Chanson
	Genre audio
		- Pop
		- Rock
		- Hip Hop
		- R&B
		- Country
```

Les patterns utilisés

* Pathauto articles : ```article/[node:title]```
* Pathauto catégories : ```categorie/[term:name]```
* pathauto genre vidéo : ```genre-video/[term:name]```
* Pathauto pages : ```page/[node:title]```
* Pathauto support vidéo : ```support-video/[term:name]```
* Pathauto étiquettes : ```etiquette/[term:name]```
* Pathauto support littéraire : ```support-litteraire/[term:name]```
* Pathauto Genre littéraire : ```genre-litteraire/[term:name]```
* Pathauto Support audio : ```support-audio/[term:name]```
* Pathauto créateur / créatrice : ```createur-creatrice/[node:title]```