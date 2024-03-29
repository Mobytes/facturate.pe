#### Items
Los items de la factura es un array con los siguientes parámetros.

Nombre de parámetro | Formato | Tipo | Obligatorio | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
quantity |  | Double(18,4) | Si | Es la cantidad de productos vendidos.
price |  | Double(18,4) | Si | Es el precio sin ningun tipo de impuesto.
price_tax |  | Double(18,4) | Si | Es el precio con todos los impuestos.
unit |  | String | Si | Es código de las unidades de medida.[Ver lista completa](https://docs.google.com/spreadsheets/d/1g4BislVBPrFvyMb0unRyYEHGCtl9UlLCepigaoNak5A/edit#gid=367466330)
tax_total_item |  | Double(18,2) | Si | Total del impuesto del item x cantidad. De no haber, cero.
tax_unit_item |  | Double(18,4) | Si | Impuesto individual del item. De no haber, cero.
type_igv | | String | No | OBSOLETO. **Catálogo No. 07 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf).
description | any | String | Si | Nombre del producto.
detail | any | String | No | Detalle extra en el nombre del producto que se quiera detallar.
system_id | any| String | Si | Id del producto en su sistema, como código de barras del producto.
correlative | any| int | Si | Correlativo en la venta. Es el orden de la lista de productos a enviar. Debe empezar con 1 y así sucesivamente.
discount |  | Double(18,4) | No | Descuento del item.
type | 2001, 2002, 2003 | String | Si | Bienes:**2001**, Servicios:**2002**, Contratos:**2003**.
igv_percentage | | Double(18,2) | No | Si el item esta sujeto al igv, se debe de enviar el porcentaje de su cálculo. Ej: 18.00
sunat_tax_code | 1000, 2000, 7152, 9995, 9996, 9997, 9998 | String | Si | **Catálogo No. 05 en el** [Catálogo de códigos de Sunat](anexo-244-2019.pdf) para el tipo de tributos.
isc_unit_item | | Double(18,2) | No | Impuesto ISC individual del item.
isc_code | 02 | String | No | El tipo de impuesto ISC del item. Por ahora solo existe el control "Sujetos a un monto fijo por una unidad de medida"
isc_percentage | | Double(18,2) | No | El valor del isc respecto al precio del item expresado en porcentaje.
icbper | | Double(18,2) | No | El valor del icbper del item. Debe estar de acuerdo al valor asignado por sunat por año.
referencial_unit_value | |Double(18,2) | No | Valor referencial del precio de la bolsa cuando su valor es cero.

* Ejemplo:

> Este es un ejemplo de 2 productos.

```js
'items': [
            {
	  'quantity': 1.0000,
	  'price': 16.9492,
	  'price_tax': 20.0000,
	  'tax_total_item': 3.05,
	  'tax_unit_item': 3.0508,
	  'description': 'SERVICIO VETERINARIO (CONSULTA)',
	  'system_id': '7750020001725',
	  'correlative': 1,
	  'discount': 0.0000,
	  'type': '2002',
	  'igv_percentage': 18.0000,
	  'unit': 'ZZ',
	  'unit_pdf': 'UND',
	  'sunat_tax_code': '10',
	  'isc_unit_item': 0.0000,
	  'isc_total_item': 0.00,
	  'isc_code': none,
	  'isc_percentage': 0,
	  'icbper': 0.00,
	  'referencial_unit_value': 0.00
            }, 
            {
              'quantity': 2.0000,
	  'price': 5.0000,
	  'price_tax': 5.0000,
	  'tax_total_item': 0.00,
	  'tax_unit_item': 0.0000,
	  'description': 'vaso descartable 6 OZ',
	  'system_id': '7750020006218',
	  'correlative': 2,
	  'discount': 0.0000,
	  'type': '2001',
	  'igv_percentage': 0.0000,
	  'unit': 'NIU',
	  'unit_pdf': 'UND',
	  'sunat_tax_code': '20',
	  'isc_unit_item': 0.0000,
	  'isc_total_item': 0.00,
	  'isc_code': none,
	  'isc_percentage': 0,
	  'icbper': 0.00,
	  'referencial_unit_value': 0.00
            }
         ]
```
