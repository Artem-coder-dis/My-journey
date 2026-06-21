## Почему `push(obj)` не работает, и что такое `Object.values`
Было задание: вернуть массив всех значений объекта

Я написал:

```js
function getValues(obj) {
    let newMassiv = []
    newMassiv.push(obj)

    return newMassiv 
}

console.log(getValues({name: "Анна", age: 25}))  // [ {name: "Анна", age: 25} ]
```
Вывод: `[ {name: "Анна", age: 25} ]` - массив, внутри которого один элемент: сам объект

Я обернул объект в массив. Не достал значения, а просто положил объект целиком в ячейку массива. Поэтому и не сработало

Правильно через `Object.values(obj)`:

```js
function getValues(obj) {
    return Object.values(obj)
}
```

`Object.values(obj)` - возвращает **массив значений** объекта

```js
let user = {name: "Анна", age: 25}

Object.values(user)  // ["Анна", 25]
Object.values({})    // [] - пустой массив для пустого объекта
```

`Object.keys` — массив ключей. `Object.values` - массив значений. `Object.entries` — массив пар `[ключ, значение]`. Три метода, работают одинаково, просто возвращают разное
