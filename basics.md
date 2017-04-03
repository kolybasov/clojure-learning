# Clojure basics

Syntax, flow control and data structures

## Operations

`(operator  operand1 operand2 … operandn)`

```clojure
(+ 1 2 3)
; => 6

(+ 1,2,3)
; => 6
```

_Commas treated as whitespace._

## Control Flow

### Truthiness

Only `false` and `nil` are falsy, all others are truthy.

### if

```clojure
(if boolean ; (truthy/falsey)
  then
  else) ; else is optional
```

### when

```clojure
(when true
  "some value")
```

### do

```clojure
(do
  (operation1)
  (operation2)
  ; …
  (operationN))
```

### let

```clojure
; (let [var value]
;   var)
(let [x 10]
  x)
; => 10
```

Destructuring is working the same way as in the [functions](./functions#destructuring).

```clojure
(let [[head & tail] [1 2 3 4]]
  [head tail])
; => [1 (2 3 4)]
```

### loop

```clojure
; (loop [var val]
;   (body)
;   (if (nil? var)
;     (println "end")
;     (recur nil))
(loop [i 1]
  (println (str "i: " i))
  (if (> i 2)
    (println "End")
    (recur (inc i))))
; =>
; i: 0
; i: 1
; i: 2
; i: 3
; End
```

## Data structures

### nil

Means no value.

### Numbers

- `93` – integer
- `1.2` – float
- `1/3` – ratio

### Strings

- `"string"`
- `"string with \"escapes\" is valid as well"`
- `'invalid string'`

### Maps

```clojure
{} ; empty map

{:key "val"} ; map with keywords

{:nested {:key "val"}} ; nested maps

{:func +} ; functions as values

(get {:key "val"} :key "default value")
; => "val"

({:key "val"} :key "default value")
; => "val"
```

### Vectors

```clojure
[1 "str" :keyword]

(get [1 2 3] 0)
; => 1
```

### Keywords

```clojure
:keyword
:1keyword
:_keyword
```

### Lists

```clojure
'(1 2 3 4)

(nth '(:a :b :c) 0)
; => :a
```

### Sets

```clojure
#{1 1 2 2}
; => #{1 2}
```

### Regular expressions

```clojure
; #"^(\d|\s)"
(clojure.string/replace "1key" #"^(\d|\s)" "")
; => "key"
```

## Common functions

- `nil?` – check if value is `nil`
- `str` – concat strings
- `=` – equal args
- `or` – return first truthy value
- `and` – return first falsy value
- `def` – bind name to value
- `hash-map` – function to create map
- `get` – lookup key/index in the `map/vector/list`
- `get-in` – get nested key in then `map/vector`
- `vector` – create vector
- `conj` – add element to `vector/list`
- `nth` – get element from the list
- `list` – create list
- `hash-set` – create set
- `set` – create set from `vector/list`
- `contains?` – check if value is present in the set
- `into` – insert seq into seq