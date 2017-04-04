### NIce Pure functions
*data in, data out*

```cs
public int Add(int x, int y) {
  return x + y;
}
```

note:

- Vad är FP?

- Data in, data out

- Returnerar alltid samma output med samma input

- Inga sidoeffekter

---

## Impure functions
### Gömda inputs och outputs

```cs
private int currentValue;

public int AddToValue(int valueToAdd) {
  currentValue = currentValue + valueToAdd;

  return currentValue;
}
```

### Pure function

```cs
private const int x = 10;

public int AddToX(int y) {
  return x + y;
}
```

---

## Gömda inputs och outputs

```cs
private Database database;

public int AddToValue(int valueToAdd)
{
  var currentVal = database.GetValue();
  var newVal = currentVal + valueToAdd;

  database.WriteValue(newVal);

  return newVal;
}
```

---

## Gömda inputs och outputs

kallas även sidoeffekter

---

## Exempel på sidoeffekter

- Mutering av state

- Rörlig tid (DateTime.Now)

- Extern kommunikation

- Slumpgenerering av data

---

## Mutering av state

```js
let x = 5;

x = 10;

console.log(x);
// 10
```

## Immutability

```js
const x = 5;

// x = 10 <-- Inte tillåtet

console.log(x);
// 5
```

---

## Mutering av state

```js
function updatePlayerScore (player, score) {
  player.score += score;
}
```

## Immutability

```elm
updatePlayerScore player score =
  { player | score = score }
```


---

## Mutering skapar osäkerhet

```js
function addToList(list, element) { ... }
```

```js
let originalItems = [ 1, 2, 3, 4 ];

// Behöver jag klona originalItems först?
let allItems = addToList(originalItems, 5);

writeToConsole(originalItems); 
// [ 1, 2, 3, 4 ] ?

writeToConsole(allItems);      
// [ 1, 2, 3, 4, 5 ] ?
```

---

### Sidoeffekter skapar beroenden

```cs
private Database database;
private UserCache userCache;

public User GetUser(int userId) {
  var user = userCache.GetUser(userId)

  if (user == null) {
    user = database.GetUser(userId);
    userCache.CacheUser(user);
  }

  return user;
}
```

---

### Sidoeffekter skapar ett isberg av komplexitet

```cs
public bool ProcessNextMessage(Queue queue) { ... }
```

![isberg](/img/iceberg.jpg)

---


## Funktionell programmering

- Undviker sidoeffekter så långt det går

- Hanterar sidoeffekter vid sidan om när man måste ha dom

- Varje funktion beskriver endast relationen mellan input och output

- Deklarativt - man beskriver *vad* man vill göra, inte *hur*

---

## Kan du hitta sidoeffekten?

*Två tips på hur man kan känna igen dom*

---

```cs
public int GetActiveItemCount() {
  ...
}
```

---

```cs
public void AddNewItem(string itemTitle) {
  ...
}
```