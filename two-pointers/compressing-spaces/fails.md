// https://algocode.io/courses/yandex-algorithms/problem/compressing-spaces
// Попытка #1
// Изначально понял, что тут надо использовать быстрый и медленный указатели.
// Проблема только в том, чтобы понять как объединять несколько пробелов в один
// Изначально решил, что можно вычитать из значения быстрого значение медленного указетеля,
// но наткнулся на ошибку в одном из кейсов. Такой вариант не подходит

```
package main

// Time: O(n)
// Space: O(1)
func compressSpaces(chars []rune) []rune {
    fast, slow := 0, 0
    for fast < len(chars) {
        if chars[fast] != ' ' {
            if fast - slow > 1 {
                slow++
            }

            chars[fast], chars[slow] = chars[slow], chars[fast]
            slow++
        }

        fast++
    }

    return chars[:slow + 1]
}

```

---

// Попытка #2
// Тогда я подумал, что возможно стоит не вычитать индексы,
// а проверить, является ли следующий за slow элемент пробелом.
// Это решение разумеется неверное, поскольку сейчас slow может быть не пробелом,
// а следующий им будет. И тогда будет неверно произведен своп

```
package main

// Time: O(n)
// Space: O(1)
func compressSpaces(chars []rune) []rune {
    fast, slow := 0, 0
    for fast < len(chars) {
        if chars[fast] != ' ' {
            if chars[slow + 1] == ' ' {
                slow++
            }

            chars[fast], chars[slow] = chars[slow], chars[fast]
            slow++
        }

        fast++
    }

    return chars[:slow + 1]
}

```

---

---

// Попытка #3
// Решил, что можно смотреть, является ли текущий и следующий slow пробелами
// Это тоже ни к чему не привело. Ломается на [' ', ' ', 'H', 'e', 'l', 'l', 'o', ' ', ' ', 'W', 'o', 'r', 'l', 'd', ' ', ' ']
// Это решение привело к результату аналогичному fast - slow

```
package main

// Time: O(n)
// Space: O(1)
func compressSpaces(chars []rune) []rune {
    fast, slow := 0, 0
    for fast < len(chars) {
        if chars[fast] != ' ' {
            if chars[slow] == ' ' && chars[slow + 1] == ' ' {
                slow++
            }

            chars[fast], chars[slow] = chars[slow], chars[fast]
            slow++
        }

        fast++
    }

    return chars[:slow + 1]
}

```

---

// Попытка #4
// Пришлось посмотреть решение, поскольку за пол часа я сам до него не дошел
// Решение оказалось в добавлении переменной spaces
// Она необходима для подсчета пробелов.
// Если их не более 1, то мы меняем символы местами.
// Когда встречается символ, отличный от пробела, мы ее обнуляем
// Медленный указатель двигается только когда происходит своп

```
package main

// Time: O(n)
// Space: O(1)
func compressSpaces(chars []rune) []rune {
    spaces := 0
    fast, slow := 0, 0
    for fast < len(chars) {
        if chars[fast] == ' ' {
            spaces++
        } else {
            spaces = 0
        }

        if spaces <= 1 {
            chars[fast], chars[slow] = chars[slow], chars[fast]
            slow++
        }

        fast++
    }

    return chars[:slow]
}

```

