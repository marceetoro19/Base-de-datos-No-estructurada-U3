[Base de datos proyecto.txt](https://github.com/user-attachments/files/28931938/Base.de.datos.proyecto.txt)

bd =  inventario

colección = Registro_Productos
 
[
  {
    _id: ObjectId('6a05179e096104d31211402b'),
    Id_Producto: 102,
    Nombre: 'Leche Entera',
    Descripcion: 'Caja 1L',
    Fecha_Vencimiento: ISODate('2023-06-14T00:00:00.000Z'),
    Precio: 950,
    Stock: 30
  },
  {
    _id: ObjectId('6a05179e096104d31211402c'),
    Id_Producto: 103,
    Nombre: 'Aceite de Maravilla',
    Descripcion: 'Botella 900ml',
    Fecha_Vencimiento: ISODate('2025-08-10T00:00:00.000Z'),
    Precio: 2500,
    Stock: 20
  },
  {
    _id: ObjectId('6a05179e096104d31211402d'),
    Id_Producto: 104,
    Nombre: 'Tallarines Lucchetti',
    Descripcion: 'Paquete 400g',
    Fecha_Vencimiento: ISODate('2026-01-05T00:00:00.000Z'),
    Precio: 850,
    Stock: 100
  },
  {
    _id: ObjectId('6a05179e096104d31211402e'),
    Id_Producto: 105,
    Nombre: 'Azúcar Granulada',
    Descripcion: 'Bolsa 1kg',
    Fecha_Vencimiento: ISODate('2026-03-12T00:00:00.000Z'),
    Precio: 1100,
    Stock: 45
  },
  {
    _id: ObjectId('6a05179e096104d31211402f'),
    Id_Producto: 106,
    Nombre: 'Café Instantáneo',
    Descripcion: 'Frasco 170g',
    Fecha_Vencimiento: ISODate('2025-11-30T00:00:00.000Z'),
    Precio: 4200,
    Stock: 15
  },
  {
    _id: ObjectId('6a05179e096104d312114030'),
    Id_Producto: 107,
    Nombre: 'Atún en Lomitos',
    Descripcion: 'Lata 160g',
    Fecha_Vencimiento: ISODate('2027-05-20T00:00:00.000Z'),
    Precio: 1300,
    Stock: 60
  },
  {
    _id: ObjectId('6a05179e096104d312114031'),
    Id_Producto: 108,
    Nombre: 'Sal de Mesa',
    Descripcion: 'Paquete 1kg',
    Fecha_Vencimiento: ISODate('2028-10-15T00:00:00.000Z'),
    Precio: 600,
    Stock: 80
  },
  {
    _id: ObjectId('6a05179e096104d312114032'),
    Id_Producto: 109,
    Nombre: 'Harina con Polvos',
    Descripcion: 'Bolsa 1kg',
    Fecha_Vencimiento: ISODate('2024-12-01T00:00:00.000Z'),
    Precio: 1050,
    Stock: 25
  },
  {
    _id: ObjectId('6a05179e096104d312114033'),
    Id_Producto: 110,
    Nombre: 'Salsa de Tomate',
    Descripcion: 'Doypack 200g',
    Fecha_Vencimiento: ISODate('2025-04-22T00:00:00.000Z'),
    Precio: 450,
    Stock: 120
  },
  {
    _id: ObjectId('6a05179e096104d312114034'),
    Id_Producto: 111,
    Nombre: 'Mermelada de Frambuesa',
    Descripcion: 'Frasco 250g',
    Fecha_Vencimiento: ISODate('2025-07-18T00:00:00.000Z'),
    Precio: 1800,
    Stock: 10
  },
  {
    _id: ObjectId('6a05179e096104d312114035'),
    Id_Producto: 112,
    Nombre: 'Legumbres Lentejas',
    Descripcion: 'Bolsa 1kg',
    Fecha_Vencimiento: ISODate('2025-09-05T00:00:00.000Z'),
    Precio: 2200,
    Stock: 35
  },
  {
    _id: ObjectId('6a05179e096104d312114036'),
    Id_Producto: 113,
    Nombre: 'Galletas de Soda',
    Descripcion: 'Paquete familiar',
    Fecha_Vencimiento: ISODate('2024-11-10T00:00:00.000Z'),
    Precio: 1150,
    Stock: 55
  },
  {
    _id: ObjectId('6a05179e096104d312114037'),
    Id_Producto: 114,
    Nombre: 'Té en Bolsitas',
    Descripcion: 'Caja 100 unidades',
    Fecha_Vencimiento: ISODate('2026-05-23T00:00:00.000Z'),
    Precio: 3200,
    Stock: 45
  }
]





db.Registro_Productos.insertOne({
  "Id_Producto": NumberInt(125),
  "Nombre": "Producto de Prueba",
  "Descripcion": "Descripción detallada desde CMD",
  "Fecha_Vencimiento": new ISODate("2026-12-31T00:00:00Z"),
  "Precio": NumberInt(1800),
  "Stock": NumberInt(50)
})



reglas de validación cmd 

db.runCommand({
   collMod: "Registro_Productos",
   validator: {
      $jsonSchema: {
         bsonType: "object",
         required: [ "Id_Producto", "Nombre", "Precio", "Stock", "Fecha_Vencimiento" ],
         properties: {
            Id_Producto: {
               bsonType: "int",
               minimum: 1,
               description: "Id_Producto debe ser un número entero positivo (Mayor a 0) y es obligatorio"
            },
            Nombre: {
               bsonType: "string",
               minLength: 1,
               description: "Nombre debe ser un texto válido y es obligatorio"
            },
            Descripcion: {
               bsonType: "string",
               description: "Descripcion debe ser un texto"
            },
            Precio: {
               bsonType: "int",
               minimum: 1,
               description: "El precio debe ser un número entero positivo (Mayor a 0) y es obligatorio"
            },
            Stock: {
               bsonType: "int",
               minimum: 0,
               description: "El stock debe ser un número entero no negativo (Cero o mayor) y es obligatorio"
            },
            Fecha_Vencimiento: {
               bsonType: "date",
               description: "La fecha de vencimiento debe ser un tipo Date de MongoDB (ISODate) y es obligatoria"
            }
         }
      }
   },
   validationLevel: "strict",
   validationAction: "error"
})


eliminar validador cmd 

db.runCommand({
   collMod: "Registro_Productos",
   validator: {},
   validationLevel: "off",
   validationAction: "warn"
})

db.Registro_Productos.insertOne({
   Id_Producto: 130,
   Nombre: "Fideos Quilicura",
   Descripcion: "Paquete de 400g",
   Precio: 990,
   Stock: 120,
   Fecha_Vencimiento: new ISODate("2026-08-25")
})
