# Carnet d'erreurs — cursus js-ts-nextjs

Chaque erreur faite en TD, TP ou révision, classée par concept : ce que j'ai écrit, la bonne réponse, la règle à retenir.

---

## 01 — Arrow functions et `this`

### Convertir une fonction en arrow function
- **Ce que j'ai écrit :**
  ```js
  function isOverBudget((budget) => {
    return budget.spent > budget.allocated
  })
  ```
- **Bonne réponse :**
  ```js
  const isOverBudget = (budget) => budget.spent > budget.allocated;
  ```
- **Règle :** une arrow function n'a pas de nom. On la range dans une `const`. On ne garde pas le mot `function` : `=>` le remplace, **après** les paramètres.

### Accolades après `=>` = pas de return automatique
- **Ce que j'ai répondu :** `(x) => { x * 2 }` renvoie 10 et `(x) => x * 2` est une erreur de syntaxe.
- **Bonne réponse :** c'est l'inverse. `(x) => { x * 2 }` renvoie `undefined` et `(x) => x * 2` renvoie `10`.
- **Règle :** `=>` suivi de `{` ouvre un bloc d'instructions. Sans `return`, la fonction renvoie `undefined`. Si autre chose suit `=>`, cette expression est la valeur retournée.
- ✅ Corrigé dans la foulée (Q3 / Q4 justes).
