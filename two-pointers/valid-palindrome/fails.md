// https://algocode.io/courses/yandex-algorithms/problem/valid-palindrome
// Попытка #1
// Неверно прочитал задание и делал проверку на то, что символы должны являться только буквами, а не буквами или цифрами

```
package main

import (
    "strings"
    "unicode"
)

// Time: O(n)
// Space: O(1)
func isPalindrome(s string) bool {
    p1, p2 := 0, len(s) - 1
    for p1 < p2 {
        if !unicode.IsLetter(rune(s[p1])) {
            p1++

            continue
        }
        if !unicode.IsLetter(rune(s[p2])) {
            p2--

            continue
        }

        if strings.ToLower(string(s[p1])) != strings.ToLower(string(s[p2])) {
            return false
        }

        p1++
        p2--
    }

    return true
}

```
---

// Попытка #2
// Неверно написал условия. Сделал проверку на то, что если символ не является буквой ИЛИ не является цифрой, то пропускаем его
// Надо было написать, что если символ не является буквой И не является цифрой, то пропускаем его

```
package main

import (
    "strings"
    "unicode"
)

// Time: O(n)
// Space: O(1)
func isPalindrome(s string) bool {
    p1, p2 := 0, len(s) - 1
    for p1 < p2 {
        if !unicode.IsLetter(rune(s[p1])) || !unicode.IsDigit(rune(s[p1])) {
            p1++

            continue
        }
        if !unicode.IsLetter(rune(s[p2])) || !unicode.IsDigit(rune(s[p1])) {
            p2--

            continue
        }

        if strings.ToLower(string(s[p1])) != strings.ToLower(string(s[p2])) {
            return false
        }

        p1++
        p2--
    }

    return true
}

```
---

// Попытка #3
// Успех. Исправил условие проверки символов. Теперь если символ не является буквой И не является циврой, то пропускаем его

```
package main

import (
    "strings"
    "unicode"
)

// Time: O(n)
// Space: O(1)
func isPalindrome(s string) bool {
    p1, p2 := 0, len(s) - 1
    for p1 < p2 {
        if !unicode.IsLetter(rune(s[p1])) && !unicode.IsDigit(rune(s[p1])) {
            p1++

            continue
        }
        if !unicode.IsLetter(rune(s[p2])) && !unicode.IsDigit(rune(s[p1])) {
            p2--

            continue
        }

        if strings.ToLower(string(s[p1])) != strings.ToLower(string(s[p2])) {
            return false
        }

        p1++
        p2--
    }

    return true
}

```
---

// Эталонное решение
// Проверка не через пакет unicode, а проверку диапазонов байт.
// Думаю, что без разницы, т.к. используется тот же strings, а unicode под капотом и так оперирует диапазонами байт.

```
package main

import (
    "strings"
)

func isPalindrome(s string) bool {
    l := 0
    r := len(s) - 1

    for l < r {
        // переходим к следующей букве пока l и r
        // не будут указывать на буквы или цифры
        for l < r && !isAlnum(s[l]) {
            l++
        }
        for l < r && !isAlnum(s[r]) {
            r--
        }
        // оба символа - буквы или цифры
        if strings.ToLower(string(s[l])) != strings.ToLower(string(s[r])) {
            return false
        }
        l++
        r--
    }
    return true
}

func isAlnum(c byte) bool {
    return ('a' <= c && c <= 'z') || ('A' <= c && c <= 'Z') || ('0' <= c && c <= '9')
}

```
