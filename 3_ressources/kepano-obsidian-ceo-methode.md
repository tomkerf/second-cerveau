# Kepano — Méthode du CEO d'Obsidian

#obsidian #prise-de-notes #pkm #ressource

**Source** : Transcription YouTube — "How the CEO of Obsidian Takes his Notes (Underrated Genius)"
**Sujet** : Vault template de Stephan "kepano" Ango, CEO d'Obsidian

---

## Qui est kepano ?

**Stephan Ango**, CEO d'Obsidian MD. A publié son vault template sur Reddit/GitHub. Philosophie minimaliste, orientée vitesse et connexions.

---

## Philosophie : File over App

> "Ce qu'on écrit va dans des fichiers markdown. Si le logiciel cesse de fonctionner, les notes existent encore. Elles outlastent le software."

- Les notes ne sont **jamais prisonnières d'un format propriétaire**
- Vault = simple dossier de fichiers `.md`
- Pas de dépendance au cloud ni à un éditeur spécifique

---

## Structure : le root d'abord

**Contrairement aux systèmes classiques (PARA, Karpathy), kepano met la majorité de ses notes à la racine du vault**, pas dans des dossiers.

> "Most of my notes are in the root of the vault, not a folder. If a note is in the root, I know it's something I wrote or relates directly to me."

- Pas de dossier `Notes/` — trop d'overhead décisionnel
- Les catégories et le dossier `notes/` dans le template ne sont là que pour la clarté initiale → à supprimer ensuite
- Résultat apparent : "chaos" dans l'explorateur de fichiers → mais c'est **voulu**

---

## Organisation par propriétés, pas par dossiers

Au lieu de décider où ranger chaque note, kepano utilise une **propriété `categories`** en frontmatter.

```yaml
---
id: 20251202070000
created: 2025-12-02
tags: [journal, note]
categories: [meetings, journal]
---
```

### Pourquoi les propriétés > dossiers

- Une note peut appartenir à **plusieurs catégories simultanément** (impossible avec les dossiers)
- Zéro friction au moment d'écrire — on ajoute la propriété, on passe à autre chose
- Les **Bases Obsidian** génèrent automatiquement une vue de toutes les notes d'une catégorie

### Consulter une catégorie

Pas besoin de naviguer dans les dossiers. Chaque fichier dans `categories/` est une **Obsidian Base** qui affiche toutes les notes ayant ce tag/propriété.

---

## Créer une note : Unique Note Creator

Kepano utilise quasi-exclusivement **Create new unique note** (plugin core) :
- Génère automatiquement un ID timestamp (`20251202070423`)
- Pré-remplit `created` et `tags` via un template
- Résultat : chaque note sait quand elle a été créée, même si le titre change

---

## Cycle de révision

| Fréquence | Action |
|-----------|--------|
| **Mensuel** | Relire les notes du mois, compiler les idées marquantes dans une note de synthèse mensuelle |
| **Aléatoire** | "Open Random Note" → traverser le vault au hasard, trouver des connexions inattendues |
| **Annuel** | Revoir toutes les synthèses mensuelles + répondre à 40 questions de bilan (sur son blog) |

---

## Types de notes

| Type | Description |
|------|-------------|
| **Journal entries** | Capture quotidienne, timestampée |
| **Evergreen notes** | Notes durables, long format, polies dans le temps |
| **Essays** | Textes longs, réflexions approfondies |
| **Meetings** | CR de réunions/conversations (catégorie `meetings`) |

---

## Ce que ça change vs Karpathy (numérotation de dossiers)

| Kepano | Karpathy (2nd cerveau de Tom) |
|--------|-------------------------------|
| Root-first, propriétés | Dossiers numérotés (1_projets/, 2_casquettes/…) |
| Zéro friction catégorisation | Catégorisation explicite à la création |
| Bases pour naviguer | Structure visible dans l'explorateur |
| Chaos apparent, connexions émergentes | Ordre apparent, rangement intentionnel |

Les deux approches sont valides — kepano optimise pour la **vitesse de capture** et les **connexions inattendues**, Karpathy pour la **clarté de navigation**.

---

## Ce que Tom peut en tirer

- **Unique Note Creator** pour les captures rapides dans `raw/inbox/` sans friction de nommage
- **Propriété `categories`** à ajouter aux fiches dans `3_ressources/` pour une navigation par thème via Bases
- **Open Random Note** comme outil de révision/inspiration du vault
- **40 questions annuelles** de kepano → à retrouver sur son blog pour le bilan annuel
- La philosophie "file over app" renforce le choix d'Obsidian + GitHub (pas de lock-in)

---

## Liens

- Blog de kepano : kepano.notion.site / stephango.com
- Vault template GitHub : github.com/kepano/kepano-obsidian
- [[claude-code-obsidian-2nd-cerveau]] — système Tom actuel
