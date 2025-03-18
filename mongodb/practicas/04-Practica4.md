# Arrays y documentos anidados

1. Para hacer esta práctica vamos a cargar unos datos ficticios de empresas.
2. Tienes un fichero denominado “personas.json”
3. Debes poner el resultado de las consultas en cada apartado

- Buscar las personas que vivan en Colombia

```Json
db.personas.find({'direccion.pais':'Colombia'})
```

- Personas a las que le guste el color rosa

```Json
db.personas.find({colores:{$regex:/Pink/i}})
```

- Personas cuyo tercer color preferido sea el amarillo (yellow). Recuerda que los arrays comienzan por Cero. Deben salir 3

```json
db.personas.find({
  "colores.2":{$eq:'yellow'}
  },{nombre:1, 'direccion.pais':1, colores:1})
```

- Personas cuyo tercer color preferido sea el amarillo (yellow) y que vivan en Mauritania (debe salir uno)

```json
db.personas.find({
    $and:[
        {"colores.2":{$eq:'yellow'}},
        {"direccion.pais":'Mauritania'}
    ]
  })
```

- Usando el operador $all averiguar las personas que les gusta el plata (silver) y el salmon (salmon)

```json
db.personas.find({
  colores:{$all:['silver', 'salmon']}
},{nombre:1, 'direccion.pais':1, colores:1})
```

- Con el operador $elemMatch, averigua las personas que les guste el rosa (Pink) o el rojo (red)

```json
db.personas.find({
  colores:{$elemMatch:{$eq:'pink', $eq:'red'}}
})
```

```json
db.personas.find({
  colores: {
    $elemMatch: {
      $in: ["pink", "red"]
    }
  }
})
```