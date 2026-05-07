# Recomp — App mobile fitness & recomposition corporelle

> Document de cadrage complet.
> À lire avant toute action de développement.

---

## 1. Contexte et objectif

**Recomp** est une app mobile personnelle de suivi fitness, nutrition et lifestyle orientée recomposition corporelle.

**Utilisateur unique :** Tom Kerfendal

**Objectifs actifs :**
- Poids cible : 80 kg (départ ~82,8 kg)
- Programme : 4 sessions/semaine (Zone 2 + PUSH + PULL)
- Points de vigilance : alcool (~18 bières/semaine), sommeil, énergie

**Problème résolu :** centraliser en une seule app ce qui est aujourd'hui épars (courbes de poids mentales, carnets d'entraînement, aucun suivi nutrition) pour piloter une recomposition sérieuse avec données.

---

## 2. Stack technique

| Composant | Choix | Raison |
|-----------|-------|--------|
| Framework | React Native + Expo | Transfert direct compétences React, cross-platform iOS/Android |
| Navigation | Expo Router | File-based routing, même logique Next.js |
| Styling | NativeWind v4 | Tailwind CSS adapté mobile |
| State | Zustand | Déjà maîtrisé (PMC v2) |
| Backend/DB | Supabase (PostgreSQL) | Données relationnelles fitness, requêtes analytiques, free tier |
| Data fetching | TanStack Query | Cache, sync, offline-ready |
| Charts | Victory Native XL | Courbes poids, progressions, tendances — performant React Native |
| Auth | Supabase Auth | Simple, email/magic link |
| Storage | Supabase Storage | Photos de progression |
| Notifications | Expo Notifications | Rappels séances, pesée du matin |

---

## 3. Modules

### 3.1 Poids & mensurations

**Saisie quotidienne :**
- Poids (kg) — saisie rapide dès l'ouverture de l'app
- Mensurations optionnelles : tour de taille, poitrine, hanches, bras, cuisses (cm)
- Photo de progression (upload Supabase Storage)
- Note libre (contexte : lendemain de fête, nuit courte, etc.)

**Règles métier :**
- Poids affiché = moyenne glissante 7 jours (évite la variabilité eau/sel)
- Delta depuis le début, delta sur 30 jours
- Alerte si pas de pesée depuis 2 jours

---

### 3.2 Entraînements

**Programme prédéfini (4 sessions/semaine) :**

```
Zone 2      Cardio aérobie 45-60 min (vélo, marche rapide, footing lent)
            Cible FC : 60-70% FCmax
            Durée, distance, FC moy

PUSH        Développé couché / Développé incliné / Développé épaules
            Triceps (dips, extensions)
            Chaque exercice : N séries × N reps × charge (kg)

PULL        Tractions / Rowing / Curl biceps
            Chaque exercice : N séries × N reps × charge (kg)
```

**Log de séance :**
- Sélection du type (Zone 2 / PUSH / PULL / Libre)
- Pour Zone 2 : durée (min), distance optionnelle (km), FC moyenne optionnelle
- Pour PUSH/PULL : exercices prédéfinis avec ajout/suppression, saisie séries en temps réel
- Timer de repos entre séries (configurable, défaut 90s)
- Note de séance (ressenti, douleur, énergie)
- Statut RPE 1-10 (effort perçu)

**Suivi PR (Personal Records) :**
- Calcul automatique 1RM (formule Epley)
- Badge PR affiché si record battu sur la séance
- Historique PR par exercice

---

### 3.3 Nutrition

**Saisie par repas :**
- Repas du jour : Petit-déj / Déjeuner / Dîner / Collation
- Par repas : aliments + quantités
- Base alimentaire : CIQUAL (base française officielle) ou saisie manuelle
- Macros calculées automatiquement : protéines (g), glucides (g), lipides (g), calories (kcal)

**Objectifs nutritionnels :**
- Calories cible (configurable, ex : 2200 kcal/jour)
- Objectif protéines (ex : 160g/jour pour recomp)
- Barre de progression journalière visible sur le dashboard

**Règles métier :**
- Pas d'obsession : saisie optionnelle, pas de jauge culpabilisante
- Affichage en positif : "160g protéines atteints ✓" plutôt que déficit rouge

---

### 3.4 Lifestyle (alcool + sommeil)

**Alcool :**
- Saisie par consommation (bière 25cl / 33cl / 50cl, verre de vin, autre)
- Total hebdomadaire (verres + unités alcool)
- Objectif hebdo configurable (ex : ≤ 10 verres)
- Visualisation semaine courante vs objectif

**Sommeil :**
- Heure de coucher / lever
- Durée calculée automatiquement
- Qualité subjective 1-5 (étoiles)
- Niveau d'énergie au réveil 1-5

---

## 4. Architecture des écrans

### Navigation principale (Tab bar, 5 onglets)

```
📈 Progression   → Dashboard courbes et tendances (écran principal)
💪 Séance        → Log entraînement du jour
🍽️ Nutrition     → Saisie repas du jour
⚖️ Corps         → Pesée du jour + mensurations
👤 Profil        → Objectifs, réglages, programme
```

---

### Écran : Progression (`/progression`) — ÉCRAN PRINCIPAL

**Bloc Poids**
- Courbe poids brut + moyenne glissante 7j sur 30/90/180 jours (toggle)
- Poids du jour vs objectif (barre de progression vers 80 kg)
- Delta sur 7 jours et 30 jours

**Bloc Entraînements**
- Heatmap des sessions sur 12 semaines (type GitHub contributions)
- Séances réalisées ce mois / objectif (ex : 12/16)
- Derniers PR par exercice clé

**Bloc Nutrition (si saisie active)**
- Moyenne calories sur 7 jours
- Moyenne protéines sur 7 jours

**Bloc Lifestyle**
- Bières cette semaine vs objectif
- Sommeil moyen 7 jours (heures)

---

### Écran : Séance (`/seance`)

- Si programme du jour prévu : affiche le type suggéré (ex : "PUSH — J4 de la semaine")
- Bouton "Démarrer la séance"
- En cours de séance :
  - Liste des exercices avec sets à cocher
  - Timer repos entre séries
  - Bouton "Ajouter un exercice"
- Fin de séance : résumé (volume total, durée, RPE, PR battus)
- Historique des 5 dernières séances

---

### Écran : Nutrition (`/nutrition`)

- Barre macros du jour (protéines / glucides / lipides / calories)
- 4 repas avec ajout d'aliments par repas
- Recherche aliment (base CIQUAL + favoris)
- Saisie rapide des favoris

---

### Écran : Corps (`/corps`)

- Saisie poids du matin (champ numérique + bouton valider)
- Mensurations (optionnel, expandable)
- Photo du jour (optionnel, upload)
- Historique pesées des 30 derniers jours (liste)

---

### Écran : Profil (`/profil`)

- Nom, prénom, objectif poids, date début
- Configuration programme (jours Zone 2 / PUSH / PULL)
- Objectifs nutritionnels (calories, protéines)
- Objectif alcool hebdo
- Notifications (rappel pesée matin, rappel séance)
- Export données (CSV)

---

## 5. Structure Supabase

### Table `weight_entries`
```sql
id            uuid    PK
user_id       uuid    FK → auth.users
date          date    UNIQUE
weight_kg     decimal(5,2)
note          text
created_at    timestamptz
```

### Table `measurements`
```sql
id            uuid    PK
user_id       uuid    FK
date          date
waist_cm      decimal(5,1)
chest_cm      decimal(5,1)
hips_cm       decimal(5,1)
arm_cm        decimal(5,1)
thigh_cm      decimal(5,1)
photo_url     text
created_at    timestamptz
```

### Table `workouts`
```sql
id            uuid    PK
user_id       uuid    FK
date          date
type          text    'zone2' | 'push' | 'pull' | 'free'
duration_min  integer
distance_km   decimal(5,2)    -- Zone 2 seulement
hr_avg        integer         -- FC moyenne
rpe           integer         -- 1-10
note          text
created_at    timestamptz
```

### Table `workout_sets`
```sql
id            uuid    PK
workout_id    uuid    FK → workouts
exercise_name text
set_number    integer
reps          integer
weight_kg     decimal(5,2)
is_pr         boolean  DEFAULT false
created_at    timestamptz
```

### Table `nutrition_entries`
```sql
id            uuid    PK
user_id       uuid    FK
date          date
meal          text    'breakfast' | 'lunch' | 'dinner' | 'snack'
food_name     text
quantity_g    decimal(7,2)
calories      decimal(7,2)
protein_g     decimal(7,2)
carbs_g       decimal(7,2)
fat_g         decimal(7,2)
created_at    timestamptz
```

### Table `lifestyle_entries`
```sql
id            uuid    PK
user_id       uuid    FK
date          date    UNIQUE
alcohol_units decimal(4,1)   -- Unités alcool (1 bière = 1,5-2 unités)
sleep_start   time
sleep_end     time
sleep_quality integer    -- 1-5
energy_level  integer    -- 1-5
created_at    timestamptz
```

### Table `user_goals`
```sql
user_id           uuid    PK FK → auth.users
target_weight_kg  decimal(5,2)
calories_target   integer
protein_target_g  integer
alcohol_weekly_max decimal(4,1)
workout_per_week  integer
updated_at        timestamptz
```

---

## 6. Design system

**Philosophie :** même Apple-style que PMC v2 — épuré, aéré, sobre. Pas de rouge culpabilisant. Données affichées en positif.

**Palette spécifique Recomp :**
```
Accent principal :  #0071E3  (bleu Apple — actions)
Succès / PR :       #34C759  (vert — objectif atteint, record)
Neutre :            #8E8E93  (gris — données passées)
Warning doux :      #FF9F0A  (orange — à surveiller, pas d'alarme)
Fond :              #F5F5F7  (gris très clair)
Cartes :            #FFFFFF
```

**Typographie :** -apple-system (SF Pro sur iOS)

**Composants clés :**
- `WeightChart` — courbe Victory Native XL (poids brut gris clair + moyenne 7j bleu)
- `MacroBar` — barre horizontale tricolore (protéines / glucides / lipides)
- `WorkoutHeatmap` — grille 12 semaines × 7 jours, couleur selon intensité (RPE)
- `PRBadge` — badge vert "PR 🏆" affiché sur le set record
- `RestTimer` — countdown circulaire pendant les repos
- `AlcoholWeekBar` — 7 jours avec icônes verre, rouge si objectif dépassé

---

## 7. Roadmap d'implémentation

### Étape 0 — Init projet
- [ ] `npx create-expo-app recomp --template blank-typescript`
- [ ] Installer : `expo-router`, `nativewind`, `zustand`, `@tanstack/react-query`
- [ ] Installer : `supabase-js`, `victory-native`, `expo-notifications`
- [ ] Configurer Supabase (créer projet, schéma SQL, RLS)
- [ ] Configurer NativeWind v4
- [ ] Git init + repo GitHub privé

### Étape 1 — Auth
- [ ] Écran login (email magic link Supabase)
- [ ] Store `useAuthStore`
- [ ] Navigation protégée

### Étape 2 — Corps (pesée)
- [ ] Écran `/corps` — saisie poids
- [ ] Table `weight_entries` + RLS
- [ ] Validation et feedback immédiat

### Étape 3 — Progression (dashboard)
- [ ] `WeightChart` avec Victory Native XL
- [ ] Moyenne glissante 7 jours calculée côté client
- [ ] Affichage delta et objectif

### Étape 4 — Entraînements
- [ ] Écran `/seance` — log séance
- [ ] Programme Zone 2 / PUSH / PULL
- [ ] Timer repos
- [ ] Calcul PR + badge

### Étape 5 — Nutrition
- [ ] Écran `/nutrition`
- [ ] Base CIQUAL (import JSON)
- [ ] `MacroBar`
- [ ] Favoris

### Étape 6 — Lifestyle
- [ ] Alcool + sommeil dans `/corps` ou onglet dédié
- [ ] `AlcoholWeekBar`
- [ ] Heatmap entraînements

### Étape 7 — Polish
- [ ] Notifications (rappel pesée 7h, rappel séance)
- [ ] Export CSV
- [ ] TestFlight (distribution iOS perso)

---

## Notes de développement

- **Offline first** : TanStack Query avec cache persistant (MMKV ou AsyncStorage)
- **Pas de dark mode** pour l'instant
- **Langue UI : français**
- **TypeScript strict**, pas de `any`
- **Icônes : Lucide React Native**
- **Jamais de rouge culpabilisant** — l'app doit motiver, pas punir
- **Données = propriété de Tom** — export CSV disponible à tout moment

---

*Document créé le 2026-05-01 — Version cadrage initiale.*
