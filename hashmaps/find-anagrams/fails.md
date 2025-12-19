// https://algocode.io/courses/yandex-algorithms/problem/find-anagrams
// Попытка #1
// Сам не решил. Пришлось разбирать решение. Но в целом понял
// Нужно загнать символы строки t в мапу, по которой можно определить количество того или иного символа.
// Далее мы итерируемся по строке s до максимального индекса строки t и декрементируем в мапе количество символов и удаляем ключ, если их значения равны нулю.
// Если получилось так, что мапа пустая, то мы записываем левый индекс окна (да, тут применяется скользящее окно).
// Далее мы итерируемся до конца строки. Левым указателем инкрементируем символы, правым - декрементируем. В обоих случах, если по ключу значение 0, то удялем
// На каждой итерации смотрим пустая ли мапа.

```
package main

func findAnagrams(s string, t string) []int {
    diff := make(map[byte]int, len(s))
    for i := 0; i < len(t); i++ {
        diff[t[i]]++
    }

    result := make([]int, 0, len(s))

    l, r := 0, 0
    for r < len(t) {
        diff[s[r]]--
        if diff[s[r]] == 0 {
            delete(diff, s[r])
        }

        r++
    }

    if len(diff) == 0 {
        result = append(result, l)
    }

    for r < len(s) {
        diff[s[l]]++
        if diff[s[l]] == 0 {
            delete(diff, s[l])
        }
        l++

        diff[s[r]]--
        if diff[s[r]] == 0 {
            delete(diff, s[r])
        }
        r++

        if len(diff) == 0 {
            result = append(result, l)
        }
    }

    return result
}

```

---

// Попытка #2
// Успех. Добавил проверку на длины строк

```
package main

func findAnagrams(s string, t string) []int {
    if len(t) > len(s) {
        return nil
    }

    diff := make(map[byte]int, len(s))
    for i := 0; i < len(t); i++ {
        diff[t[i]]++
    }

    result := make([]int, 0, len(s))

    l, r := 0, 0
    for r < len(t) {
        diff[s[r]]--
        if diff[s[r]] == 0 {
            delete(diff, s[r])
        }

        r++
    }

    if len(diff) == 0 {
        result = append(result, l)
    }

    for r < len(s) {
        diff[s[l]]++
        if diff[s[l]] == 0 {
            delete(diff, s[l])
        }
        l++

        diff[s[r]]--
        if diff[s[r]] == 0 {
            delete(diff, s[r])
        }
        r++

        if len(diff) == 0 {
            result = append(result, l)
        }
    }

    return result
}

```
