// https://algocode.io/courses/yandex-algorithms/problem/y-symmetry-strong
// Попытка #1
// Ошибки синтаксиса.
// 1) Неверно проинициализировал minX и maxX. Случайно указал их массивами, а не числами
// 2) Забыл написать return в функции abs
// Логика верная с самого начала.
// Нужно заполнить мапу, где ключ - массив с координатами, значение - количество таких координат
// Найти minX и maxX для формулы |x - maxX| + minX. Так мы найдем "зеркальный" х для текущей координаты в каждой итерации
// Ищем в мапе зеркальные иксы. Если есть, уменьшаем их количество. Если нет - значит нет симметрии.

```
package main

// Time: O(n)
// Space: O(n)
func isSymmetric(points [][]int) bool {
    coordsMap := make(map[[2]int]int, len(points))
    minX, maxX := points[0], points[0]
    for _, coords := range points {
        coordsMap[[2]int{coords[0], coords[1]}]++
        minX = min(minX, coords[0])
        maxX = max(maxX, coords[0])
    }

    for _, coords := range points {
        reversed := [2]int{abs(coords[0] - maxX) + minX, coords[1]}
        if _, ok := coordsMap[reversed]; !ok {
            return false
        }

        coordsMap[reversed]--
        if coordsMap[reversed] == 0 {
            delete(coordsMap, reversed)
        }
    }

    return true
}

func abs(num int) int {
    if num < 0 {
        return -num
    }
}

```

---

// Попытка #2
// Успех

```
package main

// Time: O(n)
// Space: O(n)
func isSymmetric(points [][]int) bool {
    coordsMap := make(map[[2]int]int, len(points))
    minX, maxX := points[0][0], points[0][0]
    for _, coords := range points {
        coordsMap[[2]int{coords[0], coords[1]}]++
        minX = min(minX, coords[0])
        maxX = max(maxX, coords[0])
    }

    for _, coords := range points {
        reversed := [2]int{abs(coords[0] - maxX) + minX, coords[1]}
        if _, ok := coordsMap[reversed]; !ok {
            return false
        }

        coordsMap[reversed]--
        if coordsMap[reversed] == 0 {
            delete(coordsMap, reversed)
        }
    }

    return true
}

func abs(num int) int {
    if num < 0 {
        return -num
    }

    return num
}

```