# Statement 
Інструкція, відділяється `;`.

# Expression
Вираз, не завжди якась операція, може бути просто число чи змінна.

В дужках всі expressions `((a) = ((b) * (2)));`

Очевидно, шо разом це statement.

`a = b * 2 + foo(c * 3);` - так, як в  нас вже є (), юзанем [].

`[ [a] = [ [ [b] * [2] ] + [ [foo]([ [c] * [3] ]) ] ] ];`

`*` має більший пріоритет, ніж `+`, шоб обійти це, можна виділити дужками потрібну операцію.

# Programming LVL
```js
Set the variable a to the value 2 - highest lvl programming
a = 2
mov 2,a
10010100101010101011110101010101010101011110 - lowest lvl programming
```
Javasript engine – те, шо перетворює javascript на код нижчого рівня, встроєний в більшість браузерів.

Javascript – мова скриптів, її вважають інтерпретуючою мовою, тому шо ми считуємо стейтмент за стейтментом. Коли ми виконуємо 3 стейтмент, ми не знаємо, шо буде в 5 стейтменті. Але це не зовсім так. Javascript схожий на компілюючу мову, де спочатку engine проходить весь код, якшо код коректний, тоді ранить його(2 етапи). В Javascript програмі, коли є два стейтменти і один з них неправильний, перший стейтмент не зараниться.

# Conversion and Coersion(not obvious)
Зведення типів.
### Conversion
```js
a = String(a);
b = Number(a);
c = Boolean(a);
```
### Coersion
```js
a = a + "";
```
# Block
Об’єднання statements
```js
{
    var a = 42;
    foo(a / 2);
}
```
Після блоку `;` ставити не потрібно.

# Functions
* `function foo() {}` – function declaration
* `var bar = function() {}` – function expression attached to variable declaration
* `var bar = function baz() {}` – named function expression attached to variable declaration

`function foo(b,bar,zaz) {}` 
b,bar,zaz - параметри

`foo(100);` 
“100” - аргумент

# “Falsy” values:
```js
0
-0
NaN
""
false
null
undefined
```

# Types
* `string`
* `number`
* `boolean`
* `null`
* `undefined`
* `object`
* `symbol` //ES6
### Function and Array are Object subtypes
```js
var a;
typeof a;				// "undefined"

a = "hello world";
typeof a;				// "string"

a = 42;
typeof a;				// "number"

a = true;
typeof a;				// "boolean"

a = null;
typeof a;				// "object" — ЙОПТА! Давній баг. Не виправляють, бо тупо багато коду спирається не нього.

a = undefined;
typeof a;				// "undefined"

a = { b: "c" };
typeof a;				// "object"

a = Symbol();
typeof a;               // "symbol"

a = function() {}
typeof a;               // "function"
```
`typeof null` - давній баг. Не виправляють, бо тупо багато коду спирається не нього.

# Objects
```js
obj.a;                  // "hello world"
```
```js
obj["a"];               // "hello world"
```
"Лапкова" нотація може використовуватись, коли ім`я властивості зберігається в змінній 
або властивість містить спеціальні символи.