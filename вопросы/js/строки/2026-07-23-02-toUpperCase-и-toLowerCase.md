## toUpperCase / toLowerCase

`toUpperCase` и `toLowerCase` - это методы которые меняют регистр строки 

`toUpperCase` - ВЕРХНИЙ регистр

`toLowerCase` - нижний регистр

Легко запомнить по приставками **low** - низкий и **up** - вверх

```javascript
let str = "Hello";
console.log(str.toUpperCase()); // "HELLO"
console.log(str.toLowerCase()); // "hello"
console.log(str);               // "Hello" — исходная не изменилась
```

**Где пригодится:**

- Сравнение без учёта регистра: `"JS" === "js"` → `false`, а `"JS".toLowerCase() === "js".toLowerCase()` → `true`
- Нормализация ввода (email, логин)
- Форматирование текста (заголовки, кнопки)

**Пример сравнения:**

```javascript
let answer = "Да";
if (answer.toLowerCase() === "да") {
    console.log("Правильно!");
}
// сработает и для "Да", и для "ДА", и для "да"
```

&nbsp;

**Задача.** Нужно написать функцию, которая принимает email и возвращает его в нижнем регистре. Если email не содержит `@`, вернуть "Некорректный email"

```javascript
function emailVerification(str) {
    if (!str.includes("@")) return "Некорректный email";

    return str.toLowerCase();
}

console.log(emailVerification("User@Mail.Ru")); // user@mail.ru
console.log(emailVerification("UserMail.ru"));  // "Некорректный email"
```

В условии, благодаря методу [includes](2026-07-24-03-includes.md), мы проверяем, есть ли символ `@` в строке. Если нет - сразу возвращаем `"Некорректный email"` и не идём дальше

Если символ есть - просто переводим строку в нижний регистр

Это учебный пример. В реальных задачах проверка строже (длина, домен, пробелы)

---

**Задачи**

```javascript
// 1. Что выведет?
let str = "JavaScript";
console.log(str.toUpperCase());
```

<details>
<summary>Ответ</summary>

`"JAVASCRIPT"` - все буквы стали заглавными

</details>

```javascript
// 2. Что выведет?
let str = "HELLO";
console.log(str.toLowerCase());
```

<details>
<summary>Ответ</summary>

`"hello"` - все буквы стали строчными

</details>

```javascript
// 3. Что выведет?
let a = "JS";
let b = "js";
console.log(a.toLowerCase() === b.toLowerCase());
```

<details>
<summary>Ответ</summary>

`true` - сравнение без учёта регистра

</details>

---

**Задачи со звёздочкой ⭐**

```javascript
// 4. ⭐ Что выведет?
let str = "";
console.log(str.toUpperCase() === str.toLowerCase());
```

<details>
<summary>Ответ</summary>

`true` - пустая строка в любом регистре остаётся пустой строкой. `"" === ""` → `true`
</details>

```javascript
// 5. ⭐ Что выведет?
let str = "123";
console.log(str.toUpperCase() === str.toLowerCase());
```

<details>
<summary>Ответ</summary>

`true` - у цифр нет регистра, оба метода возвращают `"123"`

</details>
