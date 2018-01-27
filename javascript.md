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
typeof a;   // "undefined"

a = "hello world";
typeof a;   // "string"

a = 42;
typeof a;   // "number"

a = true;
typeof a;   // "boolean"

a = null;
typeof a;   // "object" — ЙОПТА! Давній баг. Не виправляють, бо тупо багато коду спирається не нього.

a = undefined;
typeof a;   // "undefined"

a = { b: "c" };
typeof a;   // "object"

a = Symbol();
typeof a;   // "symbol"

a = function() {}
typeof a;   // "function"
```
`typeof null` - давній баг. Не виправляють, бо тупо багато коду спирається не нього.

# Objects
```js
obj.a;      // "hello world"
```
```js
obj["a"];   // "hello world"
```
"Лапкова" нотація може використовуватись, коли ім`я властивості зберігається в змінній 
або властивість містить спеціальні символи.

# Built-In Type Methods


# Shadowing variables when we have the 2 vars with the same name in different scopes.

# Compiling
Javascript Engine компілює програму в 2 кроки.
1. Find Formal Declaration - проходимось по всіх дефайнінгах змінних, функції, etc.
Запихаємо всі змінні і функції у відповідну коробку(Lexical Environment), яка і буде Scope(Або не буде, можливо не до кінця одне і те саме).
Самий верхній scope - global scope.
2. Runtime(execution) - робить всі операції, assigning, function execution, etc. 
Якшо знаходить змінну, яка не є задефайнена, видасть помилку(в strict mode).

# Use Strict
`"use strict;"` - запуск скрипта в правилах es5, допомагая оптимізувати код. 
В більшості випадків, якшо не дотримуватись його, код буде виконуватись помаліше.
Наприклад, якшо (implicit defining)ми не задефайнили змінну і Javascript Engine задефайнив її(в global scope)
при 2 кроці компіляції - це набагато помаліше.

#Undefined and Not Defined(Not Declared)
Undefined - задефайнина змінна, в якої нема значення.

Not Defined - не задефайнили змінну.

# LHS & RHS (Left-Hand Side and Right-Hand Side)
LHS - target reference, коли ми дефайнимо змінну, функцію

RHS - source reference, коли ми есайнимо значення змінній, виконання функції.

# Function Declaration, Function Expression(anonymus) and Named Function Expression

Якшо потрібно писати Function Expression, то краще вибрати Named Function Expression, тому шо:
1. Handy function self-reference. Можна всередині функції викликати herself. Fuck recursion!
2. More debuggable stack traces. В консольці замість anonymus function буде ім`я проблемної функції. Profit!
3. More self-documenting code. Ти будеш знати, шо робить ця функція з її імені(при умові, шо ти не мудак, і норм назвеш). 
А шо ти будеш знати з анонімної фунції?! Fuckin Amazing!


# Lexical Scope

```js
var foo = function bar() {
    var foo = "baz";

    function baz(foo) {
        foo = bar;
        foo;   //function
    }
    baz();
};

foo();
bar();   //error
```
Error, тому шо в функція bar об`явлена не як Function Declaration(слово function - перше в statement),
а як Named Function Expression і належить internal scope.
Іншими словами Function Declaration аттачить саму функції до external scope і її можна буде викликати в ньому,
а Function Expression і Named Function Expression - HI.

# Lexical Scope vs Dynamic Scope
Більшість мов мають або Lexical Scope, або Dynamic Scope.
В Javascript, як я розумію, можна використовувати обидва підходи.

Lexical Scope is predictable.

Dynamic Scope is flexibale.

### Lexical Scope
```js
function foo() {
    var bar = "bar";

    function baz() {
        console.log(bar);   //lexical!
    }
    baz();
}
foo();
```
### Dynamic Scope
```js
//theoretical dynamic scoping
function foo() {
    console.log(bar);   //dynamic!
}

function baz() {
    var bar = "bar";
    foo();
}

baz();
```

# Try Catch
```js
var foo;
try {
    foo.length;
}
catch err {
    console.log(err);   //TypeError
}
};

console.log(err);   // ReferenceError
```

# IIFE(Immediately-Invoked Function Expression)
```js
var foo = "foo"

// ..

var foo = "foo2";
console.log(foo);   // "foo2"

// ..

console.log(foo);   // "foo2" -- oops!
```
Коли в нас є великий проект якіта, і ми задефайнили foo, крім нас є ше чуваки і вони, з якоїсь причини, також задефайнили foo, в результаті
вийшов трабл. Шоб уникнути цього і інкапсулюватись можна просто створити Scope.
Інкапсуляція - винесення всіх даних і функцій, об`єднаних одним сенсом, в єдину сутність(в javascript це робиться через функції, в інших мовах через модифікатори доступу).
При цьому для користувача дані ховаються в сутності і доступні тільки всередині неї.
unit of scope - function.
Але, для прикладу, в es6
```js
function diff(x,y) {
    if (x > y) {
        let tmp = x;
        x = y;
        y = tmp;
    }
}
```
Тут `tmp` не належить Scope of diff.
`tmp` належить Scope of `if (x > y)`.
Але в `if (x > y)` нема Scope.
Не біда, `let` його створить. Створить Scope з Lexical Environment(нашу коробку) і добавить туди `tmp`
fantastisch!
```js
var foo = "foo"

function bob() {
    var foo = "foo2";
    console.log(foo);
}
bob();

console.log(foo);   // "foo" -- nice!
```
Але нам потрібно визвати цю функцію `bob()`, тому шо це Function Declaration.
А якийсь мудак назве свою функцію так само, це не вирішить наш трабл до кінця. 
Тоді ми перетворимо функцію в Function Expression!
```js
var foo = "foo"

( function bob() {
    var foo = "foo2";
    console.log(foo);
} )();

console.log(foo);   // "foo" -- nice!
```
Чому це Function Expression?Дуже просто, тому шо слова function не є першим в statement :)
І це означає, шо 'bob' вже є в іншому(своєму) scope. І виконується сама негайно immediately.


