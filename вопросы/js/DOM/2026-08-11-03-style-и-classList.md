## Изменение стилей через JS

Можно менять внешний вид элементов двумя способами: напрямую через `style` или через добавление/удаление CSS-классов.

**`element.style` - изменить конкретное CSS-свойство**

```javascript
const title = document.querySelector("h1");
title.style.color = "red";        // цвет текста
title.style.fontSize = "40px";    // размер шрифта
title.style.backgroundColor = "#eee"; // цвет фона
```

Свойства пишутся в camelCase: `background-color` → `backgroundColor`, `font-size` → `fontSize`.

---

## classList 

`classList` - это свойство DOM-элемента, которое управляет CSS-классами. Через него можно добавлять, удалять и переключать классы, не затрагивая другие классы элемента

**`classList.add("класс")` - добавить класс**

```javascript
const el = document.querySelector("h1");
el.classList.add("highlight"); // добавили класс highlight
```

Если класс уже есть - ничего не произойдёт, дубликата не будет

**`classList.remove("класс")` - убрать класс**

```javascript
el.classList.remove("highlight"); // убрали класс highlight
```

Если класса нет - ничего не произойдёт, ошибки не будет

**`classList.toggle("класс")` - переключить класс. Если его нет - добавляет, если есть - убирает**

```javascript
// Видимость элемента
el.classList.toggle("hidden"); // был виден → скрыли, был скрыт → показали

// Тёмная тема
document.body.classList.toggle("dark"); // переключили тему

// Активный пункт меню
menuItem.classList.toggle("active"); // выделили/сняли выделение
```

Удобно для включения/выключения: видимость элемента, тёмная тема, активный пункт меню



**`classList.contains("класс")`** - проверяет, есть ли у элемента указанный класс. Возвращает `true` или `false`.

```javascript
const el = document.querySelector("h1");
el.classList.add("big");

console.log(el.classList.contains("big"));    // true - класс есть
console.log(el.classList.contains("hidden")); // false - класса нет
```

Используется для проверки состояния элемента: видимый/невидимый, активный/неактивный, тёмная/светлая тема

**Преимущество перед `style`:**

`style` меняет конкретное CSS-свойство напрямую. `classList` позволяет повесить готовый набор стилей из CSS - это чище и удобнее

```javascript
// Через style - одно свойство
el.style.color = "red";

// Через classList - готовый набор стилей из CSS
el.classList.add("error"); // в CSS: .error { color: red; font-weight: bold; }
```

На практике чаще используют `classList` - стили хранятся в CSS, JS только управляет классами

---

**Простые задачи**

HTML и CSS для задач:

```html
<ul>
    <li>Яблоко</li>
    <li>Груша</li>
    <li>Банан</li>
</ul>

<p id="text">Абзац с текстом</p>
```

```css
.highlight {
    background-color: yellow;
    font-weight: bold;
}
    .hidden {
    display: none;
}
    .big {
    font-size: 30px;
}
```

&nbsp;

```text
1. Надо увеличить размер шрифта у всех li до 20px (циклом)
```

<details> <summary>Ответ</summary> 
  
Я сначала написал 

```javascript
const allLi = document.querySelectorAll("li");
for (let i of allLi) {
    allLi[i].style.fontSize = "20px";
}
```

Но оно не работает потому что `i` в `for...of` - это сам элемент (`<li>`), а не индекс. Я пытался использовать элемент как индекс: `allLiAhf[элемент]`, что даёт `undefined`.

Правильно:

```javascript
const allLiAhf = document.querySelectorAll("li");
for (let i of allLiAhf) {
    i.style.fontSize = "20px";
}
```

</details>

```text
2. Надо применить класс big к первому `li` и класс highlight ко второму `li`
```

<details> <summary>Ответ</summary> 
  
```javascript
const items = document.querySelectorAll("li");
items[0].classList.add("big");
items[1].classList.add("highlight");
```

</details>

```text
3. Переключи класс hidden у элемента с id text и выведи в консоль, видимый он сейчас или нет (подсказка: проверь наличие класса через classList.contains)
```

<details> <summary>Ответ</summary> 
  
```javascript
const itemAhr = document.querySelector("#text");
console.log(itemAhr.classList.contains("hidden")); // false
```

</details>

**Задачи со звёздочкой ⭐**

```text 
4. Нужно сделать невидимым последний `li` через добавление класса hidden
```

<details> <summary>Ответ</summary> 

Сначала я вообще не понимал как делать, написал `items.length - 1.classList.add("hidden");`. я знал что будет неправильно, но потом попробовал сначала получить последний элемент через индекс, а потом уже работать с ним

```javascript
const items = document.querySelectorAll("li");
const lastItem = items[items.length - 1];
lastItem.classList.add("hidden");
```

</details>

```text
5. ⭐ Найди все li. Убери класс hidden у последнего элемента и добавь класс big первому и последнему элементу, а класс highlight - всем остальным (обычный цикл с условием)
```

<details> <summary>Ответ</summary> 
  
```javascript
const items = document.querySelectorAll("li");
const lastItem = items[items.length - 1]; // находим последний элемент как в задаче 4
lastItem.classList.remove("hidden"); // убираем hidden

for (let i = 0; i < items.length; i++) {
    if (i === 0 || i === items.length - 1) {
        items[i].classList.add("big");
    } else {
        items[i].classList.add("highlight");
    }
}
```

Так выглядит визуально коллекция элементов NodeList:

```javascript
// NodeList(3)
// 0: <li>Яблоко</li>
// 1: <li>Груша</li>
// 2: <li>Банан</li>
// length: 3
```

- document.querySelectorAll("li") - находим все <li> на странице. Это коллекция из трёх элементов
- цикл for с индексом i проходит по всем элементам от 0 до length - 1
- условие i === 0 || i === items.length - 1 проверяет, является ли текущий элемент первым (индекс 0) или последним (индекс 2)
- если да - добавляем класс big (шрифт 30px)
- если нет (индекс 1, средний элемент) - добавляем класс highlight (жёлтый фон, жирный)

</details>
