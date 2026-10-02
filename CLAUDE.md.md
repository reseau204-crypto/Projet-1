# Reprise du travail : cockpit 360° v3

Fichier de référence : `cockpit-360-comprehension-multi-agents-communaute-ia-v3.html` (à joindre à la prochaine conversation).

## État au 2 octobre 2026
Les 7 tâches de la v3 sont faites et testées (Chromium) : contrôle visuel, débordements mobiles, graphiques SVG (Impact, Options, Qualité, Sécurité), actions directes (lever un blocage par escalade, annuler et rouvrir une décision, note au journal), DEMO_DATA, accessibilité, table des matières §01 à §73.
Tests passés : 451 routes à 1440, 820, 390 et 360 px sans erreur ni débordement ; 55/55 vérifications fonctionnelles ; axe-core sans violation WCAG A/AA ; 131/176 vues de l’Atlas identiques à la v2 (les 45 autres : accords « (s) » ou bandeau démo seulement).

## Reste à faire
1. Valider les définitions des filtres « Problèmes & Décisions » et « Résultats & Contrôle ».
2. Remplacer DEMO_DATA (section §02) par les données réelles : bénéficiaires, budgets, coûts, fournisseurs, contrats, registre des traitements.
3. Tester sur Safari / iPhone, Firefox, et avec un lecteur d’écran (NVDA, VoiceOver, TalkBack) ; zoom 200 % ; impression.
4. Annulation de décision : seulement la dernière décision d’un workflow non clos dont l’effet n’est pas appliqué ; impossible pour les décisions antérieures à la v3.
5. « Options » : retard estimé à partir des durées prévues, sans les attentes ni les imprévus.
6. Graphiques Sécurité : pas de vraies données d’incidents ou de vulnérabilités.
7. Découpage en modules : seulement proposé (fichier unique de 1,2 Mo).
8. Notifications de la simulation annoncées au lecteur d’écran : envahissantes en vitesse ×3 ou ×8.

## Pour la prochaine conversation
Joindre ce fichier et le HTML v3, puis donner en un seul message : les décisions sur le point 1, les données réelles du point 2 (en fichier), et la liste des défauts trouvés au point 3. Demander des tests ciblés sur les routes modifiées plutôt qu’un passage complet des 451 routes.
