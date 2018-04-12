
>Para obtener las urls de envío, tiene que ir al panel de configuración de su cuenta en [facturaya.pe](https://facturate.pe). Para efectos de este tutorial usare una cuenta llamada **demo**.


## Enviar una Factura y Boleta eléctronica

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/efactura/ | POST | nro_document, date, type_receipt, method_name, invoice_type, customer, currency, taxes, discount, amount_total, items

## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
nro_document | FXXX-XXXXXXXX ó BXXX-XXXXXXXX | String | Si | Es el número de documento.
date | YYYY-MM-DD | String | Si | La fecha de cuando se emitio la factura.
type_receipt | A4 or Ticket | String | Si | Módelo de documento a imprimir o enviar a correo eléctronico.
method_name | Efectivo, Visa, Cheque, Deposito a cuenta | String | Si | Por que medio se hizo el pago.
invoice_type | 01 ó 03 | String | Si | **Catálogo No. 01 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el tipo de documento enviado. 
currency | PEN, USD | String | Si | **Catálogo No. 02 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el Códigos de tipo de monedas.
discount |  | Double(18,2) | Si | Descuento por la venta.
amount_total |  | Double(18,2) | Si | Monto total de la venta.
customer | [CUSTOMER](CUSTOMER.md) | Array | Si | Cliente de la venta.
taxes | [TAXES](TAXES.md) | Array | Si | Impuestos de la venta.
items | [ITEMS](ITEMS.md) | Array | Si | Productos de la venta.
