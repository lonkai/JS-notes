# Statement 
Інструкція, відділяється `;`.
# Expression
Вираз, не завжди якась операція, може бути просто число чи змінна.

В дужках всі expressions `((a) = ((b) * (2)));`

Очевидно, шо разом це Statement.

`a = b * 2 + foo(c * 3);` - так, як в  нас вже є (), юзаєм [].

`[ [a] = [ [ [b] * [2] ] + [ [foo]([ [c] * [3] ]) ] ] ];`

`*` має більший пріоритет, ніж `+`, шоб обійти це, можна виділити дужками потрібну операцію.
# Programming LVL
```js
Set the variable a to the value 2 - highest lvl programming
a = 2
mov 2,a
10010100101010101011110101010101010101011110 - lowest lvl programming
```
Javasript Engine – те, шо перетворює Javascript на код нижчого рівня. Javasript Engine встроєний в більшість браузерів.

Javascript – мова скриптів, її вважають інтерпретуючою мовою. Але це не зовсім так. Javascript схожий і на компілюючу мову, де спочатку Javascript Engine по суті компілює код зразу перед виконанням і ця компіляція проходить в 2 етапи. В Javascript програмі, коли є 2 стейтменти і один з них неправильний, перший стейтмент не виконається.
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
Block - об’єднання Statements.
```js
{
    var a = 42;
    foo(a / 2);
}
```
Блок виділяти `;` не потрібно.
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
# Objects
```js
obj.a;      // "hello world"
```
```js
obj["a"];   // "hello world"
```
"Лапкова" нотація здебільшого використовується, коли ім'я властивості зберігається в змінній 
або властивість містить спеціальні символи.
# Built-In Type Methods

# Shadowing variables when we have the 2 vars with the same name in different Scopes.

# Compiling
Javascript Engine компілює програму в 2 етапи:
1. Find Formal Declaration - проходимось по LHS, шукаємо декларейшни, проходимось по всіх дефайнінгах змінних і функції(only Function Declaration).
Поміщаємо всі змінні і функції(Function Declaration) у відповідну скриньку(Lexical Environment), яка аттачиться до Scope(по суті Lexical Environment == Lexical Scope, можливо поняття Scope дещо ширше).
Самий верхній Scope - global Scope.

2. Runtime(execution) - проходимось по RHS, виконуємо всі операції, assigning, function execution, etc. 
Якшо знаходить змінну, яка не була задефайнена на 1 етапі компіляції, задефайнить її(Implicit Defining) в Global Scope або видасть помилку(в Strict Mode).
# Use Strict
`"use strict;"` - скрипт виконується згідно правил es5.
Це допоможе уникнути різних непередбачуваних ситуацій і оптимізує наш код.
У більшості випадків, якшо не дотримуватись його, код буде виконуватись значно повільніше.
Наприклад, Implicit Defining, якшо ми не задефайнили змінну і Javascript Engine в Runtime задефайнив її(в Global Scope)
Ця операція буде значно повільніша.
# Undefined and Not Defined(Not Declared)
* `Undefined` - задефайнена змінна, існує в Scope, але не має значення.
* `Undeclared`,`Not Defined` - не існує, не задефайнена змінна в Scope.
# LHS & RHS (Left-Hand Side and Right-Hand Side)
* LHS - target reference, коли ми дефайнимо змінну, функцію(only Function Declaration).
* RHS - source reference, коли ми есайнимо значення змінній, виконання функції.
# Function Declaration, Function Expression(anonymus) and Named Function Expression
Якшо потрібно писати Function Expression, то краще вибрати Named Function Expression, тому шо:
1. Handy function self-reference. Можна всередині функції викликати herself. Fuck recursion!
2. More debuggable stack traces. В консольці замість anonymus function буде ім'я проблемної функції. Profit!
3. More self-documenting code. Ти будеш знати, шо робить ця функція з її імені(якшо назвати її правильно). 
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
Error, тому шо в функція `bar` об'явлена, як Function Expression і належить internal Scope, а не Function Declaration(коли слово function - перше в Statement).
Іншими словами Function Declaration аттачить саму функції до external Scope і її можна буде викликати в ньому, а Function Expression і Named Function Expression - HI.
### Lexical Scope vs Dynamic Scope
Більшість мов мають або Lexical Scope, або Dynamic Scope.
В Javascript є Lexical Scope і є this, яке є джаваскриптовою версією Dynamic Scope.
* Lexical Scope is predictable.
* Dynamic Scope is flexibale.
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
### New Scoped Variable
Як створити змінну в новому Scope. Є 3 шляхи:
1. let в блоці чи функції.
2. var в функції.
3. catch (err).
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
Нехай в нас є великий проект, ми задефайнили змінну foo, але крім нас є ше девелопери і, з якоїсь причини, хтось також задефайнив foo, в результаті
виходить конфуз і зламана функціональність. Шоб уникнути цього, відгородитись, інкапсулюватись можна просто створити Scope.
Інкапсуляція - винесення всіх даних і функцій, об'єднаних одним сенсом, в єдину сутність(в Javascript це робиться через функції, в інших мовах через модифікатори доступу).
При цьому дані, які не потрібні корустувачу приховуються в сутності і доступні тільки всередині неї.
unit of Scope - function. Але в ES6 за допомогою `let` ми можем створювати Block Scoping.
```js
var foo = "foo"

function bob() {
    var foo = "foo2";
    console.log(foo);   // "foo2"
}
bob();

console.log(foo);   // "foo" -- nice, but..
```
Нам потрібно окремо виконувати функцію через `bob()`, це ж Function Declaration.
Але хтось може назвати свою функцію так само, тому це не вирішить проблему до кінця. 
Тоді ми перетворимо функцію в Function Expression!
```js
var foo = "foo"

( function bob() {
    var foo = "foo2";
    console.log(foo);   // "foo2"
} )();

console.log(foo);   // "foo" -- perfect!
```
Чому це Function Expression? Дуже просто, тому шо слова function не є першим в Statement :)
Це означає, шо `bob` вже є в іншому(своєму) internal Scope і виконується immediately сама.
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
Але так не може бути, в `if (x > y)` нема Scope!
Не біда, `let` його створить, Scope з Lexical Environment(нашу скриньку) і добавить туди `tmp`.
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
Кайл каже, шо об'явити один раз всі змінні зверху це не така і хороша ідея.
Краще декларувати змінні там, де вони юзаються в рамках одного скріна. 
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
`const` працює так, як `let` і робить Block Scoping.
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
# Hoisting
Дефайнення змінних і функцій відбувається на 1 кроці компіляції.
Тим самим ми, ніби переносим всі define наверх перед виконанням операцій.
Hoisting це додавання в Scope, коли дефайнення йде після виклику.
```js
a;   // ???
b;   // ???
var a = b;
var b = 2;
b;   // 2
a;   // ???
```
при компіляції цей код, по суті, перетворюється на
```js
var a;
var b;
a;   // undefined
b;   // undefined
a = b;
b = 2;
b;   // 2
a;   // undefined
```
з функціями(Function Declaration) така ж сама історія
```js
var a = b();
var c = d();
a;   // ???
b;   // ???

function b() {
    return c;
}

var d = function() {
    return b();
};
```
хойститься як
```js
function b() {
    return c;
}
var a;
var c;
var d;
a = b();
c = d();
a;   // undefined 
с;   // undefined
d = function() {
    return b();
};
```
Тобто Function Expression не хойститься.
Також не хойстяться `let`.
```js
function foo(bar) {
    if (bar) {
        console.log(baz);   // ReferenceError
        let baz = bar;
    }
}
```
Точніше хойститься, але не до кінця.
При `var` наша змінна декларується(додається) в Scope і ессайниться, як `undefined`.
При `let` виконується тільки декларування до Scope, без assign. Тому в нас `ReferenceError`.
# Closure
Замикання - це коли функція пам'ятає свій Lexical Scope, коли вона виконана за межами цього Lexical Scope.
Щоб створити замикання потрібно створити функцію всередині іншого Scope і послатись на змінну з зовнішнього `Scope`.
Цей інший `Scope` залишається з функцію так довго, як будуть замкнені змінні. Якшо цих замкнутих змінних не стане, Garbage Collector захаває цей Scope.
```js
function foo() {
    var bar = "bar";

    function baz() {
        console.log(bar);
    }

    bam(baz);
}

function bam(baz) {
    baz();   // "bar"
}

foo();
```
Передавати функцію це не єдиний спосіб використати Closure.
Можна ретурнути функцію.
```js
function foo() {
    var bar = "bar";

    return function() {
        console.log(bar);
    };

    bam(baz);
}

function bam() {
    foo()();   // "bar", тут ми екзекютим ретурнуту функцію
}

bam();
```
При замиканні Garbage collector не видаляє Scope, і можна доступитись до змінних цього Scope. 
```js
function foo() {
    var bar = "bar";

    seTimeout(function() {
        console.log(bar);
    }, 1000);
}

foo();
```
Як ця функція буде виконуватись по таймауту? Garbage Collector мав би її з'їсти вже давно.
Closure не дає цього зробити і ця функція продовжує виконуватись.
Функція замикає змінну `bar`.
```js
function foo() {
    var bar = "bar";

    $("#btn").click(function(evt){
        console.log(bar);
    });
}

foo();
```
Те саме.
Замикання продовжує життя цих змінних настільки наскільки це потрібно функції, яка виконує це замикання.
Іншими словами, Closure запобігає роботі Garbage Collector.
### Loops
```js
for (var i=1; i<=5; i++) {
    setTimeout(function() {
        console.log("i: " + i);
    }, i*1000);
}
```
На виході не буде того, шо ми очікуємо, бо ми не кріейтимо нову `i` кожен раз. 
Нема нової `i` для кожної нової ітерації.
В нас буде `(5)i: 6`.
Застосуємо IIFE.
```js
for (var i=1; i<=5; i++) {
    (function(i) {
        setTimeout(function() {
            console.log("i: " + i);
        }, i*1000);
    })(i);
}
```
Ми кожен раз створили новий Scope з новою `i` і одержимо очікуваний результат.
### Loops + Block Scope
```js
for (var i=1; i<=5; i++) {
    let j = i;
    setTimeout(function() {
            console.log("j: " + j);
    }, i*1000);
}
```
Ми замикаємо кожен раз нову `j`.
Ми можемо навіть окремо не дефайнити `j` через `let`, а написати так
```js
for (let i=1; i<=5; i++) {
    setTimeout(function() {
            console.log("i: " + i);
    }, i*1000);
}
```
Тобто діло було в тому, шо нам у цьому випадку потрібно було замикати кожен раз нову `i`,
а не ту саму, як було з `var`.
# Modules
Інкапсуляція це приховання тих змінних, методів etc, які не є необхідні для використання ззовні.
Для паттерна Module потрібно:
1. Одна зовнішня enclosed(обгороджена) функція, яка буде виконуватись лише раз.
2. Внутрішня функція, яка буде робити замикання на внутрішній Scope і ретурнати publicAPI(публічний інтерфейс).

Переваги паттерну:
1. Організація коду, хоча для цього ми могли юзати Namespaces.
2. Обмежувати доступ до того, чого ми не хочемо, шоб використовували чи використали непередбачувано. Інкапсуляція.

Недоліки паттерну:
1. Тестування. Як протестити(unit tests) фунція, яка є прихованою? Кайл каже, шо на його думку, потрібно тестити тільки publicAPI.
### Classic Module Pattern
```js
var foo = (function() {
    var o = { bar: "bar" };

    return {
        bar: function() { 
            console.log(o.bar);
        }
    };
})();
foo.bar();   // "bar"
foo.o;   // undefined
```
### Classic Module Pattern: modified
```js
var foo = (function() {
    var publicAPI = {
        bar: function() {
            publicAPI.baz();
        },
        baz: function() {
            console.log("baz");
        }
    };
    return publicAPI;
})();
foo.bar();   // "baz"
```
### ES6 + Module Pattern
`foo.js`
```js
var o = { bar: "bar" };

export function bar() {
    return o.bar;
};
```
```js
import { bar } from "foo.js";

bar();   // "bar"

import { * } from "foo.js";

foo.bar();   // "bar"
```
Кожен модуль це окремий файл. Все, шо не попадає в `export` інкапсулюється.
Модулі є Singleton, це коли є тільки один instance(екземпляр) в ES6.
Якшо ми пишемо `import from "foo.js"` 50 разів, ми не рікріейтимо модуль foo.js 50 разів.
Він буде створений і виконаний лише один раз. І ми будем мати 50 копій reference одного екземпляру модуля.

# Object-Orienting
### this(context)
Кожна(крім arrow functions) функція, поки виконується, має reference(вказівник, посилання) на контекст виконання(то, де виконується функція), який називають this.
Ми говорили, шо в Javascript є тільки Lexical Scope, але this - це джаваскриптова версія Dynamic Scope.

Не важливо, де задана функція, звідки відбувся її виклик, що навколо. Важливо те, як відбувся виклик функції!
Це і детермінує this - як відбувся виклик функції.
Є 4 варіанти, як відбувається виклик функції
* implicit(неявний), `o2.foo();` - виконай функцію `foo` в контексті об'єкту `o2`. "Позичаємо" функцію і сетаємо `this`.
```js
function foo() {
    console.log(this.bar);
}

var bar = "bar1";
var o2 = { bar: "bar2", foo: foo };
var obj = { bar: "bar3" };


foo();   // bar1
o2.foo();   // bar2
foo.call(obj);   // bar3
```
* explicit(явний), `foo.call(obj);` - зроби виклик `foo` і використай `obj`, як контекст. Щоб явно засетати `this` юзам `call` і `apply`. До explicit можна віднести і hard binding. `orig.call(obj);` - захардбіндили контекст. Ми локаєм this до функція і вона завжди тепер буде виконуватись в цьому контексті(крім того випадку, коли ми викличимо функцію через `new`). Це збільшує передбачуваність, але зменшує гнучкість.
```js
function foo() {
    console.log(this.bar);
}

var obj = { bar: "bar" };
var obj2 = { bar: "bar2" };

var orig = foo;
foo = function() { orig.call(obj); };

foo();   // bar
foo.call(obj2);   // not bar2, but bar
```
* new binding, створює новий this для виклику функції.
```js
function foo() {
    this.baz = "baz";
    console.log(this.bar + " " + baz);
}

var bar = "bar";
var baz = new foo();   // ???
```
* default binding, якшо не підходить жодному з 3 попередніх правил, то, коли ми не Strict Mode, default binding робить default this = Global Object. В Strict Mode defaut this = undefined. Що призведе до помилки. Не можна так писати.

`new` - "constructor call".
`new foo()`:
* створює новий пустий об'єкт
* лінкує цей об'єкт до іншого об'єкту
* новостворений об'єкт проходить в цьому контексті до виклику функції
* повертає this, якшо нічого не вертається(?)
### Arrow Functions
Arrow functions не міняють `this`. Вони не мають `this`, вони нічого про це не знають.
Вони піднімаються на рівень вище і питають чи хтось знає шось про `this`.
```js
function foo() {
    return () => this.bar;
}

var bar = "bar1";
var o1 = { bar: "bar2", foo: foo };
var o2 = { bar: "bar3" };

var f1 = foo();
var f2 = o1.foo();
var f3 = foo.call(o2);

f1();   // bar1
f2();   // bar2
f3();   // bar3

f1.call(02);   // bar1 <---- hmmm
```