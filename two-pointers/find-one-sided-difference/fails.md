// https://algocode.io/courses/yandex-algorithms/problem/find-one-sided-difference
// Попытка #1
// В случае окончания проходки по nums2 надо смерджить оставшиеся элементы из nums1
// Если nums1 закончится раньше, то с таким подходом будет паника

```
package main

func findDifference(nums1 []int, nums2 []int) []int {
    result := make([]int, 0, len(nums1))
    p1, p2 := 0, 0
    for p1 < len(nums1) && p2 < len(nums2) {
        if nums1[p1] < nums2[p2] {
            result = append(result, nums1[p2])
            p1++
        } else if nums1[p1] == nums2[p2] {
            p1++
        } else {
            p2++
        }
    }

    return append(result, result[p1:]...)
}

```

---

// Попытка #2
// В случае окончания проходки по nums2 надо смерджить оставшиеся элементы из nums1
// Панику поправил, но были опечатки
// В слайс result добавлял nums1[p2], а не nums1[p1]
// Делал result = append(result, result[p1:]...), т.е. брал срез не от того массива
// Надо было result = append(result, nums1[p1:]...)

```
package main

func findDifference(nums1 []int, nums2 []int) []int {
    result := make([]int, 0, len(nums1))
    p1, p2 := 0, 0
    for p1 < len(nums1) && p2 < len(nums2) {
        if nums1[p1] < nums2[p2] {
            result = append(result, nums1[p2])
            p1++
        } else if nums1[p1] == nums2[p2] {
            p1++
        } else {
            p2++
        }
    }

    if p1 < len(nums1) {
        result = append(result, result[p1:]...)
    }

    return result
}


```

---

// Попытка #2
// Успех
// Сделал добавление оставшихся в nums1 элементов после окончания проходки по nums2
// Исправил опечатки, сделанные по невнимательности

```
package main

func findDifference(nums1 []int, nums2 []int) []int {
    result := make([]int, 0, len(nums1))
    p1, p2 := 0, 0
    for p1 < len(nums1) && p2 < len(nums2) {
        if nums1[p1] < nums2[p2] {
            result = append(result, nums1[p2])
            p1++
        } else if nums1[p1] == nums2[p2] {
            p1++
        } else {
            p2++
        }
    }

    if p1 < len(nums1) {
        result = append(result, nums1[p1:]...)
    }

    return result
}


```

---

// Попытка #3
// Успех
// Новое решение из головы, но оно очень похоже на эталонное

```
package main

func findDifference(nums1 []int, nums2 []int) []int {
    result := make([]int, 0, len(nums1))
    p1, p2 := 0, 0
    for p1 < len(nums1) && p2 < len(nums2) {
        if nums1[p1] < nums2[p2] {
            result = append(result, nums1[p2])
            p1++
        } else if nums1[p1] == nums2[p2] {
            p1++
        } else {
            p2++
        }
    }

    if p1 < len(nums1) {
        result = append(result, result[p1:]...)
    }

    return result
}


```