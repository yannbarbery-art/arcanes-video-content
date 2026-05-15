# Maps — choropleths animées

> Cartes choroplèthes animées (ex. rendement locatif par commune) pour
> Instagram et autres plateformes.

## Structure d'une map

`maps/AAAA-MM-slug/` contient :

- `brief.md` — sujet, données, angle
- `config.yml` — données commune -> valeur, palette, légende FR/NL
- `data.csv` — jeu de données d'entrée (si léger ; sinon `assets-raw/`)
- `publish.md` — captions FR/NL
- `meta.yml` — métadonnées
- `output/` — rendu animé (non versionné)

## Outils de génération

[À compléter par Yann — outil / bibliothèque retenu pour générer les
choropleths animées. Les scripts vont dans `maps/scripts/`.]

## Étapes

[À compléter par Yann après la première map]

## Garde-fous FSMA

- Une carte de rendement présente une **estimation** par commune, datée et
  sourcée.
- La légende précise la source et la période des données.
