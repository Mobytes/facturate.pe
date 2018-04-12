#### Items
Los items de la factura es un array de estos parametros

Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
quantity |  | int | Si | Es la cantidad de productos vendidos
price |  | Double(18,2) | Si | Es el precio sin impuesto
price_tax |  | Double(18,2) | Si | Es el precio con impuesto
tax_total_item |  | Double(18,2) | No | Impuesto total
tax_unit_item |  | Double(18,2) | No | Impuesto por item
type_igv |  | String | No | **Catálogo No. 07 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el tipo de afectación del IGV.
description | any | String | No | Nombre del producto
system_id | any| String | Si | id del producto en tu sistema
correlative | any| int | Si | Correlativo en la venta
type | any| String | Si | Bienes:2001, Servicios:2002, Contratos:2003


* Ejemplo:
```js
'items': [
            {
              'quantity': 2.00, 
              'price': 4.00, 
              'price_tax': 4.00, 
              'tax_total_item': 0.00, 
              'tax_unit_item': 0.00, 
              'type_igv': '20', 
              'description': 'GASEOSA INCAK', 
              'system_id': '7750002000164', 
              'correlative': 1, 
              'type': '2001'
            }, 
            {
              'quantity': 1.00, 
              'price': 8000.00, 
              'price_tax': 8000.00, 
              'tax_total_item': 0.00, 
              'tax_unit_item': 0.00, 
              'type_igv': '20', 
              'description': 'CONSULTORIA DE EXPEDIENTE TECNICO', 
              'system_id': '7750002000122', 
              'correlative': 2, 
              'type': '2002'
            }
         ]
```
