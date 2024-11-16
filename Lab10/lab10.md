// Inefficient loop handling and excessive DOM manipulation

```bash
function updateList(items) {
  let list = document.getElementById("itemList");
  list.innerHTML = "";
  for (let i = 0; i < items.length; i++) {
    let listItem = document.createElement("li");
    listItem.innerHTML = items[i];
    list.appendChild(listItem);
  }
}

```
- Utilizar el items.length en una variable para no tener que calcularlo en cada iteración
- Crear el elemento li fuera del loop para no tener que crearlo en cada iteración

```bash

function updateList(items) {
  let list = document.getElementById("itemList");
  list.innerHTML = "";
  const listItem = document.createElement("li");

  let itemsLength = items.length;
  for (let i = 0; i < itemsLength; i++) {
    listItem.innerHTML = items[i];
    list.appendChild(listItem);
  }
}
```


```bash
// Redundant database queries
public class ProductLoader {
  public List<Product> loadProducts() {
      List<Product> products = new ArrayList<>();
      for (int id = 1; id <= 100; id++) {
          products.add(database.getProductById(id));
      }
      return products;
  }
}
```
- Se puede hacer una sola consulta a la base de datos para obtener todos los productos en lugar de hacer una consulta por cada producto
```bash
public class ProductLoader {
  public List<Product> loadProducts() {
      return DataBase.GetProductsRange(1,100);
  }
}
public class DataBase {
  public List<Product> GetProductsRange(int start, int end) {
      //Obtener los productos en una sola consulta a la base de datos y usar el between
      return GetProductsRange(start, end); 
  }
}
```


// Unnecessary computations in data processing

```bash
public List<int> ProcessData(List<int> data) {
    List<int> result = new List<int>();
    foreach (var d in data) {
        if (d % 2 == 0) {
            result.Add(d * 2);
        } else {
            result.Add(d * 3);
        }
    }
    return result;
}
```
//usar un ternario para eliminar el if else y hacer el cálculo en una sola línea
```bash
public List<int> ProcessData(List<int> data) {
    List<int> result = new List<int>();
    foreach (var d in data) {
        result.Add( d % 2 == 0 ? d * 2 : d * 3); 
    }
    return result;
}
```




