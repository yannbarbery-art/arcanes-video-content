# Higgsfield — presets & conventions

> Configuration de génération via Higgsfield MCP.
> Notes basées sur les sessions de production effectives — à enrichir au fil
> des tests. Voir aussi `docs/workflow-claude-code.md` § « Conventions de
> fichiers générés ».

## Modèles utilisés

### Seedance 2.0 (`seedance_2_0`, provider Bytedance)

Modèle vidéo de référence pour la plupart des shots de la série Le Colosse.

- **Pourquoi ce modèle :** seul modèle de la shortlist Higgsfield qui déclare
  `role: "video"` dans `medias[]` (les autres acceptent uniquement
  `image` / `start_image` / `end_image`).
- **Paramètres clés :** `mode` (std / fast), `genre`
  (auto / action / horror / comedy / noir / drama / epic), `resolution`
  (480p / 720p / 1080p). Pas de `generate_audio` — l'audio se fournit via
  `medias[{role: "audio"}]`.
- **Aspect ratios :** auto, 21:9, 16:9, 4:3, 1:1, 3:4, 9:16.
- **Durée :** 4–15 s.
- **Coût constaté (1080p / std / 4 s) :** **36 crédits**, indépendant de la
  présence d'un `medias[]`. Le pricing dépend de durée / résolution / mode,
  pas du nombre de références.

### Marketing Studio (`marketing_studio_video`, provider Higgsfield)

Pertinent pour pubs produit / UGC / unboxing avec presets (hook_id,
setting_id). N'accepte que des médias `image` — pas de référence vidéo.
Non utilisé pour Le Colosse pour cette raison.

### Cinema Studio Video (`cinematic_studio_video`, provider Higgsfield)

Compositions cinématiques avec `slow_motion` et `sound`. Durées contraintes
à **5 ou 10 s exactement** (champ `durations`, pas `duration_range`).
Référence média image seulement.

### Kling 3.0 (`kling3_0`, provider Kling)

Multi-shot, audio sync, motion transfer. Modes std / pro / 4k. Référence
limitée à start_image / end_image — pas adapté pour incruster un média
arbitraire.

### Soul (character entraîné)

**Statut au 2026-06-01 :** pas encore entraîné. Tests effectués jusqu'ici
avec character générique (prompt-only). Voir
`series/le-colosse/characters/soul.md`.

## Conclusion : incrustation d'une référence vidéo (test 2026-06-01)

Test effectué : passer un screen recording vertical de `arcanes.be/commune/liege`
en `medias[{role: "video"}]` à Seedance 2.0, avec prompt décrivant un
personnage tenant un téléphone dont l'écran « affiche la vidéo de
référence ».

**Résultat :** Seedance fait du **content embedding stylisé**, pas une
incrustation fidèle. L'écran du téléphone est régénéré avec l'esthétique
de la référence (couleurs, ambiance) mais pas le contenu réel — les UI
labels, les chiffres, le logo Arcanes ne sont pas reproduits.

**Conséquence :** Seedance 2.0 est **INADAPTÉ** pour incruster un produit
reconnaissable (interface SaaS, page web identifiable, captures lisibles).
Si l'écran doit montrer un contenu fidèle, il faut le composer en post-prod.

## Workflow validé pour shot « téléphone à écran »

1. **Générer un asset canvas** avec Seedance : même shot, mais téléphone
   à **écran vide sombre** (prompt insistant sur « screen completely off,
   uniform deep black blank screen, no reflections, no glare, perpendicular
   to camera, screen flat, no fingers covering »).
2. **Incruster manuellement** le screen recording (ou capture) en
   post-prod, **CapCut** par défaut. L'écran sombre uniforme se kéie
   facilement et offre un canvas net pour l'incrustation.
3. Bénéfice secondaire : indépendance créative — un même asset canvas peut
   servir pour plusieurs versions linguistiques ou plusieurs produits sans
   re-génération.

### Asset canvas de référence

- **Fichier :** `output/tests/2026-06-01-hf-test-incrustation-seedance-v2-ecran-vide.mp4`
- **Job :** `182629d2-d614-49c5-a874-24063db3bbec`
- **Specs :** 1080×1920, 4 s, std, drama, sans `medias[]`.
- À réutiliser comme référence visuelle / starting point pour les futurs
  shots « character + téléphone » de la série.

## Conventions de prompt

- **Langue :** prompts en anglais (Seedance détecte `prompt_language`,
  l'anglais donne les meilleurs résultats cinematiques).
- **Structure recommandée :** type de shot → description du sujet → action →
  composition / cadrage → lumière / ambiance → style référencé → format.
- **Pour un écran de téléphone :** toujours préciser perpendicularité,
  absence de reflets, absence de doigts couvrant l'écran. Sinon le modèle
  introduit des éléments imprévus.

## Workflow MCP : étapes types

1. `models_explore` (action `recommend`) pour confirmer le bon modèle.
2. `media_upload` puis PUT vers l'URL présignée + `media_confirm` si on
   passe une référence. **Note SSL :** `curl` échoue souvent en PUT depuis
   Windows (exit 35) — fallback `Invoke-WebRequest` PowerShell vers la
   même URL.
3. `generate_video` avec `get_cost: true` pour préflight, puis sans
   `get_cost` pour soumettre.
4. `job_status` avec `sync: true` (le serveur attend jusqu'à ~25 s avant
   de répondre — réduit le nombre d'appels).
5. Téléchargement du résultat vers `output/...` selon les conventions de
   `docs/workflow-claude-code.md`.

## Choix du modèle par type de shot

| Type de shot | Modèle | Raison |
|---|---|---|
| Character action / Old Spice / talking head | `seedance_2_0` (std, drama) | Qualité cinematique, contrôle character via prompt |
| Shot avec téléphone à écran composable | `seedance_2_0` + post-prod CapCut | Voir workflow ci-dessus |
| Compositions cinématiques pures, sans référence | `cinematic_studio_video` | Bonne option si durée 5 ou 10 s OK |
| Pub produit avec presets UGC | `marketing_studio_video` | À tester quand on aura un cas produit pur |
