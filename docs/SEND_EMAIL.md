## Enviar email un documento electrónico

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/send_email/ | POST | voucher_id, reason


## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
voucher_id |  | String | Si | Es el identificador en la plataforma. 
email | any | String | Si | Es el email a donde se enviara el documento.


### Enviar email
```js
{
  'voucher_id': '0822ed63-68cd-47a7-b804-b8d2aefa0ab9', 
  'reason': 'Se devolvío el dinero', 
}
```

## Lenguajes

#### PHP
```php
$data_boleta = array(
    'invoice_id' => $objsunat->codigo_unico,
    'email' => $_REQUEST['mail_enviar']
);
$data_string = json_encode($data_boleta);
$ch = curl_init('https://artesano.facturate.pe/api/v1/invoice/send_email/');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $data_string);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
        'Content-Type: application/json',
        'Authorization: Token 7bd7bc9ff628669d56fd38526925455',
        'Content-Length: ' . strlen($data_string))
);
$result = curl_exec($ch);
curl_close($ch);
$data = json_decode($result);
```
