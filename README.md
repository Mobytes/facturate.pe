# facturate.pe
La API REST le permite interactuar con **facturate.pe** para que pueda enviar sus documentos eléctronicos por una petición HTTP.

Los documentos elétronicos que puede enviar son:

* [Factura y Boleta eléctronica](docs/INVOICE.md)
* [Comunicación de baja](docs/UNSUBSCRIBE.md)
* Nota de Crédito (muy pronto)
* Nota de Debito (muy pronto)
* [Enviar email](docs/SEND_EMAIL.md)


### Configuración
Para poder empezar a enviar sus documentos eléctronicos tiene que crearse una cuenta en [facturaya.pe](https://facturate.pe), validar tu cuenta y obtener el **Token**

### Seguridad
Para efectos de seguridad se ha implementado el método **Token**, para poder hacer cualquier petición HTTP al servidor de [facturaya.pe](https://facturate.pe). Tienes que adjuntar el token al header de esta manera. 

```py
Authorization: <type> <credentials>
```

### Envío al Servidor por Lenguaje de programación
> Llamaremos **data** a los datos que enviaremos.

### PHP

```php
$data_boleta = array(
  'data' => []
);
$data_string = json_encode($data_boleta);
$ch = curl_init('https://[store].facturate.pe/api/v1/invoice/efactura/');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $data_string);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'Authorization: Token [token]',
    'Content-Length: ' . strlen($data_string))
);
$result = curl_exec($ch);
curl_close($ch);
$data = json_decode($result);
```

### Python
```py
#!/usr/bin/python
import requests
query = requests.Session()
query.headers.update({'Authorization': 'Token %s' % company.token_facturate})
query.headers.update({'content-type': 'application/json'})
response = query.post('https://demo.facturate.pe/api/v1/invoice/efactura/' ,
                              data=simplejson.dumps(data))
```
