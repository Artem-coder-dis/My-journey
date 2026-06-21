## Что такое Array.isArray()

Array.isArray() - это метод, который проверяет, является ли значение массивом. Возвращает true или false

```js
Array.isArray([1, 2, 3])  // true
Array.isArray({a: 1})     // false
Array.isArray("hello")    // false
Array.isArray(null)       // false
Array.isArray(undefined)  // false
```

**Зачем нужен, если есть typeof**

typeof для массивов возвращает "object" - не отличить от обычного объекта. Array.isArray() решает эту проблему

```js
typeof [1, 2, 3]         // "object"
Array.isArray([1, 2, 3]) // true
```

**Где использовать**

В условии, когда нужно узнать, массив перед тобой или нет:

- Проверить аргумент функции - прислали массив или что-то другое
- Проверить, можно ли применять методы массивов (map, filter) к значению
- Фильтровать данные - отобрать только массивы

**Задача 1: Функция удваивает числа, только если передан массив**

```js
function doubleIfArray(value) {
    if (Array.isArray(value)) {
        return value.map(x => x * 2)
    }
    return value
}

console.log(doubleIfArray([1, 2, 3])) // [2, 4, 6]
console.log(doubleIfArray(5))         // 5
```

**Задача 2: Функция считает, сколько массивов среди переданных аргументов**

```js
function countArrays(...args) {
    let result = 0

    for (let arg of args) {
        if (Array.isArray(arg)) {
            result++
        }
    }

    return result
}

console.log(countArrays([1,2], "hi", [3], 42)) // 2
```

**С чем можно спутать**

Array.isArray() - это метод конструктора Array, а не метод, который вызывается на самом массиве. Поэтому пишем `Array.isArray(значение)`, а не `значение.isArray()`

Это не метод массива вроде map или filter, которые вызываются прямо на массиве через точку. Это проверка снаружи - мы передаём значение, а метод говорит, массив это или нет
