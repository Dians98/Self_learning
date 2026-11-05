# Brief — cursus js-ts-nextjs

Décisions validées avec l'apprenant (2026-11-04). Ne pas modifier sans son accord.

## Apprenant

- Sait déjà programmer et connaît SQL.
- **Aucun parallèle avec PHP** dans les explications.
- JS : ne pas repartir de zéro (variables, boucles, conditions acquises) ; commencer aux concepts avancés.
- Objectif : être autonome et propre en TypeScript + Next.js sur de vrais projets pro.
- Rythme : séances de 1 h à 1 h 30 (TD ~30 min, TP ~45 min).
- Langue : français ; termes techniques et code en anglais.
- **Conception = le senior.** L'apprenant ne veut pas réfléchir à la logique métier ni à l'architecture : le senior conçoit tout et donne les consignes de TP en langage naturel ("fais ça, puis ça"). L'apprenant code.

## Parcours (dans cet ordre)

1. **JS avancé** : arrow functions et `this` · destructuring, spread / rest · `map` / `filter` / `reduce` / `find` · closures et portée · modules ES · Promises (+ event loop, juste ce qu'il faut) · `async` / `await` et `try/catch` · `fetch` (TP bonus sur une API publique, hors fil rouge) · `?.` et `??`
2. **TypeScript** (détail fixé dans le plan)
3. **Bases de React**, directement dans Next : composants, props, state, événements, formulaires
4. **Next.js (App Router)** : routing et layouts, Server / Client Components, Server Actions, Route Handlers. `fetch` réutilisé là où il est justifié (ex. Route Handler d'export CSV, ou recherche en direct côté client) — et expliquer pourquoi on ne l'utilise PAS pour lire ses propres données (Server Components lisent la BDD directement).
5. **Base de données** : SQLite + Prisma. Rappel rapide des relations seulement, pas de deep dive SQL.

Next.js et non React/Vite seul. Vérifier les versions actuelles dans la doc au moment du plan.

## Fil rouge : budget manager (usage réel, sur PC)

Modèle :
- **Cycle** : en fin de mois, l'apprenant reçoit son salaire (montant **variable**) et clique sur "Démarrer le mois suivant" en saisissant le montant reçu. Ce montant finance le **mois à parcourir**, qui porte son nom (salaire reçu fin novembre → "Décembre 2026"). Les dépenses fixes et les budgets du mois précédent sont recopiés comme modèle (montants modifiables), le dépensé repart à zéro.
- Un **mois** : un ou plusieurs **revenus** (salaire + éventuels extras en cours de mois, chacun avec description et montant), dépenses fixes, budgets.
- Un **budget** : montant alloué mis de côté, emplacement `cash` ou `compte`, liste de dépenses → reste = alloué − dépensé.
- **Dépenses variables** : rattachées à un budget **ou** hors budget (prises sur le reste libre). Toujours une **description**.
- **Reste libre** = total des revenus − dépenses fixes − budgets alloués − dépenses hors budget.
- Fin de mois : les budgets repartent à zéro. Le report du reliquat sur le mois suivant = TP avancé en fin de cursus.
- Devise unique : **roupie mauricienne (MUR, Rs)**. Montants stockés en **cents (entiers)**.
- Pas d'authentification (local, un seul utilisateur). Mobile / déploiement = bonus éventuel.

Exemple de mois :

```
Décembre 2026  (financé par le salaire reçu fin novembre)
  Revenus                     Rs 50 000   (salaire reçu le 28/11)
  Dépenses fixes              - Rs 18 000
  Budgets mis de côté         - Rs 12 000
     Courses   Rs 8 000 [compte]  dépensé Rs 2 500 → reste Rs 5 500
     Essence   Rs 3 000 [cash]    dépensé Rs 1 200 → reste Rs 1 800
     Loisirs   Rs 1 000 [cash]    dépensé Rs     0 → reste Rs 1 000
  Reste libre                 Rs 20 000
```

Évolution prévue de `app/` : modules 1-2 = projet Node (logique métier dans `lib/` + Vitest), JS puis migration en TS ; modules 3-5 = projet Next qui reprend `lib/`, puis persistance SQLite/Prisma.

## Validation des TP

- Tests Vitest sur la logique métier (`lib/` : calculs de restes, reste libre, conversion en cents, validation des saisies) — fournis par le senior, `fetch` mocké.
- Review du senior sans point bloquant.
- Checklist manuelle pour l'interface (modules 3+).
- Commit par le senior à chaque TP validé.
