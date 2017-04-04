### Naming

- Types and Modules in camelCase
- Functions and variables in PascalCase
- There are some exceptions...

---

### Pure functions
*data in, data out*

```cs
public int Add(int x, int y) {
  return x + y;
}
```

- Return value is only dependant on the arguments. 
- Same arguments always yields the same result.


note:

- Vad är FP?

- Data in, data out

- Returnerar alltid samma output med samma input

- Inga sidoeffekter, inga utskrifter, ingen io, ingen loggning, ingen inmatning.....

---

## Immutable data

```elm

age = 29
-- 29

age = 30
-- Detected errors in 1 module. DUPLICATE DEFINITION
````

- Variables can not be reassigned.
- Adding an element to a collection returns a new collection with the added element.

---

## Funktioner i ELM

### CShark

```cs
public bool IsAnswerCorrect(Question question, string answer)
{
  return question.answer == answer;
}
```

### Elm


```elm    
isAnswerCorrect question answer =
  question.answer == answer
```

note: 
Notera att vi inte anger några typer. Det betyder dock inte att funktionen är otypad. Återkommer till det.

---

## Typdeklarationer i ELM

### CShark

```cs
public bool IsAnswerCorrect(Question question, string answer)
//     ^                    ^                  ^
//  Returtyp             Argument           Argument
```

### Elm

```elm
isAnswerCorrect : Question -> String -> Bool
--                ^           ^         ^
--             Argument   Argument   Returtyp

isAnswerCorrect question answer =
  question.answer == answer
```

note: Pilnotation. Förklarar senare varför denna syntax används. Typnotation för funktion inte alltid nödvändigt.


---

### Type inference

```elm
canBuyAlcohol age =
  age >= 21

-- canBuyAlcohol : number -> Bool

```

---

### Type inference

```elm
canBuyAlcohol age =
  age >= 21

-- canBuyAlcohol : number -> Bool

```


```elm
canBuyAlcohol "21"
```

![elm-ti-error](/img/elm-ti-error.png)

---

## Higher order functions

```elm
square : Int -> Int
square n = n * n

List.map square [1,2,3]
-- [1,4,9]

-- List.map : (Int -> Int) -> List Int -> List Int
-- List.map : (a -> b) -> List a -> List b

```

- Higher order functions accepts another function as an argument, and/or returns a function.

---

## let / in

```elm

mean a b c =
  let
    sum = a + b + c
  in
    sum / 3

mean a b c = (a + b + c) / 3

```

- Binds a value to a variable, for use in function body (after in)
- Syntactic sugar, can always be replaced by inlining the code.

---

## Partial application

```elm
add : number -> number -> number
add x y = x + y
```

```elm
addFive : number -> number
addFive = add 5

addFive 3
-- 8
```

---

## Partial application II

```elm
add : number -> number -> number
add x y = x + y

listAdder x = List.map (add x)
-- number -> (List number -> List number)

listAdder 2 [ 1, 2, 3 ]
-- [ 3, 4, 5 ]
```

---

## The Elm architecture

![elm-architecture](/img/elm_architecture_simple.png)

---

## Type alias

```elm
type alias Age = Int

type alias Person = { name : String, age : Int }

Person : String -> Int -> Person
Person "Bill" 46 
```
- Types are defined by there signature, not by their names as in most OO language.
- Two alias referring to the same type signature are of equivalent type.

---


## HTML in Elm

-- HTML as data (nested lists)

```elm
fragment =
  div [ class "content" ] 
  [ p []
    [ text "Check this site out: "
    , a [ href "http://elm-lang.org/" ] [ text "Elm" ]
    ]
  ]
```

```html
<div class="content">
  <p>
  Check this site out:
  <a href="http://elm-lang.org/">Elm</a>
</div>
```

---

## Records

```elm
point = { x = 3, y = 4, z = 5}
-- { x = 3, y = 4, z = 5 }

point.x + point.y
-- 7

{ point | x = 8,y = 12 }
-- { x = 8, y = 12, z = 5 } 

point
-- { x = 3, y = 4, z = 5 } 
```

---

## Lists

```elm
list = [1, 2, 3, 4]
listByAppending = [1, 2] ++ [3, 4]
listByPrepending = 1 :: 2 :: [3, 4]

-- [1,2,3,4] : List number
```

---

## Union Types

```elm
type Bool = True | False
```

```elm
type Visibility
= Visible 
| Hidden 
| Collapsed
```

---

## Union types II

```elm
type User = Named String | Anonymous 
```

### Type constructor

```elm
Named : String -> User
Named "Bill"

Anonymous : User
```

---

## Pattern Matching

```elm
userName : User -> String
userName u =   
  case u of
    Anonymous ->
      "guest"

    Named name ->
      name
      
``` 

##### Wildcard

```elm
userName u =   
  case u of
    Named name ->
      name

    _ ->
      "guest"
```

---

## Tuples

```elm
point = ( 3, 4, 5 ) 
-- ( 3, 4, 5 )

( x, _, z ) = point
-- ( 3, 4, 5 )

x
-- 3
```

---

## Anonymous function

```elm
square x = x * x

List.map square [ 1, 2, 3 ]
```

```elm
List.map (\x -> x * x) [ 1, 2, 3 ]
```

- "lambda"


---

## ELM architecture recap


![elm-architecture](/img/elm_architecture_recap.png)


---

## Maybe

```elm

-- Builtin type
type Maybe a = Just a | Nothing

formatData result =
  case result of
    Just data ->
      data.type ++ ":" ++ data.payload

    Nothing ->
      "No data available!"
```

- Handle values which might not be available
- Like a typesafe Null
- If the case of Nothing is not handled, compilation fails.

---

## Hantering av sidoeffekter (Cmd Msg, Task.perform, Html.program istället för Html.beginnerProgram)