# /commit

> Commande pour sauvegarder et envoyer le travail sur GitHub en toute sécurité.

---

## Mission

Quand je lance `/commit`, exécute la séquence suivante :

### Étape 1 : Vérifier l'état Git

Vérifie si le dossier est déjà un dépôt Git :

- Si **non** : lance `git init`, explique que c'est la première fois, et demande si un dépôt GitHub distant existe déjà. Si oui, demande l'URL du remote et fais `git remote add origin [URL]`. Si non, explique comment en créer un sur github.com et attends que je le fasse.
- Si **oui** : continue normalement.

### Étape 2 : Montrer ce qui va être sauvegardé

Lance `git status` et présente clairement :

```
Voici ce qui sera sauvegardé :

Fichiers modifiés :
- [liste des fichiers]

Fichiers nouveaux :
- [liste des fichiers]

Fichiers ignorés (secrets, système) :
- secrets/ ← protégé, ne sera pas envoyé
```

Si rien n'a changé, dis-le simplement et arrête là.

### Étape 3 : Demander le message de commit

Propose un message de commit automatique basé sur les fichiers modifiés, puis demande confirmation :

```
Message de commit suggéré :
"[message suggéré]"

Tu valides ce message, ou tu veux le modifier ?
```

### Étape 4 : Sauvegarder

Une fois validé :

1. `git add .` (le .gitignore protège automatiquement secrets/)
2. `git commit -m "[message validé]"`
3. Si un remote GitHub est configuré : `git push origin main` (ou la branche active)
4. Si pas de remote : sauvegarde locale uniquement, rappelle comment ajouter un remote

### Étape 5 : Confirmer

```
Sauvegarde terminée.

- Commit : [message]
- Fichiers sauvegardés : [nombre]
- Envoyé sur GitHub : Oui / Non (local uniquement)
```

---

## Règles importantes

- Ne jamais inclure le dossier `secrets/` dans un commit (le .gitignore s'en charge, mais vérifier quand même)
- Si `secrets/` apparaît dans `git status` malgré le .gitignore, stoppe tout et alerte Mariam immédiatement
- Toujours montrer ce qui sera sauvegardé avant de commiter
- Ne jamais forcer un push (`--force`) sans confirmation explicite
- Communication en français, tutoiement
- Pas de tirets longs (em dashes) dans les réponses
