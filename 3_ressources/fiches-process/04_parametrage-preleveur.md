# Fiche Process 04 — Paramétrage préleveur automatique
_Fréquence : ponctuelle (installation / modification campagne) · Durée : ~30 min → cible <10 min avec Claude_

---

## Déclencheur
> "Process : paramétrage préleveur" ou "Configure le préleveur pour [campagne]"

---

## Contexte
Les préleveurs automatiques (ISCO, Teledyne, Manning...) doivent être programmés avant chaque campagne de prélèvement. Tom est le référent technique pour ces appareils. La configuration porte sur : fréquence de prélèvement, volumes, déclenchement (temps, débit, niveau), étiquetage des flacons.

---

## Inputs nécessaires

| Champ | Exemple | Obligatoire |
|-------|---------|-------------|
| Modèle préleveur | ISCO 6712 / Manning S-4040 | ✅ |
| Type de campagne | Chronométrique / proportionnel au débit / événementiel | ✅ |
| Fréquence | 1 prélèvement / heure | ✅ |
| Volume par prélèvement | 500 mL | ✅ |
| Nombre de flacons | 24 × 1L | ✅ |
| Durée campagne | 24h / 48h / 7 jours | ✅ |
| Déclencheur | Heure fixe / seuil débit / seuil niveau | ✅ |
| Date/heure démarrage | 29/04/2026 à 08h00 | ✅ |
| Site | Station Odet amont | ✅ |
| Type prélèvement | Eau superficielle / souterraine / rejet | ❌ |

---

## Process Claude

1. **Calculer** : nb flacons nécessaires = durée × fréquence → vérifier cohérence
2. **Générer** la feuille de programmation (paramètres à entrer dans l'appareil)
3. **Générer** l'étiquetage des flacons (heure théorique de chaque prélèvement)
4. **Générer** la fiche de mission pour le terrain

---

## Calculs automatiques

```
Nb prélèvements total = durée (h) × fréquence (/h)
Volume total = nb prélèvements × volume unitaire (mL)
Nb flacons = ceil(nb prélèvements / capacity_flacon)

Si nb prélèvements > nb flacons disponibles → ALERTE : ajuster fréquence ou durée
```

---

## Template fiche de programmation

```markdown
## Fiche de programmation — [MODÈLE] — [SITE] — [DATE]

**Site** : [SITE]
**Préleveur** : [MODÈLE] — N° [SN]
**Campagne** : [TYPE]
**Opérateur** : [OP]

### Paramètres de programmation

| Paramètre | Valeur à entrer |
|-----------|----------------|
| Mode | [CHRONOMÉTRIQUE / PROPORTIONNEL] |
| Fréquence | [FREQ] |
| Volume / prise | [VOL] mL |
| Déclencheur | [DÉCLENCHEUR] |
| Heure démarrage | [HEURE] |
| Nb flacons | [NB_FLACONS] |

### Planning des prélèvements

| Flacon | Heure théorique | Volume |
|--------|----------------|--------|
| 1 | [H+00] | [VOL] mL |
| 2 | [H+01] | [VOL] mL |
[...etc...]

### Vérifications avant départ terrain
- [ ] Batterie chargée / secteur branché
- [ ] Tuyau d'aspiration propre et raccordé
- [ ] Flacons propres et numérotés
- [ ] Heure appareil synchronisée
- [ ] Test aspiration manuel OK
- [ ] Fiche de mission signée

---
_Fiche générée le [DATE] · Labocea Quimper_
```

---

## Automatisation future
- Agent : génération fiche depuis saisie rapide vocale post-briefing campagne
- PMC v2 : intégration module "campagnes préleveur" avec génération auto
