# Learn-TypeScript

*yarn add typescript*

## Базовые типы

Typescript является языком со статической типизацией. Тип не может быть изменен в ходе выполнения программы. Это позволяет снизить большое количество ошибок и выявить многие из них еще на этапе компиляции.

### Boolean

Наиболее базовым типом является логический ture/false, который в Javascript и Typescript называется boolean.
```js
let isDone: boolean = false;
```

### Number

Как и в Javascript, тип number в Typescript является числом с плавающей точкой. Кроме десятичного и шестнадцатиричного формата, поддерживаются бинарный и восьмеричный, введенные в ECMAScript 2015.
```js
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

### String 

Еще одна важная часть программ в веб-страницах и серверах это текстовые данные. Как и в других языках, в Typescript используется то же обозначение "string" для таких данных. Как и Javascript, в Typescript используются двойные (") или одинарные (') кавычки для обрамления текстовых данных.
```js
let name: string = "bob";
name = 'smith';
```

Вы также можете использовать строки с шаблонами, которые могут быть многострочными и иметь встроенные выражения. 
```js
let name: string = `Gene`;
let age: number = 37;

let sentence: string = `Hello, my name is ${ name }. 
I'll be ${ age + 1 } years old next month.`
```

### Null и Undefined

Как и в JavaScript, в TypeScript есть специальные типы undefined и null, которые принимают соответствующие значения undefined и null.
```js
let country: undefined = undefined;
let city: null = null;
```

### Array

TypeScript, как и JavaScript, имеет массивы значений. Тип массива может быть определен одним из двух способов. Первый - обозначать тип элементов массива перед []:
```js
let list: number[] = [1, 2, 3];
```
Второй способ - использовать обобщение Array<elemType>:
```js
let list: Array<number> = [1, 2, 3];
```

### Tuple

Тип Tuple дает возможность объявить массив с известным фиксированным количеством элементов, которые не обязаны быть одного типа. Например, вы хотите иметь значение Tuple как пару "строка" и "число":
```js
let x: [string, number] = ['hello', 10]; // декларирование и инициализация типа tuple
x = [10, 'hello']; // некорректная инициализация вызовет ошибку
```
Если в массиве будет много данных, то лучше записать это в две строки:
```js
let x: [string, number, number, number, string];
x = ['hello', 10, 6, 3, 'bye'];
```

### Any

Нам может потребоваться описать тип переменных, который мы не знаем, когда пишем наше приложение. Эти значения могут быть получены из динамического контента, например от пользователя или от сторонней библиотеки. В этих случаях мы хотим отключить проверку типов и позволить значениям пройти проверку на этапе компиляции. Чтобы это сделать, нужно использовать тип any:
```js
let notSure: any = 4; // теперь можем менять тип данных
notSure = "maybe a string instead";
notSure = false; 
```
Тип any может быть также полезен, если вы не знаете какие типы данных будут в массиве. 
```js
let a: any[] = [1, true, "free"];
let b: [any, any] = [2, true, "car"];
let c: Array[any] = [3, false, "home"];
с[1] = 100; // также можем менять тип данных
```

### Enum (Перечисления)

Полезным дополнением к стандартному набору типов из Javascript является тип Enum. Данный тип - это более удобный способ задания понятных имен набору численных значений. Данный тип представляет из себя некую смесь объекта и массива. При обращении к значению Enum возвращается его индекс. 
```js
enum Directions {
    Up,
    Down,
    Left,
    Right
}

Directions.Up // 0
Directions.Down // 1
Directions.Left // 2
Directions.Right // 3
```
По умолчанию, перечисления (Enum) начинаются с 0, но можно изменить это путем прямого указания значения или даже задать значения для всех.
```js
enum Directions {
    Up = 4,
    Down = 6,
    Left = 8,
    Right
}

Directions.Up // 4
Directions.Down // 6
Directions.Left // 8
Directions.Right // 9
```
Получить данные мы можем не только по значению, но и по ключу. Такой подход называется Reverse Enum.
```js
Directions[4] // Up
Directions[6] // Down
Directions[8] // Left
Directions[9] // Right
```
### Void 

Чаще всего он используется в качестве возвращаемого типа функций, которые не возвращают никакого значения.
```js
const warnUser = (): void => {
    alert("This is my warning message");
}
```
Объявление переменных с типом void бесполезно, потому что вы можете присвоить им только значения undefined или null:
```js
let unusable: void = undefined;
```

### Never

Тип Never указывает на то, что функция ни при каких обстоятельствах не может ничего вернуть из себя, например, она всегда бросает ошибку или включает в себя бесконечный цикл, который не может ничего вернуть из функции. Этот тип является субтипом и может быть присвоен любому типу, но не наоборот.
```js
const fail = (message: string): never => {
	throw new Error(message);
}
```
Здесь важно понять отличие never от void, потому что поначалу это может сбивать с толку. Функция, которая ничего не возвращает – это void, но как мы убедились выше, она может вернуть undefined. Функция, которая никогда ничего не возращает – это never.
```js
const pitfall = (): never => {
	return;
}
// Error → Type 'undefined' is not assignable to type 'never'.
```
never можно представить себе как вариант запрета использовать ключевое слово return в функции.
	
### object
	
Тип object в TypeScript определяет все не примитивные типы, то есть тип, который не является number, string, boolean, symbol, null или undefined. Этот тип был введён в TypeScript 2.2, который вышел в феврале 2017 года – раньше для определения типа нужно было либо использовать any, либо писать интерфейсы.

Также, в TypeScript существует тип Object, который включает в себя все JavaScript-объекты. Такой тип подразумевает наличие метода hasOwnProperty и других стандартных методов у объекта.
```js
const isObject: object = 1;
// Error → Type '1' is not assignable to type 'object'.

const isObject: object = {};
const isObject: Object = 1;
const isObject: Object = {};
```

### Union
	
Объединения или union не являются собственно типом данных, но они позволяют комбинировать или объединить другие типы. Так, с помощью объединений можно определить переменную, которая может хранить значение двух или более типов:
```js	
let id : number | string;
id = "1345dgg5";
console.log(id); // 1345dgg5
id = 234;
console.log(id);  // 234
```
Чтобы определить все типы, которые должно представлять переменная, все эти типы разделяются прямой чертой: number | string. В данном случае переменная id может представлять как тип string, то есть строку, так и число.
	
Подобным образом можно использовать union для определения параметров функции:
```js	
const printId = (id: number|string): void => {
    console.log(`Id: ${id}`);
}
```
### Type Aliases
	
В TypeScript есть возможность создавать свои типы, называемые Type Aliases. Создаётся собственный тип через ключевое слово type.
```js	
type Human = {firstName: string, age: number, height: number}
```	
В примере выше создаётся собственный тип Human, содержащий 3 разных свойства. Пример создания объекта типа Human:
```js	
const human: Human = {firstName: ‘Franz’, age: 32, height: 185}
```
	
# Функции
```js	
const createPassword = (name, age) => `${name}${age}` // обычная функция в JavaScript
createPassword('Jack', 30) // 'Jack30'
```
В TypeScript нам нужно описать аргументы функции: 
```js		
const createPassword = (name: string, age: number) => `${name}${age}`
Для большей гибкости, мы можем добавить тип Union в аргументы.
const createPassword = (name: string, age: number | sting) => `${name}${age}` // Теперь age может быть, как строкой, так и числом.
createPassword('Jack', '30') // 'Jack30'	
```
