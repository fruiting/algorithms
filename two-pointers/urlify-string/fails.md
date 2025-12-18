// https://algocode.io/courses/yandex-algorithms/problem/urlify-string
// Попытка #1
// Изначально начал движение указателей слева. Потом понял, что это ни к чему не приведет и начал движение справа
// Быстро понял, что медленный указатель ставится в самый конец, а быстрый на k - 1,
// это значит, что он поставится на первый символ после #
// Логику написал с первого раза правильно, хоть и потратил 35 минут, но допустил ошибку в синтакисе
// Сравнивал с пробелом само значение переменной fast, а не значение элемента под этим индексом s[fast]

```
package main

// Time: O(n)
// Space: O(1)
func urlify(s []rune, k int) []rune {
    fast, slow := k - 1, len(s) - 1
    for fast >= 0 {
        if string(fast) != " " {
            s[fast], s[slow] = s[slow], s[fast]
            fast--
            slow--

            continue
        }

        s[slow] = '0'
        s[slow - 1] = '2'
        s[fast] = '%'

        slow -= 2
    }

    return s
}
```

---

// Попытка #2
// Исправил ошибку в синтаксисе. Успех

```
package main

// Time: O(n)
// Space: O(1)
func urlify(s []rune, k int) []rune {
    fast, slow := k - 1, len(s) - 1
    for fast >= 0 {
        if string(fast) != " " {
            s[fast], s[slow] = s[slow], s[fast]
            fast--
            slow--

            continue
        }

        s[slow] = '0'
        s[slow - 1] = '2'
        s[fast] = '%'

        slow -= 2
    }

    return s
}
```