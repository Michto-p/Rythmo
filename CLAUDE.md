# Rythmo — instructions agent

Le contexte complet du projet est dans `.github/copilot-instructions.md`.
**Lis-le avant toute modification** : il contient les invariants de la bande rythmo
et les pièges audio iOS / Android qui ne se devinent pas à la lecture du code.

@.github/copilot-instructions.md

Résumé minimal, si tu ne lis rien d'autre :

- Un seul fichier `index.html`. Pas de build, pas de npm, pas de framework, pas de CDN.
- Vanilla JS, français, mobile d'abord.
- La bande défile en `transform` piloté par `video.currentTime` dans une boucle `requestAnimationFrame`.
- L'espacement des caractères d'une réplique est proportionnel à sa durée. C'est le principe du projet, pas un effet visuel.
- Ne code jamais un type MIME audio en dur : iOS renvoie `audio/mp4`, Android `audio/webm`.
