---

## Руководства по стилю (JS)

---

#### 1.Уменьшите количество глобальных переменных.

---

_Глобальные переменные будут доступны во всем коде JavaScript, поэтому существует вероятность конфликта имен, когда разные части кода будут определять глобальные переменные с одинаковым именем, но используемые для различных целей._

``` 
// bad
let name = 'Harry';  
let lastName = 'Potter';  
  
function doSomething() {...}
  
console.log(name); // Harry 

// good
let person = {  
   name : 'Harry',  
   lastName : 'Potter',
   
   function doSomething() {...},
}

console.log(person.name); // Harry 
```
---

#### 2.Используйте === Сравнение.

---

_Использование данного оператора позволяет избежать нежелательного преобразования типов данных. Если нам необходимо удостовериться, что переменные действительно идентичны друг другу, стоит использовать строгое равенство._

``` 
// bad
0 == "";        // true
1 == "1";       // true
1 == true;      // true

// good
0 === "";       // false
1 === "1";      // false
1 === true;     // false
```
---

#### 3.Ограничить количество параметров.

---

_Если ваша функция или метод имеет более 3 параметров, тогда используйте объект в качестве параметра._

``` 
// bad
function a(p1, p2, p3) {
  // ...
};

// good
function a(p) {
  // ...
};
```
---

#### 4.Избегайте побочных эффектов в конструкторах.

---

_Избегайте асинхронных вызовов, запросов API или манипуляций с DOM в constructor. Вместо этого переместите их в отдельные функции._

``` 
// bad
class myClass {
  constructor(config) {
    this.config = config;
    axios.get(this.config.endpoint)
  }
}

// good
class myClass {
  constructor(config) {
    this.config = config;
  }

  makeRequest() {
    axios.get(this.config.endpoint)
  }
}
const instance = new myClass();
instance.makeRequest(); 
```
---

#### 5.Избегайте классов для обработки событий DOM.

---

_Если единственная цель класса - связать событие DOM и обработать обратный вызов, используйте функцию._

``` 
// bad
class myClass {
  constructor(config) {
    this.config = config;
  }

  init() {
    document.addEventListener('click', () => {});
  }
}

// good

const myFunction = () => {
  document.addEventListener('click', () => {
    // handle callback here
  });
}
```
---

#### 6.Используйте ParseInt.

---

_Используется ParseInt при преобразовании числовой строки в число._

``` 
// bad
Number('10')

// good
parseInt('10', 10); 
```
---

#### 7.Абсолютные и относительные пути для модулей.

---

_Используйте относительные пути, если модуль, который вы импортируете, находится ниже двух уровней._

``` 
// bad
import GitLabStyleGuide from '~/guides/GitLabStyleGuide';

// good
import GitLabStyleGuide from '../GitLabStyleGuide';
```
---

#### 8.Функции.

---

_Стремитесь написать много маленьких чистых функций и минимизируйте, где происходят мутации._

``` 
// bad
const values = {foo: 1};

function impureFunction(items) {
  const bar = 1;

  items.foo = items.a * bar + 2;

  return items.a;
}

const c = impureFunction(values);

// good
var values = {foo: 1};

function pureFunction (foo) {
  var bar = 1;

  foo = foo * bar + 2;

  return foo;
}

var c = pureFunction(values.foo); 
```
---

#### 9.Для работы с прототипами предпочтительнее использовать классы.

---

_До ES6 классы нужно было создавать, добавляя к функции-конструктору свойства, расширяя прототип. ES6 предоставляет весьма удобный синтаксический сахар. Классы можно создавать достаточно просто. Хотя такой синтаксис и скрывает реализацию, новичкам в нём будет проще разобраться, да и написанный код будет чище._

``` 
function Person(name, age, gender) {
    this.name   = name;
    this.age    = age;
    this.gender = gender;
}

Person.prototype.incrementAge = function () {
    return this.age += 1;
};

class Person {
    constructor(name, age, gender) {
        this.name   = name;
        this.age    = age;
        this.gender = gender;
    }

    incrementAge() {
      this.age += 1;
    }
}
```
---

#### 10.Комментируйте ваш код(но без избыточности).

---

_Это кажется излишним в начале, но может случится так, что когда вы вернетесь к проекту через несколько месяцев и обнаружите, что не помните, что этот кусок кода делает. Или что будет, если ваш коллега будет смотреть ваш код в процессе код-ревью? Поэтому всегда комментируйте важные части кода._

``` 
// Проходим циклом по массиву и выводим каждый его элемент   
for(var i = 0, len = array.length; i < len; i++) {  
   console.log(array[i]);
```
---
