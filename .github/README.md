# Workflow spec → plan → dev — Version GitHub Copilot

Cinq commandes pour structurer un projet sans overhead documentaire inutile.

---

## Installation

Copie le dossier `.github/` à la racine de ton projet. C'est tout.

- Les commandes vivent dans `.github/prompts/` et s'invoquent avec `/nom` dans le chat Copilot
- `.github/copilot-instructions.md` est chargé automatiquement par Copilot dans tous les chats du workspace

> Fonctionnalité en **public preview** — nécessite VS Code avec l'extension GitHub Copilot activée.

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
- `spec.md` — spécification du projet
- `.github/copilot-instructions.md` — constitution mise à jour + commande de tests

---

### `/plan` — Planification

Lance après `/spec`. Nécessite `spec.md`.

Analyse les dépendances, propose une décomposition en groupes `[séquentiel]` / `[parallélisable]`. Valide avec toi avant d'écrire.

**Produit :**
- `tasks.md` — tâches avec checkboxes, groupées et marquées

> Note : les groupes `[parallélisable]` sont traités **séquentiellement** dans cette version (Copilot ne supporte pas les agents parallèles).

---

### `/dev` — Implémentation

Lance après `/plan`. Nécessite `tasks.md`.

Pour chaque tâche :
1. Cite les principes de la constitution qui s'appliquent
2. Implémente
3. Vérifie le respect de la constitution
4. Lance les tests si une commande est définie
5. Coche la tâche — uniquement si constitution respectée **et** tests verts

---

### `/resume` — Reprendre une session

Lance en début de session sur un projet existant.

Lit `spec.md`, `tasks.md` et `copilot-instructions.md`, produit un résumé d'état et indique la prochaine action. Ne modifie aucun fichier.

---

### `/add` — Ajouter une feature

Lance pour étendre un projet en cours, sans repartir de zéro.

Pose 3 questions ciblées, vérifie la compatibilité avec la constitution, ajoute un addendum à `spec.md` et de nouvelles tâches à la fin de `tasks.md` sans toucher à l'existant.

---

## Constitution — comment ça marche

`/spec` génère les principes non-négociables du projet en impératif (`JAMAIS de backend`, `TOUJOURS localStorage`...) dans `.github/copilot-instructions.md`.

Ce fichier est **chargé automatiquement par Copilot dans tous les chats** — la constitution est donc toujours présente sans action manuelle.

`/dev` cite les principes applicables **avant chaque tâche** et vérifie leur respect **après** — checkpoint actif, pas suggestion passive.

---

## Différences avec la version Claude Code

| | Claude Code | Copilot |
|---|---|---|
| Groupes `[parallélisable]` | Agents en parallèle | Séquentiel |
| Constitution auto-chargée | `CLAUDE.md` | `copilot-instructions.md` |
| Commandes | `.claude/commands/` | `.github/prompts/` |

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
├── .github/
│   ├── copilot-instructions.md    ← constitution (auto-chargé par Copilot)
│   ├── prompts/                   ← commandes du workflow
│   │   ├── spec.prompt.md
│   │   ├── plan.prompt.md
│   │   ├── dev.prompt.md
│   │   ├── resume.prompt.md
│   │   └── add.prompt.md
│   └── README.md                  ← cette doc
├── spec.md                        ← spécification (enrichie par /add)
└── tasks.md                       ← tâches [ ] / [x] avec marqueurs
```
