# CLAUDE.md — Arcanes Video Content

Repo de production de contenu vidéo social pour Arcanes (Digital Arcanes SRL).
Lire `docs/SKILL.md` avant toute tâche — ce fichier ne rappelle que les règles
non négociables.

## Règles FSMA d'or (non négociable)

Arcanes est une proptech soumise à la réglementation FSMA. Ne jamais formuler
de conseil financier.

**Vocabulaire INTERDIT** (jamais, FR comme NL) :
- conseil / advies
- recommandation / aanbeveling
- opportunité / opportuniteit
- verdict / oordeel
- toute incitation : « il faut acheter », « bon plan », « placement sûr »

**Vocabulaire de REMPLACEMENT :**
- simulation / simulatie
- estimation / raming
- analyse / analyse

**Formulations INTERDITES** (incitations, promesses de gain) :
- « il faut acheter », « investissez maintenant », « profitez-en », « ne ratez pas »
- « rendement garanti », « X % assuré », « placement sûr »
- Toute projection présentée comme une certitude (toujours « scénario », jamais
  « ce qui va arriver »)

Équivalents NL interdits :
- « je moet kopen », « investeer nu », « mis dit niet », « gegarandeerd rendement »,
  « veilige belegging »

Table complète et nuances : `docs/fsma-lexique.md`.

## Bilingue FR/NL — systématique

Tout contenu publié existe en français ET en néerlandais. Un script n'est jamais
« terminé » tant que `.fr.md` et `.nl.md` ne sont pas tous deux complets et
vérifiés contre le lexique FSMA dans les deux langues.

## Ton brand

Tier 1 SaaS : sobre, data-driven, précis. Jamais creator-economy (pas de hype,
pas d'emojis en rafale, pas de « game changer »). On montre des chiffres
sourcés, pas des promesses. Détail : `docs/brand.md`.

## Avant de committer

Vérifier : lexique FSMA OK (FR+NL) · scripts bilingues complets · sources data
citées dans le brief · aucun secret ni média lourd (voir `.gitignore`).
Ne jamais push sans demande explicite.
