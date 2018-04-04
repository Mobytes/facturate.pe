## Taxes
Es un array de los impuestos de la venta.

#### Parametros

Nombre | Formato | Tipo | Obligatorio | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
tax_total | X.XX| Double(18,2) | Si | Es el total del impuesto
tribute_code | XXXX | String | Si | El el código del impuesto en la Sunat, IGV(1000) o ISC(1003)

#### Códigos de la Sunat

Código | Descripción | UN/ECE 5153- Duty or tax or fee type name code
------------ | ------------- | ------------- 
1000 | IGV IMPUESTO GENERAL A LAS VENTAS | VAT
2000 | ISC IMPUESTO SELECTIVO AL CONSUMO | EXC
9999 | OTROS CONCEPTOS DE PAGO | OTH

#### Ejemplo:

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
