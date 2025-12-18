// https://algocode.io/courses/yandex-algorithms/problem/single-edit-apart
// Попытка #1
// Сразу понял, что это паттерн "каждому по указателю", но решение придумал неверное
// Главным вопросом было для меня "как перемещать указатель", если символы не равны.

```
package main

import "math"

// Time: O(n)
// Space: O(1)
func isSimilar(s string, t string) bool {
    if math.Abs(float64(len(s) - len(t))) > 1 {
        return false
    }

    p1, p2 := 0, 0
    remainings := 1
    for p1 < len(s) && p2 < len(t) {
        if s[p1] == t[p2] {
            p1++
            p2++

            continue
        }

        if len(s) >= len(t) {
            p1++
        } else {
            p2++
        }

        remainings--
        if remainings < 0 {
            return false
        }
    }

    if p1 < len(s) {
        remainings -= len(s) - p1
    }
    if p2 < len(t) {
        remainings -= len(t) - p2
    }
    if remainings < 0 {
        return false
    }

    return true
}

```

---

// Попытка #2
// Посмотрел решение и изучил его.
// Идея оказалась в том, чтобы найти первое отличие в строках,
// затем в зависимости от длины строк инкрементировать один или оба указателя,
// найти следующее отличие (по условию их может быть максимум одно)
// и потом сравнить значения указателей с длинами строк. Они должны быть одинаковыми, тогда считается,
// что раз указатели равны длинам своих строк, то проверка пройдена.
// Забыл добавить bool в качестве возвращаемого типа данных в сигнатуре метода equal

```
package main

import "math"

// Time: O(n)
// Space: O(1)
func isSimilar(s string, t string) bool {
    if s == t {
        return true
    }
    if math.Abs(float64(len(s) - len(t))) > 1 {
        return false
    }

    missMatch := findMissmatch(s, t, 0, 0)
    p1, p2 := missMatch[0], missMatch[1]

    if len(s) == len(t) {
        return equal(findMissmatch(s, t, p1+1, p2+1), []int{len(s), len(t)})
    } else if len(s) < len(t) {
        return equal(findMissmatch(s, t, p1, p2+1), []int{len(s), len(t)})
    } else {
        return equal(findMissmatch(s, t, p1+1, p2), []int{len(s), len(t)})
    }
}

func findMissmatch(s string, t string, p1 int, p2 int) []int {
    for p1 < len(s) && p2 < len(t) {
        if s[p1] != t[p2] {
            break
        }

        p1++
        p2++
    }

    return []int{p1, p2}
}

func equal(a, b []int) {
    return a[0] == b[0] && a[1] == b[1]
}
```

---

// Попытка #3
// Успех

```
package main

import "math"

// Time: O(n)
// Space: O(1)
func isSimilar(s string, t string) bool {
    if s == t {
        return true
    }
    if math.Abs(float64(len(s) - len(t))) > 1 {
        return false
    }

    missMatch := findMissmatch(s, t, 0, 0)
    p1, p2 := missMatch[0], missMatch[1]

    if len(s) == len(t) {
        return equal(findMissmatch(s, t, p1+1, p2+1), []int{len(s), len(t)})
    } else if len(s) < len(t) {
        return equal(findMissmatch(s, t, p1, p2+1), []int{len(s), len(t)})
    } else {
        return equal(findMissmatch(s, t, p1+1, p2), []int{len(s), len(t)})
    }
}

func findMissmatch(s string, t string, p1 int, p2 int) []int {
    for p1 < len(s) && p2 < len(t) {
        if s[p1] != t[p2] {
            break
        }

        p1++
        p2++
    }

    return []int{p1, p2}
}

func equal(a, b []int) bool {
    return a[0] == b[0] && a[1] == b[1]
}
```

---
