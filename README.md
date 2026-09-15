# Ovalie — Classements rugby

Application web de saisie de scores et de calcul de classements rugby, paramétrable par compétition. Les scores sont encodés à la main, le classement est recalculé à la volée.

PWA installable, fonctionne hors ligne, aucune donnée ne quitte l'appareil.

## Fonctionnement

Chaque compétition a son propre barème : points de victoire, de nul et de défaite, bonus offensif et bonus défensif.

**Bonus offensif**, deux modes :
- *absolu* — toute équipe atteignant le seuil d'essais, même battue (style Six Nations)
- *relatif* — le vainqueur seulement, s'il marque X essais de plus que l'adversaire (style Top 14)

**Bonus défensif** : réservé au perdant, dans une marge de points réglable.

**Départage** : points, puis différence de points, puis essais marqués, puis points marqués, puis ordre alphabétique.

Préréglages fournis : Six Nations (4/2/0, bonus offensif absolu à 4 essais, défensif à 7 points) et Top 14 (4/2/0, bonus offensif relatif à 3 essais, défensif à 5 points).

**Groupes** : un champ libre par équipe permet des sous-classements (hémisphères, poules) sans dédoubler le tableau. Les filtres n'apparaissent que si au moins une équipe est affectée à un groupe.

## Structure

```
index.html            application complète (HTML, CSS et JS dans un seul fichier)
manifest.json
service-worker.js
icon.png              apple-touch-icon 180×180 — doit rester à la racine
icons/                icônes du manifest (192 et 512 utilisées)
```

## Données

Stockées dans le `localStorage` du navigateur sous la clé `ovalie_data_v1`. Export et import JSON de toutes les compétitions d'un coup, depuis l'onglet Compétition.

Deux conséquences à garder en tête :

- Changer de domaine d'hébergement = repartir de zéro. Exporter avant, importer après.
- Sur iOS, le stockage de la PWA installée est isolé de celui de l'onglet Safari. Exporter depuis le contexte réellement utilisé.

## Modifier l'application

Tout se passe dans `index.html`. Après chaque modification, incrémenter `CACHE` dans `service-worker.js` (`ovalie-v3`, `ovalie-v4`…), sans quoi les appareils déjà installés continueront à servir l'ancienne version depuis leur cache.

## Historique

- `v3` — correction de l'en-tête « Équipe » du classement (fond effacé par un `background:inherit` hérité de la règle des cellules) et `z-index` des colonnes collantes ; migration de Netlify vers GitHub Pages
- `v2` — groupes d'équipes et filtres de sous-classement
- `v1` — version initiale

## Typographie

Fraunces (titres), Atkinson Hyperlegible (texte), JetBrains Mono (chiffres).
Palette : vert terrain `#1E4633`, cuir `#8B5E3C`, papier `#F6F1E7`.
