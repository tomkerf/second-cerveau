# raw/ — Notes brutes

> **Règle absolue : Claude ne modifie jamais ce dossier. Il le lit seulement.**

Ce dossier est ta zone de dépôt. Tu y jettes tes notes sans te soucier du format.
Claude les lit via `/ingest` pour alimenter le wiki (`.claude/memory/`).

## Sous-dossiers

| Dossier | Contenu |
|---------|---------|
| `terrain/` | Notes de terrain brutes (observations, mesures hors rapport, anomalies) |
| `reunions/` | Notes de réunions, échanges informels, CR rapides |
| `idees/` | Idées projet, reconversion, tech, réflexions perso |
| `inbox/` | Tout le reste — à trier plus tard |

## Comment l'utiliser

1. Tu notes n'importe quoi, n'importe comment, dans le bon sous-dossier
2. Nommage suggéré : `YYYY-MM-DD_sujet.md`
3. Quand tu veux que Claude intègre ces notes : `/ingest`

## Ce que Claude fait avec raw/

- **Lit** les fichiers pour extraire les informations importantes
- **Ne modifie jamais** les fichiers originaux
- **Synthétise** dans `.claude/memory/` ou crée des notes wiki
