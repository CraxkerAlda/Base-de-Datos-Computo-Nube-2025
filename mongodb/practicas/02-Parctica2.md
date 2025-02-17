
# Consultas 

1. Cargar el fichero empleados.json

- En local:
    Comando:
      mongoimport --db curso --collection empleados --file empleados.json

- Docker:
    comando:
      mongoimport --port 80 --db curso --collection empleados --file empleados.json

2. Utilzar la base de datos curso

```json
use curso
```

3. Buscar todos los empleados que trabajen en Google

```Json
db.empleados.find({empresa:'Google'})
```

4. Empleados que vivan en Perú

```Json
db.empleados.find({pais:'Peu'})
```

5. Empleados que ganen mas de 8000 dolares

```Json
db.empleados.find({
       salario: {$gt:8000}
       })
```

6. Empleados con ventas inferiores a 10000

```Json
db.empleados.find({ ventas: { $lt: 10000} } )
```

7. Realizar la consulta anterior pero devolviendo una sola fila

```Json
db.empleados.findOne({ ventas: { $lt: 10000} } )
```

8. Empleados qur trabajan en Google o En Yahoo con el operador $in

```json
db.empleados.find({ empresa: { $in: ['Yahoo', 'Google']} } )
```

9. Empleados de Amazon que ganen mas de 9000 dolares 

```json
db.empleados.find({ empresa: { $eq: 'Amazon'}, salario: {$gt: 9000} } )
```

10. Empleados que trabajan en Google o en Yahooo con el operador $or

```json
db.empleados.find({
  $or:[{empresa:'Amazon'}, {empresa:{$eq:'Yahoo'}}]
})
```

11. Empleados que trabajen en Yahoo que ganen mas de 6000 o empleados que trabajen 
en Google que tengan ventas inferiores a 20000

```json
db.empleados.find( { 
  $or: [ 
    { $and:[{empresa: 'Yahoo'}, {salario: {$gt:6000}}] }, 
    { $and: [{empresa: 'Google'}, {ventas: {$lt:20000}}] } 
    ] 
  })
```

12. Vizualizar el nombre, apellidos y pais de cada empleado
```json
db.empleados.find({}, {nombre:1, apellidos:1, pais:1, _id:0})
```

