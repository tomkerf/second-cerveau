# Claude Code & Claude Cowork — Leçon de Boris (créateur)

**Source** : Transcription YouTube — "Leçon privée sur Claude Cowork et Claude Code"
**Interviewé** : Boris (créateur de Claude Code, co-créateur de Claude Cowork)
**Intervieweur** : Greg (Startup Ideas Podcast)
**Enregistré** : Janvier 2026

---

## Claude Cowork — C'est quoi ?

- Interface UI du Claude desktop app (onglet "Cowork"), Mac OS uniquement pour l'instant
- Sous le capot : **exactement le même agent que Claude Code** (Claude Agent SDK)
- Accès aux fichiers en opt-in (tu choisis les dossiers)
- Contrôle du navigateur Chrome via extension
- Parallélisme : plusieurs tâches en même temps
- Pas pour le code uniquement — files, emails, Slack, spreadsheets, recherche web

### Cas d'usage démontrés
- Renommer des fichiers selon les dates des reçus
- Créer un Google Sheet depuis des PDFs de reçus
- Envoyer l'email via Gmail (contrôle navigateur)
- Slack : détecter les colonnes non remplies dans un tableur et notifier les devs

---

## Les 13 tips de Boris pour Claude Code

### Tip 1 — Plusieurs tâches en parallèle
> "It's not about going deep on one task, it's doing a bunch of tasks in parallel"

Workflow : ouvre un onglet, donne une tâche, passe à l'onglet 2, donne une tâche, onglet 3... Reviens au 1 quand ils ont fini. Boris code ~50% depuis son téléphone, le reste en web/terminal.

### Tip 2 — Utilise iOS et web + terminal
Kick off des sessions depuis le phone le matin, vérifie dans la journée. Claude Code disponible partout : terminal, mobile app (iOS/Android), web, IDE, Slack, GitHub.

### Tip 3 — Opus 4.5 + Thinking pour tout
> "It's counterintuitive — even though it's bigger and slower, it uses so many fewer tokens it's often cheaper than a smaller model"

Opus 4.5 avec thinking = meilleur résultat ET moins de tokens au total = plus efficace ET moins cher que Sonnet.

### Tip 4 — CLAUDE.md est essentiel
> "Invest in your Claude.md — that's super duper important"

- Format libre (juste un fichier texte, pas de format spécial)
- L'équipe Anthropic : **un seul CLAUDE.md partagé sur le repo**, versionné sur Git
- Mise à jour collective : dès qu'on voit Claude faire une erreur → on l'ajoute au MD
- Chaque équipe maintient le sien

### Tip 5 — GitHub Action + @claude = compound engineering
Commande : `/command/install-github-action` dans Claude Code → installe l'app Claude dans le repo.

Utilisation : @claude dans une PR review → Claude pousse des corrections directement sur la branche. Ou : @claude dans une issue → Claude traite.

Cas d'usage clé : mentionner @claude pour **mettre à jour le CLAUDE.md** quand un problème revient. "Tu ne devrais jamais avoir à commenter la même chose deux fois."

### Tip 6 — Plan mode d'abord
> "Once the plan is good, the code is good"

Boris : plan mode pour presque toutes ses sessions. Itère sur le plan jusqu'à ce qu'il soit bon → switch auto-accept edits → Opus exécute sans supervision.

### Tip 13 — Donne à Claude un moyen de vérifier son output
> "If you have to paint blindfolded, it's not going to be good"

- Développeur : toujours lancer les tests ET ouvrir le navigateur (Chrome extension)
- Co-work : Claude utilise le browser pour vérifier son propre travail
- Résultat largement supérieur quand Claude peut voir et tester sa propre output

---

## La grande idée de Boris

En 2 mois (avant janvier 2026) : **100% de son code écrit par Claude Code**, zéro ligne à la main. Il livre 200-300 PRs/mois. Ce n'est pas de la SF — c'est déjà sa réalité.

Workflow actuel : "je tends mes Claudes comme un jardinier" — il surveille, débloque, répond aux questions. Plus de code directement.

> "Now is the age of multi-Clauding — being more of a generalist and tending to your Claudes"

---

## Sécurité de Cowork

- VM dédiée sous le capot (isolation des actions)
- Deletion protection (prompt avant suppression)
- Protections prompt injection (en cours d'amélioration)
- Modèle aligné (mechanistic interpretability, alignment research Anthropic)

---

## Pour aller plus loin

Skills (dans Claude Code/Cowork) = workflows réutilisables. Si Cowork n'est pas bon pour un logiciel spécifique → crée un skill. Plus tu as de skills, plus il performe.

---

## Pertinence pour Tom

- Valide le setup actuel : CLAUDE.md déjà en place, plan mode déjà utilisé ✅
- **Action** : envisager le GitHub action @claude sur les repos actifs (PMC V2, labocea-app)
- **Action** : tester Claude Cowork pour des tâches non-dev (rapports, organisation fichiers terrain)
- Workflow parallèle applicable : lancer plusieurs Claude sur PMC V2 features en parallèle
- Tip Opus 4.5 : vérifier si le switch vers Opus 4.5 + thinking réduit le coût total (~160€/mois API)
