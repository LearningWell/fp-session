## Vi kommer hålla till i pure FP-världen

---

## Hur skriver man kod i funktionell programmering?

---

## Sidoeffekter i FP är svårt

... och det är bra att det är svårt

---

## Deklarativt

Man beskriver *vad* man vill göra, inte *hur*

---

## Imperativt

```cs
var activeUsers = new List<User>();

foreach (var user in _allUsers)
{
  if (user.IsActive)
  {
    list.Add(user);
  }
}

return activeUsers;

```

## Deklarativt

```js
return filter(allUsers, user => user.isActive);
```

---

## Immutability

---

```js
let x = 5;

function addToX(y) {
  return x + y; 
};

x = 10; // Inte tillåtet

let result = addToX(10); // 15?
```

---

## Allt är en expression

*någonting måste alltid returneras*

---

### void är ingen giltig returtyp i FP

```cs
public void WriteToLog(string logMessage)
{
  _logger.Log(logMessage);
}
```

---

### Implicita returvärden tillåts inte

```js
function getSomeValue(x) {
  if (x === 42) {
    return "The number is 42!";
  }
}

getSomeValue(42);
// "The number is 42!"

getSomeValue(10);
// undefined
```