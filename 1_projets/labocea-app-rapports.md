# Labocea App Rapports

## Statut
🟡 **En production partielle — CI/CD bloqué (secrets GitHub manquants)**
Staging : labocea-app-rapports-dev.tomkerf.workers.dev ✅

## Description
PWA React/TypeScript pour techniciens terrain Labocea. Deux modules indépendants :
- **Fiches terrain** — saisie sur le terrain, auto-save Dexie (IndexedDB), offline-ready
- **Génération rapports** — import XLS DiPLABO → rapport Word .docx

## Fiches terrain implémentées (4/4 ✅)
| Code | Norme | Statut |
|------|-------|--------|
| PAUTO | FD T90-523-2 — prélèvement automatique asservi débit | ✅ |
| ESO | FD T90-523-3 — eaux souterraines | ✅ |
| ESO_SSP | NF X 31-615 — eaux souterraines sites pollués | ✅ |
| ESU | PENV-SU-0117 — eaux superficielles | ✅ |

Autocomplete client (Firestore `clients-v2`) + opérateur (Firestore `users`) dans tous les formulaires.

## Module rapports ✅
- Workflow : choix type → N° rapport + rédacteur → import XLS DiPLABO → VLE → volume rejeté (PAUTO) → génération .docx
- Rapport : page de garde bandeau LABOCEA, tableau visa, en-tête/pied de page, tableau résultats (dépassements en rouge), tableau charges de pollution (kg)
- VLE mémorisées par client (Dexie)

## Stack
React 19 · TypeScript strict · Vite · React Hook Form · Zod · Dexie (IndexedDB) · Firebase Firestore (lecture seule) · Tailwind CSS · Cloudflare Workers · docx · xlsx · file-saver

## Repo
`~/Documents/dev/labocea-app-rapports/`
Déploiement local : `bash deploy-dev.sh` ✅
CI GitHub Actions : ⚠️ secrets manquants

## ⚠️ Bloquant CI/CD
Ajouter dans GitHub Settings → Secrets → Actions :
- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

## À faire
- [ ] Configurer secrets GitHub CI
- [ ] Tester avec un vrai export DiPLABO
- [ ] Ajuster mise en forme rapport selon retours terrain
- [ ] Tester avec Romain

## Liens
- [[app-pmc-v2]] — même stack, même équipe
- [[labocea-app-rapports-cadrage]] — document de référence complet
