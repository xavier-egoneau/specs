---
name: add
description: Ajouter une feature en cours de projet sans repartir de zéro
agent: agent
---

Tu viens d'être invoqué par `/add`. Objectif : intégrer une nouvelle feature dans un projet existant.

## Process

**Étape 1 — Vérifie les prérequis :**

- Lis `spec.md` et `tasks.md`. Si absents, dis à l'utilisateur de lancer `/spec` et `/plan` d'abord.
- Lis `.github/copilot-instructions.md` pour prendre en compte la constitution.

**Étape 2 — Pose 3 questions ciblées :**

1. Quelle feature veux-tu ajouter ? (description en 1-2 phrases)
2. Quel est le périmètre exact ? (ce qui est IN / ce qui est OUT)
3. Y a-t-il des contraintes spécifiques à cette feature ? (si non, la constitution existante s'applique)

**Étape 3 — Vérifie la compatibilité avec la constitution :**

Analyse si la feature demandée entre en conflit avec un principe de `.github/copilot-instructions.md`. Si oui, signale le conflit et demande comment le résoudre avant de continuer.

**Étape 4 — Mets à jour `spec.md` :**

Ajoute une section à la fin du fichier sans modifier le contenu existant :

```markdown
## Addendum — [Nom de la feature]

**Objectif :** ...
**IN :** ...
**OUT :** ...
**Contraintes :** ...
```

**Étape 5 — Propose les nouvelles tâches :**

Décompose la feature avec marqueurs `[séquentiel]` / `[parallélisable]`. Présente à l'utilisateur pour validation avant d'écrire.

**Étape 6 — Ajoute les tâches à `tasks.md` après accord :**

```markdown
## [Nom de la feature] [séquentiel|parallélisable]
- [ ] ...
- [ ] ...
```

Ne touche pas aux tâches existantes.

## Règles

- Ne commence pas à implémenter — `/dev` vient ensuite
- Ne modifie jamais les tâches déjà présentes dans `tasks.md`
- Si la feature contredit la constitution, bloque et demande une décision explicite
