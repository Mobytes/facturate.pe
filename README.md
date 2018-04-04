# FacturaYa
La API REST le permite interactuar con **FacturaYa.pe** para que pueda enviar sus documentos eléctronicos por una petición HTTP.

Los documentos elétronicos que puede enviar son:

* Factura y boleta eléctronica
* Baja de una factura o boleta elécronica
* Nota de Crédito (muy pronto)
* Nota de Debito (muy pronto)

### Configuración
Para poder empezar a enviar sus documentos eléctronicos tiene que crearse una cuenta en [facturaya.pe](https://facturate.pe), validar tu cuenta y obtener el **Token**

### Seguridad
Para efectos de seguridad se ha implementado el método **Token**, para poder hacer cualquier petición HTTP al servidor de [facturaya.pe](https://facturate.pe) tienes que adjuntar el token al header de esta manera. 

```py
Authorization: <type> <credentials>
```

>Para obtener las urls de envío, tiene que ir al panel de configuración de su cuenta en [facturaya.pe](https://facturate.pe). Para efectos de este tutorial usare una cuenta llamada **demo**.


## Enviar una factura eléctronica

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/efactura/ | POST | nro_document, date, type_receipt, method_name, invoice_type, customer, currency, taxes, discount, amount_total, items

## Parametros

Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
nro_document | FXXX-XXXXXXXX| String | Si | Es el número de documento de la factura. Ejemplo F001-00002321
date | MM-DD-YYY | String | Si | La fecha de cuando se emitio la factura. ``Ejemplo 23-03-2018``.
type_receipt | A4 or Ticket| String | Si | Módelo de documento a imprimir o enviar a correo eléctronico.
method_name | Efectivo, Visa, Cheque, Deposito a cuenta | String | Si | Por que medio de pago se cancelo la factura.
invoice_type | 01 | String | Si | Tipo de comprobante, ```01 es de una factura```.
currency | PEN, USD | String | Si | El tipo de moneda que se hizo el pago, ```PEN => Soles```.
discount | 23.56 | Double(18,2) | Si | Descuento por la venta
amount_total | 134.90 | Double(18,2) | Si | Monto total de la venta
customer | [Customer](CUSTOMER.md) | Array | Si | Cliente de la venta
taxes | []  | Array | Si | Impuestos
items | ['quantity', 'price', 'price_tax', 'tax_total_item', 'tax_unit_item', 'type_igv', 'description', 'system_id', 'correlative', 'type'] | Array | Si | Productos de la venta

#### Customer
Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
document | [-]| String | Si | Es el número de documento del cliente
client_id | any| String | Si | El el id de tu sistema
type_document | any| String | No | El el tipo de documento
business_name | any| String | No | Es obligatorio si es una factura
telephone | any| String | No | El número de teléfono
email | any| String | No | El el email del cliente
address | any| String | Si | Es obligatorio si es una factura

#### Taxes []
Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
tax_total | X.XX| Double(18,2) | Si | Es el total del impuesto
tribute_code | XXXX | String | Si | El el código del impuesto en la Sunat, IGV(1000) o ISC(1003)

#### Items []
Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
quantity | XX | int | Si | Es la cantidad de productos vendidos
price | XX.XX | Double(18,2) | Si | Es el precio sin impuesto
price_tax | XX.XX | Double(18,2) | Si | Es el precio con impuesto
tax_total_item | XX.XX | Double(18,2) | No | Impuesto total
tax_unit_item | XX.XX | Double(18,2) | No | Impuesto por item
type_igv | any | String | No | Código del impuesto
description | any | String | No | Nombre del producto
system_id | any| String | Si | id del producto en tu sistema
correlative | any| String | Si | Correlativo en la venta
type | any| String | Si | Tipo de producto según Sunat

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
