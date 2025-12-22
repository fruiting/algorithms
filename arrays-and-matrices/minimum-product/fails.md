// https://algocode.io/courses/yandex-algorithms/problem/minimum-product
// Попытка #1
// Сам не решил, пришлось смотреть решение.
// Идея закдючается в следующем:
// 1) Берем первые два числа и среди них определяем min1, min2, max1, max2
// 2) Итерируемся от третьего числа и до конца массива
// 3) В каждой итерации смотрим есть ли числа меньше min1, min2 и больше max1, max2. При необходимости переопределяем
// 4) После определения нужных чисел мы ищем минимальное произведение среди
// 4.1) min1 * min2 - тут понятно, это просто перемножение двух минимальных чисел
// 4.2) min1 * max1 - на случай если min1 отрицательный. При умножении на максимальное положительное число даст наименьшее произведение
// 4.3) max1 * max2 - на случай если min1 и min2 оба отрицательные и дадут слишком большое число в произведении

```
package main

// Time: O(n)
// Space: O(1)
func minPossibleProduct(nums []int) int {
    a, b := nums[0], nums[1]
    min1, min2 := min(a, b), max(a, b)
    max1, max2 := max(a, b), min(a, b)

    for i := 2; i < len(nums); i++ {
        if nums[i] < min1 {
            min2 = min1
            min1 = nums[i]
        } else if nums[i] < min2 {
            min2 = nums[i]
        }

        if nums[i] > max1 {
            max2 = max1
            max1 = nums[i]
        } else if nums[i] > max2 {
            max2 = nums[i]
        }
    }

    return min(min(min1 * min2, min1 * max1), max1 * max2)
}
```
