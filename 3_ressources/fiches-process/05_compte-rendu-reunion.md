# Fiche Process 05 — Compte-rendu réunion technique
_Fréquence : ponctuelle · Durée rédaction : ~20 min → cible <5 min avec Claude_

---

## Déclencheur
> "Process : CR réunion" ou "Génère le CR de la réunion [sujet]"

---

## Contexte
Tom participe à des réunions techniques (coordination PMC v2, réunions DSIN, points équipe) et doit produire des comptes-rendus. Ces CR sont utilisés pour traçabilité, suivi d'actions, et communication avec N+1/N+2.

---

## Inputs nécessaires

| Champ | Exemple | Obligatoire |
|-------|---------|-------------|
| Date réunion | 28/04/2026 | ✅ |
| Objet / titre | Point avancement PMC v2 + DSIN | ✅ |
| Participants | Tom K., Sébastien ROUBAUD (DSIN), [N+2] | ✅ |
| Points abordés | Liste libre, quelques mots par point | ✅ |
| Décisions prises | Liste libre | ✅ |
| Actions à suivre | Qui fait quoi pour quand | ✅ |
| Prochaine réunion | 15/05/2026 | ❌ |

---

## Process Claude

1. **Recueillir** les inputs (Claude pose max 3 questions groupées si nécessaire)
2. **Structurer** en CR format standard
3. **Extraire** automatiquement le tableau des actions (qui / quoi / quand)
4. **Proposer** : sauvegarder dans vault ou envoyer par email

---

## Template CR

```markdown
## Compte-rendu — [OBJET] — [DATE]

**Date** : [DATE]
**Lieu / mode** : [PRÉSENTIEL / TEAMS / etc.]
**Rédacteur** : Tom Kerfendal
**Participants** : [LISTE]

---

### Points abordés

**1. [POINT 1]**
[Résumé discussion]

**2. [POINT 2]**
[Résumé discussion]

[...etc...]

---

### Décisions

- [DÉCISION 1]
- [DÉCISION 2]

---

### Actions à suivre

| # | Action | Responsable | Échéance |
|---|--------|-------------|----------|
| 1 | [ACTION] | [NOM] | [DATE] |
| 2 | [ACTION] | [NOM] | [DATE] |

---

**Prochaine réunion** : [DATE ou "À définir"]

_CR rédigé le [DATE] · Tom Kerfendal — Labocea Quimper_
```

---

## Automatisation future
- Agent : dicter le résumé post-réunion en vocal → Claude génère le CR formaté
- n8n : envoi automatique par email aux participants après validation Tom
