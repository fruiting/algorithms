https://algocode.io/courses/yandex-algorithms/problem/find-common-prefix-v2
// Попытка #1
// Ошибка. Сделал подход, аналогичный тому, что в find-common-prefix,
// но без проверки существования в текущей мапе. Такой подход добавляет лишние инкрементирования счетчика

```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefixV2(nums1 []int, nums2 []int) []int {
    m1 := make(map[int]struct{}, len(nums1))
    m2 := make(map[int]struct{}, len(nums2))

    var count int
    result := make([]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        m1[nums1[i]] = struct{}{}
        if _, ok := m2[nums1[i]]; ok {
            count++
        }

        m2[nums2[i]] = struct{}{}
        if _, ok := m1[nums2[i]]; ok {
            count++
        }

        result[i] = count
    }

    return result
}

```

// Попытка #2
// Успех, но пришлось смотреть решение. Сам не справился
// Нужно было сделать не хеш сет, а мапу, где ключ - число, значение - количество этих чисел в строке
// И смотреть, если в текущей мапе значение меньше или равно текущему значению в другой мапе, то инкрементируем
// Был близок, но я искал min() в мапах, а не инкрементировал счетчик

```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefixV2(nums1 []int, nums2 []int) []int {
    m1 := make(map[int]struct{}, len(nums1))
    m2 := make(map[int]struct{}, len(nums2))

    var count int
    result := make([]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        m1[nums1[i]] = struct{}{}
        if _, ok := m2[nums1[i]]; ok {
            count++
        }

        m2[nums2[i]] = struct{}{}
        if _, ok := m1[nums2[i]]; ok {
            count++
        }

        result[i] = count
    }

    return result
}

```
