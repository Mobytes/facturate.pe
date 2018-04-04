### Customer
Son datos del cliente, dependiendo si es Jurídico o Natural

Nombre de parámetro | Formato | Tipo | Obligatorio | Descripcion 
------------ | ------------- | ------------- | ------------- | -------------
document | XXXXXXXX, XXXXXXXXXXX | String | Si | Es el número de documento del cliente. ```DNI => Natural, RUC => Jurídico```
client_id | any| String | Si | El el id de tu sistema
type_document | any| String | No | El el tipo de documento
business_name | any| String | No | Es obligatorio si es una factura
telephone | any| String | No | El número de teléfono
email | any| String | No | El el email del cliente
address | any| String | Si | Es obligatorio si es una factura
