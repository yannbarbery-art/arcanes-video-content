# SKILL — Travailler dans ce repo

> Mode d'emploi pour Claude Code. À lire avant toute tâche de production.
> Les règles non négociables sont rappelées dans `CLAUDE.md` (chargé
> automatiquement). Ce fichier détaille le « comment ».

## Mission du repo

Produire le contenu vidéo social d'Arcanes (proptech belge, marque Arcanes /
Digital Arcanes SRL) : séries épisodiques, snippets réactifs, choropleths
animées. Tout est bilingue FR/NL et conforme FSMA.

## Les 5 étapes du pipeline

1. **Idéation** — un brief part d'une donnée Arcanes (Statbel, SPF Finances,
   CommunePages...). Voir `templates/data-brief.md`.
2. **Scripting** — script FR puis NL. Aucun script n'est terminé sans sa
   version NL, les deux vérifiées contre `docs/fsma-lexique.md`.
3. **Génération** — Higgsfield MCP (Soul, Cinema Studio, Veo selon le shot).
   Voir `docs/higgsfield.md`.
4. **Post-prod** — assemblage, sous-titres, sound design (outils externes).
5. **Publication** — TikTok, Reels, LinkedIn (manuel). Voir `docs/platforms.md`.

Le champ `statut` de `meta.yml` suit ces étapes :
`idee -> brief -> script -> prompts -> genere -> post-prod -> publie`.

## Types de contenu

| Type | Dossier | Démarré depuis |
|---|---|---|
| Épisode de série | `series/<serie>/episodes/EPNN-slug/` | `templates/episode/` |
| Snippet réactif | `snippets/AAAA-MM-JJ-slug/` | `templates/snippet/` |
| Choropleth / map | `maps/AAAA-MM-slug/` | voir `maps/README.md` |
| Nouvelle série | `series/<slug>/` | `templates/series.md` |

## Démarrer un épisode

1. Identifier la série (ex. `le-colosse`) et le numéro d'épisode.
2. Copier `templates/episode/` vers `series/<serie>/episodes/EPNN-slug/`.
3. Remplir `brief.md` avec les données fournies par Yann — **ne jamais
   inventer de chiffre ni de source**.
4. Renseigner `meta.yml` (statut `brief`).
5. Rédiger `script.fr.md`, puis `script.nl.md`.
6. Vérifier les deux scripts contre `docs/fsma-lexique.md` -> statut `script`.
7. Produire `shotlist.md` et un `prompts/shot-NN.md` par shot -> statut `prompts`.

## Démarrer un snippet

Idem en plus léger : copier `templates/snippet/`, dossier daté
`AAAA-MM-JJ-slug/`. Les snippets sont réactifs (data ou news du jour).

## Démarrer une map

Voir `maps/README.md`. Une map = données + config + script de génération.

## Le character Soul

La série « Le Colosse » utilise Soul, un character entraîné Higgsfield.
Pour toute génération impliquant Soul, partir de
`series/le-colosse/characters/soul.md` (look, prompts de référence, `refs/`).
La cohérence du character d'un épisode à l'autre est une priorité.

## Règles non négociables (rappel)

- **FSMA :** jamais de conseil. Vocabulaire : `docs/fsma-lexique.md`.
- **Bilingue :** FR + NL, à parité, toujours.
- **Données :** tout chiffre est sourcé et daté dans le `brief.md`.
- **Ton :** Tier 1 SaaS, data-driven — `docs/brand.md`.

## Quoi committer

- **Oui :** briefs, scripts, prompts, shotlists, configs, méta, `series/**/refs/`.
- **Non :** `output/`, `assets-raw/`, médias lourds, secrets — voir `.gitignore`.
- Ne jamais push sans demande explicite de Yann.

## Checklist avant le statut `publie`

- [ ] Lexique FSMA vérifié — FR **et** NL.
- [ ] Scripts bilingues complets.
- [ ] Tout chiffre est sourcé et daté dans le brief.
- [ ] `publish.md` rempli (captions + hashtags FR/NL).
- [ ] Specs plateforme respectées (`docs/platforms.md`).
- [ ] `meta.yml` à jour.
