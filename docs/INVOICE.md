
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
method_name | Efectivo, Visa, Cheque, Deposito a cuenta | String | Si | Por que medio de pago se hizo el pago.
invoice_type | 01 ó 03 | String | Si | **Catálogo No. 01 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el tipo de documento enviado. 
currency | PEN, USD | String | Si | **Catálogo No. 02 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el Códigos de tipo de monedas.
discount |  | Double(18,2) | Si | Descuento por la venta.
amount_total |  | Double(18,2) | Si | Monto total de la venta.
customer | [CUSTOMER](CUSTOMER.md) | Array | Si | Cliente de la venta.
taxes | [TAXES](TAXES.md) | Array | Si | Impuestos de la venta.
items | [ITEMS](ITEMS.md) | Array | Si | Productos de la venta.

### Enviar Factura
```js
{
  'nro_document': 'F001-00000047', 
  'date': '2018-04-04', 
  'invoice_type': '01', 
  'method_name': 'Efectivo', 
  'amount_total': 8008.00, 
  'type_receipt': 'A4', 
  'currency': 'PEN', 
  'taxes': [
              {
                'tax_total': 0.00, 
                'tribute_code': '1000'
              }
           ], 
  'customer': {
                'client_id': 3, 
                'document': '20600767765', 
                'type_document': '6', 
                'business_name': 'EL CULTURAL S.A.C', 
                'telephone': None, 
                'email': None, 
                'address': 'JR. SOFIA DELGADO 234'
              }, 
  'items': [
            {
              'quantity': 2.00, 
              'price': 4.00, 
              'price_tax': 4.00, 
              'tax_total_item': 0.00, 
              'tax_unit_item': 0.00, 
              'type_igv': '20', 
              'description': 'GASEOSA INCAK', 
              'system_id': '7750002000164', 
              'correlative': 1, 
              'type': '2001'
            }, 
            {
              'quantity': 1.00, 
              'price': 8000.00, 
              'price_tax': 8000.00, 
              'tax_total_item': 0.00, 
              'tax_unit_item': 0.00, 
              'type_igv': '20', 
              'description': 'CONSULTORIA DE EXPEDIENTE TECNICO', 
              'system_id': '7750002000122', 
              'correlative': 2, 
              'type': '2002'
            }
           ], 
  'discount': 0.00
}
```

### Enviar Boleta
```js
{
  'nro_document': 'B001-00000308', 
  'date': '2018-04-04', 
  'invoice_type': '03', 
  'method_name': 'Efectivo', 
  'amount_total': 16.00, 
  'type_receipt': 'Ticket', 
  'currency': 'PEN', 
  'taxes': [
              {
              'tax_total': 0.00, 
              'tribute_code': '1000'
              }
            ], 
  'customer': {
                'document': '-', 
                'client_id': 1, 
                'type_document': '-', 
                'business_name': 'Cliente', 
                'telephone': '-', 
                'email': '', 
                'address': '-'
              }, 
  'items': [
              {
                'quantity': 4.00, 
                'price': 4.00, 
                'price_tax': 4.00, 
                'tax_total_item': 0.00, 
                'tax_unit_item': 0.00, 
                'type_igv': '20', 
                'description': 'GASEOSA INCAK', 
                'system_id': '7750002000164', 
                'correlative': 1, 
                'type': '2001'
              }
           ], 
  'discount': 0.00
}
```

### Respuesta
```js
{
  'date': '04/04/2018 05:08 PM', 
  'nro_document': 'F001-00000048', 
  'customer': {
                'name': 'EL CULTURAL S.A.C', 
                'address': 'JR. SOFIA DELGADO 234', 
                'nro_document': '20600767765', 
                'email': '-'
              }, 
  'products': [
                {
                  'unit_code': 'NIU', 
                  'quantity': '2.00', 
                  'correlative': 2, 
                  'description': 'GASEOSA INCAK', 
                  'price_without_tax': '4.00', 
                  'discount': '0.00', 
                  'total': 8.0, 
                  'code': '7750002000164'
                }, 
                {
                  'unit_code': 'NIU', 
                  'quantity': '1.00', 
                  'correlative': 1, 
                  'description': 'CONSULTORIA DE EXPEDIENTE TECNICO', 
                  'price_without_tax': '8000.00', 
                  'discount': '0.00', 
                  'total': 8000.0, 
                  'code': '7750002000122'
                }
              ], 
  'amount_to_word': 'Ocho Mil Ocho con 00/100 Soles', 
  'total_amount': '8008.00', 
  'additional': [
                  {
                    'id': 5, 
                    'code': '2002', 
                    'description': 'SERVICIOS PRESTADOS EN LA AMAZONIA REGION SELVA PARA SER CONSUMIDOS EN LA MISMA', 
                    'label': 'Leyenda'
                  }
                ], 
  'company': {
              'business_name': 'DEMO S.A.C.', 
              'address': 'JR. MANCO CAPAC #529', 
              'telephone': '976143808', 
              'logo': '/media/company/new-user-icon_AHV7WJF.png', 
              'ruc': '10425475148', 
              'email': 'demo@facturate.pe', 
              'tradename': None, 
              'name': 'demo', 
              'slug': 'demo'
            }, 
  'information_invoice': [
                           { 'label': 'Operación Exonerada', 'is_invoice': True, 'amount': 8008.0 }, 
                           { 'label': 'Operación Gravada', 'is_invoice': True, 'amount': 0 }, 
                           { 'label': 'Operación Inafecta', 'is_invoice': True, 'amount': 0 }, 
                           { 'label': 'Operación Gratuita', 'is_invoice': True, 'amount': 0 }], 
  'hash_value': 'c3ExF89ry3iWFX/XusoF0RxcR3bbGD8PsspmyfJ47XY=', 
  'qr_code':'qr_code en base64', 
  'barcode_pdf417': 'image in base_64', 
  'global_tax': [
                  {
                    'amount': '0.00', 'tax': 1, 
                    'tax_name': 'IGV'
                  }
                ], 
  'voucher': 'FACTURA ELECTRÓNICA', 
  'voucher_code': '01', 
  'pdf': 'No se encontro el documento pdf, comuniquese con el administrador', 
  'xml': 'http://demo.facturate.demo:8001/resource/demo/2018/4-April/signed/10425475148-01-F001-00000048.xml',
  'method_name': 'Efectivo', 'voucher_id': '03ead121-fbc4-470f-83de-3e2c49a8f83e', 'pdf_base64': 'pdf in base64'}
  'information_invoice': [
                          { 'label': 'Operación Exonerada', 'is_invoice': True, 'amount': 8008.0}, 
                          {'label': 'Operación Gravada', 'is_invoice': True, 'amount': 0}, 
                          {'label': 'Operación Inafecta', 'is_invoice': True, 'amount': 0}, 
                          {'label': 'Operación Gratuita', 'is_invoice': True, 'amount': 0}], 
  'hash_value': 'c3ExF89ry3iWFX/XusoF0RxcR3bbGD8PsspmyfJ47XY=', 
  'qr_code': 'qr_code en base64', 
  'barcode_pdf417': 'image in base_64', 
  'global_tax': [
                  {'amount': '0.00', 'tax': 1, 'tax_name': 'IGV'}
                ], 
  'voucher': 'FACTURA ELECTRÓNICA', 
  'voucher_code': '01', 'pdf': 'No se encontro el documento pdf, comuniquese con el administrador', 'xml':
  'http://demo.facturate.demo:8001/resource/demo/2018/4-April/signed/10425475148-01-F001-00000048.xml', 
  'method_name': 'Efectivo', 
  'voucher_id': '03ead121-fbc4-470f-83de-3e2c49a8f83e', 
  'pdf_base64': 'pdf in base64'
}
```

> Llamaremos **data** a los datos que enviaremos.

### PHP

```php
curl_setopt_array($ch = curl_init(), array(
  CURLOPT_URL => "https://demo.facturate.pe/api/v1/invoice/efactura/",
  CURLOPT_POSTFIELDS => **data**,
  CURLOPT_SAFE_UPLOAD => true,
));
curl_exec($ch);
curl_close($ch);
```

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
