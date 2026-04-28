# Labocea App Rapports

## Statut
🔴 **En développement — Phase cadrage**

## Description
Application web interne pour l'équipe PMC. Saisie terrain + import LIMS + génération automatique de rapports d'intervention PDF.

Deux types de rapports :
- **Bilan 24h** — prélèvement automatique, norme FD T90-523-2
- **Eau souterraine** — norme NF X 31-615

## Stack
React + Vite + TypeScript + Firebase + Cloudflare Workers + PWA + jsPDF + PapaParse

## Repo
`~/Documents/dev/labocea-app-rapports/` ← à initialiser

## Cadrage
Voir [[app-rapports-CLAUDE]] pour le document de référence complet.

## V1 (archive)
Script Python `generate_pdf_report.py` + template Excel — conservé, ne pas supprimer.

## Liens
- [[app-pmc-v2]] — même stack, même équipe, même design system
- [[3_ressources/fiches-process/07_bilan-24h]] — process bilan 24h
- [[3_ressources/fiches-process/06_prelevement-eaux-souterraines]] — process ES
