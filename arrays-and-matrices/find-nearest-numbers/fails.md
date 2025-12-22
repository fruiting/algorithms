// https://algocode.io/courses/yandex-algorithms/problem/find-nearest-numbers
// Попытка #1
// Ошибка
// Идея в целом правильная, но не дожал ее
// Инициализировал результирующий массив и заполняю его, проходя левым и правым указателями

```
package main

// Time: O(n)
// Space: O(n)
func findNearestNumbers(nums []int, idx int, k int) []int {
    l, r := idx - 1, idx + 1
    result := make([]int, len(nums))
    result[idx] = nums[idx]

    for l >= 0 && r < len(nums) {
        if abs(nums[l] - nums[idx]) <= abs(nums[r] - nums[idx]) {
            result[l] = nums[l]
            l--
        } else {
            result[r] = nums[r]
            r++
        }
    }

    if l < 0 {
        l = 0
    }

    return result[l:r]
}

func abs(num int) int {
    if num < 0 {
        return -num
    }

    return num
}

```

---

// Попытка #2
// Пришлось смотреть решение
// Я невнимательно прочитал/забыл, что можно возвращать значения В ЛЮБОМ порядке
// Из-за того, что у меня не было такой мысли, я пытался вернуть в строго соответствии, чем усложнял себе жизнь
// При любом порядке достаточно просто добавлять в массив значения
// и идти пока не добавим k элементов

```
package main

// Time: O(n)
// Space: O(n)
func findNearestNumbers(nums []int, idx int, k int) []int {
    if k == 0 {
        return nil
    }

    result := make([]int, 0, len(nums))
    result = append(result, nums[idx])

    l := idx - 1
    r := idx + 1
    for i := 0; i < k - 1; i++ {
        if r >= len(nums) ||
            (l >= 0 && abs(nums[l] - nums[idx]) <= abs(nums[r] - nums[idx])) {
            result = append(result, nums[l])
            l--
        } else {
            result = append(result, nums[r])
            r++
        }
    }

    return result
}

func abs(num int) int {
    if num < 0 {
        return -num
    }

    return num
}

```
