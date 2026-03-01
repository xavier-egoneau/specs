# /add — Ajouter une feature en cours de projet

Tu viens d'être invoqué par `/add`. Objectif : intégrer une nouvelle feature dans un projet existant sans repartir de zéro.

## Process

**Étape 1 — Vérifie les prérequis :**

- Lis `spec.md` et `tasks.md`. Si absents, dis à l'utilisateur de lancer `/spec` et `/plan` d'abord.
- Lis `CLAUDE.md` pour prendre en compte la constitution.

**Étape 2 — Pose 3 questions ciblées :**

1. Quelle feature veux-tu ajouter ? (description en 1-2 phrases)
2. Quel est le périmètre exact ? (ce qui est IN / ce qui est OUT)
3. Y a-t-il des contraintes spécifiques à cette feature ? (si non, la constitution existante s'applique)

**Étape 3 — Vérifie la compatibilité avec la constitution :**

Analyse si la feature demandée entre en conflit avec un principe de la constitution dans `CLAUDE.md`. Si oui, signale le conflit et demande comment le résoudre avant de continuer.

**Étape 4 — Mets à jour `spec.md` :**

Ajoute une section à la fin du fichier :

```markdown
## Addendum — [Nom de la feature]
> Ajouté le [date]

**Objectif :** ...
**IN :** ...
**OUT :** ...
**Contraintes :** ...
```

Ne modifie pas le contenu existant de spec.md.

**Étape 5 — Propose les nouvelles tâches :**

Décompose la feature en tâches concrètes avec marqueurs séquentiel/parallélisable. Présente-les à l'utilisateur pour validation avant d'écrire.

**Étape 6 — Ajoute les tâches à `tasks.md` :**

Après accord, ajoute un nouveau groupe à la fin de `tasks.md` :

```markdown
## [Nom de la feature] [séquentiel|parallélisable]
- [ ] ...
- [ ] ...
```

Ne touche pas aux tâches existantes (cochées ou non).

## Règles

- Ne commence pas à implémenter — `/dev` vient ensuite
- Ne modifie jamais les tâches déjà présentes dans `tasks.md`
- Si la feature contredit la constitution, bloque et demande une décision explicite
