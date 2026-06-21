## Object.entries()

Возвращает массив пар `[ключ, значение]`

**Рассмотрим на примерах**

**Задача 1: вернуть массив пар [ключ, значение]**

```js
function getEntries(obj) {
    return Object.entries(obj)
}

console.log(getEntries({a: 1, b: 2})) // [["a", 1], ["b", 2]]
```

Просто возвращает пары

**Задача 2: вернуть количество свойств объекта**

```js
function countEntries(obj) {
    return Object.entries(obj).length
}

console.log(countEntries({a: 1, b: 2, c: 3})) // 3
```

Object.entries превращает объект в массив и у массива возвращает длину

Это учебный пример. В реальном коде для подсчёта свойств используют `Object.keys(obj).length`. Но задача хороша тем, что показывает: entries возвращает массив, а у массивов есть `.length`

**Задача 3: вернуть первую пару [ключ, значение]**

```js
function firstEntry(obj) {
    let result = Object.entries(obj)

    if (result.length > 0) return result[0]
    return null
}

console.log(firstEntry({a: 1, b: 2})) // ["a", 1]
```

Object.entries превращает объект в массив и если длина массива больше 0, то вернёт первую пару. То есть получается массив `[["a", 1], ["b", 2]]`

                (Индекс 0)↑          ↑(Индекс 1)

`result[0]` - это `["a", 1]`. Чтобы сразу получить ключ и значение по отдельности, можно написать `let [key, value] = result[0]` - это деструктуризация, разбирает массив на переменные

`return null` вернёт null если объект был пуст

**Задача 4: вернуть массив ключей объекта через Object.entries**

```js
function getKeysViaEntries(obj) {
    let entries = Object.entries(obj)
    let newMassiv = []

    for (let [key, value] of entries) {
        newMassiv.push(key)
    }

    return newMassiv
}

console.log(getKeysViaEntries({a: 1, b: 2, c: 3})) // ["a", "b", "c"]
```

Хочу сразу сказать - это учебная задача, чтобы освоить Object.entries(). В реальном коде для получения ключей/значений используют Object.keys()/.values(), но понимание, как устроен entries, пригодится, когда нужно будет одновременно и ключ, и значение - фильтровать, сортировать, преобразовывать и тд

**Что происходит в задаче:**

- Создаём переменную entries - Object.entries превращает объект в массив пар `[["a", 1], ["b", 2], ["c", 3]]`
- Создаём пустой массив
- Цикл `for...of` перебирает массив entries, деструктуризация `[key, value]` раскладывает каждую пару на две переменные
- В цикле пушим ключ в массив
- Возвращаем новый массив

**Рассмотрим Object.entries на немного более сложной похожей задаче**

Нужно вернуть массив ключей, значения которых - массивы. Использовать Object.entries() и Array.isArray()

```js
function keysWithArrayValues(obj) {
    let entries = Object.entries(obj)
    let result = entries
        .filter(([key, value]) => Array.isArray(value))
        .map(([key, value]) => key)

    return result
}

console.log(keysWithArrayValues({a: [1,2], b: "hi", c: [3], d: 42})) // ["a", "c"]
```

Что такое Array.isArray() написано в отдельном посте. Кратко: Array.isArray() проверяет, массив ли это

Можно написать и без отдельной переменной:
```js
return Object.entries(obj)
    .filter(([key, value]) => Array.isArray(value))
    .map(([key, value]) => key)
```

Но первый вариант просто читаемее

**Что происходит в задаче по действиям:**

Object.entries(obj) превращает объект в массив пар. Как это выглядит:
```
[
    ["a", [1, 2]],
    ["b", "hi"],
    ["c", [3]],
    ["d", 42]
]
```

`.filter(([key, value]) => Array.isArray(value))` — `[key, value]` это деструктуризация: из каждой пары `["a", [1, 2]]` key получает `"a"`, value получает `[1, 2]`

Оставляем только те пары, где значение - массив (через Array.isArray):

- `["a", [1, 2]]` → `Array.isArray([1, 2])` → `true` → оставляем
- `["b", "hi"]` → `Array.isArray("hi")` → `false` → выкидываем
- `["c", [3]]` → `Array.isArray([3])` → `true` → оставляем
- `["d", 42]` → `Array.isArray(42)` → `false` → выкидываем

`.map(([key, value]) => key)` — из каждой оставшейся пары берём только ключ:

- `["a", [1, 2]]` → `"a"`
- `["c", [3]]` → `"c"`

Возвращаем `["a", "c"]`

**Ту же задачу можно решить и через цикл for...of:**

```js
let result = []
for (let [key, value] of Object.entries(obj)) {
    if (Array.isArray(value)) {
        result.push(key)
    }
}
return result
```

Такую задачу, для будущего, лучше решать через методы массивов. Это современнее, короче и читаемее, но цикл ты должен уметь написать - на случай, если коллега попросит объяснить без методов или в проекте другой стиль

**Когда использовать Object.entries():**
- Нужны и ключ, и значение одновременно
- Нужно применить методы массивов (filter, map, sort) к объекту
- Нужно превратить объект в другую структуру

**Когда НЕ использовать:**
- Нужны только ключи - бери Object.keys()
- Нужны только значения - бери Object.values()
- Простой перебор - for...in короче
