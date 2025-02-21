---
title: API Kashpay

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - java
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

## Crear orden

Este servicio ejecuta varios tipos de operaciones de Remesas. Transferir fondos (también conocido como SPEI), ingreso y retiro de efectivo, pago Swift, Mastercard y Visa.
El envío de dinero nacional se realiza a través del operativo "1 - Transferencia Interbancaria SPEI", se puede visualizar en la pestaña Modelo.

```java
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-centauri.kashplataforma.com/OKPay/createOrder")
  .header("Authorization", "Basic YWRtaW46c2VjcmV0")
  .header("Content-Type", "application/json")
  .body("{\n  \"alphanumericReference\": \"PROVV0011712091\",\n  \"amount\": 250,\n  \"beneficiaryAcount\": 87459854,\n  \"beneficiaryAcountSPEI\": 87459854,\n  \"beneficiaryAddress1\": \"Vicente G 132 Mz5 Lt14\",\n  \"beneficiaryAddress2\": \"Vicente G 132 Mz5 Lt14\",\n  \"beneficiaryCity\": \"CDMX\",\n  \"beneficiaryName\": \"Florentino Eter\",\n  \"beneficiaryTypeAcount\": \"string\",\n  \"codeInstituteBank\": \"002\",\n  \"concept\": \"Deposito Maria\",\n  \"currency\": 484,\n  \"dataAccreditationBeneficiary\": 99,\n  \"dateTransaction\": \"030421\",\n  \"description\": \"prueba\",\n  \"email\": \"testrest@gmail.com\",\n  \"idBank\": 4177,\n  \"idEntity\": 4177,\n  \"numericReference\": 43223123,\n  \"observation\": \"test@gmail.com\",\n  \"orderingAccount\": 111,\n  \"orderingTypeAcount\": \"string\",\n  \"postalCode\": 57800,\n  \"referenceCreatedPayment\": 811111112,\n  \"rfc\": \"ROPL951201091\",\n  \"typeTransaction\": 1\n}\n")
  .asString();
```

```php
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

## Agregar Entidad

```java
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```php
{
  "bussinesName": "Test blumon 12",
  "bussinesNameShort": "SUC",
  "contextFatherID": "com.sub.blumonpay",
  "userRequest": {   
    "email": "useremail@gmail.com",   
    "telephoneNumber": "565311111",
    "user": "72663-7266-8j71-76112" 
  }
}
```

> El codigo anterior devuelve un JSON estructurado así:

```json

```

### HTTP Request

`POST http://sdbx-sirio.kashplataforma.com/EntitiesServices/addEntity`

### Query Parameters

Parameter | Description
--------- | -----------
bussinesName | Nombre de la entidad
bussinesNameShort | Nombre corto de la entidad
contextFatherID | ID de la entidad
email | Correo electronico 
telephoneNumber | Telefono
user | Usuario


# API Emision

## Iniciar sesion

Valida las credenciales para acceder en la app wallet, permite o deniega el acceso. Una vez que los accesos sean correctos, dicho servicio devuelve los saldos  asignados, así como el estatus, información y la tarjeta asociada a la cuenta. 


```java
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("http://sdbx-aldebaran.kashplataforma.com/aldbrn/internal/aw/registerOnboard ")
  .header("Authorization", "Basic YWRtaW46c2VjcmV0")
  .header("Content-Type", "application/json")
  .body("\"loginRequest\": { \n   \"authentication\": { \n    \"user\": \"test@gmail.com\", \n    \"mail\": \"test@gmail.com\", \n    \"password\": \"**********\" \n   }, \n   \"latitude\": \"19.6735912\", \n   \"longitude\": \"-99.0711819\", \n   \"dateTransaction\": \"20230113\", \n   \"hourTransaction\": \"134209\", \n }, \n \"device\": { \n   \"os\": \"Android\", \n   \"systemOperativeName\": \"Version Desconocida\", \n   \"systemOperativeVersion\": \"15\", \n   \"manufacturer\": \"Google\", \n   \"model\": \"Pixel 7 Pro\", \n   \"latitude\": \"19.6735912\", \n   \"longitude\": \"-99.0711819\" \n }, \n \"appInfo\": { \n   \"nameApp\": \"eVolv\", \n   \"versionApp\": \"21.0.0\", \n   \"enviroment\": \"SANDBOX\", \n   \"versionConnector\": \"2.0.0\" \n } ")
  .asString();

```

```php
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
 


