
>La **Comunicación de Baja** se hace con el **voucher_id** guardado en tu base de datos.


## Enviar una Comunicación de Baja

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/unsubscribe/ | POST | voucher_id, reason

## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
voucher_id |  | String | Si | Es el identificador en la plataforma. 
reason | any | String | Si | Es la razón por que se esta dando de baja al documento.
