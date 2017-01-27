### Elm

- Frontend (web) <!-- .element: class="fragment" -->

- Transpileras till JavaScript <!-- .element: class="fragment" -->

- Virtual DOM <!-- .element: class="fragment" -->

- Pure FP <!-- .element: class="fragment" -->

- Strikt statiskt typat (på ett bra sätt) <!-- .element: class="fragment" -->

- No runtime errors (!!!) <!-- .element: class="fragment" -->

- Type inference <!-- .element: class="fragment" -->

- Fantastiskt hjälpsam kompilator (din nya vän) <!-- .element: class="fragment" -->

---

### Blazing fast

![blazingfast](/img/blazingfast.png)

*http://elm-lang.org/blog/blazing-fast-html-round-two*

---

### The Elm architecture

![elm-architecture](/img/elm_architecture.png)

---

## Funktioner

### CShark

```cs
public bool IsAnswerCorrect(Question question, string answer)
       ^                    ^                  ^
    Returtyp             Argument           Argument
```

### Elm

```elm
isAnswerCorrect : Question -> String -> Bool
                  ^           ^         ^
                Argument   Argument   Returtyp
```

---

## Type inference

### CShark

```cs
public bool IsAnswerCorrect(Question question, string answer)
{
  var isAnswerCorrect = question.answer == answer;

  return isAnswerCorrect;
}
```

### Elm

```elm
isAnswerCorrect : Question -> String -> Bool
isAnswerCorrect question answer =
  question.answer == answer
```

```elm
isAnswerCorrect question answer =
  question.answer == answer
```

---

### Types

```elm
type Bool = True | False
```

---

### Types

```elm
type Visibility
  = Visible
  | Hidden
  | Collapsed
```

```elm
type TrueOrFalse = Bool
```

```elm
type Dollars = Float
```

---

### Union types

```elm
type LoggedInUser
  = LoggedIn String
  | Anonymous 
```

---

### Records

```elm
{ id : Int
, username : String
, age : Int
}
```

```elm
isOver50 : { id : Int, username : String, age : Int } -> Bool
isOver50 user =
  user.age > 50
```

```elm
type LoggedInUser
  = LoggedIn { id : Int, username : String, age : Int }
  | Anonymous
```

---

### Type alias

```elm
type alias User =
  { id : Int
  , username : String
  , age : Int
  }
```

```elm
user = { id = 1, username = "Göran", age = 87 }
```

```elm
user = User 1 "Göran" 87
```

```elm
setUsername : User -> String -> User
setUsername user newUsername =
  { user | username = newUsername }
```

---

### Type alias

```elm
type alias User =
  { id : Int
  , username : String
  , age : Int
  }
```

```elm
type LoggedInUser
  = LoggedIn User
  | Anonymous
```

---

### Pattern matching

```elm
getLoggedInUsername : LoggedInUser -> String
getLoggedInUsername loggedInUser =
  case loggedInUser of
    LoggedIn user ->
      user.name

    Anonymous ->
      "Anonymous"

```

---

### Pattern matching

```elm
getLoggedInUsername : LoggedInUser -> String
getLoggedInUsername loggedInUser =
  case loggedInUser of
    LoggedIn user ->
      user.name

    _ ->
      "Not logged in"

```

---

### Pattern matching

```elm
getLoggedInUsername : LoggedInUser -> String
getLoggedInUsername loggedInUser =
  case loggedInUser of
    LoggedIn user ->
      user.name

```

![elm-pm-error](/img/elm-pm-error.png)

---

### Maybe

*null finns inte i Elm*

```
type Maybe a 
  = Just a 
  | Nothing
```

---

### Maybe

```elm
getAgeIfUserCanBuyAlcohol : User -> Maybe Int
getAgeIfUserCanBuyAlcohol user =
  if user.age >= 21 then
    Just user.age
  else
    Nothing
```

---

### Explicit kanske-värde

```elm
getLoggedInUsername : LoggedInUser -> Maybe String
getLoggedInUsername loggedInUser =
  case loggedInUser of
    LoggedIn user ->
      Just user.name

    _ ->
      Nothing
```

```elm
getUsername : LoggedInUser -> String
getUsername loggedInUser =
  case getLoggedInUsername loggedInUser of
    Just username ->
      username

    Nothing ->
      "Not logged in"
```

---

### Maybe

```elm
type alias User =
  { id : Int
  , name : String
  , age : Maybe Int
  }
```

---

### Maybe

```elm
getAgeIfUserCanBuyAlcohol : User -> Maybe Int
getAgeIfUserCanBuyAlcohol user =
  if user.age >= 21 then
    Just user.age
  else
    Nothing
```

```elm
getAgeIfUserCanBuyAlcohol : User -> Maybe Int
getAgeIfUserCanBuyAlcohol user =
  case user.age of
    Just age ->
      if age >= 21 then
        Just age
      else
        Nothing
    
    _ ->
      Nothing
```

---
