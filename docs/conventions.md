# Conventions

## Nommage des fichiers et dossiers

- **Casse :** `kebab-case`, minuscules, ASCII — pas d'accents ni d'espaces.
- **Dossiers d'épisodes :** `EPNN-slug/` — ex. `EP01-rendement/`.
- **Dossiers de snippets :** `AAAA-MM-JJ-slug/` — ex. `2026-05-15-peb-bruxelles/`.
- **Dossiers de maps :** `AAAA-MM-slug/` — ex. `2026-05-rendement-wallonie/`.
- **Suffixe de langue :** `.fr.md` / `.nl.md` — ex. `script.fr.md`.
- **Prompts de shot :** `shot-NN.md` dans `prompts/` — ex. `shot-01.md`.

## Anatomie d'un dossier de contenu

### Épisode (`series/<serie>/episodes/EPNN-slug/`)

| Fichier | Versionné | Rôle |
|---|---|---|
| `brief.md` | oui | Brief créatif + données sources |
| `script.fr.md` / `script.nl.md` | oui | Scripts bilingues |
| `shotlist.md` | oui | Découpage en shots |
| `prompts/shot-NN.md` | oui | Prompt de génération par shot |
| `publish.md` | oui | Captions + hashtags FR/NL |
| `meta.yml` | oui | Métadonnées et statut |
| `assets-raw/` | non | Sources brutes, downloads |
| `output/` | non | Renders et exports |

### Snippet (`snippets/AAAA-MM-JJ-slug/`)

Même logique, sans `shotlist.md` obligatoire (contenu plus court).

### Map (`maps/AAAA-MM-slug/`)

`brief.md`, `config.yml`, `data.csv` (si léger), `publish.md`, `meta.yml`,
`output/`.

## Schéma de `meta.yml`

| Champ | Type | Valeurs |
|---|---|---|
| `id` | string | `EPNN-slug` ou `AAAA-MM-JJ-slug` |
| `serie` | string | slug de série, ou `—` pour un snippet |
| `titre_fr` / `titre_nl` | string | titres bilingues |
| `format.ratio` | string | `9:16`, `1:1`... |
| `format.duree_s` | number | durée en secondes |
| `statut` | enum | `idee` -> `brief` -> `script` -> `prompts` -> `genere` -> `post-prod` -> `publie` |
| `plateformes` | list | `tiktok`, `reels`, `linkedin` |
| `sources_data` | list | sources citées |
| `date_brief` | date | `AAAA-MM-JJ` |
| `date_publication_prevue` | date | `AAAA-MM-JJ` |
| `langues` | list | `fr`, `nl` |

## Statuts du pipeline

`idee` -> `brief` -> `script` -> `prompts` -> `genere` -> `post-prod` -> `publie`

Un contenu ne passe pas à `script` tant que FR **et** NL ne sont pas vérifiés
contre `docs/fsma-lexique.md`.

## Versionné vs non versionné

- **Versionné :** scripts, prompts, briefs, configs, méta, `series/**/refs/`.
- **Non versionné :** `output/`, `assets-raw/`, médias lourds, secrets — voir
  `.gitignore`.
