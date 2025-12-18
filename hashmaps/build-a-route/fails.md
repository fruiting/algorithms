// https://algocode.io/courses/yandex-algorithms/problem/build-a-route
// Попытка #1
// Успех
// Решил задачу с первой попытки и по симптоматике прохожу,
// но эталонное решение немного оптимальнее в абсолютных числах памяти

```
package main

// Time: O(n)
// Space: O(n)
func route(tickets [][]string) []string {
    fromMap := make(map[string]struct{}, len(tickets))
    toMap := make(map[string]struct{}, len(tickets))
    routeMap := make(map[string]string, len(tickets))

    for _, ticket := range tickets {
        routeMap[ticket[0]] = ticket[1]

        fromMap[ticket[0]] = struct{}{}
        toMap[ticket[1]] = struct{}{}
    }

    for city := range fromMap {
        if _, ok := toMap[city]; ok {
            delete(fromMap, city)
            delete(toMap, city)
        }
    }

    var fromCity string
    for city := range fromMap {
        fromCity = city

        break
    }

    route := make([]string, 0, len(tickets) + 1)
    route = append(route, fromCity)
    nextCity := routeMap[fromCity]
    for nextCity != "" {
        route = append(route, nextCity)
        nextCity = routeMap[nextCity]
    }

    return route
}

```

---

// Попытка #2
// Успех
// Можно было убрать мапу fromMap и сделать решение более оптимальным

```
package main

// Time: O(n)
// Space: O(n)
func route(tickets [][]string) []string {
    toMap := make(map[string]struct{}, len(tickets))
    routeMap := make(map[string]string, len(tickets))

    for _, ticket := range tickets {
        routeMap[ticket[0]] = ticket[1]
        toMap[ticket[1]] = struct{}{}
    }

    var fromCity string
    for _, ticket := range tickets {
        if _, ok := toMap[ticket[0]]; !ok {
            fromCity = ticket[0]

            break
        }
    }

    route := make([]string, 0, len(tickets) + 1)
    route = append(route, fromCity)
    nextCity := routeMap[fromCity]
    for nextCity != "" {
        route = append(route, nextCity)
        nextCity = routeMap[nextCity]
    }

    return route
}

```
