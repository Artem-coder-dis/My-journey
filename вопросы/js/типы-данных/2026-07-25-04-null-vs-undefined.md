## null vs undefined

`null` и `undefined` - это два типа «пустоты» в JS. Они похожи, но используются в разных ситуациях

---

### undefined

`undefined` означает «значение не присвоено». JS сам присваивает `undefined`, когда переменная объявлена, но не инициализирована

```javascript
let x;
console.log(x); // undefined - переменная есть, значения нет
```

**Когда появляется `undefined`:**
- Переменная объявлена, но без значения
- Функция ничего не вернула (нет `return`)
- Обращение к несуществующему свойству объекта
- Параметр функции не был передан

```javascript
let obj = { name: "Анна" };
console.log(obj.age); // undefined - свойства нет

function test() {}
console.log(test()); // undefined - нет return
```

Редко специально присваивают `undefined`. Обычно JS ставит его сам, когда значения нет. Если нужно явно указать «пусто» - используют `null`

Единственный частый случай для `undefined` - проверка, был ли передан аргумент в функцию:

```javascript
function greet(name) {
    if (name === undefined) {
        console.log("Привет, гость!");
    } else {
        console.log("Привет, " + name + "!");
    }
}

greet(); // "Привет, гость!"
```

---

### null

`null` означает «намеренная пустота». Его присваивают, чтобы явно указать: здесь ничего нет

```javascript
let user = null; // пользователь пока не выбран
```

**Когда используют `null`:**
- Переменная будет содержать объект, но пока его нет
- Сброс значения (было - стало пусто)
- Результат поиска, когда ничего не найдено

```javascript
let selectedUser = null; // никто не выбран

// позже выбрали пользователя
selectedUser = { name: "Анна" };

// потом сбросили
selectedUser = null; // снова пусто
```

---

### Сравнение

При нестрогом равенстве `==` они равны друг другу, но не равны ничему больше:

```javascript
console.log(null == undefined);  // true - особое правило JS
console.log(null === undefined); // false - разные типы
console.log(null == 0);          // false
console.log(undefined == 0);     // false
console.log(null == false);      // false
```

Всегда используй `===` для проверки. Если нужно проверить и `null`, и `undefined` одновременно - `value == null` (это единственный случай, где `==` допустим)

---

### typeof

```javascript
console.log(typeof undefined); // "undefined"
console.log(typeof null);      // "object"
```

Для проверки на `null` используй прямое сравнение: `value === null`

---

**Задачи**

```javascript
// 1. Что выведет?
let x;
console.log(x);
```

<details>
<summary>Ответ</summary>

`undefined` - переменная объявлена, но не инициализирована

</details>

```javascript
// 2. Что выведет?
let user = { name: "Анна" };
user = null;
console.log(user);
```

<details>
<summary>Ответ</summary>

`null` - переменной явно присвоили `null`

</details>

```javascript
// 3. Что выведет?
function test() {}
console.log(test());
```

<details>
<summary>Ответ</summary>

`undefined` - функция ничего не возвращает

</details>

---

**Задачи со звёздочкой ⭐**

```javascript
// 4. ⭐ Что выведет?
let a = null;
let b = undefined;
console.log(a == b);
console.log(a === b);
console.log(typeof a);
console.log(typeof b);
```

<details>
<summary>Ответ</summary>

`true`, `false`, `"object"`, `"undefined"`. `==` считает `null` и `undefined` равными. `===` - разные типы. `typeof null` → `"object"` (баг), `typeof undefined` → `"undefined"`

</details>

```javascript
// 5. ⭐ Что выведет?
let obj = { a: null, b: undefined };
console.log("a" in obj); // in проверяет есть ли свойство в объекте
console.log("b" in obj);
console.log(obj.a === obj.b);
```

<details>
<summary>Ответ</summary>

`true`, `true`, `false`. Оба свойства существуют в объекте (ключи есть), поэтому `in` возвращает `true`. Но `null !== undefined` по строгому равенству - `false`

</details>
