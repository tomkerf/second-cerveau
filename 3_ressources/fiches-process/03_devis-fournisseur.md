# Fiche Process 03 — Devis fournisseur matériel
_Fréquence : ponctuelle (2–5×/mois) · Durée : ~15 min → cible <3 min avec Claude_

---

## Déclencheur
> "Process : devis" ou "Rédige une demande de devis pour [matériel]"

---

## Contexte
Tom est l'interlocuteur principal pour les achats de matériel PMC. Il sollicite régulièrement des devis auprès de fournisseurs spécialisés (YSI/Xylem, WTW/Xylem, Hach, OTT Hydromet, ISCO/Teledyne, etc.) pour : renouvellement, SAV, pièces détachées, nouveaux équipements.

---

## Inputs nécessaires

| Champ | Exemple | Obligatoire |
|-------|---------|-------------|
| Matériel / référence | Sonde O₂ YSI ProODO + câble 10m | ✅ |
| Fournisseur cible | YSI / Hach / WTW / OTT / ISCO | ✅ |
| Quantité | 2 unités | ✅ |
| Motif | Remplacement station Odet (panne) | ✅ |
| Délai souhaité | Urgent / sous 15j / pas de contrainte | ❌ |
| Adresse livraison | Labocea Quimper (par défaut) | ❌ |
| Contact client Labocea | Tom Kerfendal, tomkerf@labocea.fr | ❌ |

---

## Process Claude

1. **Générer** l'email de demande de devis au format professionnel
2. **Inclure** les infos techniques nécessaires (référence, quantité, motif)
3. **Adapter le ton** selon fournisseur (technique / commercial)
4. **Proposer** : copier l'email ou envoyer via Gmail (si connecté)

---

## Template email devis

```
Objet : Demande de devis — [MATÉRIEL] — Labocea Quimper

Bonjour,

Je me permets de vous contacter pour solliciter un devis pour le matériel suivant :

**Désignation** : [MATÉRIEL]
**Référence** : [RÉFÉRENCE si connue]
**Quantité** : [QTÉ]
**Motif** : [MOTIF]

[Si urgent :] Nous avons un besoin urgent — merci de me faire parvenir votre devis dans les meilleurs délais.

Merci de bien vouloir adresser votre devis à :
Thomas Kerfendal — Technicien environnemental
Labocea — Quimper
Email : tomkerf@gmail.com / [email pro]
Tél : [téléphone]

En vous remerciant par avance,
Thomas Kerfendal
```

---

## Fournisseurs principaux (contacts)

| Fournisseur | Spécialité | Contact habituel |
|-------------|-----------|-----------------|
| YSI / Xylem | Sondes O₂, multi-paramètres | [à renseigner] |
| WTW / Xylem | pH, conductivité, oxygène | [à renseigner] |
| Hach | Turbidité, analyseurs | [à renseigner] |
| OTT Hydromet | Niveau, débit, hydrologie | [à renseigner] |
| ISCO / Teledyne | Préleveurs automatiques | [à renseigner] |

---

## Automatisation future
- Agent : déclencher depuis PMC v2 (bouton "Demander devis" sur fiche matériel)
- n8n : envoi email automatique via Gmail après confirmation Tom
