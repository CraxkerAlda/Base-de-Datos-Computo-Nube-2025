
# Crud y Consultas en MongoDB

## Crear una Base de datos
Solo se crea si contiene por lo menos una coleccion

**use db1**


## Como crear una coleccion

use db1
db.createCollection("Empleado")


## Mostrar las colecciones
show collections

## Insertar un documento
```Json
db.Alumnos.insertOne(
{
    nombre: 'Soyla',
    apellido1: 'Vaca',
    edad: 32,
    ciudad: 'Cenderos'
}
)
```

## Insercion de un documento más complejo con arrays

```Json
bdejemplo> db.Alumnos.insertOne(
    {
      nombre: 'Kylian',
      apellido: 'Mbappe',
      apellido2: 'Lottin',
      edad: 26,
      aficiones: ['Fútbol', 'Travesaños', 'Real Madrid']
})
```

## Inserción de documentos más complejos con anidado y ID

```Json
bdejemplo> db.Alumnos.insertOne(
    {
      nombre: 'Aldair',
      apellido1: 'Andrade',
      apellido2: 'Rojo',
      edad: 19,
      estudios: ['TSU en Desarrollo de Software', 'Tecnico en Ciencia de Datos'],
      experiencia: {
                     lenguaje: 'Java',
                     sbd: 'SQL Server',
                     aniosExp: 7
                   }
})
```

```Json
bdejemplo> db.Alumnos.insertOne(
    {
      id: 3,
      nombre: 'Sergio',
      apellido: 'Ramos',
      equipo: 'Monterrey',
      aficiones: [ 'Dinero', 'Mujeres', 'Fútbol'],
      talentos: {
           futbol: true,
           ejercicio: true,
        }
    }
)
```

## Insertar Múltiples documentos

```Json
bdejemplo> db.Alumnos.insertMany(
   [
      {
         _id: 12,
         nombre: 'Roberto',
         apellido: 'Gomez',
         edad: 23,
         descripcion: "Es un comendiante buenp"
       },
       {
         nombre: 'Luis',
         apellido: 'Suarez',
         edad: "43",
         habilidades: [
                        'Correr', 'Morder', 'Malo'
                      ],
         direcciones: {
                        calles: 'Del Infierno',
                        numero: 66
                      },
         esposas: [
                     {
                        nombre: 'Marisol',
                        edad: 20,
                        pension: 350,
                        hijos: ['Pepsi', 'Bridget']
                      },
                      {
                        nombre: 'Dorien',
                        edad: 55,
                        pension: 6500.33,
                        complaciente: true
                      }
                   ]
         }
       ]
     )
```


# Practica1


## Cargar Datos
[lirbros.json](./data/libros.json)

## Búsquedas. Condiciones Simples de Igualdad. Método find()

1. Seleccionar todos los documentos de la colección "libros"

```Json
db.libros.find({})
```

2. Mostrar todos los documentos que sean de la editorial "Biblio"

```Json
db.libros.find({editorial:'Biblio'})
```

3. Mostrar todos los documentos que el precio sea 25

```Json
db.libros.find({precio:25})
```

4. Seleccionar todos los documentos donde el titulo sea JSON para todos 

```Json
db.libros.find({titulo:'JSON para todos'})
```

## Operadores de Compración

[Operadores de Comparación](https://www.mongodb.com/docs/manual/reference/operator/query/)

![Operadores de Comparación](image.png)


1. Mostrar todos los documentos donde el precio sea mayor a 25

```Json
db.libros.find({
       precio: {$gt:25}
    }
)
```

2. Mostrar los documentos donde el precio sea 25

```json
db.libros.find({ precio: { $eq: 25 } } )
```

3. Mostrar los documentos cuya cantidad sea menor a 5 

```json
db.libros.find({ cantidad: { $lt: 5} } )
```

4. Mostar los documentos que pertenezcan a la editorial Biblio o Planeta

```json
db.libros.find({ editorial: { $in: ['Biblio', 'Planeta']} } )
```

5. Mostrar todos los documentos de libros que cuesten 20 o 25

```json
db.libros.find({ precio: { $in: [20, 25]} } )
```

6. Mostrar todos los documentos de libros que no cuesten 20 o 25

```json
db.libros.find({ precio: { $nin: [20, 25]} } )
```

7. Mostrar el primer documentos de libros que cueste 20 o 25

```json
db.libros.findOne({ precio: { $in: [20, 25]} } )
```

## Operadores Lógicos

[Operadores de Lógicos](https://www.mongodb.com/docs/manual/reference/operator/query/)

![Operadores de Lógicos](image-1.png)

### Operador AND

Dos posibles opciones de AND

1. La simple, mediante condiciones separadas por comas

**Sintaxis**

```json
db.collection.find({ condicion1, condicion2 } ) -> Con esto asume que es una and
```

2. Usando el operador $and

**Sintaxis**

```json
db.collection.find({$and[{condicion1}, {condicion2}]} ) -> Con esto asume que es una and
```


#### Ejercicios

1. Mostrar todos aquellos documentos que cuesten más de 25 y cuya cantidad sea inferior a 15

**Forma Simple**

```json
db.libros.find({ precio: { $gte: 25}, cantidad: {$lt: 15} } )
```

**Operador AND**

```json
db.libros.find({ $and:[ {precio: { $gte: 25}}, {cantidad: {$lt: 15}}] } )
```

2. Mostrar todos aquellos libros que cuesten más de 25 y cuya 
  cantidad sea inferior a 15 y id igual a 4

**Forma Simple**

```json
db.libros.find({ precio: { $gte: 25}, cantidad: {$lt: 15}, _id:4 } )
```

**Operador AND**

```json
db.libros.find({ $and:[ {precio: { $gt: 25}}, {cantidad: {$lt: 15}}, {_id:{$eq: 4}}] } )
```

### Operadores OR

1. Mostrar todos aquellos libros que cuesten mas de 25 o cuya cantidad sea inferior a 15

```json
db.libros.find( { 
  $or: [ 
    { precio: { $gt: 25 } }, 
    { cantidad: { $lt: 15 } } 
    ] 
  })
```

### AND y OR Combinados

1. Mostrar los libros de la editorial Biblio con precio mayor a 30 o libros de la editorial
  Planeta con precio mayor a 20

```json
db.libros.find( { 
  $or: [ 
    { $and:[{editorial: 'Biblio'}, {precio: {$gt:30}}] }, 
    { $and: [{editorial: {$eq:'Planeta'}}, {precio: {$gt:20}}] } 
    ] 
  })
```

### Forma Simple

```json
db.libros.find( 
      {
      $or: [ 
        {editorial:'Biblio',precio:{ $gt:30}},
        {editorial:{$eq:'Planeta'},precio:{$gt:20}}
      ]
    })
```

## Proyección de Columnas

*** Sintaxis ***

db.collection.find(filtro, columnas)

db.libros.find({},{titulo:1})

1. Seleccionar todos los documentos, mostrando el titulo y la editorial

```json
db.libros.find({}, {titulo:1, editorial:1})

db.libros.find({}, {titulo:1, editorial:1, _id:0})
```

2. Seleccionar todos los documentos de la editorial Planeta, 
  mostrando solamente el titulo y la editorial

```json
db.libros.find({editorial: 'Planeta'}, {titulo:1, editorial:1, _id:0})
```