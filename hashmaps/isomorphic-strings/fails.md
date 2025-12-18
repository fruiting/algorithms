// https://algocode.io/courses/yandex-algorithms/problem/isomorphic-strings
// Попытка #1
// Изначально идея была в том, чтобы создать одну мапу для маппинга символов из двух строк
// Итерироваться по второй строке, записывать в мапу в качестве ключа символ из первой строки по текущему индексу,
// если его там нет, и текущий символ из второй строки, а если есть, то смотреть, что в мапе под этим ключом лежит текущий символ
// Проблема в том, что к примеру в кейсе s = "badc", t = "baba"
// Мы запишем в мапу новый ключ "d" и под него значение "b", и ничего не будем знать о том, что
// вообще-то значение "b" уже принадлежит ключу "b"

```
package main

// Time: O(n)
// Space: O(n)
func isIsomorphic(s string, t string) bool {
    equalityMap := make(map[byte]rune, len(s))
    for k, v := range t {
        if mapValue, ok := equalityMap[s[k]]; ok {
            if mapValue != v {
                return false
            }

            continue
        }

        equalityMap[s[k]] = v
    }

    return true
}

```

---

// Попытка #2
// Решил исправить это добавлением второго маппинга
// Т.е. должны быть две зеркальные мапы. Идея правильная, но не смог нормально написать код,
// словил ошибку, устал и пошел смотреть видео разбор 

```
package main

// Time: O(n)
// Space: O(n)
func isIsomorphic(s string, t string) bool {
    m1 := make(map[rune]rune, len(s))
    m2 := make(map[rune]rune, len(s))

    for idx, ch := range t {
        m1Val, ok := m2[ch]
        if !ok {
            m1[ch] = ch
        } else {
            if m1Val != ch {
                return false
            }
        }

        m2Val, ok := m2[ch]
        if !ok {
            m2[ch] = rune(s[idx])
        } else {
            if m2Val != m1[rune(s[idx])] {
                return false
            }
        }
    }

    return true
}


```

---

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