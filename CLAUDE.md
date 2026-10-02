# Reprise du travail : cockpit 360° (version finale)

Fichier unique et autonome : `cockpit-360-comprehension-multi-agents-communaute-ia-final.html` (s'ouvre directement dans un navigateur, sans serveur). Description du projet et de l'architecture : `DESCRIPTION-PROJET.md`.

## Fait
- Cockpit 360° (7 vues, contexte croisé, aspects, sous-vues, « Vue d'ensemble » partout), cockpit classique, Kanban, Décisions, Preuves, Journal, Rapport, Référentiel, Système, Atlas des 176 vues, routes, filtres, sauvegarde : tout est conservé.
- v3 : contrôle visuel, débordements mobiles, graphiques SVG (Impact, Options, Qualité, Sécurité), actions directes (lever un blocage par escalade, annuler et rouvrir une décision, note au journal), DEMO_DATA, accessibilité, table des matières §01 à §74.
- **Nouvel espace « 1 — Pilotage du projet »** (§74, route `#/pilotage/<aspect>/<sous-vue>`), premier bouton de la navigation. Il répond à 4 questions, chacune étant un aspect :
  - Où en sommes-nous ? → Projet, Objectifs, Planning, KPI
  - Qui fait quoi ? → Agents IA, Workflows, Tâches
  - Qu'est-ce qui bloque ? → Blocages, Décisions, Preuves
  - Que faut-il faire ensuite ? → Prochaines actions
  La Vue d'ensemble (tuiles, état des objectifs, tableau des objectifs, accès aux aspects, prochaines actions) est toujours affichée en premier. Les filtres de contexte (7 dimensions) s'appliquent partout et se partagent avec les autres vues.
- Fichier renommé `CLAUDE.md.md` → `CLAUDE.md` (lu automatiquement à chaque session) et HTML renommé en `-final`.

## Choix faits (option la plus simple)
- Aucune donnée nouvelle : chaque sous-vue du Pilotage appelle, au moment de l'affichage, la sous-vue existante du cockpit 360° (`cxFind(vue, aspect, sous-vue).fn`). Elle hérite donc de ses graphiques, de ses liens vers l'Atlas et de ses actions directes (lever un blocage, etc.).
- « Prochaines actions » est seulement une sous-vue de « Que faut-il faire ensuite ? » (pas de bandeau fixe).
- Le Pilotage utilise la dimension Projet comme première ligne de filtres de contexte.
- Les anciennes routes (`#/c/…`, `#/objectives`, `#/kanban`…) sont inchangées.
- La police est chargée depuis Google Fonts si le réseau est disponible ; sans réseau, le navigateur utilise ses polices système (la mise en page reste correcte).
- Point 1 (définitions des filtres « Problèmes & Décisions » et « Résultats & Contrôle ») : les valeurs de filtre sont celles du cahier des charges ; les règles de sélection actuelles du code sont conservées (décrites dans `DESCRIPTION-PROJET.md` §4), faute de définitions reçues.

## Testé (Chromium, ordinateur 1440 px et mobile 390 px)
- Les 16 routes du Pilotage (`#/pilotage`, 4 aspects, 11 sous-vues) : aucune erreur JavaScript, aucun débordement horizontal, aucun « undefined / NaN / Contenu indisponible ».
- Navigation par clic (entrée du menu, aspects, sous-vues), filtres croisés (ex. Agent Planification : 343 → 47 tâches ; Travail « Bloqué » : 3 tâches), actions de blocage héritées, route ancienne `#/c/projet` intacte.
- Contrôle de non-régression de 27 routes existantes (cockpit classique, objectifs, agents, workflows, Kanban, Décisions, Preuves, Journal, Rapport, Référentiel, Système, Atlas, recherche, 7 vues 360° et des sous-vues) à 1440 et 390 px : aucune erreur.
- Tests antérieurs de la v3 (451 routes, 55/55 vérifications fonctionnelles, axe-core WCAG A/AA) : non rejoués en entier sur cette version.

## Reste à faire
1. Valider les définitions des filtres « Problèmes & Décisions » et « Résultats & Contrôle » (voir plus haut).
2. Remplacer DEMO_DATA (section §02) par les données réelles : bénéficiaires, budgets, coûts, fournisseurs, contrats, registre des traitements.
3. Tester sur Safari / iPhone, Firefox, et avec un lecteur d'écran (NVDA, VoiceOver, TalkBack) ; zoom 200 % ; impression ; accessibilité du nouvel espace (axe-core non rejoué).
4. Annulation de décision : seulement la dernière décision d'un workflow non clos dont l'effet n'est pas appliqué ; impossible pour les décisions antérieures à la v3.
5. « Options » : retard estimé à partir des durées prévues, sans les attentes ni les imprévus.
6. Graphiques Sécurité : pas de vraies données d'incidents ou de vulnérabilités.
7. Découpage en modules : seulement proposé (fichier unique de 1,2 Mo).
8. Notifications de la simulation annoncées au lecteur d'écran : envahissantes en vitesse ×3 ou ×8.
9. Option écartée pour le Pilotage : bandeau « Prochaines actions » visible dans toutes les sous-vues.

## Pour la prochaine conversation
Joindre ce fichier et le HTML final, puis donner en un seul message : les décisions sur le point 1, les données réelles du point 2 (en fichier), et la liste des défauts trouvés au point 3. Demander des tests ciblés sur les routes modifiées plutôt qu'un passage complet des 451 routes.
