# ECMAScript 2015 (ES6)

> Traducido originalmente del repo [es6features](https://github.com/lukehoban/es6features).

## Introducción

> ECMAScript 2015 es un stándar de ECMAScript ratificado en junio de 2015.

ES6, también conocido como ECMAScript 6 o ECMAScript 2015, es una mejora significativa al lenguaje desde que ES5 fue estandarizado en 2009. La implementación de estas características en motores principales de JavaScript está [actualmente en marcha](http://kangax.github.io/compat-table/es6/).

Mira el [estándar ES6](http://www.ecma-international.org/ecma-262/6.0/) para la especificación completa del lenguaje ECMAScript.

ES6 incluye las siguientes nuevas características:

* [let + const](#let-+-const)
* [ámbito](#ámbito)
* [funciones flecha](#funciones-flecha)

## Características de ECMAScript 6

### let + const

Instrucciones con ámbito de bloque (un bloque es un conjunto de sentencias encerradas entre `{` y `}`). `let` es el nuevo var. `const` es de asignación única. Las restricciones estáticas previenen el uso antes de la asignación.

```javascript
{
  let x;
  {
    // ok, constante con ámbito de bloque
    const x = 'sneaky';
    // error, variable constante
    x = 'bar';
  }
  // error, ya declarado en el bloque
  let x = 'inner';
  // ok, reasigna un valor a la variable
  x = 'bat';
}
```

Más información: [MDN Let statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), [MDN Const statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

### Ámbito

Las variables y funciones definidas dentro de un bloque (código entre `{` y `}`) son accesibles únicamente dentro del mismo bloque.

```javascript
for (let i = 0; i < arr.length; i++) {
  // ok, i está definido para el bloque 'for'
  let x = arr[i];
}
// error, i no está definido
console.log(i);

function foo() {
  function bar() {
    return 'bar';
  }
  // ok, bar está definido dentro de 'foo'
  bar();
}
// error, bar no está definido
bar();
```

### Funciones Flecha

Las funciones flecha son funciones de rápida escritura usando la sintaxis `=>`. Son sintácticamente similares a la característica relacionada en C#, Java 8 y CoffeeScript. Admiten ambos cuerpos como bloques de sentencias que devuelven el valor de la expresión. A diferencia de las funciones clásicas, las funciones flecha comparten el mismo `this` que el código que los rodea.

```javascript
// Cuerpos de expresión
const odds = evens.map(v => v + 1);
const nums = evens.map((v, i) => v + i);
const pairs = evens.map(v => ({even: v, odd: v + 1}));

// Cuerpos de sentencia
nums.forEach(v => {
  if (v % 5 === 0) fives.push(v);
});

// Palabra clave this
const bob = {
  name: 'Bob',
  friends: [],
  printFriends() {
    this.friends.forEach(f => console.log(this.name + ' knows ' + f));
  }
}
```

Más información: [MDN Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
