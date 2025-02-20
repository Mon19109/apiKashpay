---
title: API Kashpay

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - ruby
  - python
  - php

toc_footers:
  - <a href='#'>Kashpay</a>
  - <a href='#'>Onsigna</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentacion de Kashpay API
---

# Introduccion

Bienvenidos a la API de Kashpay, donde encontraras servicios web para uso de las dos APIS  que conforman el entorno Kashpay (emision y adquirencia). 

Nuestros servicios estan diseñados con la estructura RESTful. Los request y response se presentan en  formato JSON.

Para poder hacer uso de los siguientes servicios, es necesario llenar el siguiente  formulario para poder registrarlo en nuestro sistema y generar credenciales de  operación. 

# API Adquirencia
## Autenticacion

```java
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate")
  .header("Content-Type", "application/json")
  .body("{\n  \"entity\": \"com.cascade\",\n  \"password\": \"cascTest4333\",\n  \"user\": \"jim@cascadefintech.com\"\n\n}")
  .asString();
```

```ruby
require "uri"
require "json"
require "net/http"

url = URI("http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "entity": "com.cascade",
  "password": "cascTest4333",
  "user": "jim@cascadefintech.com"
})

response = http.request(request)
puts response.read_body
```

```python
import requests
import json

url = "http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate"

payload = json.dumps({
  "entity": "com.cascade",
  "password": "cascTest4333",
  "user": "jim@cascadefintech.com"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "entity": "com.cascade",
    "password": "cascTest4333",
    "user": "jim@cascadefintech.com"

  }',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

> El codigo anterior devuelve un JSON estructurado así:

```json
{
  "success": true,
  "authenticationResponse": {
    "token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqaW1AY2FzY2FkZWZpbnRlY2guY29tIiwiZXhwIjoxNjY5Nzk5MjA4LCJpYXQiOjE2Njk3OTMyMzJ9.Xhk_B_iOaXPQzkiEdMnvpuUVI8nz6_6uZB9HF4rEJI2zpi0G3K7UqfeBTsbWHP-hFtkHgLDnNHXKnMWc8ixFzA",
    "expires": "5975999"
  }
}
```

Para utilizar los Servicios de la Plataforma Onsigna (POS, Comercio Electrónico, Pago de Facturas, Libro a Libro, etc.) es obligatorio que se pueda generar un Token de Sesión.

### HTTP Request

`POST http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate`

### Query Parameters

Parameter | Description
--------- | -----------
entity    | Entidad previamente registrada.
password  | Clave privada asignada por el usuario.
user      | Correo electronico registrado.

<aside class="success">
Recuerda — Las credenciales para este propósito se proporcionan a nivel de Entidad.
</aside>

## createOrder

Este servicio ejecuta varios tipos de operaciones de Remesas. Transferir fondos (también conocido como SPEI), ingreso y retiro de efectivo, pago Swift, Mastercard y Visa.
El envío de dinero nacional se realiza a través del operativo "1 - Transferencia Interbancaria SPEI", se puede visualizar en la pestaña Modelo.

```java
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate")
  .header("Content-Type", "application/json")
  .body("{\n  \"entity\": \"com.cascade\",\n  \"password\": \"cascTest4333\",\n  \"user\": \"jim@cascadefintech.com\"\n\n}")
  .asString();
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```php
cUnirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate")
  .header("Content-Type", "application/json")
  .body("{\n  \"entity\": \"com.cascade\",\n  \"password\": \"cascTest4333\",\n  \"user\": \"jim@cascadefintech.com\"\n\n}")
  .asString();

```

> El codigo anterior devuelve un JSON estructurado así, si la respuesta success es true:

```json
{
  "success": true,
  "orderEntityResponse": {
    "createdAt": "2022-12-20T17:11:46.794+0000",
    "uptadedAt": "2022-12-20T17:11:46.794+0000",
    "id": "13699",
    "numericReference": "43223123",
    "alphanumericReference": "PROVV0011712091",
    "referenceCreatedPayment": "on000000011598",
    "status": 25,
    "initialBalance": 10000,
    "finalBalance": 10250
  },
  "totalItems": 0,
  "totalPages": 0,
  "currentPage": 0
}
```
> Si la respuesta success es false

```json
{
  "success": false,
  "error": {
    "name": "EntityException",
    "message": "No se pudo procesar el pago",
    "code": 1022
  },
  "totalItems": 0,
  "totalPages": 0,
  "currentPage": 0
}
```

### HTTP Request

`POST http://sdbx-centauri.kashplataforma.com/OKPay/createOrder`

### URL Parameters

Parameter | Description
--------- | -----------
alphanumericReference | nd
amount | Monto de la transaccion
beneficiaryAcount | Cuenta beneficiaria
beneficiaryAddress1 | Direccion del beneficiario
beneficiaryCity |CDMX
beneficiaryName | Nombre del beneficiario
beneficiaryTypeAcount | Tipo de la cuenta beneficiaria
codeInstituteBank | Codigo de la institucion
concept | Concepto de la transaccion
currency | 484 por default
dataAccreditationBeneficiary | 99
dateTransaction | 030421
description | descripcion de la transaccion
email | Correo electronico
idBank | ID de la institucion bancaria
idEntity | ID de la entidad 
numericReference | Referencia numerica
postalCode | Codigo postal
referenceCreatedPayment | 811111112
typeTransaction | Tipo de la transaccion

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

# API Emision

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>



