## Taxes
Es un array de los impuestos de la venta.

#### Parametros

Nombre | Formato | Tipo | Obligatorio | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
tax_total |  | Double(18,2) | Si | Es el total del impuesto.
tribute_code |  | String | Si | **Catálogo No. 05 en el** [Catálogo de códigos de Sunat](catalogo-de-codigos.pdf) para el tipo de tributos.


##### Ejemplos:

* Es obligatorio, si no tiene IGV el **tax_total** será **0.00**
```js
    [
        {
            'tax_total': 23.2,
            'tribute_code': '1000'
        }
    ]
```

* Cuando solo tiene ISC, no es obligatorio ponerlo
```js
    [
        {
            'tax_total': 12.2,
            'tribute_code': '1003'
        }
    ]
```

* Cuando tiene IGV y ISC
```js
    [
        {
            'tax_total': 23.2,
            'tribute_code': '1000'
        },
        {
            'tax_total': 12.2,
            'tribute_code': '1003'
        }
    ]
```
