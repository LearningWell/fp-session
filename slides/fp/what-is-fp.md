## Vad är FP?

---

### Pure functions

```js
function add(x, y) {
  return x + y;
}
```

*data in, data out*

note:

- Vad är FP?

- Data in, data out

- Returnerar alltid samma output med samma input

- Inga sidoeffekter

---

## Gömda inputs och outputs

```cs
private int currentValue;

public int AddToValue(int valueToAdd)
{
  currentValue = currentValue + valueToAdd;

  return currentValue;
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

kallas sidoeffekter

---

## Mutering av state

```js
let x = 5;

function addToX(y) {
  return x + y; 
};

x = 10;

let result = addToX(10); // 15?
```

---

## Mutering av state

```js
function addToList(list, element) { ... }

let originalItems = [ 1, 2, 3, 4 ];

let allItems = addToList(originalItems, 5);

writeToConsole(originalItems); // [ 1, 2, 3, 4 ] ?
writeToConsole(allItems);      // [ 1, 2, 3, 4, 5 ] ?
```

---

### Sidoeffekter skapar ett isberg av komplexitet

```cs
public bool ProcessNextMessage(Queue queue) { ... }
```

![isberg](/img/iceberg.jpg)

---

## Kan du hitta sidoeffekten?

---

```js
itemList.getActiveItemCount = function() {
  let count = 0;
  
  for (let item in this.list) {
    count += item.active ? 1 : 0;
  }

  return count;
}
```

---

```js
itemList.addNewItem = function(itemText) {
  this.list.push({
    text: itemText, 
    active: true 
  });
}
```

---

## Exempel på sidoeffekter

- Mutering av state

- Tid (DateTime.Now)

- Extern kommunikation

- Slumpning av data

---

## Sidoeffekter försvårar enhetstestning

Ingen blackbox-testning

---

## Sidoeffekter försvårar isolering

Beroenden mellan komponenter

---

## Sidoeffekter förstör composition

Små delar kan inte enkelt sättas ihop för ett större sammanhang

---

## Så... vad är FP?

---

## Funktionell programmering

- Undviker sidoeffekter

- Kontrollerar sidoeffekter när man måste ha dom

- Varje funktion/komponent beskriver relationen mellan input och output

---

## FP definieras inte av

- map, filter, fold

- higher order functions

- type classes

- monads

- ...

---

## FP förenklar

- förståelse av kod

- enhetstester

- återanvändbarhet

- concurrency