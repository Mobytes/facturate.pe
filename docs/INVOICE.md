
>Para obtener las urls de envío, tiene que ir al panel de configuración de su cuenta en [facturaya.pe](https://facturate.pe). Para efectos de este tutorial usare una cuenta llamada **demo**.


## Enviar una factura eléctronica

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/efactura/ | POST | nro_document, date, type_receipt, method_name, invoice_type, customer, currency, taxes, discount, amount_total, items

## Parametros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
nro_document | FXXX-XXXXXXXX| String | Si | Es el número de documento de la factura. Ejemplo F001-00002321
date | MM-DD-YYY | String | Si | La fecha de cuando se emitio la factura. ``Ejemplo 23-03-2018``.
type_receipt | A4 or Ticket| String | Si | Módelo de documento a imprimir o enviar a correo eléctronico.
method_name | Efectivo, Visa, Cheque, Deposito a cuenta | String | Si | Por que medio de pago se cancelo la factura.
invoice_type | 01 | String | Si | Tipo de comprobante, ```01 es de una Factura y 03 es una Boleta```.
currency | PEN, USD | String | Si | El tipo de moneda que se hizo el pago, ```PEN => Soles, USD => Dolares```.
discount | XX.XX | Double(18,2) | Si | Descuento por la venta
amount_total | XXX.XX | Double(18,2) | Si | Monto total de la venta
customer | [CUSTOMER](CUSTOMER.md) | Array | Si | Cliente de la venta
taxes | [TAXES](TAXES.md) | Array | Si | Impuestos de la venta
items | [ITEMS](ITEMS.md) | Array | Si | Productos de la venta

### PHP
```php
curl_setopt_array($ch = curl_init(), array(
  CURLOPT_URL => "https://pushiner/api/v1/send_message/",
  CURLOPT_POSTFIELDS => array(
    "token_user" => "my_token_user",
    "token_app" => "my_token_app",
    "title" => "mi título",
    "message" => "hola mundo",
  ),
  CURLOPT_SAFE_UPLOAD => true,
));
curl_exec($ch);
curl_close($ch);
```

### Laravel
Sendpush has its library for laravel 5. * [SendPush][1]

### Python
```py
#!/usr/bin/python 
import json, httplib 
connection = httplib.HTTPSConnection('https://pushiner', 443) 
connection.connect() 
connection.request('POST', '/api/v1/send_message/', json.dumps({ "token_user": "my_token_user", "token_app": "my_token_app", "title": "mi título", "message": "mi contenido"}), { "Content-Type": "application/json" } ) result = json.loads(connection.getresponse().read())
print result
```

### Ruby

```ruby
require "net/https"

url = URI.parse("https://pushiner.com/api/v1/send_message/")
req = Net::HTTP::Post.new(url.path)
req.set_form_data({
  :token_user => "my token_user",
  :token_app => "my token_app",
  :title => "mi título",
  :message => "mi contenido",
})
res = Net::HTTP.new(url.host, url.port)
res.use_ssl = true
res.verify_mode = OpenSSL::SSL::VERIFY_PEER
res.start {|http| http.request(req) }
```

### Consola
```sh
curl -s \
  --form-string "token_user=abc123" \
  --form-string "token_app=user123" \
  --form-string "title=mi título" \
  --form-string "message=mi contennido" \
  https://pushiner.com/api/v1/send_message/
```

## Manejo de respuesta

### Envío éxitoso
```js
{
  "message": "la notificacion fue enviada con éxito",
  "code": 200,
  "success": true
}
```

### Envío errado
```js
{
  "message": "mensaje de error",
  "code": 400,
  "success": false
}
```

[1]: https://github.com/evervasquez/laravel-sendpush