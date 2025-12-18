https://algocode.io/courses/yandex-algorithms/problem/two-arrays-common-prefix
// Попытка #1
// Успех - реализация через хеш мапу

```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefix(nums1 []int, nums2 []int) []int {
    result := make([]int, len(nums1))
    count := make(map[int]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        count[nums1[i]]++
        count[nums2[i]]++

        if i != 0 {
            result[i] += result[i - 1]
        }
        if count[nums1[i]] == 2 {
            result[i]++
        }
        if nums1[i] != nums2[i] && count[nums2[i]] == 2 {
            result[i]++
        }
    }

    return result
}

```

---

// Попытка #2
// Ошибка - реализация через массив
// По невнимательности писал в массив count, а не в result

```
// Time: O(n)
// Space: O(n)
func findCommonPrefix(nums1 []int, nums2 []int) []int {
    result := make([]int, len(nums1))
    count := make([]int, len(nums1) + 1)
    for i := 0; i < len(nums1); i++ {
        count[nums1[i]]++
        count[nums2[i]]++

        if i != 0 {
            count[i] += count[i - 1]
        }
        if count[nums1[i]] == 2 {
            count[i]++
        }
        if nums1[i] != nums2[i] && count[nums2[i]] == 2 {
            count[i]++
        }
    }

    return result
}

```

---

// Попытка #3
// Успех

```
package main

// Time: O(n)
// Space: O(n)
func findCommonPrefix(nums1 []int, nums2 []int) []int {
    result := make([]int, len(nums1))
    count := make([]int, len(nums1) + 1)
    for i := 0; i < len(nums1); i++ {
        count[nums1[i]]++
        count[nums2[i]]++

        if i != 0 {
            result[i] += result[i - 1]
        }
        if count[nums1[i]] == 2 {
            result[i]++
        }
        if nums1[i] != nums2[i] && count[nums2[i]] == 2 {
            result[i]++
        }
    }

    return result
}

// Time: O(n)
// Space: O(n)
func findCommonPrefixHash(nums1 []int, nums2 []int) []int {
    result := make([]int, len(nums1))
    count := make(map[int]int, len(nums1))
    for i := 0; i < len(nums1); i++ {
        count[nums1[i]]++
        count[nums2[i]]++

        if i != 0 {
            result[i] += result[i - 1]
        }
        if count[nums1[i]] == 2 {
            result[i]++
        }
        if nums1[i] != nums2[i] && count[nums2[i]] == 2 {
            result[i]++
        }
    }

    return result
}
```