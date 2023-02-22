
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
method_name | Efectivo, Visa, Cheque, Deposito a cuenta, Credito | String | Si | Por que medio se hizo el pago.
expiration_credit | YYYY-MM-DD | String | No/Si(method_name es Credito) | La fecha de expiración del crédito. Es obligatorio en el caso que una venta tenga su método de pago como crédito y debe ser diferente a la fecha de la emisión del comprobante.
invoice_type | 01 ó 03 | String | Si | **Catálogo No. 01 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el tipo de documento enviado. 
currency | PEN, USD | String | Si | **Catálogo No. 02 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el Códigos de tipo de monedas.
discount |  | Double(18,2) | Si | Descuento por la venta.
amount_total |  | Double(18,2) | Si | Monto neto total de la venta. Valor que no toma en cuenta el impuesto y el descuento.
type_operation_code | 0101, 0401, 0200, 0201, 0208 | String | Si | **Catálogo No. 51 en el** [Catálogo de códigos de Sunat](anexo-244-2019.pdf) para el Códigos de tipo de operación.
seller |  | String | No |  Nombre usuario que realiza el comprobante.
customer | [CUSTOMER](CUSTOMER.md) | Array | Si | Cliente de la venta.
observation |  | String | No | Observación asociada al comprobante.
guides_remission |  | String | No | Guía de remisión del remitente. Se recomienda que cumpla con el criterio de la sunat sobre este tipo de documento.
guides_carrier  |   | String | No | Guía de remisión transportista. Se recomienda que cumpla con el criterio de la sunat sobre este tipo de documento.
taxes | [TAXES](TAXES.md) | Array | Si | Impuestos de la venta.
total_taxes |  | Double(18,2)| Si | Sumatoria total del igv de cada uno de los productos. Al no existir IGV, el valor es cero.
items | [ITEMS](ITEMS.md) | Array | Si | Productos de la venta.

### Enviar Factura
Gravado
```js
{
  'nro_document': 'F001-00001287',
  'date': '2021-10-04',
  'invoice_type': '01',
  'method_name': 'Efectivo',
  'amount_total': 36.7796,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 6.6204,
      'tribute_code': '1000'
    }
  ],
  'type_operation_code': '0101',
  'total_taxes': 6.6204,
  'customer': {
    'client_id': 3,
    'document': '20600629922',
    'type_document': '6',
    'business_name': 'MOBYTES SAC',
    'telephone': null,
    'email': null,
    'address': 'JR. 16 DE MAYO NRO 746 SAN MARTIN - SAN MARTIN - MORALES'
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 4.2373,
      'price_tax': 5.0000,
      'tax_total_item': 0.76,
      'tax_unit_item': 0.7627,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 1.0000,
      'price': 25.4237,
      'price_tax': 30.0000,
      'tax_total_item': 4.58,
      'tax_unit_item': 4.5763,
      'description': 'DESPACHO A AGENCIA',
      'system_id': '7750020034617',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2002',
      'igv_percentage': '18.0000',
      'unit': 'ZZ',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 3.5593,
      'price_tax': 4.2000,
      'tax_total_item': 1.28,
      'tax_unit_item': 0.6407,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 3,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    }
  ],
  'discount': 0.00,
  'seller': 'NGZ Negosy',
  'observation': '',
  'guides_remission': '',
  'guides_carrier': ''
}
```

Exonerado
```js
{
  'nro_document': 'F001-00001287',
  'date': '2021-10-04',
  'invoice_type': '01',
  'method_name': 'Efectivo',
  'amount_total': 43.4000,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 0.0000,
      'tribute_code': '9997'
    }
  ],
  'type_operation_code': '0101',
  'total_taxes': 0.0,
  'customer': {
    'client_id': 3,
    'document': '20600629922',
    'type_document': '6',
    'business_name': 'MOBYTES SAC',
    'telephone': null,
    'email': null,
    'address': 'JR. 16 DE MAYO NRO 746 SAN MARTIN - SAN MARTIN - MORALES'
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 5.0000,
      'price_tax': 5.0000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '20',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 1.0000,
      'price': 30.0000,
      'price_tax': 30.0000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'DESPACHO A AGENCIA',
      'system_id': '7750020034617',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2002',
      'igv_percentage': '0.0000',
      'unit': 'ZZ',
      'unit_pdf': 'UND',
      'sunat_tax_code': '20',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 4.2000,
      'price_tax': 4.2000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 3,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '20',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    }
  ],
  'discount': '0.00',
  'seller': 'NGZ Negosy',
  'observation': '',
  'guides_remission': '',
  'guides_carrier': ''
}
```
Gravado y Exonerado
```js
{
  'nro_document': 'F001-00001287',
  'date': '2021-10-04',
  'invoice_type': '01',
  'method_name': 'Efectivo',
  'amount_total': 38.0610,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 5.3390,
      'tribute_code': '1000'
    },
    {
      'tax_total': 0.0000,
      'tribute_code': '9997'
    }
  ],
  'type_operation_code': '0101',
  'total_taxes': 5.3389,
  'customer': {
    'client_id': 3,
    'document': '20600629922',
    'type_document': '6',
    'business_name': 'MOBYTES SAC',
    'telephone': null,
    'email': null,
    'address': 'JR. 16 DE MAYO NRO 746 SAN MARTIN - SAN MARTIN - MORALES'
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 4.2373,
      'price_tax': 5.0000,
      'tax_total_item': 0.76,
      'tax_unit_item': 0.7627,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 1.0000,
      'price': 25.4237,
      'price_tax': 30.0000,
      'tax_total_item': 4.58,
      'tax_unit_item': 4.5763,
      'description': 'DESPACHO A AGENCIA',
      'system_id': '7750020034617',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2002',
      'igv_percentage': '18.0000',
      'unit': 'ZZ',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 4.2000,
      'price_tax': 4.2000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 3,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '20',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    }
  ],
  'discount': '0.00',
  'seller': 'NGZ Negosy',
  'observation': '',
  'guides_remission': '',
  'guides_carrier': ''
}
```
Exportacion de bienes (Aplicable también a exportación de servicios)
```js
{
  'nro_document': 'F001-00001287',
  'date': '2021-10-04',
  'invoice_type': '01',
  'method_name': 'Efectivo',
  'amount_total': 13.4000,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 0.0000,
      'tribute_code': '9995'
    }
  ],
  'type_operation_code': '0200',//0200: Bienes, 0201: Servicios realizados en el país, 0208: Servicios parcialmente en el extranjero
  'total_taxes': 0.0,
  'customer': {
    'document': '-',
    'client_id': 18,
    'type_document': '-',
    'business_name': 'JUAN FLORES',
    'telephone': '-',
    'email': '',
    'address': null
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 5.0000,
      'price_tax': 5.0000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '40',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 4.2000,
      'price_tax': 4.2000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '40',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    }
  ],
  'discount': '0.00',
  'seller': 'NGZ Negosy',
  'observation': '',
  'guides_remission': '',
  'guides_carrier': ''
}
```
Impuesto de bolsa con un precio de 0.00
```js
{
  'nro_document': 'F001-00001287',
  'date': '2021-10-04',
  'invoice_type': '01',
  'method_name': 'Efectivo',
  'amount_total': 13.4000,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 0.0000,
      'tribute_code': '9997'
    },
    {
      'tax_total': 0.0000,
      'tribute_code': '9998'
    },
    {
      'tax_total': 0.30,
      'tribute_code': '7152'
    }
  ],
  'type_operation_code': '0101',
  'total_taxes': 0.3,
  'customer': {
    'client_id': 3,
    'document': '20600629922',
    'type_document': '6',
    'business_name': 'MOBYTES SAC',
    'telephone': null,
    'email': null,
    'address': 'JR. 16 DE MAYO NRO 746 SAN MARTIN - SAN MARTIN - MORALES'
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 5.0000,
      'price_tax': 5.0000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '20',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 4.2000,
      'price_tax': 4.2000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '20',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 1.0000,
      'price': 0.0000,
      'price_tax': 0.0000,
      'tax_total_item': 0.00,
      'tax_unit_item': 0.0000,
      'description': 'Bolsa plástica',
      'system_id': '7750020015449',
      'correlative': 3,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '0.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '30',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.30,
      'referencial_unit_value': 0.30
    }
  ],
  'discount': '0.00',
  'seller': 'NGZ Negosy',
  'observation': '',
  'guides_remission': '',
  'guides_carrier': ''
}
```
Factura al crédito
```js
{
  'nro_document': 'F001-00001287',
  'date': '2021-10-04',
  'invoice_type': '01',
  'method_name': 'Credito',
  'amount_total': 11.3559,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 2.0441,
      'tribute_code': '1000'
    }
  ],
  'type_operation_code': '0101',
  'total_taxes': 2.0441,
  'customer': {
    'client_id': 3,
    'document': '20600629922',
    'type_document': '6',
    'business_name': 'MOBYTES SAC',
    'telephone': null,
    'email': null,
    'address': 'JR. 16 DE MAYO NRO 746 SAN MARTIN - SAN MARTIN - MORALES'
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 4.2373,
      'price_tax': 5.0000,
      'tax_total_item': 0.76,
      'tax_unit_item': 0.7627,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 3.5593,
      'price_tax': 4.2000,
      'tax_total_item': 1.28,
      'tax_unit_item': 0.6407,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    }
  ],
  'discount': '0.00',
  'seller': 'NGZ Negosy',
  'observation': '',
  'guides_remission': '',
  'guides_carrier': '',
  'expiration_credit': '2022-01-02'
}
```

### Enviar Boleta
Boleta sin cliente seleccionado
```js
{
  'nro_document': 'B001-00000097',
  'date': '2021-10-04',
  'invoice_type': '03',
  'method_name': 'Efectivo',
  'amount_total': 11.8645,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 2.1355,
      'tribute_code': '1000'
    }
  ],
  'type_operation_code': '0101',
  'total_taxes': 2.1355,
  'customer': {
    'document': '-',
    'client_id': 1,
    'type_document': '-',
    'business_name': 'Cliente',
    'telephone': '-',
    'email': '',
    'address': null
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 4.2373,
      'price_tax': 5.0000,
      'tax_total_item': 0.76,
      'tax_unit_item': 0.7627,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 3.8136,
      'price_tax': 4.5000,
      'tax_total_item': 1.37,
      'tax_unit_item': 0.6864,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    }
  ],
  'discount': '0.00',
  'seller': 'NGZ Negosy',
  'observation': ''
}
```
Boleta con cliente seleccionado
```js
{
  'nro_document': 'B001-00000097',
  'date': '2021-10-04',
  'invoice_type': '03',
  'method_name': 'Efectivo',
  'amount_total': 11.8645,
  'type_receipt': 'A4',
  'currency': 'PEN',
  'taxes': [
    {
      'tax_total': 2.1355,
      'tribute_code': '1000'
    }
  ],
  'type_operation_code': '0101',
  'total_taxes': 2.1355,
  'customer': {
    'client_id': 28,
    'document': '123456789',
    'type_document': '1',
    'business_name': 'Juan Perez',
    'telephone': null,
    'email': null,
    'address': null
  },
  'items': [
    {
      'quantity': 1.0000,
      'price': 4.2373,
      'price_tax': 5.0000,
      'tax_total_item': 0.76,
      'tax_unit_item': 0.7627,
      'description': 'vaso descartable 6 OZ',
      'system_id': '7750020006218',
      'correlative': 1,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    },
    {
      'quantity': 2.0000,
      'price': 3.8136,
      'price_tax': 4.5000,
      'tax_total_item': 1.37,
      'tax_unit_item': 0.6864,
      'description': 'YESO CERAMICO',
      'system_id': '7750020032231',
      'correlative': 2,
      'discount': '0.0000',
      'type': '2001',
      'igv_percentage': '18.0000',
      'unit': 'NIU',
      'unit_pdf': 'UND',
      'sunat_tax_code': '10',
      'isc_unit_item': 0.0000,
      'isc_total_item': 0.00,
      'isc_code': null,
      'isc_percentage': 0,
      'icbper': 0.00,
      'referencial_unit_value': 0.00
    }
  ],
  'discount': '0.00',
  'seller': 'NGZ Negosy',
  'observation': ''
}
```


## Manejo de respuesta
> El parámetro **voucher_id** es el identificador del documento en nuestra plataforma [facturate.pe](https://facturate.pe), se tiene que guardar en su base de datos para próximas operaciones sobre ese documento.

### Envío éxitoso

```js
{
    "date": "22-02-2023 11:36",
    "nro_document": "F001-00001506",
    "customer": {
        "name": "SERVICIOS GENERALES DAMIRADI S.A.C.",
        "address": "AV. COSTA RICA LT. - MZ. R MONSERRATE 4TA ETAPA - ED LA LIBERTAD - TRUJILLO - TRUJILLO",
        "nro_document": "20601332559",
        "email": "-",
        "type_document_name": "RUC"
    },
    "products": [
        {
            "unit_code": "NIU",
            "quantity": "1.0000",
            "correlative": 1,
            "description": "ESTUCHE  BABY SERIES FUNNY X 6",
            "price_with_tax": "28.0000",
            "price_without_tax": "23.7288",
            "discount": "0.0000",
            "total": 23.73,
            "code": "7750020138933",
            "unit": {
                "code": "NIU",
                "description": "UNIDAD (BIENES)",
                "abbreviation": "ud",
                "plural": "UNIDADES"
            },
            "detail": null,
            "unit_pdf": "UND",
            "price_isc_tax": "0.0000",
            "isc_percentage": "18.00",
            "address_starting_point": null,
            "address_arrival_point": null,
            "referential_value_transport_service": null,
            "referential_value_effective_cargo": null,
            "referential_value_nominal_payload": null,
            "trip_detail": null,
            "detraction_ubigeo_starting_point": null,
            "detraction_ubigeo_arrival_point": null
        },
        {
            "unit_code": "NIU",
            "quantity": "1.0000",
            "correlative": 2,
            "description": "INTERRUPTOR PARA CONSERVADORA 425769",
            "price_with_tax": "12.0000",
            "price_without_tax": "10.1695",
            "discount": "0.0000",
            "total": 10.17,
            "code": "7750294008871",
            "unit": {
                "code": "NIU",
                "description": "UNIDAD (BIENES)",
                "abbreviation": "ud",
                "plural": "UNIDADES"
            },
            "detail": null,
            "unit_pdf": "UND",
            "price_isc_tax": "0.0000",
            "isc_percentage": "18.00",
            "address_starting_point": null,
            "address_arrival_point": null,
            "referential_value_transport_service": null,
            "referential_value_effective_cargo": null,
            "referential_value_nominal_payload": null,
            "trip_detail": null,
            "detraction_ubigeo_starting_point": null,
            "detraction_ubigeo_arrival_point": null
        }
    ],
    "amount_to_word": "Cuarenta con 00/100 Soles",
    "total_amount": "33.90",
    "additional": [],
    "company": {
        "id": 2,
        "business_name": "NEGOSY Y S.A.C.",
        "address": "JR. MANCO CAPAC NRO. 241 (MANCO CAPAC 241 4TO PISO)",
        "telephone": "65351553 Cel. 942924807",
        "logo": "/media/company/Storm_Viewer_01.jpg",
        "ruc": "20604747369",
        "email": "epedropablo@hotmail.com",
        "tradename": "NEGOSY",
        "name": "demo",
        "slug": "demo",
        "owner_of": null
    },
    "information_invoice": [
        {
            "code": "1001",
            "label": "Operación Gravada",
            "is_invoice": true,
            "amount": 33.9,
            "receipt_code": "01"
        },
        {
            "code": "1002",
            "label": "Operación Inafecta",
            "is_invoice": true,
            "amount": 0,
            "receipt_code": "03"
        },
        {
            "code": "1003",
            "label": "Operación Exonerada",
            "is_invoice": true,
            "amount": 0,
            "receipt_code": "02"
        },
        {
            "code": "1004",
            "label": "Operación Gratuita",
            "is_invoice": true,
            "amount": 0,
            "receipt_code": "05"
        },
        {//solo se muestra si la venta es de tipo exportacion
            "code": "1000",
            "label": "Operación Exportación",
            "is_invoice": false,
            "amount": 0,
            "receipt_code": "04"
        }
    ],
    "note": "",
    "hash_value": "rgxdfo6FxAHCwFvE2Z0vBQudjIA=",
    "qr_code": null,
    "barcode_pdf417": null,
    "global_tax": [
        {
            "amount": "6.10",
            "tax": 1,
            "tax_name": "I.G.V."
        }
    ],
    "voucher": "FACTURA ELECTRÓNICA",
    "discount": "0.00",
    "prepaid": [],
    "voucher_code": "01",
    "pdf": "",
    "xml": "https://{esquema}.facturate.pe/resource/demo/2023/22-February/signed/20604747369-01-F001-00001506.xml",
    "method_name": "Efectivo",
    "voucher_id": "cc97e364-aace-4f88-ba03-9d6f276e1ad3",
    "seller": "NGZ Negosy",
    "total_with_tax": 40,
    "guide_remissions": "",
    "guides_carrier": "",
    "expiration_date": null,
    "amount_pending_credit": "0.00",
    "voucher_date": "2023-02-22",
    "total_isc": 0,
    "slogan": "No se aceptan devoluciones de productos o de dinero",
    "pdf_base64": "(Pdf en base64)"
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
