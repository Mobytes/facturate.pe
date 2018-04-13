# FacturaYa
La API REST le permite interactuar con **FacturaYa.pe** para que pueda enviar sus documentos eléctronicos por una petición HTTP.

Los documentos elétronicos que puede enviar son:

* [Factura y Boleta eléctronica](docs/INVOICE.md)
* [Comunicación de baja](docs/UNSUBSCRIBE.md)
* Nota de Crédito (muy pronto)
* Nota de Debito (muy pronto)


### Configuración
Para poder empezar a enviar sus documentos eléctronicos tiene que crearse una cuenta en [facturaya.pe](https://facturate.pe), validar tu cuenta y obtener el **Token**

### Seguridad
Para efectos de seguridad se ha implementado el método **Token**, para poder hacer cualquier petición HTTP al servidor de [facturaya.pe](https://facturate.pe) tienes que adjuntar el token al header de esta manera. 

```py
Authorization: <type> <credentials>
```

### Envío al Servidor por Lenguaje de programación
> Llamaremos **data** a los datos que enviaremos.

### PHP

```php
curl_setopt_array($ch = curl_init(), array(
  CURLOPT_HTTPHEADER  => array('Authorization: Token ewhifewubidncsidnc343j4nk32jn4jkjndsfnfkdsf'),
  CURLOPT_URL => "https://demo.facturate.pe/api/v1/invoice/efactura/",
  CURLOPT_POSTFIELDS => data,
  CURLOPT_SAFE_UPLOAD => true,
));
curl_exec($ch);
curl_close($ch);
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
