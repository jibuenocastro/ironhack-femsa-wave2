# Lab 5

## 1.- SQL Query Optimization

```bash
SELECT o.OrderID, SUM(od.Quantity * od.UnitPrice) AS TotalPrice
FROM Orders o
INNER JOIN OrderDetails od ON o.OrderID = od.OrderID
WHERE od.Quantity > 10
GROUP BY o.OrderID;
 ```

```bash
CREATE INDEX idx_OrdersDetails on OrderDetails(OrderID,Quantity);
```

### Optimización de consultas SQL

1.-Agregar índices a las columnas que se utilizan en las cláusulas WHERE y JOIN.


```bash
SELECT CustomerName FROM Customers WHERE City = 'London' ORDER BY CustomerName;
CREATE INDEX idx_Customers_City ON Customers(City);
 ```

### Optimización de consultas SQL

1.-Agregar índices a las columnas que se utilizan en las cláusulas WHERE y JOIN en el campo city y CustomerName


---------
## 2. NoSQL Query Implementation

```bash
db.posts
  .find({ status: "active" }, { title: 1, likes: 1 })
  .sort({ likes: -1 });
```

```bash
db.posts.createIndex({ status: 1, likes: -1, title: 1 });
```

1.-Para mejorar el rendimiento de la consulta, se puede crear un índice compuesto en los campos status, likes y title.
2.-Determinar si es necesario poner un tipo limite en la consulta o una paginación para evitar traer todos los registros de la colección.



```bash
db.users.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$location", totalUsers: { $sum: 1 } } },
]);
```


```bash
db.users.createIndex({ status: 1, location: 1 });
```

1.-Para mejorar el rendimiento de la consulta, usar un indice con status y location para mejorar la velocidad de la consulta.