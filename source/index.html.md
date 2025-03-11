---
title: API Kashpay

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - java
  - php
  - ruby
  - python
  - shell

toc_footers:
  - <a href='#'>Kashpay</a>
  - <a href='#'>Onsigna</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: false

meta:
  - name: description
    content: Documentacion de Kashpay API
---

# Introduccion

Bienvenidos a la API de Kashpay, donde encontraras servicios web para uso de las APIS  que conforman el entorno Kashpay. 

Nuestros servicios estan diseñados con la estructura RESTful. Los request y response se presentan en  formato JSON.

Para poder hacer uso de los siguientes servicios, es necesario llenar el siguiente  formulario para poder registrarlo en nuestro sistema y generar credenciales de  operación. 




# Autenticacion <span style="float: right; color:#0f70ec;font-size: 9px;">POST</span>

Valida credenciales y genera tokenSesion para el consumo de los diferentes servicios.

```java
// JAVA - Unirest
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate")
  .header("Content-Type", "application/json")
  .body("{\n    \"entity\": \"com.onsigna\",\n    \"password\": \"onsig1234qw\",\n    \"user\": \"onsigna@gmail.com\"\n\n  }")
  .asString();

```

```php
//PHP - cURL
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
    "entity": "com.onsigna",
    "password": "onsig1234qw",
    "user": "onsigna@gmail.com"

  }',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

```ruby
# RUBY - Net::HTTP
require "uri"
require "json"
require "net/http"

url = URI("http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "entity": "com.onsigna",
  "password": "onsig1234qw",
  "user": "onsigna@gmail.com"
})

response = http.request(request)
puts response.read_body

```

```python
# PYTHON - http.client
import http.client
import json

conn = http.client.HTTPConnection("sdbx-polaris.kashplataforma.com")
payload = json.dumps({
  "entity": "com.onsigna",
  "password": "onsig1234qw",
  "user": "onsigna@gmail.com"
})
headers = {
  'Content-Type': 'application/json'
}
conn.request("POST", "/AuthenticationService/authenticate", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

```

```shell
# SHELL - httpie
printf '{
    "entity": "com.onsigna",
    "password": "onsig1234qw",
    "user": "onsigna@gmail.com"

  }'| http  --follow --timeout 3600 POST 'http://sdbx-polaris.kashplataforma.com/AuthenticationService/authenticate' \
 Content-Type:'application/json'

```


> El codigo anterior devuelve un JSON estructurado así:

```json
{
  "success": true,
  "authenticationResponse": {
    "token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqaW1AY2FzY2FkZWZpbnRlY2guY29tIiwiZXhwIjoxNjY5Nzk5MjA4LCJpYXQiOjE2Njk3OTMyMzJ9.Xhk_B_iOaXPQzkiEdMnvpuUVI8nz6_6uZB9HF4rEJI2zpi0G3K7UqfeBTsbWHP-hFtkHgLDnNHXKnMWc8ixFzA",
    "expires": "5975999"
  }
}s
```

Para utilizar los Servicios de la Plataforma Kashpay (POS, Comercio Electrónico, Pago de Facturas, Libro a Libro, etc.) es obligatorio que se pueda generar un Token de Sesión.

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






# API Adquirencia





# API Emision

## login

Valida las credenciales para acceder en la app wallet, permite o deniega el acceso. Una vez que los accesos sean correctos, dicho servicio devuelve los saldos  asignados, así como el estatus, información y la tarjeta asociada a la cuenta. 


```java
// JAVA - Unirest
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-aldebaran.kashplataforma.com/aldbrn/internal/aw/registerOnboard ")
  .header("Authorization", "Basic YWRtaW46c2VjcmV0")
  .header("Content-Type", "application/json")
  .body("\"loginRequest\": { \n   \"authentication\": { \n    \"user\": \"test@gmail.com\", \n    \"mail\": \"test@gmail.com\", \n    \"password\": \"**********\" \n   }, \n   \"latitude\": \"19.6735912\", \n   \"longitude\": \"-99.0711819\", \n   \"dateTransaction\": \"20230113\", \n   \"hourTransaction\": \"134209\", \n }, \n \"device\": { \n   \"os\": \"Android\", \n   \"systemOperativeName\": \"Version Desconocida\", \n   \"systemOperativeVersion\": \"15\", \n   \"manufacturer\": \"Google\", \n   \"model\": \"Pixel 7 Pro\", \n   \"latitude\": \"19.6735912\", \n   \"longitude\": \"-99.0711819\" \n }, \n \"appInfo\": { \n   \"nameApp\": \"eVolv\", \n   \"versionApp\": \"21.0.0\", \n   \"enviroment\": \"SANDBOX\", \n   \"versionConnector\": \"2.0.0\" \n } ")
  .asString();

```

```php
// PHP - cURL
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://sdbx-aldebaran.kashplataforma.com/aldbrn/internal/aw/registerOnboard ',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'"loginRequest": { 
   "authentication": { 
    "user": "test@gmail.com", 
    "mail": "test@gmail.com", 
    "password": "**********" 
   }, 
   "latitude": "19.6735912", 
   "longitude": "-99.0711819", 
   "dateTransaction": "20230113", 
   "hourTransaction": "134209", 
 }, 
 "device": { 
   "os": "Android", 
   "systemOperativeName": "Version Desconocida", 
   "systemOperativeVersion": "15", 
   "manufacturer": "Google", 
   "model": "Pixel 7 Pro", 
   "latitude": "19.6735912", 
   "longitude": "-99.0711819" 
 }, 
 "appInfo": { 
   "nameApp": "eVolv", 
   "versionApp": "21.0.0", 
   "enviroment": "SANDBOX", 
   "versionConnector": "2.0.0" 
 } ',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Basic YWRtaW46c2VjcmV0',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

```ruby
# RUBY - Net::HTTP


```

```python
# PYTHON - http.client


```

```shell
# SHELL - httpie


```


> El codigo anterior devuelve un JSON estructurado así:

```json
{
  "success": true,
  "loginResponse": {
    "cardNumber": "23473882130001",
    "idUser": 128,
    "idStatus": 1,
    "alias": "23473882130001",
    "dni": "9739347348",
    "keyOnboard": "keyOnboard",
    "pinDriver": "",
    "clabe": "646180585000000001",
    "telephone": "2347388213",
    "fullName": "ALFREDO MEDINA REYES",
    "catalogVersion": 5,
    "email": "amedina@test.com",
    "virtualAccount": "299873",
    "idSucursal": "6506",
    "state": "Durango",
    "registrationDate": "2022-04-19",
    "userApp": "",
    "address": {
      "street": "Lilas ",
      "exteriorNumber": "34",
      "postalCode": "73483",
      "location": "Las Palmas",
      "city": "Durango",
      "state": "Durango"
    },
    "mobilePin": "86267",
    "secundaryClabeAccount": "ND"
  },
  "cardsResponse": {
    "card": [
      {
        "acount": "299873",
        "saldos": {
          "availableConsumptions": "55.80",
          "cardAvailableBalance": 1.5
        },
        "cardObFuscated": "491049******XXXX",
        "dateVen": "2030-08",
        "typeCard": "fisica",
        "stateCard": "01",
        "name": "ALFREDO MEDINA REYES",
        "typeDocument": "INE",
        "documentNumber": "9739347348",
        "alias": "23473882130001",
        "clabe": "646180585000000001"
      }
    ]
  }
}
```

This endpoint retrieves all kittens.

### HTTP Request

`POST http://sdbx-aldebaran.kashplataforma.com/aldbrn/internal/aw/login`

### Query Parameters

Parameter | Description
--------- | -----------
user | Usuario
mail | Correo electronico
password | Clave asignada 
latitude | Latitud de la ubicacion actual
longitude | Longitud de la ubicacion actual 
dateTransaction | Fecha 
hourTransaction | Hora 
os | Sistema operativo del dispositivo
systemOperativeName | Nombre de la version del sistema operativo
systemOperativeVersion | Numero de la version del sistema operativo
manufacturer | Creado por o marca 
model | Modelo del dispositivo
latitude | Latitud de la ubicacion actual
longitude | Longitud de la ubicacion actual 
nameApp | Nombre de la aplicacion 
versionApp | Numero de version de la app
enviroment | Entorno - desarrollo o produccion 
versionConnector | Numero de version del conector
 






# API OKPay
## Crear orden <span style="float: right; color:#0f70ec;font-size: 9px;">POST</span>

Este servicio ejecuta varios tipos de operaciones de Remesas. Transferir fondos (también conocido como SPEI), ingreso y retiro de efectivo, pago Swift, Mastercard y Visa.
El envío de dinero nacional se realiza a través del operativo "1 - Transferencia Interbancaria SPEI", se puede visualizar en la pestaña Modelo.

```java
// JAVA - Unirest
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-centauri.kashplataforma.com/OKPay/createOrder")
  .header("Authorization", "Basic YWRtaW46c2VjcmV0")
  .header("Content-Type", "application/json")
  .body("{\n  \"alphanumericReference\": \"PROVV0011712091\",\n  \"amount\": 250,\n  \"beneficiaryAcount\": 87459854,\n  \"beneficiaryAcountSPEI\": 87459854,\n  \"beneficiaryAddress1\": \"Vicente G 132 Mz5 Lt14\",\n  \"beneficiaryAddress2\": \"Vicente G 132 Mz5 Lt14\",\n  \"beneficiaryCity\": \"CDMX\",\n  \"beneficiaryName\": \"Florentino Eter\",\n  \"beneficiaryTypeAcount\": \"string\",\n  \"codeInstituteBank\": \"002\",\n  \"concept\": \"Deposito Maria\",\n  \"currency\": 484,\n  \"dataAccreditationBeneficiary\": 99,\n  \"dateTransaction\": \"030421\",\n  \"description\": \"prueba\",\n  \"email\": \"testrest@gmail.com\",\n  \"idBank\": 4177,\n  \"idEntity\": 4177,\n  \"numericReference\": 43223123,\n  \"observation\": \"test@gmail.com\",\n  \"orderingAccount\": 111,\n  \"orderingTypeAcount\": \"string\",\n  \"postalCode\": 57800,\n  \"referenceCreatedPayment\": 811111112,\n  \"rfc\": \"ROPL951201091\",\n  \"typeTransaction\": 1\n}\n")
  .asString();

```

```php
// PHP - cURL
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://sdbx-centauri.kashplataforma.com/OKPay/createOrder',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "alphanumericReference": "PROVV0011712091",
    "amount": 250,
    "beneficiaryAcount": 87459854,
    "beneficiaryAcountSPEI": 87459854,
    "beneficiaryAddress1": "Vicente G 132 Mz5 Lt14",
    "beneficiaryAddress2": "Vicente G 132 Mz5 Lt14",
    "beneficiaryCity": "CDMX",
    "beneficiaryName": "Florentino Eter",
    "beneficiaryTypeAcount": "string",
    "codeInstituteBank": "002",
    "concept": "Deposito Maria",
    "currency": 484,
    "dataAccreditationBeneficiary": 99,
    "dateTransaction": "030421",
    "description": "prueba",
    "email": "testrest@gmail.com",
    "idBank": 4177,
    "idEntity": 4177,
    "numericReference": 43223123,
    "observation": "test@gmail.com",
    "orderingAccount": 111,
    "orderingTypeAcount": "string",
    "postalCode": 57800,
    "referenceCreatedPayment": 811111112,
    "rfc": "ROPL951201091",
    "typeTransaction": 1
  }',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer YWRtaW46c2VjcmV0',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

```ruby
# RUBY - Net::HTTP


```

```python
# PYTHON - http.client


```

```shell
# SHELL - httpie


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

### Query Parameters

Parameter | Description
--------- | -----------
alphanumericReference | Referencia alfanumerica aleatoria
amount | Monto de la transaccion
beneficiaryAcount | Cuenta beneficiaria
beneficiaryAddress1 | Direccion del beneficiario
beneficiaryCity |Ciudad del beneficiario
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







# API EntitiesServices

## addEntity <span style="float: right; color:#0f70ec;font-size: 9px;">POST</span>

```java
// JAVA - Unirest
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-sirio.kashplataforma.com/EntitiesServices/addEntity")
  .header("Authorization", "Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTczOTM1MSwiaWF0IjoxNzQxNzMzMzc1fQ.GbzFRlsbwtLH_JyZLzZN8kJNcYKCgYScUU_ClnywK3ZHIhftKlKI2W75TAfS0ONuQmvrnMDDpX9OS_nXc-JWDA")
  .header("Entity-i", "com.onsigna")
  .header("Content-Type", "application/json")
  .body("{\n  \"bussinesName\": \"Test kash2\",\n  \"bussinesNameShort\": \"SUC kash 2\",\n  \"contextFatherID\": \"com.onsigna\",\n  \"userRequest\": {   \n    \"email\": \"userkash2@gmail.com\",   \n    \"telephoneNumber\": \"565311100\",\n    \"user\": \"72663-7266-8j71-76129\" \n  }\n}")
  .asString();

```

```php
// PHP - cURL
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://sdbx-sirio.kashplataforma.com/EntitiesServices/addEntity',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
  "bussinesName": "Test kash2",
  "bussinesNameShort": "SUC kash 2",
  "contextFatherID": "com.onsigna",
  "userRequest": {   
    "email": "userkash2@gmail.com",   
    "telephoneNumber": "565311100",
    "user": "72663-7266-8j71-76129" 
  }
}',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTczOTM1MSwiaWF0IjoxNzQxNzMzMzc1fQ.GbzFRlsbwtLH_JyZLzZN8kJNcYKCgYScUU_ClnywK3ZHIhftKlKI2W75TAfS0ONuQmvrnMDDpX9OS_nXc-JWDA',
    'Entity-i: com.onsigna',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

```ruby
# RUBY - Net::HTTP
require "uri"
require "json"
require "net/http"

url = URI("http://sdbx-sirio.kashplataforma.com/EntitiesServices/addEntity")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTczOTM1MSwiaWF0IjoxNzQxNzMzMzc1fQ.GbzFRlsbwtLH_JyZLzZN8kJNcYKCgYScUU_ClnywK3ZHIhftKlKI2W75TAfS0ONuQmvrnMDDpX9OS_nXc-JWDA"
request["Entity-i"] = "com.onsigna"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "bussinesName": "Test kash2",
  "bussinesNameShort": "SUC kash 2",
  "contextFatherID": "com.onsigna",
  "userRequest": {
    "email": "userkash2@gmail.com",
    "telephoneNumber": "565311100",
    "user": "72663-7266-8j71-76129"
  }
})

response = http.request(request)
puts response.read_body

```

```python
# PYTHON - http.client
import http.client
import json

conn = http.client.HTTPConnection("sdbx-sirio.kashplataforma.com")
payload = json.dumps({
  "bussinesName": "Test kash2",
  "bussinesNameShort": "SUC kash 2",
  "contextFatherID": "com.onsigna",
  "userRequest": {
    "email": "userkash2@gmail.com",
    "telephoneNumber": "565311100",
    "user": "72663-7266-8j71-76129"
  }
})
headers = {
  'Authorization': 'Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTczOTM1MSwiaWF0IjoxNzQxNzMzMzc1fQ.GbzFRlsbwtLH_JyZLzZN8kJNcYKCgYScUU_ClnywK3ZHIhftKlKI2W75TAfS0ONuQmvrnMDDpX9OS_nXc-JWDA',
  'Entity-i': 'com.onsigna',
  'Content-Type': 'application/json'
}
conn.request("POST", "/EntitiesServices/addEntity", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

```

```shell
# SHELL - httpie
printf '{
  "bussinesName": "Test kash2",
  "bussinesNameShort": "SUC kash 2",
  "contextFatherID": "com.onsigna",
  "userRequest": {   
    "email": "userkash2@gmail.com",   
    "telephoneNumber": "565311100",
    "user": "72663-7266-8j71-76129" 
  }
}'| http  --follow --timeout 3600 POST 'http://sdbx-sirio.kashplataforma.com/EntitiesServices/addEntity' \
 Authorization:'Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTczOTM1MSwiaWF0IjoxNzQxNzMzMzc1fQ.GbzFRlsbwtLH_JyZLzZN8kJNcYKCgYScUU_ClnywK3ZHIhftKlKI2W75TAfS0ONuQmvrnMDDpX9OS_nXc-JWDA' \
 Entity-i:'com.onsigna' \
 Content-Type:'application/json'

```


> El codigo anterior devuelve un JSON estructurado así:

```json
{
  "success": true,
  "onsignaEntity": {
    "id": "72663-7266-8j71-76129",
    "name": "Test kash2",
    "prefix": "SUC kash 2",
    "fiscalID": null,
    "clabeAccount": "002028650641359744",  //CLABE CUENTA CITI
    "virtualAccount": "6506000004135974",  //CUENTA CHEQUES
    "branchAcount": null,
    "webhookURL": null,
    "email": "userkash2@gmail.com",
    "phoneNumber": "565311100",
    "fatherID": "com.onsigna",
    "balance": 0,
    "warrantyBalance": 0,
    "customerNetworkBalance": 0,
    "warrantyClabeAccount": null,
    "warrantyVirtualAccount": null,
    "cryptedCard": null,
    "newCard": null,
    "assignClabeAccount": true,
    "feeID": 0,
    "internalReference": null,
    "liquidationLevel": null,
    "liquidationType": null,
    "entityType": null,
    "affiliationId": null
  }
}

```

### HTTP Request

`http://sdbx-sirio.kashplataforma.com/EntitiesServices/addEntity`

### Query Parameters

Parameter | Description
--------- | -----------
bussinesName | Nombre de la entidad
bussinesNameShort | Nombre corto de la entidad
contextFatherID | ID de la entidad
email | Correo electronico 
telephoneNumber | Telefono
user | Usuario


## getBalance <span style="float: right; color:#029702;font-size: 9px;">GET</span>

Servicio para obtener el saldo de la Entidad/Subentidad

```java
// JAVA - Unirest
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("http://sdbx-sirio.kashplataforma.com/EntitiesServices/getBalance")
  .header("Authorization", "Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MDY5NTQwMywiaWF0IjoxNzQwNjg5NDI3fQ.gnLouIsKyB2qs22IqU6juVsTLwZfRHX-CnSH_pUWPUrmLOZHFr83MLEbFJIB5-mu0oyBhcA1DYP7Yz0_-rwN_w")
  .header("Entity-i", "com.onsigna")
  .asString();

```

```php
// PHP - cURL
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://sdbx-sirio.kashplataforma.com/EntitiesServices/getBalance',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer eeyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MDY5NTQwMywiaWF0IjoxNzQwNjg5NDI3fQ.gnLouIsKyB2qs22IqU6juVsTLwZfRHX-CnSH_pUWPUrmLOZHFr83MLEbFJIB5-mu0oyBhcA1DYP7Yz0_-rwN_w',
    "Entity-i: com.onsigna"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

```ruby
# RUBY - Net::HTTP
require "uri"
require "net/http"

url = URI("http://sdbx-sirio.kashplataforma.com/EntitiesServices/getBalance")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Get.new(url)
request["Authorization"] = "Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcxNjY4NywiaWF0IjoxNzQxNzEwNzExfQ.44L_ar-989GzU6KTKDgS6dqzOOI4OWkJzheuMSZNd9AnJKC09R0squVMlz7b_1huq56aX1G4n8kaJYVosixPAA"
request["Entity-i"] = "com.onsigna"

response = http.request(request)
puts response.read_body

```

```python
# PYTHON - http.client
import http.client

conn = http.client.HTTPConnection("sdbx-sirio.kashplataforma.com")
payload = ''
headers = {
  'Authorization': 'Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcxNjY4NywiaWF0IjoxNzQxNzEwNzExfQ.44L_ar-989GzU6KTKDgS6dqzOOI4OWkJzheuMSZNd9AnJKC09R0squVMlz7b_1huq56aX1G4n8kaJYVosixPAA',
  'Entity-i': 'com.onsigna'
}
conn.request("GET", "/EntitiesServices/getBalance", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

```

```shell
# SHELL - httpie
http --follow --timeout 3600 GET 'http://sdbx-sirio.kashplataforma.com/EntitiesServices/getBalance' \
 Authorization:'Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcxNjY4NywiaWF0IjoxNzQxNzEwNzExfQ.44L_ar-989GzU6KTKDgS6dqzOOI4OWkJzheuMSZNd9AnJKC09R0squVMlz7b_1huq56aX1G4n8kaJYVosixPAA' \
 Entity-i:'com.onsigna'

```


> El codigo anterior devuelve un JSON estructurado así:

```json
{
    "success": true,
    "onsignaEntity": {
        "id": "com.onsigna",
        "name": "Onsigna",
        "prefix": "on",
        "fiscalID": null,
        "clabeAccount": "002028650641309053",
        "virtualAccount": "6506000004130920",
        "branchAcount": null,
        "webhookURL": null,
        "email": "suport@onsigna.com",
        "phoneNumber": "4444433333",
        "fatherID": null,
        "balance": 8437673.61,
        "warrantyBalance": 0.00,
        "customerNetworkBalance": 32769.34,
        "warrantyClabeAccount": "0",
        "warrantyVirtualAccount": null,
        "cryptedCard": null,
        "newCard": null,
        "assignClabeAccount": true,
        "feeID": 0,
        "internalReference": null,
        "liquidationLevel": "0",
        "liquidationType": null,
        "entityType": null,
        "affiliationId": null
    },
    "totalItems": 0,
    "totalPages": 0,
    "currentPage": 0
}

```


### HTTP Request

`GET   -   http://sdbx-aldebaran.kashplataforma.com/aldbrn/internal/aw/login`

### Query Parameters

Parameter | Description
--------- | -----------
Authorization | Default value : Bearer token
Entity ( entidad Maestra) | Default value : com.example



## getOperations

Servicio para obtener operaciones a nivel cuenta de la Entidad/Subentidad asociada a la entidad maestra 


```java
// JAVA - Unirest
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("http://sdbx-sirio.kashplataforma.com/EntitiesServices/getOperations")
  .header("Authorization", "Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcyNDc2NCwiaWF0IjoxNzQxNzE4Nzg4fQ.navutjFHrqxQNuI2OIaeAQfsJl8LPUJG6F1U729nOkDHIUmSnimnotl9mh9q6HY0N_g1gGU_ref1gbHDIH27RA")
  .header("Entity-i", "com.onsigna")
  .header("page", "0")
  .header("size", "10")
  .header("status", "25")
  .header("type", "1")
  .body("")
  .asString();

```

```php
# PHP - cURL
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://sdbx-sirio.kashplataforma.com/EntitiesServices/getOperations',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcyNDc2NCwiaWF0IjoxNzQxNzE4Nzg4fQ.navutjFHrqxQNuI2OIaeAQfsJl8LPUJG6F1U729nOkDHIUmSnimnotl9mh9q6HY0N_g1gGU_ref1gbHDIH27RA',
    'Entity-i: com.onsigna',
    'page: 0',
    'size: 10',
    'status: 25',
    'type: 1'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

```ruby
# RUBY - Net::HTTP
require "uri"
require "net/http"

url = URI("http://sdbx-sirio.kashplataforma.com/EntitiesServices/getOperations")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Get.new(url)
request["Authorization"] = "Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcyNDc2NCwiaWF0IjoxNzQxNzE4Nzg4fQ.navutjFHrqxQNuI2OIaeAQfsJl8LPUJG6F1U729nOkDHIUmSnimnotl9mh9q6HY0N_g1gGU_ref1gbHDIH27RA"
request["Entity-i"] = "com.onsigna"
request["page"] = "0"
request["size"] = "10"
request["status"] = "25"
request["type"] = "1"

response = http.request(request)
puts response.read_body

```

```python
# PYTHON - http.client
import http.client

conn = http.client.HTTPConnection("sdbx-sirio.kashplataforma.com")
payload = ''
headers = {
  'Authorization': 'Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcyNDc2NCwiaWF0IjoxNzQxNzE4Nzg4fQ.navutjFHrqxQNuI2OIaeAQfsJl8LPUJG6F1U729nOkDHIUmSnimnotl9mh9q6HY0N_g1gGU_ref1gbHDIH27RA',
  'Entity-i': 'com.onsigna',
  'page': '0',
  'size': '10',
  'status': '25',
  'type': '1'
}
conn.request("GET", "/EntitiesServices/getOperations", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

```

```shell
# SHELL - httpie
http  --follow --timeout 3600 GET 'http://sdbx-sirio.kashplataforma.com/EntitiesServices/getOperations' \
 Authorization:'Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJvbnNpZ25hQGdtYWlsLmNvbSIsImV4cCI6MTc0MTcyNDc2NCwiaWF0IjoxNzQxNzE4Nzg4fQ.navutjFHrqxQNuI2OIaeAQfsJl8LPUJG6F1U729nOkDHIUmSnimnotl9mh9q6HY0N_g1gGU_ref1gbHDIH27RA' \
 Entity-i:'com.onsigna' \
 page:'0' \
 size:'10' \
 status:'25' \
 type:'1'

```


> El codigo anterior devuelve un JSON estructurado así:

```json
{
  "acquiringId": "string",
  "acquiringOperation": {
    "alphanumericReference": "string",
    "amount": 0,
    "cititransaction": "string",
    "country": "string",
    "createdAt": "2025-03-11T18:47:33.673Z",
    "creditProductType": "string",
    "currency": {
      "alphabeticCode": "string",
      "createdAt": "string",
      "description": "string",
      "id": 0,
      "uptadedAt": "string"
    },
    "description": "string",
    "descriptionType": "string",
    "entity_id": "string",
    "externalReference": {},
    "finalBalance": 0,
    "id": 0,
    "initialBalance": 0,
    "internalReference": "string",
    "liquidationID": "string",
    "numericReference": "string",
    "observation": "string",
    "posDate": "string",
    "productCode": "string",
    "responseCode": "string",
    "settleAmount": 0,
    "status": 0,
    "systemSource": "string",
    "systemTraceAuditNumber": "string",
    "targetEmail": "string",
    "targetID": "string",
    "targetIDCode": "string",
    "targetName": "string",
    "timestamp": "string",
    "transactionBundler": 0,
    "transactionID": "string",
    "transactionSubType": "string",
    "transactionType": "string",
    "type": 0,
    "uptadedAt": "2025-03-11T18:47:33.673Z"
  },
  "authenticationResponse": {
    "expires": 38000,
    "timeStamp": "000",
    "token": "098NB987CV78B90JB9V8C7V8B9N0B9V8B9"
  },
  "currentPage": 0,
  "entities": [
    {
      "affiliationId": "string",
      "assignClabeAccount": true,
      "balance": 0,
      "branchAcount": "string",
      "clabeAccount": "string",
      "cryptedCard": "string",
      "customerNetworkBalance": 0,
      "email": "string",
      "entityType": "string",
      "fatherID": "string",
      "feeID": 0,
      "fiscalID": "string",
      "id": "string",
      "internalReference": "string",
      "liquidationLevel": "string",
      "liquidationType": "string",
      "name": "string",
      "newCard": "string",
      "phoneNumber": "string",
      "prefix": "string",
      "virtualAccount": "string",
      "warrantyBalance": 0,
      "warrantyClabeAccount": "string",
      "warrantyVirtualAccount": "string",
      "webhookURL": "string"
    }
  ],
  "entityID": "string",
  "entityValidationResponse": {
    "bussinesName": "string",
    "bussinesNameShort": "string",
    "context_id": 0,
    "entity": 0,
    "field1": "string",
    "rules": [
      "string"
    ],
    "user_id": 0
  },
  "error": {
    "code": 0,
    "message": "string",
    "name": "string"
  },
  "feeOperation": {
    "alphanumericReference": "string",
    "amount": 0,
    "cititransaction": "string",
    "country": "string",
    "createdAt": "2025-03-11T18:47:33.673Z",
    "creditProductType": "string",
    "currency": {
      "alphabeticCode": "string",
      "createdAt": "string",
      "description": "string",
      "id": 0,
      "uptadedAt": "string"
    },
    "description": "string",
    "descriptionType": "string",
    "entity_id": "string",
    "externalReference": {},
    "finalBalance": 0,
    "id": 0,
    "initialBalance": 0,
    "internalReference": "string",
    "liquidationID": "string",
    "numericReference": "string",
    "observation": "string",
    "posDate": "string",
    "productCode": "string",
    "responseCode": "string",
    "settleAmount": 0,
    "status": 0,
    "systemSource": "string",
    "systemTraceAuditNumber": "string",
    "targetEmail": "string",
    "targetID": "string",
    "targetIDCode": "string",
    "targetName": "string",
    "timestamp": "string",
    "transactionBundler": 0,
    "transactionID": "string",
    "transactionSubType": "string",
    "transactionType": "string",
    "type": 0,
    "uptadedAt": "2025-03-11T18:47:33.673Z"
  },
  "feeTaxOperation": {
    "alphanumericReference": "string",
    "amount": 0,
    "cititransaction": "string",
    "country": "string",
    "createdAt": "2025-03-11T18:47:33.673Z",
    "creditProductType": "string",
    "currency": {
      "alphabeticCode": "string",
      "createdAt": "string",
      "description": "string",
      "id": 0,
      "uptadedAt": "string"
    },
    "description": "string",
    "descriptionType": "string",
    "entity_id": "string",
    "externalReference": {},
    "finalBalance": 0,
    "id": 0,
    "initialBalance": 0,
    "internalReference": "string",
    "liquidationID": "string",
    "numericReference": "string",
    "observation": "string",
    "posDate": "string",
    "productCode": "string",
    "responseCode": "string",
    "settleAmount": 0,
    "status": 0,
    "systemSource": "string",
    "systemTraceAuditNumber": "string",
    "targetEmail": "string",
    "targetID": "string",
    "targetIDCode": "string",
    "targetName": "string",
    "timestamp": "string",
    "transactionBundler": 0,
    "transactionID": "string",
    "transactionSubType": "string",
    "transactionType": "string",
    "type": 0,
    "uptadedAt": "2025-03-11T18:47:33.673Z"
  },
  "liquidationId": "string",
  "onsignaEntities": [
    {
      "affiliationId": "string",
      "assignClabeAccount": true,
      "balance": 0,
      "branchAcount": "string",
      "clabeAccount": "string",
      "cryptedCard": "string",
      "customerNetworkBalance": 0,
      "email": "string",
      "entityType": "string",
      "fatherID": "string",
      "feeID": 0,
      "fiscalID": "string",
      "id": "string",
      "internalReference": "string",
      "liquidationLevel": "string",
      "liquidationType": "string",
      "name": "string",
      "newCard": "string",
      "phoneNumber": "string",
      "prefix": "string",
      "virtualAccount": "string",
      "warrantyBalance": 0,
      "warrantyClabeAccount": "string",
      "warrantyVirtualAccount": "string",
      "webhookURL": "string"
    }
  ],
  "onsignaEntity": {
    "affiliationId": "string",
    "assignClabeAccount": true,
    "balance": 0,
    "branchAcount": "string",
    "clabeAccount": "string",
    "cryptedCard": "string",
    "customerNetworkBalance": 0,
    "email": "string",
    "entityType": "string",
    "fatherID": "string",
    "feeID": 0,
    "fiscalID": "string",
    "id": "string",
    "internalReference": "string",
    "liquidationLevel": "string",
    "liquidationType": "string",
    "name": "string",
    "newCard": "string",
    "phoneNumber": "string",
    "prefix": "string",
    "virtualAccount": "string",
    "warrantyBalance": 0,
    "warrantyClabeAccount": "string",
    "warrantyVirtualAccount": "string",
    "webhookURL": "string"
  },
  "operationEntityResponse": {
    "alphanumericReference": "string",
    "amount": 0,
    "cititransaction": "string",
    "country": "string",
    "createdAt": "2025-03-11T18:47:33.673Z",
    "creditProductType": "string",
    "currency": {
      "alphabeticCode": "string",
      "createdAt": "string",
      "description": "string",
      "id": 0,
      "uptadedAt": "string"
    },
    "description": "string",
    "descriptionType": "string",
    "entity_id": "string",
    "externalReference": {},
    "finalBalance": 0,
    "id": 0,
    "initialBalance": 0,
    "internalReference": "string",
    "liquidationID": "string",
    "numericReference": "string",
    "observation": "string",
    "posDate": "string",
    "productCode": "string",
    "responseCode": "string",
    "settleAmount": 0,
    "status": 0,
    "systemSource": "string",
    "systemTraceAuditNumber": "string",
    "targetEmail": "string",
    "targetID": "string",
    "targetIDCode": "string",
    "targetName": "string",
    "timestamp": "string",
    "transactionBundler": 0,
    "transactionID": "string",
    "transactionSubType": "string",
    "transactionType": "string",
    "type": 0,
    "uptadedAt": "2025-03-11T18:47:33.673Z"
  },
  "operations": [
    {
      "alphanumericReference": "string",
      "amount": 0,
      "cititransaction": "string",
      "country": "string",
      "createdAt": "2025-03-11T18:47:33.673Z",
      "creditProductType": "string",
      "currency": {
        "alphabeticCode": "string",
        "createdAt": "string",
        "description": "string",
        "id": 0,
        "uptadedAt": "string"
      },
      "description": "string",
      "descriptionType": "string",
      "entity_id": "string",
      "externalReference": {},
      "finalBalance": 0,
      "id": 0,
      "initialBalance": 0,
      "internalReference": "string",
      "liquidationID": "string",
      "numericReference": "string",
      "observation": "string",
      "posDate": "string",
      "productCode": "string",
      "responseCode": "string",
      "settleAmount": 0,
      "status": 0,
      "systemSource": "string",
      "systemTraceAuditNumber": "string",
      "targetEmail": "string",
      "targetID": "string",
      "targetIDCode": "string",
      "targetName": "string",
      "timestamp": "string",
      "transactionBundler": 0,
      "transactionID": "string",
      "transactionSubType": "string",
      "transactionType": "string",
      "type": 0,
      "uptadedAt": "2025-03-11T18:47:33.673Z"
    }
  ],
  "orderEntityResponse": {
    "alphanumericReference": "string",
    "amount": 0,
    "beneficiaryAccountNumber": "string",
    "beneficiaryAddress1": "string",
    "beneficiaryAddress2": "string",
    "beneficiaryCode": "string",
    "beneficiaryEmail": "string",
    "beneficiaryName": "string",
    "businessTransactionCode": "string",
    "concept": "string",
    "country": "string",
    "createdAt": "2025-03-11T18:47:33.673Z",
    "creditStatus": "string",
    "creditType": "string",
    "debitType": "string",
    "descriptionType": "string",
    "entity_id": "string",
    "finalBalance": 0,
    "id": 1,
    "initialBalance": 0,
    "numericReference": 123322,
    "paymentType": "string",
    "posDate": "string",
    "productCode": "string",
    "referenceClient": "PROVV0011712091",
    "referenceCreatedPayment": 811111112,
    "responseCode": "string",
    "settleAmount": 0,
    "sourceEntity": "string",
    "status": 0,
    "systemSource": "string",
    "systemTraceAuditNumber": "string",
    "targetEntity": "string",
    "timestamp": "string",
    "transactionID": "string",
    "transactionSubType": "string",
    "transactionType": "string",
    "uptadedAt": "2025-03-11T18:47:33.673Z",
    "virtualAccount": "string"
  },
  "success": false,
  "totalItems": 0,
  "totalPages": 0,
  "transactionBundler": "string",
  "type": "string"
}

```

This endpoint retrieves all kittens.

### HTTP Request

`POST http://sdbx-aldebaran.kashplataforma.com/aldbrn/internal/aw/login`

### Query Parameters

Parameter | Description
--------- | -----------
Authorization | Default value : Bearer token
IdEntity ( entidad previamente dada de alta) | Default value : com.example
page (Numero de pagina a consultar) | Default value : 0
size (Tamaño de registro que va tener cada pagina) | Default value : 25
status (Estatus de operación, ver catalogo de estatus) | Default value : 25
type (Tipo de operación, ver catalogo de operaciones) | Default value : 1


### Catalogo de operaciones

          |             |           | 
--------- | ----------- | --------- | -----------
1 | Envia SPEI | RETIRO | SPEI DE SALIDA
1 | Envia SPEI | RETIRO | SPEI DE SALIDA
2 | Operación devuelta o rechazada | DEPOSITO | DEVOLUCIÓN SPEI
3 | SPEI recibido desde otra entidad | DEPOSITO | SPEI DE ENTRADA
4 | En una cuenta a cuenta, es el retiro a la cuenta origen | RETIRO | RETIRO ENTRE CUENTAS
10 | Compra de recargas telefonica | RETIRO | RECARGAS
11 | Compra Pago Servicios | RETIRO | PAGO DE SERVICIOS
12 | Retiro en ATM de la Red MasterCard | RETIRO | RETIRO EN ATM
13 | Compra  tarjeta presente/No presente  de la Red Mastercard | RETIRO | CONSUMO CON TARJETA
14 | Transacción por web service (Uso interno) | RETIRO/DEPOSITO | WebService (uso interno)
15 | Transacción por archivo batch (Uso interno) | RETIRO/DEPOSITO | Batch (uso interno)
16 | Retiro Corresponsal CITI (7Eleven, f.Gua, Citi, etc) | RETIRO | RETIRO EN CORRESPONSAL
17 | Retiro Corresponsal de la RED  (Came, TeCreemos, Comercios Onsigna) | RETIRO | RETIRO EN MI RED KASH
18 | Deposito Corresponsal de la  RED  (Came, TeCreemos, Comercios Onsigna) | DEPOSITO | DEPOSITO EN MI RED KASH
19 | Crear referencia- retiro sucursal | RETIRO | ORDEN DE PAGO
20 | Retiro de dinero con referencia en corresponsal  RED  (Came, TeCreemos, Comercios Onsigna) | RETIRO | RETIRO EN MI RED KASH
21 | Retiro de dinero con referencia en corresponsal CITI (7Eleven, f.Gua, Citi, etc) | RETIRO | RETIRO EN CORRESPONSAL
22 | Bolsas de Adquirencia | DEPOSITO | VENTA VISA
23 | Bolsas de Adquirencia | DEPOSITO | Venta Amex
24 | Bolsas de Adquirencia | DEPOSITO | Venta SPEI Referenciado
25 | Bolsas de Adquirencia | DEPOSITO | Devolucion Adqui
26 | Bolsas de Adquirencia | DEPOSITO | Cancelación Adqui
27 | Bolsas de Adquirencia | DEPOSITO | Venta MC
28 | Depósito a cuenta, dentro de la red de corresponsales CITI (7Eleven, f.Gua, Citi, etc) | DEPOSITO | DEPÓSITO EN CORRESPONSAL
29 | Depósito a  cuenta dentro de la red de corresponsales de la  RED  (Came, TeCreemos, Comercios Onsigna) | DEPOSITO | DEPÓSITO ENTRE CUENTAS
57 | Bolsas de Adquirencia | DEPOSITO | Venta Internacional
104 | Deposito en Efectivo | DEPOSITO | DEPÓSITO EN EFECTIVO
105 | Pago Referenciado | DEPOSITO | PAGO REFERENCIADO
106 | Traspaso Referenciado | DEPOSITO | TRASPASO REFERENCIADO
107 | Pago Recibido de Convenio | DEPOSITO | PAGO RECIBIDO
108 | Transferencia entre cuentas Citi | DEPOSITO | TRANSFERENCIA ENTRE CUENTAS CITI
109 | Deposito Mixto | DEPOSITO | DEPÓSITO MIXTO
110 | Deposito cheques | DEPOSITO | DEPOSITO CHEQUE
10007 | Liquidación Compra Individual |  | Liquidación Compra Individual
10008 | Liquidación Compras |  |  LIQUIDACIÓN TOTAL



# API CardServices

## Inicia

Valida las credenciales para acceder en la app wallet, permite o deniega el acceso. Una vez que los accesos sean correctos, dicho servicio devuelve los saldos  asignados, así como el estatus, información y la tarjeta asociada a la cuenta. 


```java
// JAVA - Unirest
```

```php
// PHP - cURL
```

```ruby
# RUBY - Net::HTTP


```

```python
# PYTHON - http.client


```

```shell
# SHELL - httpie


```


> El codigo anterior devuelve un JSON estructurado así:

```json

```

This endpoint retrieves all kittens.

### HTTP Request

`POST http://sdbx-aldebaran.kashplataforma.com/aldbrn/internal/aw/login`

### Query Parameters

Parameter | Description
--------- | -----------
user | Usuario
mail | Correo electronico
password | Clave asignada 

