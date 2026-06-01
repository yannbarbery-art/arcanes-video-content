# Idées futures — backlog stratégique

> Idées capturées en cours de session, à NE PAS implémenter maintenant.
> Revenir ici quand le pilot Le Colosse est publié et qu'on a 10-15 
> contenus produits manuellement avec retour d'audience.

## Système d'automatisation de production de contenu social

**Date capture :** 2026-06-01
**Origine :** Session Claude Code, après upload Higgsfield pilot EP01

### Objectif
Système qui produit automatiquement (briefs + drafts) du contenu 
qualitatif pour les réseaux Arcanes (TikTok, Reels, Instagram carrousels, 
LinkedIn posts), nourri par la data Arcanes (Supabase), avec validation 
humaine sur les décisions créatives uniquement.

### Architecture en 4 niveaux

**Niveau 1 — Brief automatisé depuis data Arcanes**
- Cron n8n quotidien qui scrute Supabase pour repérer chiffres saillants
  (variations rendement par commune, anomalies, top performers)
- Génère via Claude API un brief par chiffre, avec 3 angles : snippet 
  TikTok 8s, carrousel Instagram 5 slides, post LinkedIn long
- Dépose dans snippets/inbox/ ou ailleurs dans le repo
- Yann valide 1 brief/jour (5 min), le passe en production

**Niveau 2 — Production assistée par format**
- Claude Code prend le relais une fois le brief validé
- Carrousel Instagram : 5 slides générées (titres + corps) + export images 
  via Pillow avec template brand
- Reel court : shotlist + prompts Higgsfield (validation Yann + montage 
  manuel)
- Post LinkedIn : texte long + ton à valider + hashtags Belgique B2B
- Choropleth animée : script Python qui produit SVG → MP4
- Chaque format = template + SKILL.md spécifique

**Niveau 3 — Pipeline distribution**
- n8n pousse vers plateformes (Buffer, Hootsuite, ou APIs directes 
  Meta/LinkedIn/TikTok)
- 100% automatisé sur cette dernière étape uniquement

**Niveau 4 — Boucle d'apprentissage**
- Tracking performances (vues, engagements, scroll-through)
- Table Supabase qui informe Claude Code des formats/sujets qui performent
- Bias automatique des briefs futurs vers ce qui marche
- Suppose niveaux 1-3 opérationnels d'abord

### Effort estimé
- Niveau 1 : 2-3 jours
- Niveau 2 : 2-4 semaines itératif (carrousel d'abord, reels en dernier)
- Niveau 3 : 1 semaine (n8n excelle à ça)
- Niveau 4 : 6-12 mois d'usage réel avant data exploitable

### Prérequis avant d'attaquer
- Pilot Le Colosse publié + 10-15 contenus produits manuellement
- Retour d'audience exploitable
- Templates de format validés sur 3-5 contenus chacun (sinon on automatise 
  des erreurs)

### Risques identifiés
- Industrialiser avant d'avoir trouvé la voix : on produit beaucoup de 
  contenu interchangeable, sans signature Arcanes
- Délégation excessive de la décision éditoriale : perte du point de vue 
  unique qui fait Arcanes
- Dépendance technique multi-systèmes (n8n + Claude Code + Supabase + 
  Higgsfield + APIs publication) : un point de friction peut bloquer tout
