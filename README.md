# Examen Final MongoDB 1 - Grupo U2

## Crear Base de Datos y coleccion
```bash 
show dbs

use anime_store
db.createCollection("products")
 ```

 ## Agrega producto a la coleccion
 ```bash

    db.products.insertOne(
        {
        "sku": "A101",
        "name": "Figura Naruto Uzumaki",
        "category": "Figuras",
        "price": 120000,
        "stock": 10,
        "anime": "Naruto",
        "rating": 4.8,
        "tags": ["coleccionable", "resina", "edición especial"],
        "provider": {
            "name": "OtakuDistribuciones",
            "country": "Japón"
            }
        }
    )
````

## Agregar a todos los productos las siguientes propiedades
#### - available: true
#### ​- origin: "Importado"  
```bash 

db.products.updateMany(
{},
{$set: {avalible: true, origin: "Importado"}}
)
 ```

## Realizar las siguientes actualizaciones
#### Producto con sku: A034, actualizar stock a 15.
```bash 

db.products.updateOne(
    {sku: "A034"},
    {$set: {stock: 15}}
)
 ```


 #### Producto con sku: A018, cambiar el country del provider a "Colombia".
```bash 

db.products.updateOne(
    {sku: "A018"},
    {$set: {"provider.country": "Colombia"}}
)
 ```

#### Producto con sku: A059, agregar un nuevo tag: "oferta".
* El producto no existe, por ende no hay nada que modificar 
```bash 

db.products.updateOne(
    {sku: "A059"},
    {$push: {tags: "oferta"}}
)
 ```


#### Producto con sku: A012, agregar dos nuevos tags: "nuevo", "popular".
```bash 

db.products.updateOne(
    {sku: "A012"},
    {$push: {tags: "nuevo"}}
)

db.products.updateOne(
    {sku: "A012"},
    {$push: {tags: "popular"}}
)
 ```


#### Producto con sku: A025, agregar los tags "descuento", "outlet".
```bash 

db.products.updateOne(
    {sku: "A025"},
    {$push: {tags: "descuento"}}
)

db.products.updateOne(
    {sku: "A025"},
    {$push: {tags: "outlet"}}
)
 ```


#### Producto llamado "Camiseta Goku Ultra Instinct", cambiar el price a 45000.
```bash 

db.products.updateOne(
    {name: "Camiseta Goku Ultra Instinct"},
    {$set: {price: 45000}}
)

 ```


 ## Renombrar la propiedad origin a import_type.
```bash 

db.products.updateMany(
    {},
    {$rename: {"origin": "import_type"}}
)

 ```


## Cambiar el import_type a "Nacional" para los productos cuyo proveedor esté en Colombia.
```bash 

db.products.updateMany(
    {"provider.country": "Colombia"},
    {$set: {import_type: "Nacional"}}
)

 ```


## Crear las siguientes consultas:
#### Mostrar los productos de la categoría "Mangas"
```bash 

db.products.find(
    {category: "Mangas"}
)

 ```

 #### Mostrar los productos que tienen un precio mayor a 50000
```bash 

db.products.find(
    {price: {$gt: 50000}}
)

 ```

#### Mostrar los productos que no son de la categoría "Figuras"
* Me toca Consultarlo
```bash 

db.products.find(
    {category: {$ne: "Figuras"}}
)

 ```


#### Mostrar el sku, name y tags de los productos que tienen calificación mayor a 4.5.
```bash 

db.products.find(
    {rating: {$gt: 4.5}},
    {_id: 0, sku: 1, name: 1, tags: 1}
)

 ```


#### Mostrar sku, name, y price de los productos con stock menor a 5.
```bash 

db.products.find(
    {stock: {$lt: 5}},
    {_id: 0, sku: 1, name: 1, price: 1}
)

 ```




## Eliminar la propiedad available de todos los documentos.
```bash 

db.products.updateMany(
    {},
    {$unset: {avalible: true}}
)

 ```


 ## Eliminar el tag "descuento" del producto con sku: A025.
```bash 

db.products.updateOne(
    {sku: "A025"},
    {$unset: {tags: "descuento"}}
)

 ```


  ## Eliminar los tags "nuevo" y "popular" del producto con sku: A012.
```bash 

db.products.updateOne(
    {sku: "A012"},
    {$unset: {tags: "nuevo"}}
)

db.products.updateOne(
    {sku: "A012"},
    {$unset: {tags: "nuevo"}}
)
 ```


  ## Eliminar el producto con sku: A043.
```bash 

db.products.deleteOne(
    {sku: "A043"}
)

 ```


## Eliminar todos los productos con stock igual a 0.
```bash 

db.products.deleteMany(
    {$eq: {stock: 0}}
)

 ```