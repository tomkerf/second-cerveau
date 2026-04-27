# Fiche Process 06 — Prélèvement eaux souterraines
_Fréquence : campagnes ponctuelles · Durée rédaction : ~20 min → cible <5 min avec Claude_

---

## Déclencheur
> "Process : prélèvement ES" ou "Génère le rapport de la campagne [site]"

---

## Contexte
Prélèvements d'eaux souterraines sur sites et sols pollués, méthode NF X 31-615.
Ouvrages : piézomètres (PZ). Purge statique préalable au prélèvement.
Paramètres suivis pendant purge : T°C, pH, conductivité (Cond25), toit piézométrique.

---

## Inputs nécessaires

| Champ | Exemple | Obligatoire |
|-------|---------|-------------|
| Site / lieu | KERJESQUEL | ✅ |
| Client | GBO KERJESQUEL | ✅ |
| N° dossier / convention | 127861 / 2025.00.343.431 | ✅ |
| Date | 09/04/2026 | ✅ |
| Ouvrages prélevés | PZ5, PZ3 | ✅ |
| Conditions climatiques | Sec ensoleillé | ✅ |
| Pour chaque ouvrage : | | |
| → Profondeur, toit piézo, colonne d'eau | 25,5 m / 16,25 m / 9,25 m | ✅ |
| → Horaires purge + prélèvement | 8h30→9h45 / 9h44→9h47 | ✅ |
| → Volume purgé, débit | 60 L, 4 L/min | ✅ |
| → Paramètres fin de purge (T°, pH, Cond) | 14,1°C / 4,9 / 214 µS/cm | ✅ |
| → Observations organo. (couleur, limpidité, odeur) | sans / limpide / sans | ✅ |
| → Réception labo (T° échantillon, conformité) | 7°C, conforme | ✅ |
| Matériel utilisé (références pompe, sonde, tuyau) | 12 PST 225, 12 SNI 083 | ❌ optionnel |
| Anomalies / difficultés | — | ❌ optionnel |

---

## Process Claude

1. **Recueillir** les inputs (Claude peut lire directement une fiche terrain scannée/photo)
2. **Calculer** automatiquement si besoin :
   - Volume colonne d'eau (Vc) = π × r² × H × 1000
   - Critère fin de purge : vérifier stabilisation (ΔpH ≤ 0,2 · ΔCond ≤ 5% ou 10 µS/cm)
3. **Générer** le rapport au format standard
4. **Sauvegarder** dans `4_journal/rapports/[YYYY-MM-DD]_[SITE]_[OUVRAGES].md`

---

## Template rapport

```markdown
# Rapport de prélèvement — [SITE] — [DATE]

**Date** : [DATE]
**Site** : [SITE]
**Client** : [CLIENT] — N° convention [CONV]
**Dossier** : [N°DOSSIER]
**Intervenant** : T. Kerfendal
**Méthode** : NF X 31-615 (sites et sols pollués)
**Conditions climatiques** : [MÉTÉO]

### Ouvrages prélevés
[LISTE OUVRAGES avec références]

### Matériel utilisé
| Référence | Désignation |
[TABLEAU MATÉRIEL]

### Déroulement

**[OUVRAGE]**
- Profondeur : [P] m · Toit piézo : [N] m · Colonne d'eau : [H] m
- Purge : [H_début] → [H_fin] · Débit [Q] L/min · Volume [V] L
- Critère fin de purge : stabilisation in situ ✅
- Prélèvement : [H] · Débit [Q] L/min
- Fin de purge : T° [T]°C · pH [pH] · Cond25 [C] µS/cm
- Réalimentation : [QUAL] · Couleur : [C] · Limpidité : [L] · Odeur : [O]

### Réception laboratoire
T° échantillon : [T]°C · Enceinte : [CONFORME/NON CONFORME]

### Anomalies
[ou "Aucune anomalie constatée."]

---
*Rapport généré le [DATE] · Labocea Quimper*
```

---

## Automatisation future
- Agent : lire la photo de fiche terrain → extraire données → générer rapport
- n8n : déposer photo dans dossier → rapport auto dans vault
