# Búsquedas en Arrays y Documentos Anidados

## Buscar dentro de un documento anidado

```json
db.ciudades.find({ 
    alcalde: { 
        nombre: "Crystal", 
        apellidos: "Long", 
        edad: 76 
        } 
})
```

```json
db.ciudades.find({ "alcalde.nombre": "Crystal" })
```

1. Seleccionar las ciudades donde los alcaldes 
tengan más de 70 años

```json
db.ciudades.find({ 
    "alcalde.edad": {$gt:70} 
})
```

2. Realizar las consulta anterior pero utilizando una proyeccion

```json
db.ciudades.find({ 
    "alcalde.edad": {$gt:70} 
    },
    {_id:0, nombre:1, "alcalde.edad":1}
)
```

3. Seleccionar las ciudades donde el alcalde tenga 76 años
    o 41 años

```json
db.ciudades.find({
  $or:[{"alcalde.edad":76}, {"alcalde.edad":41}]
})
```

```json
db.ciudades.find({
  $or:[{"alcalde.edad":76}, {"alcalde.edad":41}]
},
{_id:0, nombre:1, "alcalde.edad":1}
)
```

## Consultas con Arrays 

1. Crear una colección cazas
2. Cargar los documentos de la colección cazas, de la data cazas


## Ejemplos con consulta con Arrays

1. Buscar los documentos que tengan USA como paises 

```json
db.Cazas.find({paises:"usa"})
```

2. Buscar los elementos donde cualquier elemento del array dimensiones
sea mayor a 5

```json
db.Cazas.find({
  dimensiones:{$gt:5}
  })
```

3. Buscar los documentos donde las dimensiones del avión por ancho
que es la posición a 1, sea superior a 14

```json
db.Cazas.find({
  "dimensiones.1":{$gt:14}
  })
```

```json
db.Cazas.find({
  "dimensiones.1":{$eq:14}
},{_id:0, modelo:1, dimensiones:1})
```


### Arrays, Operador $all

1. Buscar los aviones que estan sirviendo en egipto y en israel 

```json
db.Cazas.find({
  paises:{$all:['egipto', 'israel']}
})
```

```json
db.Cazas.find({
  paises:{$all:['egipto', 'israel']}
}, {_id:0, modelo:1, paises:1})
```

```json
db.Cazas.find({ $and:[
  {paises:'egipto'},
  {paises:'israel'}
]
})
```

2. Seleccionar los cazas que sirven en inglaterra y en españa

```json
db.Cazas.find({ $and:[
  {paises:'inglaterra'},
  {paises:'españa'}
]
})
```

### Arrays Operador $elementMatch -> Permite busqueda dentro de arrays, este busca la lista de condiciones que estan dentro del Operador

1. Buscar que aviones tienen uso dentro de inglaterra

```json
db.Cazas.find({
  paises:{$elemMatch:{$eq:'inglaterra'}}
})
```

2. Buscar los aviones donde las dimensiones sean menores a 20 o mayores a 15

```json
db.Cazas.find({ 
  dimensiones:{$elemMatch:{$lt:20, $gt:15}}
})
```

### Buscar Arrays Documentos Anidados

1. utilizar la coleccion ciudades

2. Buscar los consejeros de nombre Jeri Flower de edad 78

```json
db.ciudades.find({
  consejeros:{identificador:1, nombre:'Jeri Flowers', edad:78}
})
```

3. Buscar en consejeros donde tengan una edad mayor a 70

```json
db.ciudades.find({
  "consejeros.edad":{$gt:70}
})
```

4. Buscar en consejeros en la posición 2 que esten entre 70 y 80 años

```json
db.ciudades.find({
  "consejeros.2.edad":{$gt:70, $lt:80}  
}, {_id:0, "consejeros.nombre":1, "consejeros.edad":1})
```

5. Buscar los consejeros de la posición 0 que sean mayores a 70 años

```json
db.ciudades.find({
  "consejeros.0.edad":{$gt:70}  
}, {_id:0, "alcalde.edad":1, "alcalde.nombre":1, nombre:1})
```

6. Buscar consejeros que sean mayores a 70

```json
db.ciudades.find({
  "consejeros.edad":{$gt:70}
})
```