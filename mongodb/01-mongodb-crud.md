
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


## Practica

1. Base de Datos, colecciones e inserts

    * Nos conectamos con mongosh

    * Crear una base de datos denominada curso

    ```json
    use curso
    ```

    * Verificar que no exista la base de datos
    
    ```json
    use curso
    ```

    * Crear una conexión denominada "facturas" con el comando createCollection
    y comprobrar que aparece tanto la colección como la base de datos

    