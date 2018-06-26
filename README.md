# ECMAScript 2015 (ES6)

<p align="center">
  <img width="600" src="https://raw.githubusercontent.com/drihu/aprende-es6/master/img/es6.png">
</p>

> Traducido originalmente del repo [es6features](https://github.com/lukehoban/es6features).

## Introducción

> ECMAScript 2015 es un stándar de ECMAScript ratificado en junio de 2015.

ES6, también conocido como ECMAScript 6 o ECMAScript 2015, es una mejora significativa al lenguaje desde que ES5 fue estandarizado en 2009. La implementación de estas características en motores principales de JavaScript está [actualmente en marcha](http://kangax.github.io/compat-table/es6/).

Mira el [estándar ES6](http://www.ecma-international.org/ecma-262/6.0/) para la especificación completa del lenguaje ECMAScript.

ES6 incluye las siguientes nuevas características:

* [let + const](#let-+-const)
* [ámbito](#ámbito)
* [funciones flecha](#funciones-flecha)
* [clases](#clases)

## Características de ECMAScript 6

### let + const

Instrucciones con ámbito de bloque (un bloque es un conjunto de sentencias encerradas entre `{` y `}`). `let` es el nuevo var. `const` es de asignación única. Las restricciones estáticas previenen el uso antes de la asignación.

```javascript
{
  let x;
  {
    const x = 'sneaky'; // ok, constante con ámbito de bloque
    x = 'bar'; // error, variable constante
  }
  let x = 'inner'; // error, ya declarado en el bloque
  x = 'bat'; // ok, reasigna un valor a la variable
}
```

Más información: [MDN Let statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), [MDN Const statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

### Ámbito

Las variables y funciones definidas dentro de un bloque (código entre `{` y `}`) son accesibles únicamente dentro del mismo bloque.

```javascript
for (let i = 0; i < arr.length; i++) {
  let x = arr[i]; // ok, i está definido para el bloque 'for'
}
console.log(i); // error, i no está definido

function foo() {
  function bar() {
    return 'bar';
  }
  bar(); // ok, bar está definido dentro de 'foo'
}
bar(); // error, bar no está definido
```

### Funciones Flecha

Las funciones flecha son funciones de rápida escritura usando la sintaxis `=>`. Son sintácticamente similares a la característica relacionada en C#, Java 8 y CoffeeScript. Admiten ambos cuerpos como bloques de sentencias que devuelven el valor de la expresión. A diferencia de las funciones tradicionales, las funciones flecha comparten el mismo `this` que el código que los rodea.

```javascript
// Cuerpos como expresión
const odds = evens.map(v => v + 1);
const nums = evens.map((v, i) => v + i);
const pairs = evens.map(v => ({even: v, odd: v + 1}));

// Cuerpos como declaración
nums.forEach(v => {
  if (v % 5 === 0) fives.push(v);
});

// Palabra clave 'this'
const bob = {
  name: 'Bob',
  friends: [],
  printFriends() {
    this.friends.forEach(f => console.log(this.name + ' knows ' + f));
  }
}
```

Más información: [MDN Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

### Clases

Las clases en ES6 son un simple azúcar sobre el patrón OO (orientado a objetos) basado en prototipos. Tener una única forma declarativa conveniente hace que los patrones de clase sean más fáciles de usar y fomenta la interorperabilidad. Las clases admiten herencia basada en prototipos, llamadas al método 'super', instancias, constructores y métodos estáticos.

```javascript
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }

  update(camera) {
    //...
    super.update();
  }

  get boneCount() {
    return this.bones.length;
  }

  set matrixType(matrixType) {
    this.idMatrix = SkinnedMesh[matrixType]();
  }

  static defaultMatrix() {
    return new THREE.Matrix4();
  }
}
```

Más información: [MDN Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
