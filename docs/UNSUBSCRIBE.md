
>La **Comunicación de Baja** se hace con el identificador **voucher_id** que se ha guardado en tu base de datos.


## Enviar una Comunicación de Baja

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/unsubscribe/ | POST | voucher_id, reason


## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
voucher_id |  | String | Si | Es el identificador en la plataforma. 
reason | any | String | Si | Es la razón por que se esta dando de baja el documento.


### Enviar Comunicación de Baja
```js
{
  'voucher_id': '0822ed63-68cd-47a7-b804-b8d2aefa0ab9', 
  'reason': 'Se devolvío el dinero', 
}
```

## Manejo de respuesta

### Envío éxitoso

```js
{
  'unsubscribe': 'Ok',
  'voucher': data
}
```

### Envío errado

```js
{
  'error': message
}
```

## Lenguajes

#### PHP
```php
$data_baja = array(
    'voucher_id' => $obj->codigo_unico,
    'reason' => $_REQUEST['razon_anular'],
);
$data_string = json_encode($data_baja);
$ch = curl_init('https://[store].facturate.pe/api/v1/invoice/unsubscribe/');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $data_string);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
        'Content-Type: application/json',
        'Authorization: Token 7bd7bc9token925455',
        'Content-Length: ' . strlen($data_string))
);
$result = curl_exec($ch);
curl_close($ch);
$data = json_decode($result);
```
