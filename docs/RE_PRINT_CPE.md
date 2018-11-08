## Volver a imprimir un documento electrónico
La respuesta es un documento PDF

Endpoint | Método HTTP | Parametros
------------ | ------------- | ------------
https://demo.facturate.pe/api/v1/invoice/invoice_view/<voucher_id> | GET | voucher_id


## Detalle de los Parámetros

Nombre | Formato | Tipo | Requerido | Descripción 
------------ | ------------- | ------------- | ------------- | -------------
voucher_id |  | String | Si | Es el identificador del voucher(CPE) en la plataforma. 


## Lenguajes

#### Python
```py
query = requests.Session()
query.headers.update({'Authorization': 'Token %s' % <token_facturate> })
query.headers.update({'content-type': 'application/pdf'})
pdf_url = 'https://[store].facturate.pe/api/v1/invoice/invoice_view/%s' % voucher_id
response = query.get(pdf_url)
response = HttpResponse(response, content_type='application/pdf')
response['Content-Disposition'] = 'inline;filename=%s.pdf' % voucher_id
return response
```
