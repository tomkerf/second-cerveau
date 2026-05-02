# Claude Code — Guide débutant complet (Agents 2026)

#claude-code #formation #débutant #agents #MCP #hooks

**Source** : Transcription YouTube — "Claude Code Full Beginner Course: Learn Agents In 2026"
**Créateur** : Instructeur anonyme (Canada) — business >4 M$/an, enseigne Claude Code à 2000+ personnes

---

## À qui s'adresse ce cours

Pas besoin de background technique. Conçu pour les débutants complets jusqu'aux usages avancés. L'objectif : productivité décuplée, pas seulement du code.

---

## Plan du cours (ce qui est couvert)

### Bases
- Installation Claude Code (terminal + interface graphique)
- IDEs : les 3 plus courants
- **CLAUDE.md** = "project brain" — le fichier de contexte structuré du projet

### Développement pratique
- Construire une web app live depuis zéro
- **Plan mode** — planifier avant d'exécuter
- **Dangerously skip permissions mode** — usages et précautions

### Gestion du contexte
- Context management et "context rot"
- Prompts structurés à haut ROI

### Fonctionnalités avancées
- Tous les **slash commands**
- **Hooks** — scripts automatiques avant/après chaque tool call
- **Skills** — fichiers de skill qui transforment Claude Code en agents spécialisés
- **MCP** (Model Context Protocol) — intégration outils externes (email, comptabilité...)
- **Plugins** et marketplace
- **Chrome DevTools integration** — scraping sans API
- **Subagents** avec scoped tool access
- **Agent teams** — feature récente
- **Worktrees** — sessions parallèles sans conflits (vs Claude bot / open claude)

### Déploiement
- Scaling en production : Modal webhooks, GitHub Actions, Claude Code web

---

## Concepts clés retenus

**CLAUDE.md = project brain** : donner à Claude le contexte structuré du projet → résultats ciblés sans répétition.

**Hooks** : scripts shell déclenchés automatiquement avant/après chaque action Claude → automatiser les vérifications, logs, validations.

**Worktrees** : paralléliser des sessions Claude sur des branches isolées → évite les conflits et les context bloat.

**Context rot** : le contexte qui s'accumule dégrade les résultats → gérer activement, repartir sur de nouvelles sessions.

---

## Pertinence pour Tom

- Le setup CLAUDE.md + slash commands du vault est exactement ce que ce cours recommande
- Les hooks = piste d'automatisation à explorer (ex : hook post-rapport pour auto-commit)
- Worktrees = à explorer pour développement PMC v2 (branches feature isolées)
- MCP email = piste pour automatiser les rapports Labocea (envoi PDF automatique)

---

## Liens

- [[claude-code-cowork-boris-setup]] — 13 tips avancés Claude Code
- [[matt-pocock-ai-coding-engineers]] — smart zone / context management
- `.claude/commands/` — slash commands du vault de Tom
