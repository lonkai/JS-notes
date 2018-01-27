# Statement 
Інструкція, відділяється `;`.

# Expression
Вираз, не завжди якась операція, може бути просто число чи змінна.

В дужках всі expressions `((a) = ((b) * (2)));`

Очевидно, шо разом це Statement.

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
Javasript Engine – те, шо перетворює Javascript на код нижчого рівня, встроєний в більшість браузерів.

Javascript – мова скриптів, її вважають інтерпретуючою мовою, тому шо ми считуємо стейтмент за стейтментом. Коли ми виконуємо 3 стейтмент, ми не знаємо, шо буде в 5 стейтменті. Але це не зовсім так. Javascript схожий на компілюючу мову, де спочатку Javascript Engine проходить весь код, якшо код коректний, тоді ранить його(2 етапи). В Javascript програмі, коли є два стейтменти і один з них неправильний, перший стейтмент не зараниться.

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
Об’єднання Statements
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
"Лапкова" нотація може використовуватись, коли ім'я властивості зберігається в змінній 
або властивість містить спеціальні символи.

# Built-In Type Methods


# Shadowing variables when we have the 2 vars with the same name in different Scopes.

# Compiling
Javascript Engine компілює програму в 2 кроки.
1. Find Formal Declaration - проходимось по всіх дефайнінгах змінних, функції, etc.
Запихаємо всі змінні і функції у відповідну коробку(Lexical Environment), яка і буде Scope(Або не буде, можливо не до кінця одне і те саме).
Самий верхній Scope - global Scope.
2. Runtime(execution) - робить всі операції, assigning, function execution, etc. 
Якшо знаходить змінну, яка не є задефайнена, видасть помилку(в Strict Mode).

# Use Strict
`"use strict;"` - запуск скрипта в правилах es5, допомагая оптимізувати код. 
В більшості випадків, якшо не дотримуватись його, код буде виконуватись помаліше.
Наприклад Implicit Defining, якшо ми не задефайнили змінну і Javascript Engine задефайнив її(в global Scope)
при 2 кроці компіляції - це набагато помаліше.

# Undefined and Not Defined(Not Declared)
`Undefined` - задефайнена змінна, існує в Scope, але не має значення.

`Undeclared`,`Not Defined` - не існує, не задефайнена змінна в Scope.

# LHS & RHS (Left-Hand Side and Right-Hand Side)
LHS - target reference, коли ми дефайнимо змінну, функцію.

RHS - source reference, коли ми есайнимо значення змінній, виконання функції.

# Function Declaration, Function Expression(anonymus) and Named Function Expression

Якшо потрібно писати Function Expression, то краще вибрати Named Function Expression, тому шо:
1. Handy function self-reference. Можна всередині функції викликати herself. Fuck recursion!
2. More debuggable stack traces. В консольці замість anonymus function буде ім'я проблемної функції. Profit!
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
Error, тому шо в функція `bar` об'явлена не як Function Declaration(слово function - перше в Statement),
а як Named Function Expression і належить internal Scope.
Іншими словами Function Declaration аттачить саму функції до external Scope і її можна буде викликати в ньому,
а Function Expression і Named Function Expression - HI.

# Lexical Scope vs Dynamic Scope
Більшість мов мають або Lexical Scope, або Dynamic Scope.
В Javascript є тільки Lexical Scope.

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
catch (err) {
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
Інкапсуляція - винесення всіх даних і функцій, об`єднаних одним сенсом, в єдину сутність(в Javascript це робиться через функції, в інших мовах через модифікатори доступу).
При цьому для користувача дані ховаються в сутності і доступні тільки всередині неї.
unit of Scope - function. Але в es6 за допомогою `let` ми можем робити Block Scoping.

```js
var foo = "foo"

function bob() {
    var foo = "foo2";
    console.log(foo);
}
bob();

console.log(foo);   // "foo" -- nice, but..
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

console.log(foo);   // "foo" -- perfect!
```
Чому це Function Expression?Дуже просто, тому шо слова function не є першим в Statement :)
І це означає, шо `bob` вже є в іншому(своєму) Scope. І виконується immediately сама.

# Block Scoping
### let
```js
function diff(x,y) {
    if (x > y) {
        let tmp = x;
        x = y;
        y = tmp;
    }
    console.log(tmp);   // ReferenceRrror
    return y - x;
}
```
Тут `tmp` не належить Scope of `diff`.
`tmp` належить Scope of `if (x > y)`.
Але в `if (x > y)` нема Scope.
Не біда, `let` його створить. Створить Scope з Lexical Environment(нашу коробку) і добавить туди `tmp`
fantastisch!

```js
function repeat(fn,n) {
    var result;

    for (let i = 0; i < n; i++) {
        result = fn(result,i);
    }
}
```
Тут ми юзаєм `let` бо ми не хочем доступатись до `i` out of Scope of `for`.
Але, є випадки, коли нам це потрібно, тоді ми пишемо `var`.
Тому не треба просто замінювати `var` на `let`, більш useful використовувати `let` + `var`.
### var vs let
Наприклад, тут `var > let`
```js
function lookupRecord(searchStr) {
    try {
        var id = getRecord(searchStr);
    }
    catch (err) {
        var id = -1;
    }
    return id;
}
```
`var` ми можемо заюзати багато разів, коли повторний `let` верне нам помилку.
Ми декларуємо змінну на 5 лінійці, на 1000 ми можемо ше раз задекларувати, шоб легше знайти, кому належить змінна.
З `let` ми цього не зробимо.
Кайл базарить, шо об'явити один раз всі змінні зверху це не така і хороша ідея.
Краще об'являти змінні там, де вони юзаються в рамках одного скріна. 

### const
```js
var a = 2;
a++;   // 3

const b = 2;
b++   // Error!

const c = [2];
c[0]++;   // 3 <--- oops!?
```
Є типова помилка. `const` - змінна, яка не може бути переесайнена, а не змінна, яка не може змінитись.
Краще не піхати в `const` массиви, функції, об'єкти.
const працює так, як `let` і робить Block Scoping.

### Explicit let block
```js
function formatStr(str) {
    { let prefix, rest;
        prefix = str.slice (0, 3);
        rest = str.slice (3);
        str = prefix.toUpperCase() + rest;
    }

    if (/^F00:/.test(str)) {
        return str;
    }
    return str.slice(4);
}
```
Таке можна творити, Кайл рекомендує.

# Quiz

Три шляхи створення new scoped variable:
1. let в блоці чи функції
2. var в функції
3. catch (err)

