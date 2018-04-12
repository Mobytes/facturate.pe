#### Items
Los items de la factura es un array de estos parametros

Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
quantity |  | int | Si | Es la cantidad de productos vendidos
price |  | Double(18,2) | Si | Es el precio sin impuesto
price_tax |  | Double(18,2) | Si | Es el precio con impuesto
tax_total_item |  | Double(18,2) | No | Impuesto total
tax_unit_item |  | Double(18,2) | No | Impuesto por item
type_igv | any | String | No | **Catálogo No. 07 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el tipo de afectación del IGV.
description | any | String | No | Nombre del producto
system_id | any| String | Si | id del producto en tu sistema
correlative | any| String | Si | Correlativo en la venta
type | any| String | Si | Bienes:2001, Servicios:2002, Contratos:2003
