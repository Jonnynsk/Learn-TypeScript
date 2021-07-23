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