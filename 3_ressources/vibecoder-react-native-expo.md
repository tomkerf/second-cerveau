# Vibecoder — App mobile React Native + Expo avec Claude Code (2026)

#claude-code #react-native #expo #mobile #dev #vibe-coding

**Source** : Transcription YouTube — "Vibecoder une app mobile : le tutorial Claude Code 2026"
**Créateur** : Virgile — dev full-stack 5 ans, fondateur agence Algomax (10+ entreprises accompagnées)

---

## Use case de la vidéo

App de **tracking médicaments** pour un patient transplanté hépatique :
- Rappels quotidiens aux heures définies
- Gestion du renouvellement (quantités variables par médicament, mois 28-31 jours)
- Scan d'ordonnance par IA pour calcul de stock automatique
- **Contrainte** : offline, sans base de données → coût de fonctionnement = 0

---

## Stack choisie

- React Native + Expo
- Pas de DB (stockage local uniquement)
- Fonctionnement hors-ligne
- Notifications push locales

---

## Process recommandé

### Étape 1 — Définir le scope avec l'IA avant de coder

**Ne pas demander du code directement.** À la place :

> "J'aimerais créer une app mobile en React Native + Expo. [Description du problème]. Pose-moi des questions pour comprendre le genre d'app que je veux. Une fois que tu auras tout le contexte, propose un plan pour commencer à la développer."

L'IA t'interviewe → scope précis → plan structuré → développement cadré.

**Toujours préciser dès le départ** : no-DB, offline, contraintes de publication.

### Étape 2 — Développement avec Claude Code

Objectif : app fonctionnelle en **30 min à 1h** avec Claude Code.

---

## Leçons clés

- **Partir d'un vrai besoin personnel** = meilleure idée d'app (motivation + compréhension du problème)
- **Prévoir multi-utilisateurs dès le début** même si usage solo au départ
- **Offline + no-DB** = apps légères, gratuites à faire tourner, plus simples à maintenir
- L'interview IA en amont remplace 2h de specs écrites

---

## Pertinence pour Tom

- Stack identique au projet **Recomp** (React Native + Expo + Supabase)
- Le process "interview avant code" s'applique au cadrage de toute feature
- Pour Recomp : offline-first serait une option à reconsidérer pour réduire la complexité

---

## Liens

- `1_projets/recomp-cadrage.md` — projet mobile fitness de Tom (même stack)
- [[claude-code-cowork-boris-setup]] — setup Claude Code de référence
