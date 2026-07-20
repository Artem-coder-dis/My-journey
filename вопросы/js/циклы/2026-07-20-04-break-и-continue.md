## break и continue

`break` и `continue` - это операторы, которые управляют поведением цикла изнутри

- `break` - полностью останавливает цикл, выходит из него
- `continue` - пропускает текущую итерацию и переходит к следующей

---

### break

**Пример 1**

```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) break;
    console.log(i);
}
// 0, 1, 2, 3, 4
```

Цикл должен был пройти от 0 до 9, но на `i = 5` сработал `break` и цикл остановился. Дальше ничего не выполняется

**Пример 2**

```javascript
let i = 0;
while (i < 10) {
    if (i % 3 === 0 && i !== 0) break;
    console.log(i);
    i++;
}
// 0, 1, 2
```

Цикл идёт по числам от 0. На `i = 3` условие `3 % 3 === 0` истинно, `break` останавливает цикл. Вывелось 0, 1, 2

`break` часто используют для оптимизации поиска: нашёл нужный элемент - выходи, дальше искать смысла нет

**Пример 3**

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 7 === 0) {
        console.log(i);
        break;
    }
}
// 7
```

Ищем первое число, кратное 7. Нашли - вывели и вышли. Остальные числа не проверяются

---

### continue

**Пример 1**

```javascript
for (let i = 0; i < 5; i++) {
    if (i === 2) continue;
    console.log(i);
}
// 0, 1, 3, 4
```

Цикл проходит от 0 до 4. На `i = 2` срабатывает `continue` - итерация пропускается, `console.log(2)` не выполняется. Цикл продолжается дальше

**Пример 2**

```javascript
let result = "";
for (let i = 0; i < 10; i++) {
    if (i % 2 === 0) continue;
    result += i;
}
console.log(result); // "13579"
```

Собираем строку только из нечётных чисел. Чётные пропускаем через `continue`. Результат: `"13579"`

**Пример 3**

```javascript
let sum = 0;
for (let i = 1; i <= 10; i++) {
    if (i % 3 === 0) continue;
    sum += i;
}
console.log(sum); // 37
```

Суммируем числа от 1 до 10, но кратные 3-ём (3, 6, 9) пропускаем. Сумма остальных: 1+2+4+5+7+8+10 = 37

---

**Задачи**

```javascript
// 1 (break). Что выведет?
for (let i = 0; i < 8; i++) {
    if (i === 4) break;
    console.log(i);
}
```

<details>
<summary>Ответ</summary>

`0, 1, 2, 3` - на 4-ёх просто выходит из цикла

</details>

```javascript
// 2 (break). Что выведет?
let a = 0;
while (a < 5) {
    if (a === 2) break;
    console.log(a);
    a++;
}
```

<details>
<summary>Ответ</summary>

`0, 1` - также как в прошлом, как только `a === 2` цикл останавливается

</details>

```javascript
// 3 (break). Что выведет?
for (let i = 20; i > 0; i--) {
    if (i % 11 === 0) {
        console.log(i);
        break;
    }
}
```

<details>
<summary>Ответ</summary>

`11` - пока i при делении на 11 не даст остаток 0 - цикл будет продолжаться

</details>

```javascript
// 4 (break). Что выведет?
let sum = 0;
for (let i = 5; i <= 10; i++) {
    sum += i;
    if (sum > 15) break;
}
console.log(sum);
```

<details>
<summary>Ответ</summary>

`18` — 5+6+7=18 > 15, выход

</details>

```javascript
// 5 (break). Что выведет?
let str = "";
for (let i = 0; i < 6; i++) {
    if (i === 4) break;
    str += i;
}
console.log(str);
```

<details>
<summary>Ответ</summary>

`"0123"` - просто складывается в строку

</details>

```javascript
// 6 (continue). Что выведет?
for (let i = 0; i < 7; i++) {
    if (i === 4) continue;
    console.log(i);
}
```

<details>
<summary>Ответ</summary>

`0, 1, 2, 3, 5, 6` - 4 пропускается

</details>

```javascript
// 7 (continue). Что выведет?
let b = 0;
while (b < 5) {
    b++;
    if (b === 3) continue;
    console.log(b);
}
```

<details>
<summary>Ответ</summary>

`1, 2, 4, 5` - тоже самое, 3 пропускается

</details>

```javascript
// 8 (continue). Что выведет?
let res = "";
for (let i = 1; i <= 6; i++) {
    if (i % 3 === 0) continue;
    res += i;
}
console.log(res);
```

<details>
<summary>Ответ</summary>

`"1245"` - 3 пропускается + складывается в строку

</details>

```javascript
// 9 (continue). Что выведет?
let sum = 0;
for (let i = 1; i <= 8; i++) {
    if (i % 4 === 0) continue;
    sum += i;
}
console.log(sum);
```

<details>
<summary>Ответ</summary>

`30` - 4 и 8 пропущены, сумма остальных: 1+2+3+5+6+7=30

</details>

```javascript
// 10 (continue). Что выведет?
for (let i = 0; i < 6; i++) {
    if (i > 3) continue;
    console.log(i);
}
```

<details>
<summary>Ответ</summary>

`0, 1, 2, 3` - если больше 3, то пропускает 

</details>

**Итог:** тема вроде лёгкая. Вначале я вообще её пропустил, изучил только теорию и всё, но когда писал этот пост, пришлось немного посидеть, подумать над задачами на `continue`
