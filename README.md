# Описание 📝

**Выполнил:** Игорь Петров

Второе домашнее задание с курса по веб-разработке – решение задач на базовое понимание и работу с JavaScript (НИУ ВШЭ, Октябрь 2023).

# Решение 🧑‍💻

### Задачка №2 – Ключи и свойства

Реализуйте функцию, которая получает на вход объект, а возвращает объект, в котором в качестве ключей указаны типы, встречающиеся в исходном объекте, а в качестве значений - как часто они встречались.

<blockquote>
<details>
<summary>Код ✨</summary>
  
```js
function solutionFn(object) { // Шаг 1: Определяем функцию solutionFn(), которая получает на вход объект
  const resultObj = {}; // Шаг 2: Создаем пустой объект resultObj
  for (let key in object) { // Шаг 3: Запускаем цикл for с проверкой условия
    const type = typeof object[key]; // Шаг 4: Говорим функции, что type это тип ключа в входном объекте. Используем оператор typeof, как и посоветовали в задании :)
    if (resultObj[type]) { // Шаг 5: Проверяем есть ли уже такой тип ключа в объекте resultObj
      resultObj[type]++; // Шаг 5.1: Если да, то увеличим соответствующее значение на 1 
    } else {
      resultObj[type] = 1; // Шаг 5.2: Если нет, то создадим новое свойство объекта, где ключ – тип, значение – 1
    }
  }
  return resultObj; // Шаг 6: Вернем объект, перечисляющий типы и частоту их появления
};

// Для тестирования:

const initialObj = {
  a: 'hello',
  b: false,
  c: 70,
  d: {name: 'Igor', course: 'Web Development'},
  e: true,
  f: 65
};

const resultObj = solutionFn(initialObj);
console.log(resultObj) // { boolean: 2, number: 2, object: 1, string: 1 }
```
</details>
</blockquote>
  
### Задачка №3 – Больше никаких шуток про 1 + '1' === '11'

Напишите функцию `sum`, которая:

- Принимает два значения
- Проверяет, является ли каждый из них числом
- Если они оба числа, то возвращается их сумма
- Если левый операнд не является числом, то выкидывается ошибка "The left operand is not number"
- Если правый операнд не является числом, то выкидывается ошибка "The right operand is not number"
- Если оба операнда не являются числами, то выкидывается ошибка "Operands are not numbers"

<blockquote>
<details>
<summary>Код ✨</summary>
  
```js
function sum(left_value, right_value) { // Шаг №1: Определяем функцию sum(), которая принимает 2 значения
    if ((typeof left_value !== 'number') && (typeof right_value !== 'number')) { // Шаг №2: Если оба операнда не являются числами...
      return 'Operands are not numbers'; // ... то выкидывается ошибка "Operands are not numbers"
    }
    else if (typeof left_value !== 'number') { // Шаг №2.1: Если левый операнд не является числом...
      return 'The left operand is not number'; // ... то выкидывается ошибка "The left operand is not number"
    }
    else if (typeof right_value !== 'number') { // Шаг №2.2: Если правый операнд не является числом...
      return 'The right operand is not number'; // ... то выкидывается ошибка "The right operand is not number"
    }
    else {
      return left_value + right_value; // Шаг №2.3: Если оба операнда являются числами, то возвращается их сумма
    }    
}

// Для тестирования:

const testSum_num = sum(2, 3)
const testSum_left = sum('hey', 12)
const testSum_right = sum(5, 'bye')
const testSum_both = sum(false, true)
console.log('testSum_num:', testSum_num, 'testSum_left:', testSum_left, 'testSum_right:', testSum_right, 'testSum_both:', testSum_both)
```
</details>
</blockquote>

### Задачка №4 – CVS на минималках

Напишите функцию getMinimalCVS, которая будет выполнять роль CVS для некоторого массива. Она должна принимать на вход массив и возвращать объект с четырьмя свойствами:

- `head` - функция, возвращающая последнюю версию массива
- `history` - функция, возвращаюся массив со всеми версиями массива
- `push` - функция, принимающая элемент и сохраняющая новую версию массива с добавленным элементом в конце
- `pop` - функция, сохраняющая новую версию массива без последнего элемента и возвращающая этот последний элемент

<blockquote>
<details>
<summary>Код ✨</summary>
<br />
  
**NB:** не совсем понял можно ли было использовать уже реализованные в JS методы или нет, но я все-таки решил упростить себе жизнь и воспользовался такими штуками как:

- [`Array.prototype.pop()`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
- [`Array.prototype.push()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
- [`Array.prototype.slice()`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

```js
function getMinimalCVS(array) {
  const history = [array.slice()] // Создадим упорядоченную коллекцию данных (= история как массив)
  return {
    head: () => array.slice(), // Вернем последнюю версию массива с помощью метода Array.prototype.slice()
    history: () => history.slice(), // Вернем всю историю, используя тот же slice()
    push: (new_element) => {
      array.push(new_element); // Добавим новый элемент в конец массива c помощью метода Array.prototype.push()
      history.push(array.slice()); // Добавим новую версию массива в конец истории
    }, 
    pop: () => {
      const new_element = array.pop(); // Удалим последний элемент c помощью метода Array.prototype.pop()
      history.push(array.slice()); // Добавим новую версию массива в конец истории
      return new_element // Выведем значение удаленного элемента
    }
  };
}

// Для тестирования:

const cvs = getMinimalCVS(['a', 'b', 'c']);
cvs.push('hello');
cvs.push('world')

console.log(cvs.pop()); 
console.log(cvs.history());
console.log(cvs.head())
```

</details>
</blockquote>

### Задачка №6 – Hit Or Run 

Напишите функцию `hitOrRun`, которая:

- Принимает на вход два натуральных числа `a` и `b` (`a < b`)
- Генерирует рандомное число в промежутке `[a, b]`
- Проверяет, является ли оно простым
- Если является, то возвращает строку `run`
- Если не является, то возвращает строку `hit`

Подсмотрел некоторые части кода для решения этой задачи в этих источниках:

- [Про генерацию случайного числа в интервале](https://stackoverflow.com/questions/1527803/generating-random-whole-numbers-in-javascript-in-a-specific-range) 
- [Про нахождение простых чисел](https://stackoverflow.com/questions/40200089/check-number-prime-in-javascript)

<blockquote>
<details>
<summary>Код ✨</summary> 

```js
function hitOrRun(a, b) {
  let randomNumber = Math.floor(Math.random() * (b - a + 1)) + a; // Шаг №1: Выбираем случайное число в интервале [a, b]
  if (randomNumber < 2) { // Шаг №2: Последовательность простых чисел начинается с 2, поэтому будем возвращать hit в случае, если randomNumber < 2
    return "hit";
  }
  for (let i = 2; i <= Math.sqrt(randomNumber); i++) { // Шаг №3: Для остальных случаев проводим эксплицитную проверку через остаток при делении
    if (randomNumber % i === 0) {
      return "run" + '\n' + randomNumber; // Шаг №3.1: Если число простое, то вернем run (для прозрачности я также решил выводить randomNumber)  
    }
  }
  return "hit" + '\n' + randomNumber; // Шаг №3.2: Если нет, то вернем hit
}

// Для тестирования:
console.log(hitOrRun(8, 15))
```
  
</details>
</blockquote>

### Задачка №7 – Case Converter

Напишите функцию, которая принимает на вход строку в `snake_case` (все слова в нижнем регистре и разделяются нижним подчёркиванием) и превращает её в строку в `camelCase` (слова не разделяются, первое слово пишется в нижнем регистре, у каждого следующего слова первая буква в верхнем регистре, остальные - в нижнем).

<blockquote>
<details>
<summary>Код ✨</summary> 

```js
function solutionFn(someString) { // Шаг №1: Определяем функцию solutionFn(), которая принимает string 
  let words = someString.split('_'); // Шаг №2: Разделяем полученный string по нижнему подчеркиванию (e.g. hello_world -> hello world)
  for (let i = 1; i < words.length; i++) { // Шаг №3: Запускаем цикл для всех слов, начиная со второго (i = 1, так как в JS нумерация с нуля)
    words[i] = words[i][0].toUpperCase() + words[i].slice(1).toLowerCase() ; // Шаг №4: Добавляем верхний регистр к первой букве слов, затем прибавляем остальные части слов.
  }
  return words.join(''); // Шаг №4: Объединяем все слова в единую конструкцию 
}

// Для тестирования:

const someString = "backend_developer_wrote_this_name"
const testFunct = solutionFn(someString)
console.log(testFunct)
```
  
</details>
</blockquote>
  
### Задачка №8 - Антиспам

Реализуйте функцию простейшей проверки текста на спам, где `text` – текст, проверяемый на спам, `keywords` - массив ключевых слов, а результат функции – логическое значение.

<blockquote>
<details>
<summary>Код ✨</summary>

```js
function isSpam(text, keywords) { // Шаг №1: Определяем функцию isSpam(), которая принимает текст и ключевые слова
  for (let len = 0; len < keywords.length; len++) { // Шаг №2: Запускаем цикл, перебирающий все элементы в массиве keywords 
    if (text.toLowerCase().includes(keywords[len].toLowerCase())) { // Шаг №3: Если текст содержит хотя бы одно из ключевых слов...
      return true; // ... выведем логическое значение true
    }
  }
  return false; // Шаг №3.1: В противном случае выведем логическое значение false
}

// Для тестирования:

const nasty_mail = "Поздравляем! Наш алгоритм выбрал вас для доступа к ПРЕМИУМ программе. Это 100% не развод"
const good_mail = "Привет! Подскажи, пожалуйста, что задано по веб-разработке?"
const stopwords = ["Алгоритм", "Премиум", "Развод", "Выигрыш"]

const spamTest = isSpam(nasty_mail, stopwords)
const noSpamTest = isSpam(good_mail, stopwords)
console.log(spamTest, noSpamTest)
```
</details>
</blockquote>

### Задачка №10 - Задача с собеседования

Напишите функцию, которая:

- Получает на вход натуральное число
- Перемножает все цифры числа, до тех пор, пока оно не станет одноразрядным
- Возвращает итоговое одноразрядное число

<blockquote>
<details>
<summary>Код ✨</summary>

```js
hello
```
</details>
</blockquote>
