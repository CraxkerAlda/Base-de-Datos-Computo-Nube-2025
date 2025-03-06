# Practica 3. Updates y Deletes

1. Cambiar el salario del empleado Imogene Nolan. Se le 
    asigna 8000
```json
db.empleados.updateOne({nombre: 'Imogene'}, {$set:{salario:'8000'}})
```

```json
db.empleados.find({nombre: 'Imogene'})
```

2. Cambiar "Belgium" por "Bélgica" en los empleados 
(debe de haber dos)

```json
db.empleados.updateMany(
  {pais:{$eq:'Belgium'}},
  {$set:{pais:'Bélgica'}}
)

```
```json
db.empleados.find({pais: 'Belgium'})
```

3. Incrementar el salario de todos los empelados de 
Google en 1000

```json
db.empleados.updateMany(
  {empresa:'Google'},
  {$inc:{salario:1000}
})
```

```json
db.empleados.find({empresa: 'Google'})
```

4. Reemplazar el empleado Omar Gentry por el siguiente documento:

```json
{
"nombre": "Omar",
"apellidos": "Gentry",
"correo": "sin correo",
"direccion": "Sin calle",
"region": "Sin region",
"pais": "Sin pais",
"empresa": "Sin empresa",
"ventas": 0,
"salario": 0,
"departamentos": "Este empleado ha sido anulado"
}
```
```Json
db.empleados.replaceOne({nombre:'Omar'}, 
    {

    "nombre": "Omar",
    "apellidos": "Gentry",
    "correo": "sin correo",
    "direccion": "Sin calle",
    "region": "Sin region",
    "pais": "Sin pais",
    "empresa": "Sin empresa",
    "ventas": 0,
    "salario": 0,
    "departamentos": "Este empleado ha sido anulado"
})
```

5. Con un find comprobar que el empleado ha sido modificado

```json
db.empleados.find({nombre: 'Omar', apellido:'Gentry'})
```

6. Borrar todos los empleados que ganen mas de 8500.
Nota: deben ser borrados 3 documentos

```json
db.empleados.deleteMany(
  {salario:{$gt:8500}}
)
```

7. Vizualizar con una expresión regular todos los empleados 
con apellidos que comiencen con "R"

```json
db.empleados.find({apellidos:/^R/})
```

8. Buscar todas las regiones que contenga una "V"
Hacerlo con el operador $regex y que distinga mayusculas
y minusculas. Deben salir 2

```json
db.empleados.find({region:{$regex: /v/i}}) 
```

9. Vizualizar los apellidos de los empleados ordenados
por el propio apellido

```json
db.empleados.find({}, {apellidos:1, _id:0}).sort({apellidos:1})
```

10. Indicar el numero de empleados que trabajan en google

```json
db.empleados.find({empresa:'Google'}).size()
```

11. Borrar la coleccion empleados y la base de datos

```json
db.empleados.drop()
```
```json
db.curso()
```