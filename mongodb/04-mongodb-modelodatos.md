# Modelo de datos en Mongo DB

 - Modelos      
    - Embebidos 
    - Referenciados

- Modelos Embebidos

*Uno a Uno*
```json
db.departamentos.insertMany(
    [
        {
        _id:1,
        nombre :"Tecnologias de la Informacion",
        responsable:{
            nombre:'Monico',
            apellidos:'Martinez Perez'
        },
        descripcion: 'ejemplo de departamento'
       
       },
       {
        _id:1,
        nombre :"Contabilidad",
        responsable:{
            nombre:'Raul',
            apellidos:'Lopez Hernandez'
        },
        descripcion: 'ejemplo de departamento'
       
       }
    ]
    
)
```


- Modelos  Referenciados 

*Uno a Uno*
```json

db.localidades.insertMany(

[
    {
        _id:'BA',
        ciudad:'Buenos Aires',
        pais:'Argentina',
        poblacion: 16 'Millones',
        turismo:["edificios","tango","gastronomia","musueos","parques"],
        direccion:"Avenida Tortolos",
        cod_departamento:1



    },
    {
        
        _id:'SA',
        ciudad:'Santiago',
        pais:'chile',
        poblacion: 20 'Millones',
        turismo:["iglesias","vinos","gastronomia","musueos"],
        direccion:"Calle soy la vaca del corral",
        cod_departamento:2


    }

]

)


```

```json
db.departamentos.aggregate(
[
    {
        $lookup:
        {
            from:"Localidades",
            localField:"_id",
            foreingField:"cod_departamento"
            as "localidades"


          }
       }
   ]
)
```