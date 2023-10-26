# Описание 📝

Второе домашнее задание с курса по веб-разработке (ВШЭ, Октябрь 2023). Состоит из нескольких задач по JavaScipt. 

**Выполнил:** Игорь Петров

# Решение 🧑‍💻

### Задачка №2 – Ключи и свойства

Реализуйте функцию, которая получает на вход объект, а возвращает объект, в котором в качестве ключей указаны типы, встречающиеся в исходном объекте, а в качестве значений - как часто они встречались.

<details>
<summary>✨Код✨</summary>
  
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
<summary>✨Код✨</summary>
  
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

### Задача №4 – CVS на минималках

Напишите функцию getMinimalCVS, которая будет выполнять роль CVS для некоторого массива. Она должна принимать на вход массив и возвращать объект с четырьмя свойствами:

- `head` - функция, возвращающая последнюю версию массива
- `history` - функция, возвращаюся массив со всеми версиями массива
- `push` - функция, принимающая элемент и сохраняющая новую версию массива с добавленным элементом в конце
- `pop` - функция, сохраняющая новую версию массива без последнего элемента и возвращающая этот последний элемент

**NB:** я не совсем понял можно ли было использовать уже реализованные в JS методы или нет, но я все-таки решил упростить себе жизнь и воспользовался таким штуками как:

- [`Array.prototype.pop()`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
- [`Array.prototype.push()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
- [`Array.prototype.slice()`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

<details>
<summary>✨Код✨</summary>

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

### Задачка №8 - Антиспам

Реализуйте функцию простейшей проверки текста на спам, где `text` – текст, проверяемый на спам, `keywords` - массив ключевых слов, а результат функции – логическое значение.

<details>
<summary>✨Код✨</summary>

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
