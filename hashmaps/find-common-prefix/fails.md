// https://algocode.io/courses/yandex-algorithms/problem/find-common-prefix
// Попытка #1
// Ошибка заключается в том, что я подумал, что эта задача аналогично two-arrays-common-prefix
// содержит числа от 1 до n. По факту если длина массива 4, в нем все равно может быть число 5
// При таком подходе непонятно какую длину массива выделять.


```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefix(nums1 []int, nums2 []int) []int {
    frequences := make([]int, len(nums1) + 1)
    result := make([]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        if i != 0 {
            result[i] += result[i - 1]
        }

        if frequences[nums1[i]] < 2 {
            frequences[nums1[i]]++
            if frequences[nums1[i]] == 2 {
                result[i]++
            }
        }

        if frequences[nums2[i]] < 2 {
            frequences[nums2[i]]++
            if frequences[nums2[i]] == 2 {
                result[i]++
            }
        }
    }

    return result
}

```

---

// Попытка #2
// Переделал на мапу, но не учел,
// что в одной строке могут быть два одинаковых числа и такой код посчитает это пересечением


```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefix(nums1 []int, nums2 []int) []int {
    frequences := make(map[int]int, len(nums1))
    result := make([]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        if i != 0 {
            result[i] += result[i - 1]
        }

        if frequences[nums1[i]] < 2 {
            frequences[nums1[i]]++
            if frequences[nums1[i]] == 2 {
                result[i]++
            }
        }

        if frequences[nums2[i]] < 2 {
            frequences[nums2[i]]++
            if frequences[nums2[i]] == 2 {
                result[i]++
            }
        }
    }

    return result
}

```

---

// Попытка #3
// Успех
// Переработал решение. Сделал массив frequences и сделал его длину равной максимальному числу из num1 и nums2 + 1
// Добавил каждому массиву по хеш сету, чтобы понимать было ли в этой строке уже такое число или нет 

```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefix(nums1 []int, nums2 []int) []int {
    var maxNum int
    for _, num := range nums1 {
        maxNum = max(maxNum, num)
    }
    for _, num := range nums2 {
        maxNum = max(maxNum, num)
    }

    frequences := make([]int, maxNum + 1)
    m1:= make(map[int]struct{}, len(nums1))
    m2 := make(map[int]struct{}, len(nums1))

    result := make([]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        if i != 0 {
            result[i] += result[i - 1]
        }

        if _, ok := m1[nums1[i]]; !ok {
            m1[nums1[i]] = struct{}{}
            frequences[nums1[i]]++
            if frequences[nums1[i]] == 2 {
                result[i]++
            }
        }
        if _, ok := m2[nums2[i]]; !ok {
            m2[nums2[i]] = struct{}{}
            frequences[nums2[i]]++
            if frequences[nums2[i]] == 2 {
                result[i]++
            }
        }
    }

    return result
}
```

---

// Попытка #4
// Посмотрел эталонное решение и решил, опираясь на него. Успех
// Можно не выделять память под еще один массив frequences, а использовать просто две мапы и счетчик использования числа
// Асимптотика та же, но все равно оптимальнее, чем мое прошлое решение.

```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefix(nums1 []int, nums2 []int) []int {
    m1 := make(map[int]struct{}, len(nums1))
    m2 := make(map[int]struct{}, len(nums2))

    var count int
    result := make([]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        if _, ok := m1[nums1[i]]; !ok {
            m1[nums1[i]] = struct{}{}
            if _, ok := m2[nums1[i]]; ok {
                count++
            }
        }

        if _, ok := m2[nums2[i]]; !ok {
            m2[nums2[i]] = struct{}{}
            if _, ok := m1[nums2[i]]; ok {
                count++
            }
        }

        result[i] = count
    }

    return result
}

```
