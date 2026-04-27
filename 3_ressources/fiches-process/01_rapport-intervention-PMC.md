# Fiche Process 01 — Rapport d'intervention PMC
_Fréquence : hebdomadaire à mensuelle · Durée rédaction : ~20 min → cible <5 min avec Claude_

---

## Déclencheur
> "Process : rapport PMC" ou "Génère un rapport d'intervention PMC"

---

## Contexte
Tom gère ~40 stations de mesure continue (PMC) pour Labocea. Après chaque intervention (maintenance, dépannage, installation), un rapport doit être produit pour traçabilité interne et communication client/commercial.

---

## Inputs nécessaires (Claude demande si manquants)

| Champ | Exemple | Obligatoire |
|-------|---------|-------------|
| Date d'intervention | 28/04/2026 | ✅ |
| Station / site | Station Odet amont Quimper | ✅ |
| Type d'intervention | Maintenance préventive / curative / installation | ✅ |
| Matériel concerné | Sonde O₂ YSI, préleveur ISCO 6712 | ✅ |
| Actions réalisées | Description libre (quelques mots suffisent) | ✅ |
| Anomalies constatées | Capteur pH dérivé, joint d'étanchéité HS | ❌ optionnel |
| Suite à donner | Commande pièce, retour dans 15j | ❌ optionnel |
| Intervenant | Tom K. (par défaut) | ❌ optionnel |

---

## Process Claude

1. **Recueillir** les inputs manquants (max 3 questions groupées)
2. **Générer** le rapport au format standard ci-dessous
3. **Proposer** : "Sauvegarder en .md dans le vault ?" ou copier pour Excel/GMAO

---

## Template rapport

```markdown
## Rapport d'intervention — [SITE] — [DATE]

**Date** : [DATE]
**Site** : [SITE]
**Intervenant** : [NOM]
**Type d'intervention** : [TYPE]

### Matériel concerné
- [LISTE MATÉRIEL]

### Actions réalisées
[DESCRIPTION ACTIONS]

### Anomalies constatées
[ANOMALIES ou "Aucune anomalie constatée"]

### Suite à donner
[SUITES ou "RAS — station opérationnelle"]

---
_Rapport généré le [DATE] · Labocea Quimper_
```

---

## Automatisation future (étape 4-5)
- Agent : déclenché par vocal/texte après retour terrain
- n8n : export automatique vers GMAO ou dossier partagé Labocea
