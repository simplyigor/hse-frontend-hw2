# Описание 📝

Второе домашнее задание с курса по веб-разработке (ВШЭ, Октябрь 2023). Состоит из нескольких задач по JavaScipt. 

**Выполнил:** Игорь Петров

# Решение 🧑‍💻

### Задачка №2 – Ключи и свойства

Реализуйте функцию, которая получает на вход объект, а возвращает объект, в котором в качестве ключей указаны типы, встречающиеся в исходном объекте, а в качестве значений - как часто они встречались.

<details>
<summary>Код</summary>
  
```js
function solutionFn(object) { // Шаг 1: Определяем функцию solutionFn(), которая получает на вход объект
  const resultObj = {}; // Шаг 2: Создаем пустой объект resultObj
  for (let key in object) { // Шаг 3: Запускаем цикл for с проверкой условия
    const type = typeof object[key]; // Шаг 4: Говорим функции, что type это тип ключа в входном объекте. Используем оператор typeof, как и указано в задании :)
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

### Задачка №3 – Больше никаких шуток про 1 + '1' === '11'

Напишите функцию `sum`, которая:

- Принимает два значения
- Проверяет, является ли каждый из них числом
- Если они оба числа, то возвращается их сумма
- Если левый операнд не является числом, то выкидывается ошибка "The left operand is not number"
- Если правый операнд не является числом, то выкидывается ошибка "The right operand is not number"
- Если оба операнда не являются числами, то выкидывается ошибка "Operands are not numbers"

<details>
<summary>Код</summary>
  
```js
function sum(left_value, right_value) { // Шаг №1: Определяем функцию sum(), которая принимает 2 значения
    if ((typeof left_value !== 'number') && (typeof right_value !== 'number')) { //Шаг №2: Если оба операнда не являются числами...
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

### Задачка №8 - Антиспам

Реализуйте функцию простейшей проверки текста на спам, где `text` – текст, проверяемый на спам, `keywords` - массив ключевых слов, а результат функции – логическое значение.

<details>
<summary>Код</summary>

```js
function isSpam(text, keywords) { // Шаг №1: Определяем функцию isSpam(), которая принимает текст и ключевые слова
  for (let len = 0; len < keywords.length; len++) { // Шаг №2: Запускаем цикл, переберающий все элементы в массиве keywards 
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
