// https://algocode.io/courses/yandex-algorithms/problem/longest-common-prefix
// Попытка #1
// Сразу было ясно, что это паттерн "Каждому по указателю", но на бумаге это оказалось проще, чем в коде.
// Сначала затупил и не сразу понял, что надо итерироваться сначала по буквам, а потом по строкам, а не наоборот
// Нужно было одновременно пройти по каждой строке и сравнивать каждый символ
// Сначала неправильно произвел расчет minLen, который необходим как максимальная длина префикса (префикс не может быть длинее минимальной длины строки)
// Я инициализировал его с нулевым значением, а потом искал, что будет меньше, чем нуль

```
package main

// Time: O(n)
// Space: O(n)
func longestCommonPrefix(strs []string) string {
    var minLen int
    for i := 0; i < len(strs); i++ {
        minLen = min(minLen, len(strs[i]))
    }

    prefix := make([]byte, 0, minLen)
    for i := 0; i < minLen; i++ {
        for j := 1; j < len(strs); j++ {
            if strs[j][i] != strs[j - 1][i] {
                return string(prefix)
            }
        }

        prefix = append(prefix, strs[0][i])
    }

    return string(prefix)
}

```

---

// Попытка #2
// Успех
// Изменил способ инициализации minLen и за одно добавил проверку на то, что есть хотя бы одна строка в массиве strs

```
package main

// Time: O(n)
// Space: O(n)
func longestCommonPrefix(strs []string) string {
    if len(strs) == 0 {
        return ""
    }

    minLen := len(strs[0])
    for i := 0; i < len(strs); i++ {
        minLen = min(minLen, len(strs[i]))
    }

    prefix := make([]byte, 0, minLen)
    for i := 0; i < minLen; i++ {
        for j := 1; j < len(strs); j++ {
            if strs[j][i] != strs[j - 1][i] {
                return string(prefix)
            }
        }

        prefix = append(prefix, strs[0][i])
    }

    return string(prefix)
}

```

---

// Эталонное решение
// Можно было не выделять память под слайс байт prefix
// Можно просто выделить переменную под одну букву и в каждой строке смотреть, что под одним и тем же индексом одна и та же буква
// Если нет, то возвращать слайс до индекса с этой буквой

```
package main

// Time: O(n)
// Space: O(1)
func longestCommonPrefix(strs []string) string {
    if len(strs) == 0 {
        return ""
    }

    minLen := len(strs[0])
    for i := 0; i < len(strs); i++ {
        minLen = min(minLen, len(strs[i]))
    }

    for i := 0; i < minLen; i++ {
        ch := strs[0][i]
        for _, str := range strs {
            if ch != str[i] {
                return str[:i]
            }
        }
    }

    return strs[0][:minLen]
}

```

---

// Новая попытка на следующий день
// Ошибка по невнимательности при работе со слайсами строк. Неправильно брал буквы

```
package main

// Time: O(n)
// Space: O(1)
func longestCommonPrefix(strs []string) string {
    if len(strs) == 0 {
        return ""
    }

    minLen := len(strs[0])
    for _, str := range strs {
        minLen = min(minLen, len(str))
    }

    for i := 0; i < minLen; i++ {
        ch := strs[0]
        for k, str := range strs {
            if ch != str {
                return str[:k]
            }
        }
    }

    return strs[0][:minLen]
}

```
