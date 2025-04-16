# Compact Object

## Interview Question

Étant donné un objet ou un tableau obj, renvoie un objet compact.

Un objet compact est identique à l'objet d'origine, à la différence que les clés contenant des valeurs fausses sont supprimées. Cette opération s'applique à l'objet et à tous les objets imbriqués. Les tableaux sont considérés comme des objets dont les indices sont des clés. Une valeur est considérée comme fausse lorsque Boolean(value) renvoie false.

On peut supposer que l'objet obj est le résultat de JSON.parse. Autrement dit, il s'agit d'un JSON valide.

## Processus de résolution

### 1 - Problème Posé

Créer une fonction qui prend un objet ou un tableau d'objet puis retourne une version compacter.

### 2 - Comment ça marche

La fonction prend un objet ou un tableau (potentiellement imbriqué), supprime toutes les clés ayant des valeurs falsy, et retourne un nouvel objet ou tableau nettoyé en profondeur.

### 3 - Approche

Détecter si obj est un tableau en utilisant la méthode Array.isArray(obj) puis vérifier si obj est un objet non null ensuite appliquer récursivement la fonction sur chaque valeur.Pour finir supprimer toutes les valeurs où Boolean(value) === false.

## Pratique

```js
/**
 * @param {Object|Array} obj
 * @return {Object|Array}
 */
var compactObject = function (obj) {
  if (Array.isArray(obj)) {
    const result = [];
    for (const val of obj) {
      const compacted = compactObject(val);
      if (Boolean(compacted)) {
        result.push(compacted);
      }
    }
    return result;
  }

  if (obj !== null && typeof obj === "object") {
    const result = {};
    for (const key in obj) {
      const compacted = compactObject(obj[key]);
      if (Boolean(compacted)) {
        result[key] = compacted;
      }
    }
    return result;
  }

  return obj;
};
```

## Résultat

![Résultat capture](./compactObj-srceenshot.png)
