## Taxes
Es un array de los impuestos de la venta.

#### Parametros

Nombre | Formato | Tipo | Obligatorio | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
tax_total |  | Double(18,4) | Si | Es el total del impuesto.
tribute_code | 1000, 2000, 7152, 9995, 9996, 9997, 9998 | String | Si | **Catálogo No. 05 en el** [Catálogo de códigos de Sunat](anexo-244-2019.pdf) para el tipo de tributos.


##### Ejemplos:

* Se suma el total del gravado. En los otros casos, el total del impuesto es cero, pero debe enviarse el tipo de impuesto.*
* Cuando es gravado.
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
            'tax_total': 0.0000,
            'tribute_code': '9997'
        }
    ]
```

* Cuando es Gravado y Exonerado.
```js
    [
        {
            'tax_total': 23.2000,
            'tribute_code': '1000'
        },
        {
            'tax_total': 0.0000,
            'tribute_code': '9997'
        }
    ]
```

Recuerda que se pueden enviar varios tipos de impuesto en un comprobante.
El cálculo de los impuestos debe de estar de acuerdo a lo impuesto por la sunat.
