# Rythmo

Atelier de doublage pour téléphone. Un seul fichier HTML, aucun serveur, rien qui
sort de l'appareil.

Tu charges un extrait vidéo, tu découpes les répliques, et tu les rejoues en boucle
en enregistrant ta voix par-dessus. Sous l'image défile une **bande rythmo** : le
texte passe devant une ligne de lecture fixe, et les caractères sont espacés
proportionnellement à la durée de la réplique. L'espacement, c'est le débit — une
syllabe passe la ligne, tu la dis.

Après chaque prise, la courbe de ta voix s'affiche sous celle de la VO et l'écart
est chiffré en millisecondes.

## Utilisation

1. **Charger une scène** — un extrait court, moins de deux minutes.
2. **Détection** — lance la lecture, garde le doigt appuyé sur le gros bouton du
   premier au dernier son de chaque réplique. Relâche : une case apparaît sur la
   bande. Tape le texte ensuite dans la liste. Ou importe un `.srt`.
3. **Doublage** — sélectionne une réplique, lance la boucle. Pré-roll, trois bips,
   le quatrième est muet et c'est là que tu attaques.
4. **Relis la courbe**, corrige, recommence.

Exporte la bande en JSON pour la retrouver plus tard, et la prise en fichier audio.

## Trois choses à savoir avant

**Casque obligatoire.** Sur iOS, l'ouverture du micro fait basculer la session audio :
le son de la scène part dans l'écouteur et baisse. Et sans casque, la VO repisse dans
ta prise.

**Il faut du https.** L'accès au micro exige un contexte sécurisé. Ouvert en `file://`
depuis le téléphone, tout marche sauf l'enregistrement. Héberge la page (voir plus bas)
ou, pour tester sur ordinateur, sers-la en local — `localhost` compte comme sécurisé :

```bash
python3 -m http.server 8000   # puis http://localhost:8000
```

**Extraits courts.** L'audio est décodé entièrement en mémoire pour tracer les courbes.

## Déploiement

### GitHub Pages

Pousse le dépôt, puis *Settings → Pages → Source: Deploy from a branch*, branche
`main`, dossier `/ (root)`. La page est en ligne en https une minute plus tard.
Sur téléphone, « Ajouter à l'écran d'accueil » pour l'avoir en plein écran.

### Firebase Hosting

```json
{ "hosting": { "public": ".", "ignore": ["firebase.json", "**/.*", "**/node_modules/**"] } }
```

```bash
firebase deploy --only hosting
```

## Format de la bande

```json
{
  "pps": 110,
  "cues": [
    { "start": 12.40, "end": 14.15, "text": "Vous voulez rire ou quoi" }
  ]
}
```

Temps en secondes. `pps` est le zoom au moment de l'export, il est informatif.

## Contribuer / modifier

Tout est dans `index.html`. Pas de build, pas de dépendances : tu ouvres, tu édites,
tu recharges.

Le contexte complet du projet — architecture, invariants, pièges iOS et Android
déjà rencontrés — est dans [`.github/copilot-instructions.md`](.github/copilot-instructions.md).
Copilot le lit automatiquement ; `AGENTS.md` et `CLAUDE.md` y renvoient. Si tu
changes une règle du projet, c'est ce fichier qu'il faut mettre à jour, pas les
trois.

## Statut

Utilisable. Pas de persistance pour l'instant : la bande et les prises disparaissent
au rechargement, pense à exporter. Voir les limites connues dans le fichier de contexte.
