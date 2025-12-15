package main

// Попытка #1
// Двигал оба указателя при каждой итерации и записывал два числа за одну итерацию в результирующий массив
// Нужно было сдвигать указатель, у которого квадрат числа был больше
// Помимо этого не добавлял последний оставшийся элемент в результирующий массив

```
// Time: O(n)
// Space: O(n)
func sortedSquares(nums []int) []int {
    result := make([]int, len(nums))
    p1, p2, p3 := 0, len(nums) - 1, len(nums) - 1
    for p1 < p2 {
        squareP1 := nums[p1] * nums[p1]
        squareP2 := nums[p2] * nums[p2]

        if squareP1 > squareP2 {
            result[p3] = squareP1
            result[p3 - 1] = squareP2
        } else {
            result[p3] = squareP2
            result[p3 - 1] = squareP1
        }

        p1++
        p2--
        p3 = p3 - 2
    }

    return result
}
```

---

// Попытка #2
// Сделал запись последнего элемента в результирующий массив,
// но продолжал двигать оба указателя и писать за одну итерацию оба элемента

```
package main

// Time: O(n)
// Space: O(n)
func sortedSquares(nums []int) []int {
    result := make([]int, len(nums))
    p1, p2, p3 := 0, len(nums) - 1, len(nums) - 1
    for p1 < p2 {
        squareP1 := nums[p1] * nums[p1]
        squareP2 := nums[p2] * nums[p2]

        if squareP1 > squareP2 {
            result[p3] = squareP1
            result[p3 - 1] = squareP2
        } else {
            result[p3] = squareP2
            result[p3 - 1] = squareP1
        }

        p1++
        p2--
        p3 = p3 - 2
    }

    if p1 == p2 {
        result[p3] = nums[p1] * nums[p1]
    }

    return result
}
```

---

// Попытка #3
// Успех
// Добавление в результирующий массив по одному элементу за итерацию
// После выполнения цикла добавляю оставшийся элемент в результирующий массив

```
package main

// Time: O(n)
// Space: O(n)
func sortedSquares(nums []int) []int {
    result := make([]int, len(nums))
    p1, p2, p3 := 0, len(nums) - 1, len(nums) - 1
    for p1 < p2 {
        squareP1 := nums[p1] * nums[p1]
        squareP2 := nums[p2] * nums[p2]

        if squareP1 > squareP2 {
            result[p3] = squareP1
            p1++
        } else {
            result[p3] = squareP2
            p2--
        }

        p3--
    }

    if p1 == p2 {
        result[p3] = nums[p1] * nums[p1]
    }

    return result
}
```