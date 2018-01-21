# Statement 
Інструкція, відділяється “;”.

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

Javascript – мова скриптів, її часто називають інтерпретуємою мовою, тому шо ми считуємо стейтмент за стейтментом. Коли ми виконуємо 3 стейтмент, ми не знаємо, шо буде в 5 стейтменті. Але це не зовсім так. Javascript схожий на компілюючу мову, де спочатку engine проходить весь код, якшо код коректний, тоді ранить його. Натомысть інтерпретуюча мова ранить рядок за рядком. В Javascript програмі, коли є два стейтменти і один з них неправильний, перший стейтмент не зараниться.

# Conversion and Coversion(not obvious)
Зведення типів.
### Conversion
```js
a = String(a);
b = Number(a);
```
### Coversion
```js
a = a + “”;
```
# Block це об’єднання statements
```js
{
    var a = 42;
    foo(a / 2);
}
```
Після блоку «;» ставити не потрібно.

# Functions
* `function foo() {}` – function declaration
* `var bar = function() {}` – function expression attached to variable declaration
* `var bar = function baz() {}` – named function expression attached to variable declaration

`function foo(b,bar,zaz) {}` 
b,bar,zaz - parameters

`foo(100);` 
“100” - argument

# “Falsy” values:
```js
0
-0
NaN
“”
false
null
undefined
```
