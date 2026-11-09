# SynaClock — version de secours statique

Cette version est faite pour être publiée gratuitement avec **GitHub Pages**. Elle ne contient que la page d’affichage, les images et un fichier de données à modifier. Il n’y a pas de page admin.

## Ce que cette version fait

- Affiche l’heure, la date civile et la date hébraïque, calculées dans le navigateur.
- Affiche une affiche principale, le programme, trois halakhot bilingues, les zmanim et un carrousel d’images.
- Les affiches du carrousel apparaissent sans titre superposé, sur le même fond que la page principale, avec une barre de progression dorée. La page principale reste affichée 10 secondes entre deux affiches.
- Lit le contenu dans `content.json` et les images dans le dossier `images/`.
- Ne contacte ni Firebase, ni Vercel, ni Cloudinary. Les horaires et affiches ne se mettent pas à jour seuls.

Les changements habituels se font dans `content.json` : **pas besoin de modifier le HTML**. Il faut modifier `index.html` seulement pour changer le design ou le fonctionnement.

## Publier sur GitHub Pages

1. Crée un nouveau dépôt GitHub **public**.
2. Téléverse le contenu de ce dossier à la racine du dépôt. À la racine, tu dois voir `index.html`, `content.json`, `cfjt-logo.png`, `cfjt-background.jpg` et `images/`.
3. Dans le dépôt, ouvre **Settings → Pages**.
4. Dans **Build and deployment**, choisis **Deploy from a branch**, puis la branche `main` et le dossier `/ (root)`. Clique sur **Save**.
5. Ouvre l’adresse publiée par GitHub Pages. Après chaque mise à jour, attends la fin du déploiement puis recharge la page.

> Important : ne mets pas seulement `index.html` sur GitHub. Il a besoin de `content.json`, des deux fichiers d’apparence et du dossier `images/`.

## Modifier les horaires et les événements

Ouvre `content.json` avec un éditeur de texte. Garde les guillemets, virgules et accolades. Les heures sont du texte au format `HH:MM`, par exemple `18:12`.

Dans `events`, chaque bloc correspond à une date. Modifie la date, le titre du jour, puis les lignes dans `items` :

```json
{
  "date": "2026-11-13",
  "day": "Vendredi 13 novembre",
  "items": [
    {"time": "16:20", "name": "Min'ha", "note": "Bar Yohai · Échet 'Hayil · Chir Hachirim · Arvit"}
  ]
}
```

Pour ajouter une ligne, ajoute un nouvel objet dans `items`, séparé du précédent par une virgule :

```json
{"time": "08:30", "name": "Cha'harit", "note": "Kiddouch à l'issue de l'office"}
```

Pour changer de semaine, remplace les dates et les noms des jours dans `events`. Tu peux ajouter ou supprimer un bloc de jour. Les horaires visibles sont ceux que tu écris ici : il n’y a pas de calcul automatique.

### Zmanim

Les zmanim sont rangés par date dans `zmanim`. Chaque jour contient Netz, fin du temps du Shema, fin du temps de la Tefila, Plag, Chekia et Tset. Exemple :

```json
"zmanim": [
  {
    "date": "2026-11-13",
    "day": "Vendredi 13/11",
    "items": [
      {"label": "Netz", "time": "07:56"},
      {"label": "Sof Shema · Gra", "time": "10:16"},
      {"label": "Sof Tefila · Gra", "time": "11:02"},
      {"label": "Plag HaMin'ha", "time": "16:17"},
      {"label": "Chekia", "time": "17:15"},
      {"label": "Tset · 7,083°", "time": "17:56"}
    ]
  }
]
```

Garde ce format pour chaque date. Les horaires intégrés sont calculés pour Neuilly-sur-Seine, avec les temps du Gra et le Tset à 7,083° selon Hebcal. Les résultats peuvent varier d’une ou deux minutes selon la méthode et les coordonnées utilisées.

### Halakhot bilingues

Les textes sont dans `halakhot`. Pour modifier une règle, change ses champs `titleHebrew`, `titleFrench`, `hebrew`, `french` et `source`. Les trois présentes portent sur l’allumage familial, l’heure d’allumage et le vendredi de Hanouka.

## Contenu préparé pour ce Chabbat

Le programme est daté du vendredi 13 au dimanche 15 novembre 2026. L’entrée à 16:40 et la sortie à 17:51 sont celles fournies pour le site. Hebcal publie pour Neuilly-sur-Seine 16:55 le vendredi 13 et 18:02 le samedi 14 ; vérifie quelle grille correspond à la synagogue avant publication.

## Ajouter ou remplacer une image

1. Dépose le fichier dans `images/` (par exemple `images/affiche-21-novembre.jpg`). Évite les noms avec espaces ou accents.
2. Dans `content.json`, indique son chemin relatif.

Pour l’affiche principale, remplace `posterUrl` :

```json
"posterUrl": "./images/affiche-21-novembre.jpg"
```

Pour ajouter une image au carrousel, ajoute un objet dans `slides` :

```json
{"title": "Affiche de la semaine", "url": "./images/affiche-21-novembre.jpg", "seconds": 8}
```

`seconds` indique combien de secondes l’image reste visible. Tu peux aussi remplacer le chemin d’une image déjà listée pour la mettre à jour. Les extensions du nom (`.jpg`, `.png`, `.webp`) doivent correspondre au vrai fichier.

## Mettre les changements en ligne

Après avoir modifié `content.json` ou ajouté des images, envoie les fichiers modifiés sur GitHub (bouton **Commit changes** si tu utilises le site GitHub). GitHub Pages republiera le site. Recharge ensuite la page sur l’écran.

## Vérifier avant Chabbat

- Vérifie les dates et toutes les heures dans `content.json`.
- Vérifie que l’affiche principale pointe vers un fichier qui existe bien dans `images/`.
- Vérifie que l’adresse GitHub Pages s’ouvre et que les images sont visibles.
- Fais un rechargement complet de la page après le déploiement.

Les images déjà fournies dans `images/` sont les six affiches présentes lors de la création de cette sauvegarde. Elles peuvent être retirées du carrousel en supprimant leurs objets de `slides` ; il vaut mieux ne pas supprimer les fichiers image tant qu’un lien vers eux reste dans le JSON.
