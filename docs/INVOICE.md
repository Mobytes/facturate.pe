
>Para obtener las urls de envío, tiene que ir al panel de configuración de su cuenta en [facturate.pe](https://facturate.pe). Para efectos de este tutorial usare una cuenta llamada **demo**.


## Enviar una Factura y Boleta eléctronica

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/efactura/ | POST | nro_document, date, type_receipt, method_name, invoice_type, customer, currency, taxes, discount, amount_total, items

## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
nro_document | FXXX-XXXXXXXX ó BXXX-XXXXXXXX | String | Si | Es el número de documento.
date | YYYY-MM-DD | String | Si | La fecha de cuando se emitio la factura.
type_receipt | A4, A5 or Ticket | String | Si | Módelo de documento a imprimir o enviar a correo eléctronico.
method_name | Efectivo, Visa, Cheque, Deposito a cuenta | String | Si | Por que medio se hizo el pago.
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
                'tribute_code': '9997'
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

## Manejo de respuesta
> El parámetro **voucher_id** es el identificador del documento en nuestra plataforma [facturate.pe](https://facturate.pe), se tiene que guardar en su base de datos para próximas operaciones sobre ese documento.

### Envío éxitoso

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

### Envío errado
```js
{
  "message": "mensaje de error",
  "code": 400,
  "success": false
}
```

## Lenguajes

#### PHP
```php
$data_boleta = array(
  'nro_document' => $objsunat->nro_comprobante,
  'date' => $objsunat->fecha,
  'invoice_type' => $comprobante_id,
  'method_name' => $objsunat->metodo_pago, //METODO DE PAGO
  'amount_total' => $objsunat->total,
  'type_receipt' => "Ticket",
  'currency' => "PEN", //MONEDA
  'taxes' => $impuestos, // ARRAY
  'customer' => $cliente[0], // ARRAY
  'items' => $articulos, // ARRAY
  'discount' => $objsunat->descuento
);
$data_string = json_encode($data_boleta);
$ch = curl_init('https://[store].facturate.pe/api/v1/invoice/efactura/');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $data_string);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'Authorization: Token 62536523token2763723',
    'Content-Length: ' . strlen($data_string))
);
$result = curl_exec($ch);
curl_close($ch);
$data = json_decode($result);
````
