// https://algocode.io/courses/yandex-algorithms/problem/simple-calculator
// Попытка #1
// Успех
// Решил задачу с первой попытки и по симптоматике прохожу,
// но эталонное решение немного оптимальнее в абсолютных числах памяти

```
package main

import "strconv"

// Time: O(n)
// Space: O(1)
func calculate(s []string) int {
    if len(s) == 1 {
        res, _ := strconv.Atoi(s[0])
        return res
    }

    for i := 2; i < len(s); i = i + 2 {
        if string(s[i - 1]) == "+" {
            continue
        }

        curr, _ := strconv.Atoi(s[i])
        prev, _ := strconv.Atoi(s[i - 2])

        s[i] = strconv.Itoa(curr * prev)
        s[i - 1] = "_"
        s[i - 2] = "_"
    }

    var sum int
    for i := 0; i < len(s); i++ {
        if string(s[i]) == "_" || string(s[i]) == "+" {
            continue
        }

        curr, _ := strconv.Atoi(s[i])
        sum += curr
    }

    return sum
}

```

---

// Попытка #2
// Успех
// Эталонное решение предполагает вместо двух проходок по слайсу и перезаписей значений
// проходиться только по знакам и использовать две переменные: result и prevMultiply.
// Суть заключается в следующем:
// 1) Если мы на знаке умножения, то мы накапливаем произведение пока не уткнемся в сложение
// 2) Если мы на знаке сложения, то мы сбрасываем результат накопленного произведения в результат, а в результат произведения пишем следующую цифру
// 3) В самом конце после цикла мы прибавляем результат произведения к результату

```
package main

import "strconv"

// Time: O(n)
// Space: O(1)
func calculate(s []string) int {
    var result int
    prevMultiply, _ := strconv.Atoi(s[0])

    for i := 1; i < len(s); i += 2 {
        next, _ := strconv.Atoi(s[i + 1])
        if s[i] == "*" {
            prevMultiply *= next
        } else {
            result += prevMultiply
            prevMultiply = next
        }
    }

    return result + prevMultiply
}

```
