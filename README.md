# Best practices for Javascript


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

### .includes( )

```javascript
var string = 'name';
var substring = 'am';

console.log(string.indexOf(substring) > -1);
```

Instead of checking for a return value `> -1` to denote string containment,
we can simply use `.includes()` which will return a boolean:

```javascript
var string = 'name';
var substring = 'am';

console.log(string.includes(substring)); // true
```

### .repeat( )

```javascript
function repeat(string, count) {
    var strings = [];
    while(strings.length < count) {
        strings.push(string);
    }
    return strings.join('');
}
```

In ES6, we now have access to a terser implementation:

```javascript
// String.repeat(numberOfRepetitions)
'Manjula'.repeat(3); // 'ManjulaManjulaManjula'
```

### Template Literals

Using **Template Literals**, we can now construct strings that have special
characters in them without needing to escape them explicitly.

```javascript
var text = "This string contains \"double quotes\" which are escaped.";
```

```javascript
let text = `This string contains "double quotes" which don't need to be escaped anymore.`;
```

**Template Literals** also support interpolation, which makes the task of
concatenating strings and values:

```javascript
var name = 'Tiger';
var age = 13;

console.log('My cat is named ' + name + ' and is ' + age + ' years old.');
```

Much simpler:

```javascript
const name = 'Tiger';
const age = 13;

console.log(`My cat is named ${name} and is ${age} years old.`);
```

In ES5, we handled new lines as follows:

```javascript
var text = (
    'cat\n' +
    'dog\n' +
    'nickelodeon'
);
```

Or:

```javascript
var text = [
    'cat',
    'dog',
    'nickelodeon'
].join('\n');
```

**Template Literals** will preserve new lines for us without having to
explicitly place them in:

```javascript
let text = ( `cat
dog
nickelodeon`
);
```

## Destructuring

Destructuring allows us to extract values from arrays and objects (even deeply
nested) and store them in variables with a more convenient syntax.

### Destructuring Arrays

```javascript
var arr = [1, 2, 3, 4];
var a = arr[0];
var b = arr[1];
var c = arr[2];
var d = arr[3];
```

```javascript
let [a, b, c, d] = [1, 2, 3, 4];

console.log(a); // 1
console.log(b); // 2
```

### Destructuring Objects

```javascript
var details = { occupation: 'software engineer', name: 'manjula' };
var occupation = details.occupation; // 'software engineer'
var name = details.name; // 'anakin'
```

```javascript
let details = { occupation: 'software engineer', name: 'manjula' };
let {occupation, name} = details;

console.log(occupation); // 'software engineer'
console.log(name); // 'manjula'
```

