# AI Coding For Real Engineers — Matt Pocock (Full Workshop)

#claude-code #IA #engineering #contexte #LLM #bonnes-pratiques

**Source** : Transcription YouTube — "[FULL WORKSHOP] AI Coding For Real Engineers"
**Créateur** : Matt Pocock (@mattpocockuk) — enseignant TypeScript, AI Hero

---

## Thèse centrale

> "Les fondamentaux du software engineering qui fonctionnent avec les humains fonctionnent aussi avec l'IA."

L'IA n'est pas un paradigme entièrement nouveau — elle obéit aux mêmes contraintes que les développeurs humains. Les pratiques classiques (petites tâches, pas de gros monolithes) deviennent encore plus critiques avec l'IA.

---

## Concept clé : Smart Zone vs Dumb Zone

Source : Dex Hy (Human Layer)

| Zone | Contexte | Comportement LLM |
|------|----------|------------------|
| **Smart zone** | < ~100k tokens | Raisonnement précis, attention pleine |
| **Dumb zone** | > ~100k tokens | Dégradation progressive, erreurs stupides |

**Pourquoi ?** Les relations d'attention entre tokens scalent quadratiquement. Ajouter des tokens à un contexte déjà chargé = saturation → l'IA devient "dumb".

**Important** : peu importe la taille de la fenêtre (200k, 1M) — la dégradation commence toujours vers 100k tokens utiles. La taille de la fenêtre n'est pas la vraie limite.

---

## Implication pratique

- Ne pas demander à l'IA de "tout faire en une fois"
- Décomposer les grandes tâches en petites unités
- Commencer de nouvelles conversations plutôt qu'accumuler du contexte
- Conseil de Fowler (Refactoring) et Pragmatic Programmer : keep tasks small — vaut autant pour l'IA que pour l'humain

---

## Pertinence pour Tom

- Justifie les slash commands compartimentées (`/rapport`, `/ingest` = tâche isolée dans sa propre session)
- Sessions Claude longues avec beaucoup de fichiers lus = risque dumb zone
- Favoriser des sessions courtes et ciblées
- Justifie l'architecture claude-mem (mémoire externe) : déléguer la mémoire hors contexte plutôt que tout garder dedans

---

## Liens

- [[claude-code-obsidian-2nd-cerveau]] — même thématique (gestion contexte IA)
- [[claude-code-cowork-boris-setup]] — setup Claude Code pratique
