>Para obtener las urls de envío, tiene que ir al panel de configuración de su cuenta en [facturate.pe](https://facturate.pe). Para efectos de este tutorial usare una cuenta llamada **demo**.
>
## Enviar Nota de crédito eléctronica

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/credit_note/ | POST | voucher_id_reference, type_credit_note, nro_document, series, print_type, motive, seller

## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción
------------ | ------------- | ------------- | ------------- | -------------
voucher_id_reference |  | String | Si | El valor "voucher_id" devuelvo como respuesta por facturate.pe al momento de realizar la boleta o la factura.
type_credit_note | 01, 02 | String | Si | Tipo de nota de crédito. **Catálogo No. 09 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el Tipos de nota de crédito.
nro_document | FCxx-00000xxx ó BCxx-00000xxx | String | Si | El número de comprobante de la Nota de crédito de acuerdo a lo estipulado por la sunat.
series | FCxx ó BCxx | String | Si | La serie del número de comprobante de la Nota de crédito.
print_type | A4 | String | Si | Formato de la impresión de la Nota de crédito.
motive | any | String | Si | Motivo de la emisión de la Nota de crédito.
seller | | String | No | Nombre usuario que realiza la Nota de crédito.

### Enviar Nota de crédito
Anulación de la operación
```js
{
  'voucher_id_reference': '2a6dc753-8ca1-41a5-82a3-4f5b12224db0',
  'type_credit_note': '01',
  'nro_document': 'FC01-00000027',
  'series': 'FC01',
  'print_type': 'A4',
  'motive': 'Anulación por cambio de producto',
  'seller': 'NGZ Negosy',
  'invoice_type': '07'
}
```
