# facturate.pe
La API REST le permite interactuar con **facturate.pe** para que pueda enviar sus documentos eléctronicos por una petición HTTP.

Los documentos elétronicos que puede enviar son:

* [Factura y Boleta eléctronica](docs/INVOICE.md)
* [Comunicación de baja](docs/UNSUBSCRIBE.md)
* Nota de Crédito (muy pronto)
* Nota de Debito (muy pronto)
* [Enviar email](docs/SEND_EMAIL.md)
* [Re-imprimir CPE](docs/RE_PRINT_CPE.md)


### Configuración
Para poder empezar a enviar sus documentos eléctronicos tiene que crearse una cuenta en [facturate.pe](https://facturate.pe), validar tu cuenta y obtener el **Token**

### Seguridad
Para efectos de seguridad se ha implementado el método **Token**, para poder hacer cualquier petición HTTP al servidor de [facturate.pe](https://facturate.pe). Tienes que adjuntar el token al header de esta manera. 

```py
Authorization: <type> <credentials>
```

### Envío al Servidor por Lenguaje de programación
> Llamaremos **data** a los datos que enviaremos.

### PHP

```php
$data_boleta = array(
  'data' => []
);
$data_string = json_encode($data_boleta);
$ch = curl_init('https://[store].facturate.pe/api/v1/invoice/efactura/');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $data_string);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'Authorization: Token [token]',
    'Content-Length: ' . strlen($data_string))
);
$result = curl_exec($ch);
curl_close($ch);
$data = json_decode($result);
```

### Python
```py
#!/usr/bin/python
import requests
query = requests.Session()
query.headers.update({'Authorization': 'Token %s' % company.token_facturate})
query.headers.update({'content-type': 'application/json'})
response = query.post('https://demo.facturate.pe/api/v1/invoice/efactura/' ,
                              data=simplejson.dumps(data))
```

### Imprimir en javascript
```js
var printPdfBase64 = function (pdf_base64) {

function dataURItoBlob(dataURI) {
    var byteString;
    if (dataURI.split(',')[0].indexOf('base64') >= 0)
        byteString = atob(dataURI.split(',')[1]);
    else
        byteString = unescape(dataURI.split(',')[1]);

    // separate out the mime component
    var mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0];

    // write the bytes of the string to a typed array
    var ia = new Uint8Array(byteString.length);
    for (var i = 0; i < byteString.length; i++) {
        ia[i] = byteString.charCodeAt(i);
    }
    return new Blob([ia], {type: mimeString});
}

// console.log(pdf_base64);
var data_document = "data:application/pdf;base64," + pdf_base64;
var preBlob = dataURItoBlob(data_document);
var pdfFile = new Blob([preBlob], {type: 'application/pdf'});
var pdfUrl = URL.createObjectURL(pdfFile);
const iframe = document.createElement('iframe');
iframe.style.display = 'none';
iframe.src = pdfUrl;
document.body.appendChild(iframe);
iframe.contentWindow.print();
};
```
