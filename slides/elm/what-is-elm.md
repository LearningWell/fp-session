## Skapa en Elm-app

`npm install -g elm` <!-- .element: class="fragment" -->

`mkdir my-elm-app && cd my-elm-app` <!-- .element: class="fragment" -->

`elm package install` <!-- .element: class="fragment" -->

`vi App.elm` <!-- .element: class="fragment" -->

`elm make App.elm` <!-- .element: class="fragment" -->

`google-chrome index.html` <!-- .element: class="fragment" -->

---

### Elm

- Frontend (web) <!-- .element: class="fragment" -->

- Egen package manager (enforced semantic versioning) <!-- .element: class="fragment" -->

- Kompileras till JavaScript <!-- .element: class="fragment" -->

- Virtual DOM <!-- .element: class="fragment" -->

- Pure FP <!-- .element: class="fragment" -->

- Starkt statiskt typat (på ett bra sätt) <!-- .element: class="fragment" -->

- No runtime errors (!!!) <!-- .element: class="fragment" -->

- Type inference <!-- .element: class="fragment" -->

- Fantastiskt hjälpsam kompilator (din nya vän) <!-- .element: class="fragment" -->

---

### Blazing fast

![blazingfast](/img/blazingfast.png)

*http://elm-lang.org/blog/blazing-fast-html-round-two*

---

### TimeWell mobile

![twp](/img/twp.png)

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

## Funktioner

```elm
isAnswerCorrect : Question -> String -> Bool
isAnswerCorrect question answer =
  question.answer == answer
```

---

## Funktioner

```elm
prettyPrintTimeLeft : Int -> String
prettyPrintTimeLeft seconds =
  let
    timeLeft : Int
    timeLeft =
      secondsToString seconds
  in
    "Estimated time: " ++ timeLeft
```

---

## Funktioner

```elm
prettyPrintTimeLeft : Int -> String
prettyPrintTimeLeft seconds =
  let
    timeLeft =
      if seconds >= 300 then
        "several minutes"
      else if seconds > 60 then
        "a few minutes"
      else if seconds > 10 then
        "less than 1 minute"
      else
        "a few seconds"
  in
    "Estimated time: " ++ timeLeft
```

---

## Anonyma funktioner
## Higher order functions

```elm
higherOrderGreet : String -> (String -> String)
higherOrderGreet greeting =
  (\name -> greeting ++ " " ++ name ++ "!")
```

```elm
let
  greetingFunc : (String -> String)
  greetingFunc =
    higherOrderGreet "Hello"
in
  greetingFunc "Elm user"
```

Output: "Hello Elm user!"

---

## Partial application

```elm
List.map : (a -> b) -> List a -> List b
```

```elm
greet : String -> String -> String
greet greeting greet =
  greeting ++ " " ++ name ++ "!"
```

```elm
greet "Hello"
-- (String -> String)
```

```elm
List.map (greet "Hello") [ "Kalle", "Nisse", "Yngwie" ]
-- [ "Hello Kalle!", "Hello Nisse!", "Hello Yngwie!" ]
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

```elm
isAnswerCorrect question answer = question.answer == answer
```

---

### Type inference

```elm
canBuyAlcohol age =
  age >= 21
```

```elm
canBuyAlcohol "21"
```

![elm-ti-error](/img/elm-ti-error.png)

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
type Superhero
  = Batman
  | Superman
  | Ironman
  | LearningWellEmployee
```

---

### Type alias

```elm
type alias TrueOrFalse = Bool
```

```elm
type alias Dollars = Float
```

---

### Union types

```elm
type LoggedInUser
  = LoggedIn String
  | Anonymous 
```

---

### Modelling the explicit state

#### Implicit

```js
{ isFetchingUsers = true,
  fetchError = false,
  fetchErrorReason = '',
  users = null
}
```

#### Explicit

```elm
DataState a 
  = NotFetched
  | Fetching
  | FetchError String
  | Fetched a
```

---

### Modelling the explicit state

```elm
DataState a 
  = NotFetched
  | Fetching
  | FetchError String
  | Fetched a
```

```elm
users : DataState (List User)
```

```elm
users = Fetching
```

```elm
users = Fetched usersResult
```

```elm
users = FetchError "Internal server error"
```

#### Type constructor

```elm
Fetching : DataState a
```

```elm
Fetched : a -> Datastate a
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
type LoggedInUser
  = LoggedIn User
  | Anonymous
```

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

### Tuple

```elm
( a, b )
```

```elm
( a, b, c )
```

```elm
{ nameAndAge : ( String, Int ) }
```

```elm
{ nameAndAge = ( "Kalle", 42 ) }
```

```elm
{ nameAndAge = (,) "Kalle" 42 }
```

```elm
(,) : a -> b -> ( a, b )
```

---

### Tuple

```elm
getNameAndAge : User -> ( String, Int )
getNameAndAge user =
  ( user.username, user.age )
```

```elm
formatNameAndAge : ( String, Int ) -> String
formatNameAndAge ( name, age ) =
  name ++ " is " ++ (toString age) ++ " years old"
```

```elm
case getNameAndAge user of
  ( username, age ) ->
    ...
```

```elm
case getNameAndAge user of
  ( username, _ ) ->
    ...
```

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

### Maybe

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

```elm
Maybe.map : (a -> b) -> Maybe a -> Maybe b 
```

```elm
getAgeIfUserCanBuyAlcohol : User -> Maybe Int
getAgeIfUserCanBuyAlcohol user =
  Maybe.map (\age -> if age >= 21 then Just age else Nothing) user.age
```

---

## Let's code

http://elm-lang.org/try
