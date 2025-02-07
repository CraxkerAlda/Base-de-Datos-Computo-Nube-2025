# Parctica 1: Base de Datos, colecciones e inserts

1. Conectarnos con mongosh a MongoDB
1. Crear una base de datos llamada curso
1. Comprobar que la base de datos no existe
1. Crear una coleccion que se llame facturas y mostrarla

```Json
db.createCollection('facturas')
show collections
```

5. Insertar un documento con los siguientes datos: 

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Factura | 10 |
| Ciente | Frutas Ramirez |
| Total | 223 |


```Json
db.facturas.insertOne(
   {
    cod_facturas: 10,
    cliente: 'Frutas Ramirez',
    total: 145
   }
  )

  db.facturas.insertOne(
   {
    cod_facturas: 20,
    cliente: 'Ferreteria Juan',
    total: 140
   }
  )
```

6. Crear una nueva colección pero usando directamente el insertOne.
    insertar un documento en la colección productos con los siguientes 
    datos:


| Codigo   | Valor   |
|-------------|-------------|
| Cod_producto | 1 |
| Nombre | Tornillo x 1 |
| Precio | 2 |


```Json
db.productos.insertOne(
   {
    cod_producto: 1,
    nombre: 'Tornillo x 1',
    precio: 2, 
    unidades:1500
   }
  )
```


7. Crear un documento que tenga un arrat con los siguientes datos:

| Codigo   | Valor   |
|-------------|-------------|
| Cod_producto | 1 |
| Nombre | Martillo |
| Precio | 20 |
| Unidades | 50 |
| Fabricantes | 'fab1', 'fab2','fab3','fab4' |


```Json
db.productos.insertOne(
   {
    cod_producto: 2,
    nombre: 'Martillo',
    precio: 20, 
    unidades:50,
    aficiones: ['fab1' , 'fab2' , 'fab3' , 'fab4]
   }
  )
```

8. Borrar la colección Facturas y comprobar que se borro

```Json
db.facturas.drop()
show collections
```

9. Insertar un documento en una colección denominada **fabricantes**
    para probar los subdocumentoa y la clave _id personalizada 

| Codigo   | Valor   |
|-------------|-------------|
| _id | 1 |
| Nombre | fab1 |
| Localidad | Ciudad: Buenos Aires, pais: argentina, calle: pez 27, cod_postal:2900 |


```Json
db.fabricantes.insertOne(
   {
    _id: 1,
    nombre: 'fab1',
    localidad: {
                     ciudad: 'buenos aires',
                     pais: 'argentina',
                     calle: 'calle pez 27',
                     cod_postal:22900
                   }
   }
  )
```

10. Realizar una inserción de varios documentos en la colección productos

| Codigo   | Valor   |
|-------------|-------------|
| Cod_producto | 3 |
| Nombre | Alicates |
| Precio | 10 |
| Unidades | 25 |
| Fabricantes | 'fab1', 'fab2','fab5' |

| Codigo   | Valor   |
|-------------|-------------|
| Cod_producto | 4 |
| Nombre | Arandelas |
| Precio | 1 |
| Unidades | 500 |
| Fabricantes | 'fab1', 'fab2','fab5' |



```Json
db.productos.insertMany(
   [
      {
         _id: 3,
         nombre: 'Alicates',
         precio: 10,
         unidades: 25,
         fabricantes: ['fab1', 'fab2','fab5']
       },
       {
         _id: 4,
         nombre: 'Arandelas',
         precio: 1,
         unidades: 500,
         fabricantes: ['fab1', 'fab4','fab10']

       }
       ]
     )
```
