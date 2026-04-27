Vérifie la santé du vault.

Contrôle les points suivants et produis un rapport :

1. **Liens cassés** — liens internes `[[...]]` qui pointent vers des fichiers inexistants
2. **Notes orphelines** — fichiers dans `raw/` datant de plus de 30 jours non encore ingérés
3. **Actions expirées** — tâches dans `contexte-ipcra.md` dont l'échéance est dépassée
4. **Fiches process obsolètes** — fiches dans `3_ressources/fiches-process/` non référencées dans `00_INDEX.md`
5. **Rapports sans fichier source** — rapports dans `4_journal/rapports/` dont les données sources ne sont plus dans `raw/`

Produis une liste d'actions correctives classées par priorité. Langue française.
