https://algocode.io/courses/yandex-algorithms/problem/find-common-prefix-v2
// Попытка #1
// Ошибка. Решил, что надо создать массив длинной maxCits + 1.
// Ключи - количество цитирований, значения - номер статьи
// После этого пройтись от конца до начала и вычитать из номера статьи индекс.

```
package main

func findHirschIndex(citations []int) int {
    var maxCits int
    for i := 0; i < len(citations); i++ {
        maxCits = max(maxCits, citations[i])
    }

    citsArr := make([]int, maxCits + 1)
    for i := 0; i < len(citations); i++ {
        citsArr[citations[i]] = i + 1
    }

    idx := len(citations)
    for i := len(citsArr) - 1; i >= 0; i-- {
        if citsArr[i] == 0 {
            continue
        }

        if citsArr[i] <= idx {
            idx--
        }
    }

    return len(citations) - idx
}
```

---

// Попытка #2
// Пришлось смотреть видео урок.
// Ошибся в том, что надо возвращать. Вернул не индекс, на котором количество цитирований
// больше или равно количеству статей, а количество цитирований

```
package main

func findHirschIndex(citations []int) int {
	count := make([]int, len(citations)+1)
	for i := 0; i < len(citations); i++ {
		count[min(citations[i], len(count)-1)]++
	}

	var idx int
	for i := len(count) - 1; i >= 0; i-- {
		idx += count[i]
		if idx >= i {
			break
		}
	}

	return idx
}
```

---

// Попытка #3
// Успех

```
package main

func findHirschIndex(citations []int) int {
    count := make([]int, len(citations)+1)
	for i := 0; i < len(citations); i++ {
		count[min(citations[i], len(count)-1)]++
	}

	var idx int
	for i := len(count) - 1; i >= 0; i-- {
		idx += count[i]
		if idx >= i {
			return i
		}
	}

	return 0
}

```
