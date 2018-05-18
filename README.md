# Best practices for javascript


## var versus let / const

> Besides `var`, we now have access to two new identifiers for storing values
—`let` and `const`. Unlike `var`, `let` and `const` statements are not hoisted
to the top of their enclosing scope.

An example of using `var`:

```javascript
var name = 'Manjula';

function getName(name) {
    if (name) {
        var name = 'Tom';
        return name;
    }
    return name;
}

getName(false); // undefined
```

However, observe what happens when we replace `var` using `let`:

```javascript
let name = 'Manjula';

function getName(name) {
    if (name) {
        let name = 'Tom';
        return name;
    }
    return name;
}

getFood(false); // 'Manjula'
```

This change in behavior highlights that we need to be careful when refactoring
legacy code which uses `var`. Blindly replacing instances of `var` with `let`
may lead to unexpected behavior.

> **Note**: `let` and `const` are block scoped. Therefore, referencing
block-scoped identifiers before they are defined will produce
a `ReferenceError`.

```javascript
console.log(x); // ReferenceError: x is not defined

let x = 'hi';
```

> **Best Practice**: Leave `var` declarations inside of legacy code to denote
that it needs to be carefully refactored. When working on a new codebase, use
`let` for variables that will change their value over time, and `const` for
variables which cannot be reassigned.
