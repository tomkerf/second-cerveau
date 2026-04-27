Ingère les notes brutes du dossier `raw/` dans le wiki.

**Règles absolues :**
- Ne jamais modifier les fichiers dans `raw/` — lecture seule
- Ne créer ou mettre à jour que des fichiers dans `.claude/memory/` ou `4_journal/`

**Process :**

1. Lis tous les fichiers `.md` dans `raw/` (sous-dossiers inclus) qui n'ont pas encore été ingérés (vérifie les dates de modification)

2. Pour chaque fichier, extrais :
   - Informations factuelles importantes (personnes, projets, décisions, mesures, anomalies)
   - Actions à faire → ajouter dans `TASKS.md`
   - Informations sur des personnes → mettre à jour `.claude/memory/people/` si pertinent
   - Connaissances métier → enrichir le glossaire ou les ressources existantes

3. Si les notes concernent un rapport terrain (prélèvement, bilan, PMC) → propose de déclencher le process correspondant

4. Résume ce que tu as ingéré : combien de fichiers, quelles infos clés extraites, quelles mises à jour effectuées

5. NE PAS supprimer les fichiers raw après ingestion — ils restent comme archive
