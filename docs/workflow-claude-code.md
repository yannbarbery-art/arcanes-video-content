# Travailler avec Claude Code sur ce repo

> Comment Yann collabore avec Claude Code sur Arcanes Video Content.
> Prompts types à copier-coller en début de session.

## Avant de démarrer

En début de session, Claude lit `CLAUDE.md` automatiquement. Pour une tâche
de production, lui demander d'abord : « Lis `docs/SKILL.md` avant de commencer. »

## Prompts types (à copier-coller)

### Démarrer un épisode

```
Démarre l'épisode EP02 de Le Colosse sur le PEB. Copie templates/episode/
dans series/le-colosse/episodes/EP02-peb/, puis remplis brief.md à partir
de ces données : [coller chiffres + sources]. Statut : brief.
```

### Scripter en FR/NL

```
Rédige le script FR de EP02-peb à partir du brief. Durée cible 40 s.
Puis traduis-le en NL. Vérifie les deux contre docs/fsma-lexique.md.
```

### Générer un shotlist

```
À partir de series/le-colosse/episodes/EP02-peb/script.fr.md, génère
shotlist.md (découpage en shots) et un fichier prompts/shot-NN.md par shot.
```

### Valider un script vis-à-vis du lexique FSMA

```
Relis script.fr.md et script.nl.md de EP02-peb. Liste tout terme proscrit
par docs/fsma-lexique.md et propose un remplacement conforme.
```

### Créer un snippet réactif

```
Crée un snippet pour aujourd'hui : [sujet / chiffre du jour + source].
Copie templates/snippet/ dans snippets/AAAA-MM-JJ-slug/ et remplis le brief.
```

### Committer

```
Fais le point sur les fichiers modifiés, vérifie qu'aucun secret ni média
lourd n'est ajouté, puis commit avec un message clair. Ne push pas.
```

## Conventions de fichiers générés

Tout média produit par un outil de génération (image, vidéo, audio) est écrit
dans le repo, à un emplacement déterminé par sa nature. Jamais ailleurs.

| Nature | Destination |
| --- | --- |
| Test exploratoire | `output/tests/AAAA-MM-JJ-slug.{ext}` |
| Génération d'épisode | `series/<serie>/episodes/EPNN-slug/output/` |
| Génération de snippet | `snippets/AAAA-MM-JJ-slug/output/` |

Règles strictes :

- **Jamais** dans `/tmp/`, `$env:TEMP`, ni aucun chemin système. Un fichier
  hors du repo est un fichier perdu.
- En cas d'échec de `curl` (ex. erreur SSL en sandbox), basculer sur
  `Invoke-WebRequest` PowerShell — mais **vers la même destination cible**,
  jamais vers un répertoire temporaire système.
- Le `slug` reprend le sujet de façon lisible (`bxl-art-nouveau`,
  `peb-shot-03`), en minuscules, mots séparés par des tirets.
- Vérifier que les médias lourds restent hors commit (voir `.gitignore`).

## Bonnes pratiques

- Toujours donner à Claude les **chiffres ET leurs sources** : il ne doit
  pas inventer de données.
- Demander la version NL systématiquement — un contenu sans NL n'est pas terminé.
- Faire relire chaque script contre le lexique FSMA avant le statut `script`.
- Claude ne publie pas et ne push pas sans demande explicite.
