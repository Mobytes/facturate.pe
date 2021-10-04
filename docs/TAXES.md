## Taxes
Es un array de los impuestos de la venta.

#### Parametros

Nombre | Formato | Tipo | Obligatorio | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
tax_total |  | Double(18,4) | Si | Es el total del impuesto.
tribute_code | 1000, 2000, 7152, 9995, 9996, 9997, 9998 | String | Si | **Catálogo No. 05 en el** [Catálogo de códigos de Sunat](anexo-244-2019.pdf) para el tipo de tributos.


##### Ejemplos:

* Todos los tipos de impuestos deben de sumarse en su propio apartado. *
```js
    [
        {
            'tax_total': 23.2000,
            'tribute_code': '1000'
        }
    ]
```

* Cuando es Exonerado.
```js
    [
        {
            'tax_total': 15.0000,
            'tribute_code': '9997'
        }
    ]
```

* Cuando es ISC.
```js
    [
        {
            'tax_total': 12.2000,
            'tribute_code': '2000'
        }
    ]
```

* Cuando tiene IGV y ISC
```js
    [
        {
            'tax_total': 23.2000,
            'tribute_code': '1000'
        },
        {
            'tax_total': 12.2000,
            'tribute_code': '2000'
        }
    ]
```

Recuerda que se pueden enviar varios tipos de impuesto en un comprobante.
El cálculo de los impuestos debe de estar de acuerdo a lo impuesto por la sunat.
