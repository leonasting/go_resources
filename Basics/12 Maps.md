## Maps

A map maps keys to values.

The zero value of a map is `nil`. A `nil` map has no keys, nor can keys be added.

The `make` function returns a map of the given type, initialized and ready for use.

```go
type Vertex struct {
	Lat, Long float64
}

var m map[string]Vertex

func main() {
	m = make(map[string]Vertex)
	m["Bell Labs"] = Vertex{
		40.68433, -74.39967,
	}
	fmt.Println(m["Bell Labs"])
}

```
## Map literals

Map literals are like struct literals, but the keys are required.

## Map literals continued

If the top-level type is just a type name, you can omit it from the elements of the literal.

```go
type Vertex struct {
	Lat, Long float64
}

var m = map[string]Vertex{
	"Bell Labs": {40.68433, -74.39967},
	"Google":    {37.42202, -122.08408},
}

func main() {
	fmt.Println(m)
}
//map[Bell Labs:{40.68433 -74.39967} Google:{37.42202 -122.08408}]
```

## Mutating Maps

Insert or update an element in map `m`:

`m[key] = elem`

Retrieve an element:

`elem = m[key]`

Delete an element:

delete(m, key)

Test that a key is present with a two-value assignment:
`elem, ok = m[key]`

If `key` is in `m`, `ok` is `true`. If not, `ok` is `false`.

If `key` is not in the map, then `elem` is the zero value for the map's element type.

**Note:** If `elem` or `ok` have not yet been declared you could use a short declaration form:

`elem, ok := m[key]`

```go
func main() {
	m := make(map[string]int)

	m["Answer"] = 42
	fmt.Println("The value:", m["Answer"])

	m["Answer"] = 48
	fmt.Println("The value:", m["Answer"])

	delete(m, "Answer")
	fmt.Println("The value:", m["Answer"])

	v, ok := m["Answer"]
	fmt.Println("The value:", v, "Present?", ok)
}

//The value: 42
//The value: 48
//The value: 0
//The value: 0 Present? false
```

Excercise:
Implement `WordCount`. It should return a map of the counts of each “word” in the string `s`. The `wc.Test` function runs a test suite against the provided function and prints success or failure.

You might find [strings.Fields](https://go.dev/pkg/strings/#Fields) helpful.
```go
package main

import (
	"golang.org/x/tour/wc"
	"strings"
)

func WordCount(s string) map[string]int {
	ans := make(map[string]int)
	for _,v:= range strings.Split(s," "){
		_, ok := ans[v]
		if ok{
			ans[v] += 1
			}else{
				ans[v] = 1
				}
		} 

	return ans
	}

func main() {
	wc.Test(WordCount)
}
```