# Statement – 1 дія, 1 ідея, відділяється “;”.
# Expression – вираз, це не завжди якась операція, може бути просто число чи змінна.
В дужках всі expressions 
((a) = ((b) * (2))); 
Очевидно, шо разом це statement.
a = b * 2 + foo(c * 3); - так, як в  нас вже є (), юзанем [].
[ [a] = [ [ [b] * [2] ] + [ [foo]([ [c] * [3] ]) ] ] ]; 
Множення має більший пріоритет, ніж додавання, шоб обійти це, можна виділити дужками потрібну операцію.

# Programming LVL
Set the variable a to the value 2 - highest lvl programming
a = 2 
mov 2,a
10010100101010101011110101010101010101011110 - lowest lvl programming
Javasript engine – те, шо перетворює javascript на код нижчого рівня, встроєний в більшість браузерів.
Javascript – мова скриптів, її часто називають інтерпретуємою мовою, тому шо ми считуємо стейтмент за стейтментом. Коли ми виконуємо 3 стейтмент, ми не знаємо, шо буде в 5 стейтменті. Але це не зовсім так. Компілююча мова спочатку дивиться на весь код, чи він правильний і тоді його ранить, а інтерпретуюча мова ранить рядок за рядком. Javascript в цьому більше схожий на компілюючу. Якшо в скрипті є 2 стейтмента і один з них неправильний, 1 стейтмент не буде ранитись.

Conversion and Coversion(not obvious)
# Conversion
a = String(a);
b = Number(a);
# Coversion
a = a + “”;

# Block це об’єднання statements
{
var a = 42;
foo(a / 2);
}
Після блоку «;» ставити не потрібно.

# Функції можна деклерити:
function foo() {} – function declaration
var bar = function() {} – function expression attached to variable declaration
var bar = function baz() {} – named function expression attached to variable declaration

function foo(b,bar,zaz) {} b,bar,zaz - parameters
foo(100); “100” - argument

# “Falsy” values: 
0
-0
NaN
“”
false
null
undefined 

