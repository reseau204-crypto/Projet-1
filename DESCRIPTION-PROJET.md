# Cockpit 360° — description du projet

Fichier de référence : `cockpit-360-comprehension-multi-agents-communaute-ia-final.html` (fichier HTML unique d'environ 1,2 Mo, sans dépendance serveur).
Ce document décrit l'intention et l'architecture. L'état d'avancement et les tâches restantes sont dans `CLAUDE.md`.

## 1. Idée directrice

Le cockpit est un **cockpit de compréhension**, pas seulement de consultation. L'utilisateur ne doit pas se demander « dans quelle page chercher ? », mais seulement :

> « Qu'est-ce que je veux comprendre ? »

Il descend ensuite du plus synthétique au plus détaillé :

```
Vue principale → Contexte croisé → Aspect → Sous-vue → Contenu
```

Le contenu existant (objectifs, agents, workflows, tâches, décisions, preuves, KPI, journal, risques, blocages…) n'est pas supprimé : il est redistribué dans cette architecture. Avant la refonte, il était réparti en entrées techniques séparées (Vue par objectif, par agent, par workflow, Kanban, Décisions, Preuves, Journal).

## 2. Le système modélisé

Le HTML simule une communauté d'**agents IA** qui coopèrent sous le contrôle d'un **Humain** pour atteindre des objectifs. Le tout est piloté par des workflows.

- **Agents IA** : chacun a un rôle (quoi / quand / comment…), une mission, des responsabilités, des limites, des droits et des entrées/sorties. Parmi eux : Objectif, Planification, Organisation, Préparation, Exécution, Vérification, Preuve, Mesure.
- **Humain** : décideur. Les décisions sont graduées par niveau (N1 à N3). Par exemple, tout changement d'objectif relève de l'Humain (N3).
- **Objectifs** (OBJ-xxx) : fiche, critères de succès, KPI, valeur attendue, regroupés en projets.
- **Workflows** (WF-xxx) : instances d'étapes. Chaque étape a un statut, un agent responsable, des tâches, des preuves, des boucles de correction (B1, B3…) et une limite d'itérations avant escalade.
- **Contrôle** : qualité, conformité, sécurité, preuves, vérifications.
- **Simulation** : le temps avance (vitesses ×1, ×3, ×8) et des notifications sont émises.

## 3. Navigation en 4 niveaux

### Niveau 1 — Vue principale (navbar horizontale permanente)
`Projet | Objectif | Agent IA | Workflow | Travail / Exécution | Problèmes & Décisions | Résultats & Contrôle`

La vue choisie est l'angle de lecture principal. Elle ne supprime pas les autres dimensions.

### Niveau 2 — Contexte croisé (7 lignes de filtres)
Une ligne par dimension, chacune avec « Tous » et ses valeurs. La dimension de la vue active passe en premier. Les filtres sont **cumulables et croisés** : ils précisent ce qu'on regarde sans changer de page.

| Dimension | Valeurs de filtre |
|---|---|
| Projet | projets (P0, P1…) |
| Objectif | OBJ-001, OBJ-002… |
| Agent IA | un filtre par agent |
| Workflow | WF-001, WF-002… |
| Travail / Exécution | À faire, En cours, Bloqué, En attente, Terminé |
| Problèmes & Décisions | Risques, Blocages, Alertes, Décisions, Exceptions |
| Résultats & Contrôle | KPI, Qualité, Conformité, Sécurité, Preuves |

Exemple : *Agent Planification + OBJ-003 + WF-002 + Bloqué* filtre tout le contenu affiché dessous.

### Niveau 3 — Aspect (navbar horizontale propre à la vue)

| Vue | Aspects |
|---|---|
| Projet | Vue d'ensemble · Direction · Exécution · Contrôle · Problèmes · Résultats |
| Objectif | Vue d'ensemble · Finalité · Définition · Contribution · Exécution · Contrôle · Situation · Résultats |
| Agent IA | Vue d'ensemble · Identité · Travail · Collaboration · Contrôle · Situation · Performance |
| Workflow | Vue d'ensemble · Finalité · Structure · Acteurs · Exécution · Contrôle · Situation · Résultat |
| Travail / Exécution | Vue d'ensemble · À réaliser · En cours · Terminé · Organisation · Dépendances · Contrôle · Situation |
| Problèmes & Décisions | Vue d'ensemble · Détection · Diagnostic · Impact · Options · Décision · Actions · Suivi |
| Résultats & Contrôle | Vue d'ensemble · Résultats · Performance · Qualité · Conformité · Sécurité · Preuves · Amélioration |

### Niveau 4 — Sous-vues (navbar verticale à gauche, contenu à droite)
Exemples : Agent IA → Identité → *Rôle / Mission / Responsabilités* ; Objectif → Situation → *État / Progression / Risques / Blocages / Décisions* ; Workflow → Structure → *Étapes / Séquence / Entrées-sorties / Conditions / Boucles* ; Problèmes & Décisions → Détection → *Blocages / Risques / Alertes / Exceptions / Anomalies* ; Résultats & Contrôle → Sécurité → *Accès / Permissions / Données / Incidents / Vulnérabilités*.

### Principe « Vue d'ensemble partout »
« Vue d'ensemble » est toujours le premier bouton, aux niveaux 3 et 4. Au niveau 3, c'est une synthèse 360° (identité, travail, état, workflows, blocages, contrôle, performance, prochaine action). Au niveau 4, elle résume la catégorie (Identité → Rôle + Mission + Responsabilités). L'utilisateur choisit sa profondeur : compréhension rapide, ciblée ou détaillée.

## 4. Organisation du code (repères dans le HTML)

Le fichier est un seul HTML avec CSS et JavaScript embarqués, découpé en sections numérotées §01 à §73.

| Section | Contenu |
|---|---|
| §02 | Données (dont `DEMO_DATA`, à remplacer par les données réelles) |
| §52 à §56 | Catégories de contenu : ressources et finances, exigences et conformité, traçabilité et audit, mesures et KPI |
| §57 | Moteur du cockpit 360° : `CX_DIMS`, filtres `CXO`, clés de filtre `CXK`, contexte `cxCtx()`, comptages |
| §58 à §65 | Contenu des 7 vues (`CXS.projet`, `.objectif`, `.agent`, `.workflow`, `.travail`, `.problemes`, `.resultats`), chacune avec ses aspects et sous-vues |
| §66 à §70 | Visuels, graphiques SVG, actions directes (lever un blocage, annuler/rouvrir une décision, note au journal), accessibilité |
| §71 à §73 | Routage (`#/c/<vue>/<aspect>/<sous-vue>`), événements, démarrage |

Comment un filtre est évalué : pour chaque étape de workflow, `CXK[dimension](instance, étape)` renvoie les valeurs de la dimension. L'étape est retenue si, pour chaque dimension filtrée, au moins une de ses valeurs est sélectionnée. Les filtres Problèmes & Décisions et Résultats & Contrôle fonctionnent ainsi :

- **Problèmes & Décisions** : l'univers est construit par `cxProblems()` à partir de blocages d'étapes, décisions en attente, risques, alertes retenues et exceptions (non-conformité, preuve manquante, boucle proche de la limite). Un filtre sélectionne ceux de la nature choisie.
- **Résultats & Contrôle** : `KPI` si l'objectif a des KPI ; `Qualité` si l'étape relève de la vérification ou d'un test ; `Conformité` si l'étape a un gate ou si l'objectif relève d'exigences de conformité ; `Sécurité` si l'objectif relève d'exigences de sécurité ou si l'étape est un déploiement ; `Preuves` si l'étape a des preuves.

## 5. Qualité et limites connues

Tests déjà passés (Chromium) : 451 routes à 1440, 820, 390 et 360 px, 55/55 vérifications fonctionnelles, axe-core sans violation WCAG A/AA. Les limites connues et le reste à faire sont dans `CLAUDE.md`.

## 6. Espace « 1 — Pilotage du projet »

Premier bouton de la navigation (route `#/pilotage/<aspect>/<sous-vue>`, section §74). Il sert à faire avancer le projet et répond à 4 questions : *Où en sommes-nous ?* (Projet, Objectifs, Planning, KPI), *Qui fait quoi ?* (Agents IA, Workflows, Tâches), *Qu'est-ce qui bloque ?* (Blocages, Décisions, Preuves), *Que faut-il faire ensuite ?* (Prochaines actions). Il réutilise les sous-vues existantes du cockpit 360° et les mêmes filtres de contexte.
