// https://algocode.io/courses/yandex-algorithms/problem/validate-anagram
// Попытка #1
// Есть два способа решить задачу: через мапу и через массив
// В первой попытке выбрал мапу. Не предусмотрел, что строки могут быть разной длины

```
package main

// Time: O(n)
// Space: O(n)
func isValidAnagram(s string, t string) bool {
    m := make(map[rune]int, len(s))
    for _, ch := range s {
        m[ch]++
    }

    for _, ch := range t {
        val, ok := m[ch]
        if !ok {
            return false
        }

        if val - 1 == 0 {
            delete(m, ch)
        } else {
            m[ch]--
        }
    }

    return true
}

```

---

// Попытка #2
// Успех
// Сделал проверку на соответствие длин строк

```
package main

// Time: O(n)
// Space: O(n)
func isValidAnagram(s string, t string) bool {
    if len(s) != len(t) {
        return false
    }

    m := make(map[rune]int, len(s))
    for _, ch := range s {
        m[ch]++
    }

    for _, ch := range t {
        val, ok := m[ch]
        if !ok {
            return false
        }

        if val - 1 == 0 {
            delete(m, ch)
        } else {
            m[ch]--
        }
    }

    return true
}
```

---

// Попытка #3
// Переписал код целиком. Получилось визуально лучше, но снова напоролся на ту же самую ошибку
// Проблема была в том, что при сравнении значений мап, я обращался к мапе по индексу, а не по символу

```
func isIsomorphic(s string, t string) bool {
    sMap, tMap := make(map[byte]byte, len(s)), make(map[byte]byte, len(s))
	for i := 0; i < len(s); i++ {
		if sMapVal, ok := sMap[s[i]]; ok {
			if sMapVal != tMap[t[i]] {
				return false
			}
		} else {
			sMap[s[i]] = t[i]
		}

		if tMapVal, ok := tMap[t[i]]; ok {
			if tMapVal != sMap[s[i]] {
				return false
			}
		} else {
			tMap[t[i]] = s[i]
		}
	}

	return true
}

```

---

// Попытка #4
// Успех

```
package main

func isIsomorphic(s string, t string) bool {
    sMap, tMap := make(map[byte]byte, len(s)), make(map[byte]byte, len(s))
    for i := 0; i < len(s); i++ {
        if sMapVal, ok := sMap[s[i]]; ok {
            if sMapVal != tMap[t[i]] {
                return false
            }
        } else {
            sMap[s[i]] = t[i]
        }

        if tMapVal, ok := tMap[t[i]]; ok {
            if tMapVal != sMap[s[i]] {
                return false
            }
        } else {
            tMap[t[i]] = s[i]
        }
    }

    return true
}

```