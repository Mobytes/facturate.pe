#### Items
Los items de la factura es un array de estos parametros

Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
quantity | XX | int | Si | Es la cantidad de productos vendidos
price | XX.XX | Double(18,2) | Si | Es el precio sin impuesto
price_tax | XX.XX | Double(18,2) | Si | Es el precio con impuesto
tax_total_item | XX.XX | Double(18,2) | No | Impuesto total
tax_unit_item | XX.XX | Double(18,2) | No | Impuesto por item
type_igv | any | String | No | **Catálogo No. 05 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el tipo de tributos.
description | any | String | No | Nombre del producto
system_id | any| String | Si | id del producto en tu sistema
correlative | any| String | Si | Correlativo en la venta
type | any| String | Si | Bienes:2001, Servicios:2002, Contratos:2003
