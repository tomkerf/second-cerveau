# Fiche Process 07 — Bilan 24h (prélèvement automatique)
_Fréquence : campagnes ponctuelles · Méthode : FD T90-523-2 + ISO 5667-3/10_

---

## Déclencheur
> "Process : bilan 24h" ou "Génère le rapport bilan [site]"

---

## Contexte
Prélèvement automatique asservi au débit sur 24h (STEP, rejets industriels).
Vérification COFRAC en 4 critères selon FD T90-523-2 :
- **Volume unitaire** — fidélité ≤ 5 %, justesse ≤ 10 %, volume moyen ≥ 50 mL
- **Vitesse d'aspiration** — chaque essai ≥ 0,5 m/s
- **Pesée volume global** — écart nb prélèvements ≤ 5 %, écart volume ≤ 10 %
- **Température enceinte** — 2 °C ≤ T ≤ 8 °C (ISO 5667-3/10)

Outil de saisie terrain : **BilanPage** dans l'app PMC v2 (`/outils/bilan24h`)
→ Calcul de conformité en temps réel, génération PDF depuis l'app.

---

## Workflow complet

```
Terrain (début mission)
  → Ouvrir PMC v2 → /outils/bilan24h
  → Onglet Identification : renseigner client, site, préleveur, éprouvette
  → Onglets Volume + Vitesse : mesures DÉBUT (3 essais chacun)

Terrain (fin mission, ~24h plus tard)
  → Relever compteurs : volume rejet 24h, nb prélèvements réalisés
  → Peser flacon (vide puis plein)
  → Onglets Volume + Vitesse : mesures FIN (3 essais)
  → Onglet Pesée : saisir les données de compteurs et pesée
  → Onglet Température : relever T début, fin, min, max

Bureau (résultats LIMS disponibles)
  → Onglet Analyses : ajouter chaque paramètre analysé
    - Saisir : nom paramètre, unité, résultat LIMS, seuil arrêté préfectoral
    - Direction : ≤ seuil (polluants) ou ≥ seuil (O2 dissous...)
    - Conformité calculée automatiquement
  → Onglet Synthèse → "Générer rapport PDF" (COFRAC + analyses)
  → Dire à Claude "Process : bilan 24h" + données → rapport .md dans vault
```

---

## Inputs nécessaires

| Champ | Exemple | Obligatoire |
|-------|---------|-------------|
| Client | Commune de Plounérin | ✅ |
| Site / point d'échantillonnage | STEP Plounérin — Entrée | ✅ |
| N° convention | 2025.00.XXX.XXX | ✅ |
| Date vérification | 28/04/2026 | ✅ |
| Nature échantillon | Effluent brut | ✅ |
| Opérateur | T. Kerfendal | ✅ |
| Marque/modèle préleveur | ISCO 6712 | ✅ |
| N° série préleveur | SN-XXXXXX | ✅ |
| N° éprouvette réf. | EP-XXX | ✅ |
| **Volume** | | |
| → Volume unitaire programmé | 70 mL | ✅ |
| → 3 mesures DÉBUT (mL) | 68 / 71 / 70 | ✅ |
| → 3 mesures FIN (mL) | 69 / 70 / 72 | ✅ |
| **Vitesse** | | |
| → Distance tube (m) | 1,5 m | ✅ |
| → 3 temps DÉBUT (s) | 2,8 / 2,9 / 2,7 | ✅ |
| → 3 temps FIN (s) | 2,9 / 3,0 / 2,8 | ✅ |
| **Pesée** | | |
| → Volume rejet 24h (m³) | 1 200 m³ | ✅ |
| → Asservissement (m³/prélèvement) | 12 m³ | ✅ |
| → Nb prélèvements réalisés | 96 | ✅ |
| → Volume unitaire moyen mesuré (mL) | 70 mL | ✅ |
| → Poids flacon vide (kg) | 1,235 kg | ✅ |
| → Poids flacon plein (kg) | 8,235 kg | ✅ |
| **Température** | | |
| → T° début / fin (°C) | 4,0 / 6,5 °C | ✅ |
| → T° min / max enregistrées (°C) | 2,5 / 7,8 °C | ✅ |
| **Analyses** (autant que nécessaire) | | |
| → Paramètre | DCO, DBO5, MES, NTK, Pt… | ✅ |
| → Unité | mg/L, mg O2/L… | ✅ |
| → Résultat LIMS | valeur mesurée | ✅ |
| → Seuil arrêté préfectoral | valeur limite | ✅ |
| → Direction | ≤ seuil (polluant) / ≥ seuil (O2) | ✅ |
| Anomalies / observations | — | ❌ optionnel |

---

## Process Claude

1. **Recueillir** les inputs (lecture fiche terrain ou saisie directe)
2. **Calculer** les 4 critères COFRAC :
   - Volume : fidélité = (max–min)/moy × 100, justesse = |moy–théo|/théo × 100
   - Vitesse : v = distance/temps pour chaque essai
   - Pesée : écart nb = (réel–attendu)/attendu × 100, vol réel = poids plein – poids vide
   - Température : vérifier 2 ≤ T ≤ 8 pour chaque relevé
3. **Générer** le rapport au format standard ci-dessous
4. **Sauvegarder** dans `4_journal/rapports/[YYYY-MM-DD]_BILAN24H_[SITE].md`

---

## Template rapport

```markdown
# Rapport bilan 24h — [SITE] — [DATE]

**Date** : [DATE]
**Site** : [SITE] — [POINT_ECH]
**Client** : [CLIENT] — N° convention [CONV]
**Opérateur** : [OPERATEUR]
**Nature échantillon** : [NATURE]
**Préleveur** : [MARQUE_MODELE] — N° [SERIE]
**Éprouvette réf.** : [EPROUVETTE]

---

### Résultats vérification COFRAC (FD T90-523-2)

| Critère | Résultat | Norme | Statut |
|---------|----------|-------|--------|
| Fidélité volume DÉBUT | [X,XX] % | ≤ 5 % | ✅/❌ |
| Fidélité volume FIN | [X,XX] % | ≤ 5 % | ✅/❌ |
| Justesse volume | [X,XX] % | ≤ 10 % | ✅/❌ |
| Volume moyen global | [XX,X] mL | ≥ 50 mL | ✅/❌ |
| Vitesse aspiration DÉBUT | [X,XX] m/s (moy.) | ≥ 0,5 m/s | ✅/❌ |
| Vitesse aspiration FIN | [X,XX] m/s (moy.) | ≥ 0,5 m/s | ✅/❌ |
| Écart nb prélèvements | [X,X] % | ≤ 5 % | ✅/❌ |
| Écart volume collecté | [X,X] % | ≤ 10 % | ✅/❌ |
| Température enceinte | [X,X]–[X,X] °C | 2–8 °C | ✅/❌ |

### Résultats d'analyses

| Paramètre | Résultat | Unité | Seuil | Statut |
|-----------|----------|-------|-------|--------|
| DCO | [X] | mg/L | ≤ [Y] | ✅/❌ |
| DBO5 | [X] | mg O2/L | ≤ [Y] | ✅/❌ |
| MES | [X] | mg/L | ≤ [Y] | ✅/❌ |
| [Paramètre] | [X] | [unité] | [op] [Y] | ✅/❌ |

**Conclusion analyses : [✅ CONFORMES / ❌ NON CONFORMES] aux seuils de l'arrêté préfectoral**

### Conclusion générale

**[✅ CONFORME / ❌ NON CONFORME]** — Vérification COFRAC réalisée conformément à FD T90-523-2 et ISO 5667-3/10. Résultats d'analyses [conformes/non conformes] aux valeurs limites de rejet.

[Si non conforme : détail des critères défaillants et actions correctives]

### Anomalies / observations
[ou "Aucune anomalie constatée."]

---
*Rapport généré le [DATE] · Labocea Quimper*
```

---

## Automatisation future
- Agent : lire la fiche terrain scannée → extraire données → lancer calculs → générer rapport
- Connexion avec BilanPage : exporter les données JSON depuis l'app → Claude génère le rapport .md

