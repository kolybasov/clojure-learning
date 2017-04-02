# Functions

## Call

```clojure
; (function param1 param2 paramN)

(+ 1 2 3)
; => 6

(str "Concat " "strings")
; => "Concat strings"

(map inc [0 1 2 3]) ; inc function as map function param
; => (1 2 3 4) returns list
```

## Define

1. `defn`
2. name
3. docstring(optional)
4. params
5. body

```clojure
(defn my-func                 ; 1 2
  "Docstring for my-func"     ; 3
  [param]                     ; 4
  (str "First param " param)) ; 5

(my-func "yeah")
; => "First param yeah"

(defn rest-params ; rest params
  [& rest] ; rest – list
  (map println rest))

(rest-params 1 2 3)
; =>
; 1
; 2
; 3
; (nil nil nil)

(defn rest-params-with-regular
  [param & rest]
  (str param
    ", "
    (clojure.string/join ", " rest)))

(rest-params-with-regular 1 2 3 4 5 6)
; => "1, 2, 3, 4, 5, 6"
```

## Arity overloading

```clojure
(defn greeter
  ([first-name last-name]
    (str "Hello, " first-name " " last-name))
  ([last-name]
    (my-func "Mr." last-name)))

(greeter "Basov")
; => "Hello, Mr. Basov"
(greeter "Mykola" "Basov")
; => "Hello, Mykola Basov"
```

## Destructuring

```clojure
; vector
(defn destruct-vector
  [[first-param second-param & rest-params]]
  (str first-param
    ", "
    second-param
    ", "
    (clojure.string/join ", " rest-params)))

(destruct-vector [1 2 3 4 5 6])
; => "1, 2, 3, 4, 5, 6"

; map
(defn destruct-map
  [{first-param :first second-param :second}]
  (str first-param
    ", "
    second-param))

(destruct-map {:first 1 :second 2})
; => "1, 2"

(defn destruct-map
  [{:keys [first-param second-param] :as all-params}]
  (str first-param
    ", "
    second-param))

(destruct-map {:first 1 :second 2})
; => "1, 2"
```

## Anonymous functions

```clojure
; (fn [params]
;   body)

(map (fn [name] (str "Greetings, " name))
  ["Person1" "Person2"])
; => ("Greetings, Person1" "Greetings, Person2")

; #(+ % 2)
(#(+ % 2) 2) ; only param
; => 4
(#(+ %1 %2) 2 3) ; positional params
; => 5
(#(map inc %&) 0 1 2) ; rest params
; => (1 2 3)
```

## Returning functions

```clojure
(defn adder
  [num]
  #(+ num %))

(def add2 (adder 2))

(add2 2)
; => 4
```