Génère mon briefing de journée.

Lis d'abord `.claude/memory/contexte-ipcra.md` et `.claude/memory/profil-tom.md`.

Ensuite :

1. **Agenda du jour** — si tu as accès au calendrier Google, liste les événements d'aujourd'hui. Sinon, indique qu'aucun calendrier n'est connecté.

2. **Tâches prioritaires** — lis `TASKS.md` si il existe, sinon affiche les actions prioritaires depuis `contexte-ipcra.md`.

3. **Rappels importants** — signale toute échéance proche (< 7 jours) mentionnée dans le contexte IPCRA.

4. **Raw inbox** — si des fichiers sont présents dans `raw/inbox/` ou `raw/terrain/` depuis moins de 7 jours, mentionne qu'il y a des notes à ingérer (`/ingest`).

Format de sortie : concis, sans intro, structuré en 4 blocs. Langue française. Ton direct.
