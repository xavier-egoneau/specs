# Workflow spec → plan → dev

Cinq skills pour structurer un projet sans overhead documentaire inutile.

---

## Installation

Copie le dossier `.claude/skills/` à la racine de ton projet.

---

## Commandes

### `/spec` — Spécification

Lance en début de projet ou avant une nouvelle feature significative.

Pose 6 questions :
1. Objectif principal
2. Utilisateurs / contexte
3. Périmètre (IN / OUT)
4. Contraintes techniques
5. Critère de succès (MVP)
6. Commande de tests (`npm test`, `vitest`... ou "aucun")

**Produit :**
- `spec.md` — la spécification du projet
- `CLAUDE.md` — constitution + commande de tests + instruction de charger `tasks.md` automatiquement

---

### `/plan` — Planification

Lance après `/spec`. Nécessite `spec.md`.

Lit `spec.md`, analyse les dépendances entre tâches et propose une décomposition. Chaque groupe est marqué `[séquentiel]` ou `[parallélisable]`. Valide avec toi avant d'écrire.

**Produit :**
- `tasks.md` — tâches avec checkboxes, groupées, ordonnées et marquées

---

### `/dev` — Implémentation

Lance après `/plan`. Nécessite `tasks.md`.

Pour chaque groupe :
- `[séquentiel]` → une tâche à la fois avec checkpoint constitution + tests
- `[parallélisable]` → un agent `coder` par tâche en parallèle, tests après merge

La tâche n'est cochée que si la constitution est respectée **et** les tests passent.

---

### `/resume` — Reprendre une session

Lance en début de session sur un projet existant (après `/clear` ou nouvelle session).

Lit `spec.md`, `tasks.md` et `CLAUDE.md`, produit un résumé d'état et indique la prochaine action. Ne modifie aucun fichier.

---

### `/add` — Ajouter une feature

Lance pour ajouter une feature à un projet en cours, sans repartir de zéro.

Pose 3 questions ciblées, vérifie la compatibilité avec la constitution, met à jour `spec.md` (addendum) et ajoute des tâches à la fin de `tasks.md` sans toucher à l'existant.

---

## Constitution — comment ça marche

`/spec` génère une section `## Constitution` dans `CLAUDE.md` avec les principes formulés en impératif (`JAMAIS de backend`, `TOUJOURS localStorage`, etc.).

Ce fichier est chargé automatiquement par Claude à chaque session. `/dev` est forcé de citer les principes applicables **avant chaque tâche** et de vérifier leur respect **après** — checkpoint actif, pas suggestion passive.

---

## Quand utiliser quoi

| Situation | Commande |
|-----------|----------|
| Nouveau projet | `/spec` → `/plan` → `/dev` |
| Nouvelle session sur projet existant | `/resume` |
| Nouvelle feature mid-project | `/add` → `/dev` |
| Périmètre flou | `/spec` obligatoire |
| Tâche isolée et claire | `/dev` directement |

---

## Fichiers générés

```
projet/
├── CLAUDE.md       ← constitution + commande tests + auto-chargement tasks.md
├── spec.md         ← spécification (mise à jour par /add)
└── tasks.md        ← tâches avec état ([ ] / [x]) et marqueurs séquentiel/parallélisable
```

`spec.md` et `tasks.md` sont versionnables dans le repo.
`CLAUDE.md` l'est aussi — il sert de mémoire partagée si le projet est multi-devs.
