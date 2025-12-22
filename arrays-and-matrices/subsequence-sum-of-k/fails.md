// https://algocode.io/courses/yandex-algorithms/problem/subsequence-sum-of-k
// Попытка #1
// Ошибка
// Вообще неверно решил задачу. Пытался решить через массив префиксных сумм
// Посмотрел решение. Нужно решать через переменную sum и мапу

```
package main

// Time: O(n)
// Space: O(n)
func subsequenceSumK(nums []int, k int) int {
    prefix := make([]int, len(nums) + 1)
    for i, num := range nums {
        prefix[i + 1] = num + prefix[i]
    }

    for i := 0; i < len(prefix); i++ {
        if prefix[i] < k {
            continue
        } else if prefix[i] == k {
            return i - 1
        }

        l := 0
        for l <= i {
            if prefix[i] - prefix[l] == k || prefix[i] - l == 0 {
                return i - 1
            }

            l++
        }
    }

    return -1
}

```

---

// Попытка #2
// Успех
// Изучил решение
// Решение заключается в том, что бы писать в мапу на каждой итерации префиксные суммы
// и на каждой же итерации смотреть, если в мапе есть currSum - k
// Например есть массив [1, 2, 3] и k = 5
// Значит в мапе будет [0: 1, 1: 1, 3: 1]
// Потому что на каждой итерации суммы будут 0, 1, 3, 6
// 6 в мапу не попадает, потому что 6 - 3 = 3 и ключ 3 есть в мапе

```
package main

// Time: O(n)
// Space: O(n)
func subsequenceSumK(nums []int, k int) int {
    m := make(map[int]int, len(nums))
    m[0] = 1

    idx := -1
    var currSum int
    for i, num := range nums {
        currSum += num
        if _, ok := m[currSum - k]; ok {
            idx = i

            break
        }

        m[currSum]++
    }

    return idx
}


```
