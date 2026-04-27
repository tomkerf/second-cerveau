# Fiche Process 02 — Métrologie matériel terrain
_Fréquence : mensuelle / avant campagne · Durée : ~30 min → cible <10 min avec Claude_

---

## Déclencheur
> "Process : métrologie" ou "Prépare la métrologie pour [matériel]"

---

## Contexte
Avant toute utilisation terrain, le matériel de mesure doit être étalonné ou vérifié selon les protocoles métrologie Labocea. Tom est le référent métrologie pour le parc PMC. Les vérifications incluent : étalonnage, vérification raccordée, calcul de dérive, décision d'aptitude.

---

## Inputs nécessaires

| Champ                     | Exemple                                      | Obligatoire |
| ------------------------- | -------------------------------------------- | ----------- |
| Matériel / sonde          | Sonde O₂ YSI ProODO #SN12345                 | ✅           |
| Type de vérification      | Étalonnage / vérification / contrôle in situ | ✅           |
| Date vérification         | 28/04/2026                                   | ✅           |
| Valeurs mesurées          | pH 6.98 (étalon 7.00), O₂ 98.2% (air sat.)   | ✅           |
| Tolérance applicable      | ± 0.1 pH, ± 1% O₂                            | ✅           |
| Valeur étalon/référence   | pH 7.00 certifié COFRAC                      | ✅           |
| Opérateur                 | Tom K.                                       | ❌           |
| Conditions (T°, pression) | 20°C, 1013 hPa                               | ❌           |

---

## Process Claude

1. **Calculer** automatiquement : écart = valeur mesurée - valeur étalon
2. **Comparer** à la tolérance → verdict : CONFORME / NON CONFORME / À SURVEILLER
3. **Calculer** le taux de dérive si historique disponible
4. **Générer** la fiche de vérification
5. **Recommander** : recalibration, mise en quarantaine, ou aptitude confirmée

---

## Calculs automatiques Claude

```
Écart absolu = |Valeur mesurée - Valeur étalon|
Écart relatif (%) = (Écart absolu / Valeur étalon) × 100
Verdict : Écart ≤ Tolérance → CONFORME
          Écart > Tolérance → NON CONFORME
```

---

## Template fiche métrologie

```markdown
## Fiche de vérification métrologique — [MATÉRIEL] — [DATE]

**Matériel** : [MATÉRIEL] — N° série : [SN]
**Date** : [DATE] · **Opérateur** : [OP]
**Type** : [TYPE VÉRIFICATION]
**Conditions** : T° [TEMP]°C · Pression [PRES] hPa

### Résultats

| Paramètre | Valeur étalon | Valeur mesurée | Écart | Tolérance | Verdict |
|-----------|--------------|----------------|-------|-----------|---------|
| [PARAM] | [ETALON] | [MESURE] | [ECART] | [TOL] | ✅/❌ |

### Conclusion
**Décision d'aptitude** : [CONFORME / NON CONFORME / CONDITIONNELLE]
**Suite** : [RAS / Recalibration / Mise en quarantaine / Retour fournisseur]

---
_Fiche générée le [DATE] · Labocea Quimper_
```

---

## Sondes fréquemment vérifiées (référence rapide)

| Sonde | Paramètre | Tolérance standard |
|-------|-----------|-------------------|
| YSI ProODO | O₂ dissous (%) | ± 1% |
| WTW pH 3310 | pH | ± 0.05 pH |
| WTW Cond 3310 | Conductivité | ± 1% |
| Hach 2100Q | Turbidité (NTU) | ± 2% ou 0.02 NTU |
| OTT Hydromet | Niveau / débit | ± 1% |

---

## Automatisation future
- Agent : lecture fichier Excel métrologie → calcul automatique → alerte si non-conforme
- n8n : trigger mensuel → liste matériels à vérifier ce mois
