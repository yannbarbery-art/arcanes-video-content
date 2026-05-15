# Arcanes Video Content

Pipeline de production de contenu vidéo social pour Arcanes (Digital Arcanes SRL).
Séries épisodiques, snippets réactifs et choropleths animées — bilingue FR/NL,
conforme FSMA. Génération via Higgsfield MCP, publication TikTok / Reels / LinkedIn.

## Démarrage

Claude Code charge `CLAUDE.md` automatiquement (règles FSMA non négociables).
Pour toute tâche de production, lire d'abord `docs/SKILL.md`.

## Structure

```
docs/        Documentation : SKILL, conventions, brand, lexique FSMA, etc.
templates/   Squelettes réutilisables (épisode, snippet, brief data, série, shot)
brand/       Assets de marque (logos, typos)
series/      Séries épisodiques (le-colosse, ...)
snippets/    Contenus one-off réactifs
maps/        Choropleths animées
```

Versionné : scripts, prompts, briefs, configs. Non versionné : `output/`,
`assets-raw/`, médias lourds (voir `.gitignore`).

## Documentation

- `docs/SKILL.md` — mode d'emploi du repo
- `docs/conventions.md` — nommage et structure
- `docs/brand.md` — voix et identité
- `docs/fsma-lexique.md` — vocabulaire FSMA
- `docs/workflow-claude-code.md` — travailler avec Claude Code
