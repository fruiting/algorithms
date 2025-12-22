// https://algocode.io/courses/yandex-algorithms/problem/pivot-index
// Попытка #1
// Успех
// Первый способ: массивы префиксных и суффиксных сумм

```
// Time: O(n)
// Space: O(n)
func pivotIndex(nums []int) int {
    prefix := make([]int, len(nums) + 1)
    for i := 0; i < len(nums); i++ {
        prefix[i + 1] = nums[i] + prefix[i]
    }

    suffix := make([]int, len(nums) + 1)
    for i := len(nums) - 1; i >= 0; i-- {
        suffix[i] = nums[i] + suffix[i + 1]
    }

    for i := 0; i < len(nums); i++ {
        if suffix[i + 1] == prefix[i] {
            return i
        }
    }

    return -1
}

```

---

// Попытка #2
// Успех
// Второй способ: узнать сумму всех элементов проитерировавшись по массиву
// Зайти в массив второй раз и сравнивать сумму слева и сумму справа

```
package main

// Time: O(n)
// Space: O(1)
func pivotIndex(nums []int) int {
    var totalSum int
    for _, num := range nums {
        totalSum += num
    }

    var leftSum int
    for i, num := range nums {
        if leftSum == totalSum - leftSum - num {
            return i
        }

        leftSum += num
    }

    return -1
}
```
