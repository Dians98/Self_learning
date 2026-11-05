# Plan — cursus js-ts-nextjs

Fil rouge : budget manager (voir [brief.md](brief.md)). Statuts : ⬜ à faire · 🟡 en cours · ✅ validé · ⏭️ forcé

Stack vérifiée le 2026-11-04 : Next.js 16 (App Router), Prisma 7 (SQLite via `@prisma/adapter-better-sqlite3`), Vitest. Versions exactes revérifiées au début de chaque module.

## Module 1 — JS avancé
`app/` = projet Node (ESM) + Vitest, fichiers `.js`.

| # | Concept | Objectif / use case | Ce que le TP ajoute à l'app | Statut |
|---|---|---|---|---|
| 01 | Arrow functions et `this` | Écrire des petites fonctions concises ; comprendre pourquoi `this` change dans un callback | Setup du projet + `lib/money.js` : convertir un montant saisi en cents, formater des cents en `Rs 1 250,00`. Bonus : le piège `this` | 🟡 |
| 02 | Destructuring, spread / rest | Lire les champs d'un objet et produire une version modifiée **sans muter l'original** | `lib/month.js` : créer un mois, ajouter un revenu, une dépense fixe, un budget, une dépense — chaque fonction renvoie un nouveau mois | ⬜ |
| 03 | `map` / `filter` / `reduce` / `find` | Calculer des totaux et extraire des sous-ensembles d'une liste | Total des revenus et des fixes, dépensé et reste par budget, reste libre, total cash à retirer ; `startNextMonth(mois, montantReçu)` qui prépare le mois suivant (fixes et budgets recopiés, dépensé remis à zéro) | ⬜ |
| 04 | Closures et portée | Créer des fonctions "pré-configurées" qui gardent un état privé | Générateur d'ids de dépenses, alerte de budget configurable (ex. 80 % consommé) | ⬜ |
| 05 | Modules ES | Découper et organiser le code, exports nommés vs default | Réorganiser `lib/`, script `npm run report` qui affiche le bilan d'un mois dans le terminal | ⬜ |
| 06 | Promises (+ event loop) | Gérer une opération qui prend du temps sans bloquer | `lib/storage.js` : sauvegarder / charger un mois en JSON avec `fs/promises` et `.then()`. Bonus : prédire l'ordre des logs | ⬜ |
| 07 | `async` / `await` et `try/catch` | Écrire du code asynchrone lisible et gérer ses erreurs | Réécrire `storage` en async/await ; fichier absent → mois vide ; JSON corrompu → erreur claire | ⬜ |
| 08 | `fetch` | Appeler une API HTTP, vérifier la réponse, gérer les erreurs réseau | **Bonus hors fil rouge** (`bonus/08-fetch/`) sur une API publique | ⬜ |
| 09 | `?.` et `??` | Gérer proprement les données optionnelles ; le piège `\|\|` avec 0 | Note facultative d'une dépense, budget introuvable, corriger un bug où un montant 0 est traité comme absent | ⬜ |

## Module 2 — TypeScript
Migration de `app/` en TS, `strict` activé, `tsc --noEmit` dans la validation.

| # | Concept | Objectif / use case | Ce que le TP ajoute à l'app | Statut |
|---|---|---|---|---|
| 10 | Pourquoi TS, setup, types de base, inférence | Attraper les erreurs avant l'exécution | Setup TS, migrer `money` en `.ts` | ⬜ |
| 11 | Types d'objets : `type` / `interface`, optionnels, `readonly` | Décrire la forme des données une fois pour toutes | Types `Month`, `Budget`, `FixedExpense`, `Expense` ; migrer `month` | ⬜ |
| 12 | Unions, literal types, narrowing | Restreindre une valeur à quelques possibilités et raisonner dessus | `'cash' \| 'compte'`, parser une saisie texte en emplacement valide | ⬜ |
| 13 | Unions discriminées et exhaustivité (`never`) | Modéliser "l'un OU l'autre" sans champs incohérents | Dépense **dans un budget** vs **hors budget** ; `switch` exhaustif | ⬜ |
| 14 | Fonctions typées et generics | Écrire un utilitaire réutilisable sur n'importe quel type | `sumBy`, `groupBy` génériques ; refactor des calculs | ⬜ |
| 15 | Utility types (`Partial`, `Pick`, `Omit`, `Record`) | Dériver des types au lieu de les dupliquer | `updateBudget(…, changes: Partial<…>)`, `NewExpense`, totaux par emplacement | ⬜ |
| 16 | `unknown` et type guards | Valider des données venues de l'extérieur (fichier, formulaire) | Valider le JSON chargé par `storage` avant de l'utiliser | ⬜ |

## Module 3 — Bases de React (dans Next)
Création du projet Next, `lib/` est repris tel quel.

| # | Concept | Objectif / use case | Ce que le TP ajoute à l'app | Statut |
|---|---|---|---|---|
| 17 | Projet Next, JSX, composants | Découper une interface en briques réutilisables | Page qui affiche un mois d'exemple : `MonthSummary`, `BudgetCard` | ⬜ |
| 18 | Props typées, `children`, composition | Rendre un composant configurable | `BudgetCard` paramétrable, barre de progression | ⬜ |
| 19 | Listes (`key`) et rendu conditionnel | Afficher une collection et ses états | Liste des dépenses, état vide, badge "dépassé" | ⬜ |
| 20 | State (`useState`) et événements, `'use client'` | Réagir aux actions de l'utilisateur | Filtre cash / compte / tous, déplier les dépenses d'un budget | ⬜ |
| 21 | Formulaires contrôlés | Saisir et valider des données | Formulaire d'ajout de dépense (validation via `lib/`) | ⬜ |
| 22 | Remonter l'état, état dérivé (et quand NE PAS utiliser `useEffect`) | Une seule source de vérité, pas de state dupliqué | Formulaire + liste partagent l'état ; les restes se recalculent | ⬜ |

## Module 4 — Next.js (App Router)

| # | Concept | Objectif / use case | Ce que le TP ajoute à l'app | Statut |
|---|---|---|---|---|
| 23 | Routing, layouts, routes dynamiques | Une URL par écran | `/mois/[mois]` (ex. `2026-11`), layout avec navigation entre mois | ⬜ |
| 24 | Server vs Client Components | Lire les données côté serveur, n'envoyer au navigateur que l'interactif | Les pages lisent les mois via `storage` côté serveur | ⬜ |
| 25 | Server Actions | Écrire des données depuis un formulaire sans API à la main | Ajouter / supprimer une dépense, erreurs avec `useActionState` | ⬜ |
| 26 | `loading`, `error`, `not-found` | Gérer attente, erreurs et mois inexistant | Écrans de chargement, d'erreur et 404 | ⬜ |
| 27 | Route Handlers et `fetch` justifié | Exposer une URL qui renvoie un fichier ; savoir quand NE PAS `fetch` | Export CSV d'un mois | ⬜ |

## Module 5 — Base de données (SQLite + Prisma)

| # | Concept | Objectif / use case | Ce que le TP ajoute à l'app | Statut |
|---|---|---|---|---|
| 28 | Rappel relations, schéma Prisma, migrations | Décrire la BDD et ses relations en code | Modèles `Month`, `FixedExpense`, `Budget`, `Expense` ; première migration | ⬜ |
| 29 | Lire avec Prisma (relations, `include`) | Charger un mois complet en une requête | Les pages lisent la BDD au lieu du JSON | ⬜ |
| 30 | Écrire avec Prisma (create / update / delete) | Persister les actions de l'utilisateur | Server Actions branchées sur la BDD | ⬜ |
| 31 | Transactions, démarrer le mois suivant | Plusieurs écritures qui réussissent ou échouent ensemble | "Démarrer le mois suivant" : saisie du montant reçu, création du mois avec fixes et budgets recopiés, le tout en une transaction | ⬜ |
| 32 | TP avancé : report du reliquat | Logique métier complète de bout en bout | Option de report des restes de budgets sur le mois suivant | ⬜ |

**Bonus éventuel** : interface mobile et déploiement.
