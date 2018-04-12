
>La **Comunicación de Baja** se hace con el **voucher_id** guardado en tu base de datos.


## Enviar una Comunicación de Baja

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/unsubscribe/ | POST | voucher_id, reason

## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
voucher_id | FXXX-XXXXXXXX ó BXXX-XXXXXXXX | String | Si | Es el número de documento.
reason | YYYY-MM-DD | String | Si | La fecha de cuando se emitio la factura.
