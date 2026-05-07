# PMC v2

## Statut
🔴 **Actif — priorité haute**
Dev : en cours · Staging : ✅ en ligne · Production : bloquée (DSIN)

## Description
Application interne multi-utilisateurs de gestion du parc de mesure continue (PMC) Labocea.
Remplace app-pmc-v1 (vanilla JS). Connexion individuelle par utilisateur, design Apple-style.

## Stack
- React 18 + Vite + TypeScript
- Firebase (Auth + Firestore)
- Cloudflare Workers + Wrangler
- shadcn/ui + Tailwind CSS + Framer Motion
- Lucide React

## Repo
`~/Documents/dev/app-pmc-v2/`
GitHub : `github.com/tomkerf/labocea-pmc-v2`
Déploiement : GitHub Actions → auto sur push `main`

## URLs
- Staging : `labocea-pmc-v2-dev.tomkerf.workers.dev`
- Production : `labocea-pmc.tomkerf.workers.dev` (en attente DSIN)

## Fonctionnalités en prod (staging)
- Auth Firebase (email/password)
- Tableau de bord (KPIs, planning du jour, alertes)
- Missions — clients, plans de prélèvement, calendrier, statuts
- Planning — vue mensuelle/hebdo des interventions
- Matériel — parc équipements, fiches, états
- Métrologie — vérifications périodiques
- Maintenances — interventions préventives/correctives
- Tuyaux — gestion des tuyaux préleveurs
- Infos terrain
- Admin
- Photos terrain (upload/delete depuis un prélèvement)
- PWA / cache offline (IndexedDB Firestore)

## Décisions récentes
- **Bilan 24h retiré** (28/04/2026) — sera dans `labocea-app-rapports`
- Déploiement via GitHub Actions (push main → deploy staging auto)

## Blocage actuel
→ Contacter **Sébastien ROUBAUD** (DSIN) pour accès serveur production

## Coût
~160€/mois tokens Claude API (développement sur temps personnel)
Validé par N+2 et N+3

## Liens
- [[labocea-app-rapports]] — app complémentaire (rapports terrain PDF)
- [[Travail]] — contexte RH / revalorisation
- [[app-pmc-v1]] — ancienne version (référence, ne pas supprimer)
