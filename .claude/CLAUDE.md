# 2nd cerveau — Tom Kerfendal

## Lecture prioritaire au démarrage
1. **`.claude/memory/contexte-ipcra.md`** — contexte structuré IPCRA (projets, casquettes, actions en cours)
2. **`.claude/memory/profil-tom.md`** — profil complet (bio, finances, santé, convictions, stack)

## Règles de travail
- Langue : français, réponses directes sans intro ni résumé inutile
- Montre toujours un plan avant d'exécuter une action complexe
- Ne jamais supprimer de fichiers sans confirmation explicite
- Mettre à jour la section **Actions prioritaires** de `contexte-ipcra.md` quand le statut d'une action change
- Pour dev : terminer par la commande de déploiement

## Structure vault (Karpathy + IPCRA)
```
2nd cerveau/             ← vault Obsidian (racine)
├── .claude/             ← contexte Claude (caché dans Obsidian)
│   ├── commands/        ← slash commands Claude Code (/briefing, /ingest, etc.)
│   └── memory/
│       ├── contexte-ipcra.md   ← PRIORITÉ 1
│       └── profil-tom.md       ← PRIORITÉ 2
├── raw/                 ← NOTES BRUTES (Claude lit seulement, ne modifie jamais)
│   ├── terrain/         ← observations terrain, anomalies, mesures hors rapport
│   ├── reunions/        ← CR rapides, échanges informels
│   ├── idees/           ← idées projet, reconversion, réflexions
│   └── inbox/           ← tout le reste à trier
├── 1_projets/           ← projets actifs (app-pmc-v2, kicktrack...)
├── 2_casquettes/        ← rôles permanents
├── 3_ressources/        ← formations, guides, templates, fiches-process
│   └── fiches-process/  ← process terrain
├── 4_journal/
├── 5_archives/
├── Argent.md
├── Santé.md
├── Travail.md
└── Vision2030.md
```

## Règle RAW
`raw/` est la zone de dépôt de notes brutes. Claude **ne modifie jamais** ces fichiers.
Il les lit via `/ingest` pour enrichir `.claude/memory/` et `4_journal/`.

## Slash commands disponibles
Taper `/[commande]` dans Claude Code :

| Commande | Action |
|----------|--------|
| `/briefing` | Briefing de journée (agenda + tâches + rappels + inbox raw) |
| `/ingest` | Ingère les notes de `raw/` dans le wiki |
| `/lint` | Vérifie la santé du vault (liens cassés, notes orphelines, échéances) |
| `/rapport-pmc` | Rapport d'intervention station PMC |
| `/prelevement-es` | Rapport prélèvement eaux souterraines (NF X 31-615) |
| `/bilan24h` | Rapport bilan 24h COFRAC (FD T90-523-2) |
| `/metrologie` | Vérification/étalonnage matériel |

## Backup GitHub
Vault versionné sur GitHub (repo privé). Plugin Obsidian Git : auto-sync toutes les 10 min.
→ Pour initialiser : `git init && git remote add origin [url-repo]`
