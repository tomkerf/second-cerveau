# CLAUDE.md — Labocea App Rapports

> Document de référence pour le développement de l'application Labocea App Rapports.
> À lire intégralement avant toute action de développement.

---

## 1. Contexte et objectif

**Labocea App Rapports** est une application web interne pour l'équipe PMC de Labocea. Elle permet aux techniciens de saisir leurs observations terrain et résultats d'analyses, puis de générer automatiquement des rapports d'intervention en PDF.

**Problème résolu :** remplacer le script Python + Excel existant (`generate_pdf_report.py`) par un outil web multi-utilisateurs, utilisable directement sur le terrain (mobile), avec import LIMS et génération PDF intégrée.

**Utilisateurs cibles :** toute l'équipe PMC — même périmètre que PMC v2.

**4 fiches terrain Labocea — toutes modélisées :**

| Réf. | Norme | Nature | Méthode |
|------|-------|--------|---------|
| PENV-SU-0114 p.1 | NF X 31-615 | Eau souterraine — sites pollués | Purge statique (3-5 Vp), massif filtrant |
| PENV-SU-0114 p.2 | FD T90-523-3 | Eau souterraine — suivi environnemental | Purge (3 Vc), pompe à demeure, salinité + O2 |
| PENV-SU-0117 | FD T90-523-1 / ISO 5667-9 / FD T90-523-2 | Eaux de surface (rivière / eaux salines / ERI) | Ponctuel + composite manuel |
| PENV-SU-0120 | FD T90-523-2 | Bilan 24h — prélèvement automatique asservi au débit | Asservissement débit + vérifications débitmètre + échantillonneur |

**Contenu d'un rapport :**
1. En-tête (client, site, date, technicien, type d'intervention)
2. Observations terrain (mesures in-situ, conditions météo, anomalies)
3. Résultats d'analyses (import LIMS ou saisie manuelle)
4. Interprétation conformité par paramètre (seuils arrêté préfectoral)
5. Conclusion + signature

---

## 2. Ce qui existe (V1)

- Script Python `generate_pdf_report.py` + template Excel
- Fonctionnel mais non web, non mobile, mono-utilisateur
- Conservé en archive — ne pas supprimer

---

## 3. Stack technique

| Composant | Choix | Raison |
|-----------|-------|--------|
| Frontend | React + Vite + TypeScript | Même stack PMC v2, équipe familiarisée |
| Auth | Firebase Auth (email/password) | Cohérence avec PMC v2 |
| Base de données | Firebase Firestore | Cohérence avec PMC v2 |
| Déploiement | Cloudflare Workers + Wrangler | Cohérence avec PMC v2 |
| PWA | Vite PWA plugin | Offline terrain (connexion instable sur site) |
| PDF | jsPDF + jspdf-autotable | Déjà éprouvé dans BilanPage.tsx |
| Import LIMS | PapaParse | Parsing CSV/Excel export LIMS |
| UI | Tailwind + shadcn/ui | Cohérence design PMC v2 |
| Icônes | Lucide React | Cohérence PMC v2 |
| Animations | Framer Motion (limité) | Cohérence PMC v2 |

**Design system :** Apple-style, identique à PMC v2 (tokens CSS, typographie, composants).

---

## 4. Architecture des pages

### Navigation principale
```
📋 Rapports      → Liste des rapports générés
➕ Nouveau        → Créer un rapport d'intervention
📥 Import LIMS   → Importer un export CSV/Excel
👤 Mon compte    → Profil, déconnexion
```

---

### Page : Rapports (`/rapports`)

**Contenu :**
- Liste de tous les rapports générés (date, client, site, type, technicien, statut)
- Filtres : par type (24h / ES), par technicien, par client, par mois
- Bouton "Télécharger PDF" par ligne
- Bouton "Nouveau rapport"
- Recherche par client/site

---

### Page : Nouveau rapport (`/rapports/nouveau`)

Formulaire en étapes (wizard) :

**Étape 1 — Identification**
- Type d'intervention : Bilan 24h | Eau souterraine
- Client (sélection depuis liste PMC v2 ou saisie libre)
- Site / point de prélèvement
- Date d'intervention
- Technicien (pré-rempli avec l'utilisateur connecté)
- Conditions météo (champ libre)

**Étape 2 — Observations terrain**

*Champs communs :*
- Conditions météo (sec ensoleillé / sec couvert / humide / pluie / orage / neige / gel)
- Observations générales + anomalies (texte libre)

---

*Fiche Eau souterraine (NF X 31-615 — COP0007) :*

**Identification ouvrage**
- Nom ouvrage, lieu/site
- Date prélèvement, heure début/fin purge, heure début prélèvement
- Identité préleveur (pré-rempli)
- Références équipements : pompe, sonde, tuyau, chronomètre (N° série)

**Description de l'ouvrage**
- État margelle/capot/tête
- Diamètre intérieur / extérieur (mm)
- Hauteur zone crépinée (m), tube crépiné de … à … m
- Repère (haut du tube / fourreau / margelle / autre), hauteur repère/sol (m)
- Profondeur mesurée P (m/repère)
- Toit piézo avant purge N (m/repère)
- Hauteur colonne d'eau H (m)
- Rabattement max possible R (m)
- Volume colonne d'eau Vc (L), Volume massif filtrant Vm (L)
- Volume eau dans ouvrage Vp (L), Volume min à purger 3-5 Vp (L)
- Présence phase flottante / plongeante (oui/non + épaisseur)

**Purge statique**
- Matériel : pompe immergée 12V / prélever jetable
- Position de la pompe (m)
- Débit de purge (L/min)
- Toit piézo fin de purge (m), Rabattement début/fin
- Volume purgé (L), Volume purgé / Vp
- Critère fin de purge (stabilisation paramètres in-situ / 3 à 5 Vp)
- Gestion eaux de purge (sol / réseau EU/EP / stockage / autre)
- Si purge non réalisée : motif

**Suivi physico-chimique pendant la purge (tableau)**
Colonnes : Temps de purge (min) | T°C | pH (3 mesures stables, ±0,2-0,3) | Cond25°C µS/cm (±5% si ≤500, ±2% si >500) | Toit piézo (m) | Q (L/min)
→ Lignes ajoutées dynamiquement (toutes les 3-5 min)

**Paramètres fin de pompage**
- Codes appareils/sondes utilisées (3 champs)
- T°C | pH | Cond25°C finale

**Prélèvement et conditionnement**
- Matériel : pompe immergée 12V / prélever jetable
- Position de la pompe (m)
- Débit de prélèvement (L/min)
- Filtration sur site (oui / non / sans objet)

**Observations organoleptiques**
- Réalimentation ouvrage (Bonne / Moyenne / Mauvaise / Assèchement)
- Couleur, limpidité, odeur — pendant purge et au prélèvement

**Réception laboratoire**
- Date/heure de réception
- T° à réception 1er échantillon (°C)
- T° enceinte conforme / non conforme (Cf. PENV-IN-0035)

---

*Fiche Bilan 24h (FD T90-523-3 — PENV-SU-0120 v3) :*

**Identification**
- Client, site, N° convention/devis
- Date/heure de prélèvement (début et fin bilan)
- Opérateur (pré-rempli)
- Nature de l'échantillon (effluent brut / effluent prétraité / effluent traité / eaux pluviales)
- Localisation exacte du point d'échantillonnage

**Dispositif de mesure de débit**
- Type : Canal venturi (modèle, Hmax) / Seuil déversoir (type rectangulaire/triangulaire/client/LABOCEA, cotes) / Manchon déversoir (type circulaire/triangulaire, diamètre)

**Débitmètre**
- Type (bulle à bulle / sonde US / H/V / électromagnétique / LABOCEA / autre / client)
- Positionnement (distance sonde/ouvrage, conformité)
- Vérification hauteurs venturi/déversoir (tableau : début bilan / 50% Hmax / fin bilan — hauteur mesurée/lue, conformité ≤ 2 mm)
- Étalonnage bille à bulle (dérive/cm, conformité)
- Lecture directe si impossibilité (motif)
- Zéro dans l'air (manchon déversoir)
- Vérification hauteurs débitmètre H/V (tableau début/fin bilan)
- Débitmètre électromagnétique (taille, L amont/aval, nature conduite, épaisseur, orientation, positionnement, conformité 6-9 amont / 3-9 aval)

**Métrologie — Identification équipements**
- Débitmètre, préleveur, éprouvette, réglé, tuyau prélèvement, balance, chronomètre, flacon, tomber (N° série)

**Échantillonneur automatique**
- Type : monoflacon / multiflacon / nastiques
- Alimentation : secteur / batterie
- Pompe : péristaltique / autre
- Tuyau : PVC / téflon / verre / autre
- Flacon : diamètre (mm), longueur (m)
- Nettoyage matériel avant utilisation (O/N)
- Purge tuyaux avant utilisation (O/N)
- Asservissement : poste d'aiguillage / autre — précision
- Positionnement prise d'eau : amont dispositif/seuil / ⅓ sous la surface / autre

**Vérification de l'échantillonneur — Vitesse aspiration**
Tableau : Début bilan + Fin bilan × 3 essais → temps (s), vitesse (m/s), critère ≥ 0,5 m/s

**Volume unitaire prélevé**
Tableau : 3 essais (mL) × début + fin bilan → Volume demandé (mL)
- Justesse (%) = |(Vmoy - Vdem) / Vdem| × 100 → critère ≤ 10%
- Fidélité (%) = |(Vmax - Vmin) / Vmoy| × 100 → critère ≤ 5%
- Limites inf/sup, justesse relative

**Volume global collecté**
- Volume unitaire moyen (mL), nombre de prélèvements, volume collecté théorique (L)
- Poids flacon début/fin bilan (kg), poids étalon (kg)
- Conformité : écart entre volume collecté réel et théorique ≤ 10% (conforme / non conforme)

**Volume rejeté**
- Nombre de prélèvements réalisés vs attendus (≥ 95%)

**Température de l'enceinte**
- Tableau : début + fin bilan → mesure (°C), critère ≤ 3°C

**Mesures in situ**
- T° échantillon | T° effluent | pH + T°C mesure | conductivité µS/cm
- Codes appareils/sondes
- Type mesure : ponctuelle / in situ / sur site / sur volume collecté / au continu

**Conditionnement et transport**
- Homogénéisation : mécanique / manuelle
- Date/heure de réception, T° à réception (conforme ≤ 1,3°C)

**Observations**
- Conditions météo, autres observations
- Changement du point d'échantillonnage (O/N, motif)
- Coordonnées géographiques, client prévu

---

*Fiche Eaux de surface (PENV-SU-0117) :*

Couvre 3 natures d'eau via une fiche commune (choix au départ) :
- **ER** — Eaux de rivière (FD T90-523-1)
- **ES** — Eaux salines (ISO 5667-9 / PENV-MO-0052)
- **ERI** — Eaux résiduaires (FD T90-523-2)

**Identification**
- Client, N° convention/devis
- Date prélèvement, identité préleveur (pré-rempli)
- Conditions climatiques (sec ensoleillé / sec couvert / humide / pluie / orage / gel / neige)
- Conditions de marée (si ES) : heure BM / HM / coefficient (début + fin campagne)
- Nature de l'échantillon (ER / ES / ERI)
- Méthode de prélèvement (FD T90-523-1 / ISO 5667-9 / FD T90-523-2)

**Section Échantillonnage ponctuel**
- Références appareils et sondes utilisés
- Position du prélèvement (en rive / depuis un pont / depuis l'eau / depuis un bateau / depuis un ponton / depuis le rivage / autre)
- Technique (main / perche / seau / lest)
- Observations/remarques (couleur, limpidité, odeur, changement climatique, modification point, sous-devis)

Tableau multi-points (lignes dynamiques) :
| Libellé du point | Heure | Type mesure (in situ / sur site) | T°C | pH | Cond25°C (µS/cm) | Salinité (g/kg) | O2 (optique/électrochimique) — O2 mg/L, %O2, Pression atm. (hPa) |

**Section Échantillonnage composite manuel (ERI uniquement)**
- Références appareils et sondes
- Observations/remarques

Tableau multi-points (lignes dynamiques) :
| Libellé du point | Heures élémentaires | Volume unitaire prélevé (mL) | Matériel intermédiaire (flacon/perche/seau/lest) | Homogénéisation (seau/flacon, mécanique/manuelle) | Type mesure | T°C | pH |

**Réception laboratoire**
- Date et heure de réception
- T° à réception 1er échantillon (°C)
- T° enceinte (conforme / non conforme — Cf. PENV-IN-0035)
- Autres observations

---

**Étape 3 — Résultats d'analyses**
- Import CSV/Excel LIMS (PapaParse) → auto-mapping colonnes
- Ou saisie manuelle ligne par ligne
- Tableau dynamique : paramètre | unité | résultat | seuil | direction (≤/≥) | conformité (calculée)
- Ajout / suppression de lignes
- Seuils pré-remplis depuis la fiche client (si disponible) ou saisis manuellement

**Étape 4 — Conclusion**
- Interprétation globale (conforme / non-conforme / à surveiller)
- Commentaires libres
- Préconisations (texte libre)
- Prévisualisation PDF avant génération

---

### Page : Import LIMS (`/import`)

- Upload fichier CSV ou XLSX export LIMS
- Prévisualisation du contenu parsé
- Mapping colonnes : paramètre, unité, résultat, méthode, LQ
- Association à un rapport existant ou création d'un nouveau
- Validation avant import

---

### Page : Fiche rapport (`/rapports/:rapportId`)

- Affichage lecture seule du rapport
- Bouton "Télécharger PDF"
- Bouton "Modifier" (si statut brouillon)
- Historique des modifications

---

## 5. Structure Firebase Firestore

#### `rapports/{rapportId}`
```
id                  string
type                string    "bilan24h" | "es_sites_pollues" | "es_suivi_enviro" | "eaux_surface"
statut              string    "brouillon" | "finalise"
clientNom           string
clientId            string    (ref → clients-v2, optionnel)
siteNom             string
dateIntervention    date
technicienUid       string    (uid Firebase Auth)
technicienNom       string    (dénormalisé)

// Identification
meteo               string

// Observations terrain
heureArrivee        string    "HH:MM"
heureDepart         string    "HH:MM"
observations        string
anomalies           string

// Champs Bilan 24h
bilan24h: {
  volumeTotal       number    (L)
  vitessePrelevement number   (mL/h)
  peseeFlacons      number    (g)
  temperatureEch    number    (°C)
  metrologieConforme boolean
}

// Champs Eau souterraine
eauSouterraine: {
  profondeurNappe   number    (m NGF)
  niveauPiezometrique number  (m)
  debitPurge        number    (L/min)
  volumePurge       number    (L)
  parametresInsitu  ParametreInsitu[]
}

// Analyses
analyses            AnalyseRow[]

// Conclusion
interpretationGlobale string  "conforme" | "non_conforme" | "a_surveiller"
commentaires        string
preconisations      string

createdAt           timestamp
updatedAt           timestamp
createdBy           string    (uid)
pdfUrl              string    (optionnel, URL si stocké)
```

#### `AnalyseRow` (objet imbriqué)
```
parametre           string    "DCO" | "MES" | "NTK" | ...
unite               string    "mg/L" | "NTU" | ...
resultat            number
seuil               number
direction           string    "lte" | "gte"   (≤ ou ≥)
conforme            boolean   (calculé client-side)
methode             string    (optionnel, ex: "NF T90-101")
lq                  number    (limite de quantification, optionnel)
```

#### `ParametreInsitu` (objet imbriqué — eau souterraine)
```
nom                 string    "pH" | "conductivite" | "temperature" | "O2" | "turbidite"
unite               string
valeurInitiale      number
valeurFinale        number
valeurStabilisee    number
```

---

## 6. PDF — Structure de sortie

Format A4, portrait. En-tête Labocea sur chaque page.

```
Page 1 — En-tête + Identification
  Logo Labocea | Titre "Rapport d'intervention PMC"
  Tableau : Client / Site / Date / Technicien / Type / N° rapport

Page 1-2 — Observations terrain
  Tableau mesures in-situ (bilan 24h ou eau souterraine selon type)
  Observations et anomalies en texte

Page 2-3 — Résultats d'analyses
  Tableau : Paramètre | Unité | Résultat | Seuil | Conformité (✓ / ✗)
  Ligne surlignée en rouge si non-conforme

Page finale — Conclusion
  Interprétation globale (badge conforme/non-conforme)
  Commentaires et préconisations
  Signature technicien + date
```

---

## 7. Roadmap d'implémentation

### Étape 0 — Initialisation
- [ ] `npm create vite@latest labocea-app-rapports -- --template react-ts`
- [ ] Installer dépendances : `react-router-dom`, `zustand`, `tailwindcss`, `lucide-react`, `framer-motion`, `jspdf`, `jspdf-autotable`, `papaparse`
- [ ] Configurer shadcn/ui
- [ ] Firebase SDK (Auth + Firestore)
- [ ] Vite PWA plugin (service worker, manifest)
- [ ] Cloudflare Workers + Wrangler
- [ ] Scripts `deploy-dev.sh` et `deploy-prod.sh`

### Étape 1 — Auth
- [ ] Page `/login`
- [ ] Store Zustand `useAuthStore`
- [ ] Route guard

### Étape 2 — Layout
- [ ] Navigation principale (sidebar desktop / tab bar mobile)
- [ ] Composant `AppLayout`

### Étape 3 — Création rapport (cœur de l'app)
- [ ] Wizard 4 étapes (`/rapports/nouveau`)
- [ ] Store `useRapportStore` (état du formulaire en cours)
- [ ] Étape 1 : Identification
- [ ] Étape 2 : Observations terrain (avec switch bilan24h / eau souterraine)
- [ ] Étape 3 : Tableau analyses (dynamique + import CSV)
- [ ] Étape 4 : Conclusion + prévisualisation
- [ ] Sauvegarde Firestore (brouillon auto toutes les 30s)

### Étape 4 — Génération PDF
- [ ] Template PDF Bilan 24h (reprendre BilanPage.tsx comme base)
- [ ] Template PDF Eau souterraine
- [ ] Mise en forme conformité (ligne rouge si dépassement)
- [ ] En-tête Labocea

### Étape 5 — Import LIMS
- [ ] Page `/import`
- [ ] PapaParse CSV + SheetJS XLSX
- [ ] Mapping colonnes (interface de correspondance)
- [ ] Validation avant injection dans le rapport

### Étape 6 — Liste rapports
- [ ] Page `/rapports` avec filtres
- [ ] Téléchargement PDF depuis la liste
- [ ] Fiche lecture seule `/rapports/:id`

### Étape 7 — PWA + mobile polish
- [ ] Manifest + service worker (cache offline)
- [ ] Optimisation formulaires tactile (touch targets ≥ 44px)
- [ ] Test offline complet

### Étape 8 — Déploiement
- [ ] Staging : `bash deploy-dev.sh`
- [ ] Validation équipe
- [ ] Production : `npx wrangler deploy`

---

## Notes de développement

- **BilanPage.tsx** dans app-pmc-v2 sert de base pour le template PDF bilan 24h.
- **Langue UI : français.** Tous les labels, messages, confirmations.
- **Dates : DD/MM/YYYY** à l'affichage, ISO 8601 en base.
- **Offline first** : sauvegarder le brouillon en localStorage si pas de connexion, sync Firestore au retour réseau.
- **TypeScript strict.** Pas de `any`.
- **Pas de dark mode** pour l'instant.
- **Même design system que PMC v2** (tokens CSS Apple-style, Tailwind, shadcn/ui pour composants complexes).
- **Ne jamais supprimer** le script Python V1 (`labocea-app-rapports/`).

---

*Document généré le 2026-04-28 — Version de référence initiale.*
