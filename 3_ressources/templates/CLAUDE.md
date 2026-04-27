# CLAUDE.md — Template de projet

> Ce fichier est lu par Claude Code au début de chaque session.
> Il définit le contexte, l'architecture et les règles du projet.
> À copier dans chaque nouveau dossier de projet, puis à remplir avant de commencer le développement.

---

## 🎯 Contexte & objectif

**Qui je suis :**
<!-- Ex: Technicien en mesures environnementales à Labocea, Quimper. -->
[À compléter]

**Problème que cette app résout :**
<!-- Ex: La saisie des rapports de contrôle inopinée prend 40 min, je veux la réduire à 5 min. -->
[À compléter]

**Utilisateurs cibles :**
<!-- Ex: Moi uniquement (usage interne). / Mes collègues techniciens. / Des clients externes. -->
[À compléter]

**Résultat attendu :**
<!-- Ex: Une app web accessible sur PC, qui génère un PDF de rapport en un clic. -->
[À compléter]

---

## 🏗️ Architecture technique

**Stack choisie :**
- Langage : TypeScript
- Framework : Next.js (App Router)
- UI : Tailwind CSS + ShadCN UI
- Base de données : Supabase / PocketBase / SQLite (choisir)
- Auth : Supabase Auth / pas d'auth (usage solo)
- Hébergement : Vercel / auto-hébergé / local uniquement
- Versioning : GitHub

**Variables d'environnement nécessaires :**
```
# À créer dans .env.local
DATABASE_URL=
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
```

---

## 📄 Pages & fonctionnalités

### Page 1 — [Nom]
- **URL :** `/`
- **But :** [Description]
- **Composants :** [liste des éléments UI]
- **Données lues :** [table/champs]
- **Actions possibles :** [ce que l'utilisateur peut faire]

### Page 2 — [Nom]
- **URL :** `/[route]`
- **But :** [Description]
- **Composants :** [liste]
- **Données lues :** [table/champs]
- **Actions possibles :** [liste]

<!-- Dupliquer ce bloc pour chaque page -->

---

## 🗄️ Structure de la base de données

```sql
-- Table 1
CREATE TABLE [nom_table] (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMPTZ DEFAULT now(),
  -- champs métier
  [champ_1] TEXT NOT NULL,
  [champ_2] NUMERIC,
  [champ_3] BOOLEAN DEFAULT false
);

-- Table 2
CREATE TABLE [nom_table_2] (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  [table_1_id] UUID REFERENCES [nom_table](id),
  -- ...
);
```

---

## 🔄 Plan d'implémentation

### Étape 1 — Fondations
- [ ] Initialiser le projet Next.js avec TypeScript + Tailwind + ShadCN
- [ ] Configurer GitHub
- [ ] Connecter la base de données (Supabase ou PocketBase)
- [ ] Créer les tables SQL
- [ ] Mettre en place l'authentification (si nécessaire)
- [ ] Dashboard vide avec navigation

### Étape 2 — [Nom fonctionnalité principale]
- [ ] [Tâche 1]
- [ ] [Tâche 2]
- [ ] [Tâche 3]

### Étape 3 — [Nom fonctionnalité secondaire]
- [ ] [Tâche 1]
- [ ] [Tâche 2]

### Étape 4 — Finalisation
- [ ] Tests des cas limites
- [ ] Vérification mobile / responsive
- [ ] Déploiement sur Vercel (ou autre)

---

## 🎨 Design & UI

**Thème couleurs :**
- Primaire : `#[hex]` — [nom/usage]
- Secondaire : `#[hex]` — [nom/usage]
- Fond : blanc / gris clair
- Texte : gris foncé / noir

**Composants ShadCN à utiliser :**
<!-- Ex: Button, Card, Table, Dialog, Form, Input, Select, Badge -->
[À compléter]

**Contraintes UI :**
<!-- Ex: Interface simple, utilisée sur terrain avec une seule main. Pas de mobile pour l'instant. -->
[À compléter]

---

## ⚙️ Règles & contraintes techniques

- Langue de l'interface : **Français**
- Toujours valider les formulaires côté serveur
- Aucune donnée sensible en clair dans le code (utiliser `.env.local`)
- Chaque nouvelle feature doit être sur une branche Git séparée
- Commenter les fonctions complexes en français
- [Ajouter d'autres règles spécifiques au projet]

---

## 📌 Contexte métier spécifique

<!-- C'est ici que tu mets les infos de ton domaine que Claude doit connaître. -->
<!-- Ex pour Labocea : -->
<!--
- Les contrôles inopinés suivent la norme NF EN ISO 5667
- Les paramètres mesurés : pH, DCO, MES, azote, phosphore
- Les résultats doivent être en mg/L sauf exception
- Le code SANDRE de l'eau usée domestique est 7
- Les coordonnées sont en Lambert 93 (EPSG:2154)
-->
[À compléter avec le vocabulaire et les règles métier du domaine]

---

## 🚀 Commande de démarrage de session

Au début de chaque session Claude Code, utiliser :

```
Lis le CLAUDE.md, mémorise le contexte complet, puis propose le plan détaillé de la prochaine étape à développer. Ne commence pas à coder avant que je valide le plan.
```

---

*Dernière mise à jour : [date]*
*Statut : [En préparation / En développement / En production]*
