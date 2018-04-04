# FacturaYa
La API REST le permite interactuar con **FacturaYa.pe** para que pueda enviar sus documentos eléctronicos por una petición HTTP.

### Configuración
Para poder empezar a enviar sus documentos eléctronicos tiene que crearse una cuenta en [facturaya.pe](https://facturate.pe), validar tu cuenta y obtener el **Token**

### Seguridad
Para efectos de seguridad se ha implementado el método **Token**, para poder hacer cualquier petición HTTP al servidor de [facturaya.pe](https://facturate.pe) tienes que adjuntar el token al header de esta manera. 

```py
Authorization: <type> <credentials>
```

Los documentos elétronicos que puede enviar son:

* [Factura eléctronica](docs/FACTURA.md)
* Boleta eléctronica
* Comunicación de baja: factura o boleta elécronica
* Nota de Crédito (muy pronto)
* Nota de Debito (muy pronto)
