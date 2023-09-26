# Отчет по тестированию в Postman:

## Раздел Activities:

### 1. Activities: получение списка активностей (GET /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с массивом данных (Activities от 1 до 30-ти) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 56833729-9d60-487d-84e5-dbee248b1a82
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Mon, 26 Jun 2023 17:21:16 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
[
    {
        "id": 1,
        "title": "Activity 1",
        "dueDate": "2023-06-26T18:21:16.4571787+00:00",
        "completed": false
    },
```
### 2. Activities: добавление новой активности (POST /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 31) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: b95dfb1f-9dc6-4bf5-bc7f-05e98da649e2
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 97
```
- **Тело запроса:**
```
{
  "id": 31,
  "title": "string",
  "dueDate": "2023-06-26T13:29:02.515Z",
  "completed": true
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Mon, 26 Jun 2023 18:18:33 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 31,
    "title": "string",
    "dueDate": "2023-06-26T13:29:02.515Z",
    "completed": true
}
```
### 3. Activities: добавление уже существующей активности (POST /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 409 Conflict. Тело ответа в JSON-формате c описанием ошибки и указанием конфликта отправленного значения с текущим состоянием ресурса возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 170cf8d5-b624-45a9-8178-db3925ad16c5
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 96
```
- **Тело запроса:** 
```
{
  "id": 1,
  "title": "string",
  "dueDate": "2023-06-26T13:29:02.515Z",
  "completed": true
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Tue, 27 Jun 2023 17:14:29 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
Response Body
```
- **Тело ответа:** 
```
{
    "id": 1,
    "title": "string",
    "dueDate": "2023-06-26T13:29:02.515Z",
    "completed": true
}
```
### 4. Activities: добавление активности запросом с невалидными данными (POST /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Указана проблема валидации в поле id. 

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: b95dfb1f-9dc6-4bf5-bc7f-05e98da649e2
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 97
```
- **Тело запроса:**
```
{
  "id": 2147483648,
  "title": "string",
  "dueDate": "2023-07-26T08:49:23.841Z",
  "completed": true
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Mon, 26 Jun 2023 18:18:33 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-a4b37f335c624d49a121f2c00885ef96-b87b872e5ed3af4b-00",
    "errors": {
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 18."
        ]
    }
}
```
### 5. Activities: добавление активности запросом с некорректным JSON (POST /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Указана ошибка в синтаксисе JSON, не удалось преобразовать значение JSON.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: b95dfb1f-9dc6-4bf5-bc7f-05e98da649e2
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 97
```
- **Тело запроса:**
```
  "id": 0,
  "title": "string",
  "dueDate": "2023-06-26T13:29:02.515Z",
  "completed": true
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Mon, 26 Jun 2023 18:18:33 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-1dadb448e79f1047a6d4a360fd280837-5636a977aaadf74b-00",
    "errors": {
        "$": [
            "The JSON value could not be converted to FakeRestAPI.Models.Activity. Path: $ | LineNumber: 1 | BytePositionInLine: 6."
        ]
    }
}
```
### 6. Activities: добавление активности запросом с пустым значением id (POST /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: da02485e-9e21-46bd-98b1-188ab4e68d00
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 95
```
- **Тело запроса:**
```
  "id": ,
  "title": "string",
  "dueDate": "2023-06-26T13:29:02.515Z",
  "completed": true
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Thu, 29 Jun 2023 18:16:42 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-6d37feda306a3d41bcce06b60288aea9-276226853b031f45-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```
### 7. Activities: добавление активности запросом с пустым телом (POST /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 75d9eb48-4d68-46d0-826c-ce55f23838f5
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 0
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 30 Jun 2023 11:46:55 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-b6c7b2b90137e6439133902abdcdd9d6-ed4cf3d69e86354f-00",
    "errors": {
        "": [
            "A non-empty request body is required."
        ]
    }
}
```
### 8. Activities: добавление активности запросом с пустым JSON-объектом (POST /api/v1/Activities)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 7315094c-1d10-43eb-930b-189b2b46c932
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 2
```
- **Тело запроса:** { }
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 30 Jun 2023 17:30:43 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 0,
    "title": null,
    "dueDate": "0001-01-01T00:00:00",
    "completed": false
}
```
### 9. Activities: получение данных активности (GET /api/v1/Activities/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с данными (Activity 1) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 9a55ca8d-41dd-46d3-811e-c47d929ccb74
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Tue, 27 Jun 2023 08:57:39 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 1,
    "title": "Activity 1",
    "dueDate": "2023-06-27T09:57:39.459551+00:00",
    "completed": false
}
```
### 10. Activities: получение данных несуществующей активности (GET /api/v1/Activities/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_non-existent_Activity}}
- **Ожидаемый результат:** HTTP статус: 404 Not Found. Тело ответа в JSON-формате c описанием ошибки (запрашиваемые данные не найдены) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 0a1e79e1-4316-4a1f-910a-e337071e7093
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8; v=1.0
Date: Tue, 27 Jun 2023 09:23:15 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-cf762a493abbe7428014b8d2b0d17a72-ab4398d98227564f-00"
}
```
### 11. Activities: получение данных активности запросом с невалидными данными(GET /api/v1/Activities/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_invalid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 5b5ed4d2-0051-4dd7-a9a5-547ffe7d6391
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Tue, 27 Jun 2023 09:42:24 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-c5358a5f596be54fbddac8300819ed76-e3c205c656175040-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ]
    }
}
```
### 12. Activities: обновление данных активности (PUT /api/v1/Activities/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с обновленными данными ("title": "string1") возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 5adabe2a-06c9-4512-9603-68aec5949b62
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 97
```
- **Тело запроса:** 
```
{
  "id": 1,
  "title": "string1",
  "dueDate": "2023-06-30T06:35:16.199Z",
  "completed": true
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 30 Jun 2023 06:56:52 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 1,
    "title": "string1",
    "dueDate": "2023-06-30T06:35:16.199Z",
    "completed": true
}
```
### 13. Activities: добавление активности (PUT /api/v1/Activities/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_non-existent_Activity}}
- **Ожидаемый результат:** HTTP статус: 201 OK. Тело ответа в JSON-формате с созданными данными ("id": 31) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 5adabe2a-06c9-4512-9603-68aec5949b62
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 97
```
- **Тело запроса:** 
```
{
  "id": 31,
  "title": "string",
  "dueDate": "2023-06-30T06:35:16.199Z",
  "completed": true
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 30 Jun 2023 06:56:52 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 31,
    "title": "string",
    "dueDate": "2023-06-30T06:35:16.199Z",
    "completed": true
}
```

### 14. Activities: обновление/добавление активности запросом с невалидными данными(PUT /api/v1/Activities/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_invalid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и проблемы валидации в поле id возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 9d716b94-53e0-4af1-9abf-ca2443320c41
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 105
```
- **Тело запроса:** 
```
{
  "id": 2147483648,
  "title": "string",
  "dueDate": "2023-06-30T06:35:16.199Z",
  "completed": true
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 30 Jun 2023 08:32:29 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-b507fa778735ea47a6ee1e8802bd220a-887e7e6559bbf240-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ],
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 18."
        ]
    }
}
```
### 15. Activities: обновление активности запросом с некорректным JSON (PUT /api/v1/Activities/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 OK. Тело ответа в JSON-формате c описанием ошибки (Bad Request) и указанием ошибки в синтаксисе JSON (не удалось преобразовать значение JSON) возвращается от сервера. 

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 9d716b94-53e0-4af1-9abf-ca2443320c41
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 105
```
- **Тело запроса:** 
```
"id": 1,
  "title": "string",
  "dueDate": "2023-06-26T13:29:02.515Z",
  "completed": true
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 30 Jun 2023 08:32:29 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-6a5a5bd43898b64f8268310c15090f1a-17000a9dc7ef3542-00",
    "errors": {
        "$": [
            "The JSON value could not be converted to FakeRestAPI.Models.Activity. Path: $ | LineNumber: 1 | BytePositionInLine: 6."
        ]
    }
}
```
### 16. Activities: обновление активности запросом с пустым значением id в теле запроса (PUT /api/v1/Activities/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 OK. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 6f6fbe6d-cdc6-40c2-b463-3eaac34a1513
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 98
```
- **Тело запроса:** 
```
{
  "id": ,
  "title": "string",
  "dueDate": "2023-06-30T10:23:43.892Z",
  "completed": true
}
  
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 30 Jun 2023 10:30:49 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-032a55fef1b2074f8916415f2494fa5b-6ba14883ef046c46-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```
### 17. Activities: обновление активности запросом с пустым телом (PUT /api/v1/Activities/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 75d9eb48-4d68-46d0-826c-ce55f23838f5
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 0
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 30 Jun 2023 11:52:34 GMT
Server: Kestrel
Transfer-Encoding: chun
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-aac677f8f4c8ed4b844778a4880735b9-1fc81f4c305a194c-00",
    "errors": {
        "": [
            "A non-empty request body is required."
        ]
    }
}
```

### 18. Activities: обновление активности запросом с пустым JSON-объектом (PUT /api/v1/Activities/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 3cfc7049-4453-4df4-badd-5cf0a5c387d1
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 2
```
- **Тело запроса:** { }
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 30 Jun 2023 17:53:42 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 0,
    "title": null,
    "dueDate": "0001-01-01T00:00:00",
    "completed": false
}
```
### 19. Activities: удаление активности (DELETE /api/v1/Activities/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Activities/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 204 No Content. Активность удалена.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: b578f553-e952-496a-9983-cfdc748d3b86
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Length: 0
Date: Fri, 30 Jun 2023 12:58:17 GMT
Server: Kestrel
api-supported-versions: 1.0
```
- **Тело ответа:** -

## Раздел Authors:

### 20. Authors: получение списка авторов (GET /api/v1/Authors)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с массивом данных (Authors от 1 до ~620) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: d858eeda-1b17-4bfa-96f5-8ed75658bcca
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 01 Jul 2023 10:00:41 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
[
    {
        "id": 1,
        "idBook": 1,
        "firstName": "First Name 1",
        "lastName": "Last Name 1"
    },
    {
        "id": 2,
        "idBook": 1,
        "firstName": "First Name 2",
        "lastName": "Last Name 2"
    },
```
### 21. Authors: добавление нового автора (POST /api/v1/Authors:)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors:
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 621) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 1c2908b7-5afe-4449-8f65-8692993049ba
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 79
```
- **Тело запроса:** 
```
{
  "id": {{id_non-existent_Author}},
  "idBook": 0,
  "firstName": "string",
  "lastName": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 07:12:45 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 621,
    "idBook": 0,
    "firstName": "string",
    "lastName": "string"
}
```
### 22. Authors: добавление уже существующего автора (POST /api/v1/Authors)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors
- **Ожидаемый результат:** HTTP статус: 409 Conflict. Тело ответа в JSON-формате c описанием ошибки и указанием конфликта отправленного значения с текущим состоянием ресурса возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 59a69ae9-4343-4b32-9d42-6910c9acb0ce
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 98
```
- **Тело запроса:** 
```
{
    "id": 1,
    "idBook": 1,
    "firstName": "First Name 1",
    "lastName": "Last Name 1"
  }
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 07:35:04 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 1,
    "idBook": 1,
    "firstName": "First Name 1",
    "lastName": "Last Name 1"
  }
```
### 23. Authors: добавление автора запросом с невалидными данными (POST /api/v1/Authors)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Указана проблема валидации в поле id. 

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: b48272c0-3082-436d-b716-231db0e31600
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 107
```
- **Тело запроса:** 
```
{
    "id": {{id_invalid}},
    "idBook": 1,
    "firstName": "First Name 1",
    "lastName": "Last Name 1"
  }
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 08:10:55 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-2b6142fa19054943bf2cc3c686d05203-1d4ef8bf14495947-00",
    "errors": {
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 20."
        ]
    }
}
```
### 24. Authors: добавление автора запросом с некорректным JSON (POST /api/v1/Authors)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Указана ошибка в синтаксисе JSON, не удалось преобразовать значение JSON.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 0da8c9b1-2ad3-4b8c-8f5f-52c981f51e35
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 77
```
- **Тело запроса:** 
```
"id": 1,
"idBook": 1,
"firstName": "First Name 1",
"lastName": "Last Name 1"
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 08:16:45 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-61c1b6f0ee9c054c918c17606920b3d6-e7e6663b68bdcc48-00",
    "errors": {
        "$": [
            "The JSON value could not be converted to FakeRestAPI.Models.Author. Path: $ | LineNumber: 1 | BytePositionInLine: 4."
        ]
    }
}
```
### 25. Authors: добавление автора запросом с пустым значением id (POST /api/v1/Authors)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 67e5b4e5-e249-4dca-8fa5-6533733b3680
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 76
```
- **Тело запроса:** 
```
{
  "id": ,
  "idBook": 0,
  "firstName": "string",
  "lastName": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 08:30:21 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-8af08b41b0c35b45ad74960d997ada99-c4f8cf150de7ae4a-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```
### 26. Authors: добавление автора запросом с пустым телом (POST /api/v1/Authors)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: f2608174-0fdb-478f-b61b-43ec1fe23bed
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 0
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 09:50:27 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-13e0746c5e9d1a46ba0717864e5bf2b9-eec4a6da381b6048-00",
    "errors": {
        "": [
            "A non-empty request body is required."
        ]
    }
}
```
### 27. Authors: добавление автора запросом с пустым JSON-объектом (POST /api/v1/Authors)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: f4e7067c-543a-4418-b7ee-4ac393a19789
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 2
```
- **Тело запроса:** { }

- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 11:07:32 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 0,
    "idBook": 0,
    "firstName": null,
    "lastName": null
}
```
### 28. Authors: получение данных авторов конкретной книги (GET /api/v1/Authors/authors/books/{существующий idBook})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/authors/books/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с массивом данных авторов книги (idBook 1) возвращается от сервера.

- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 46a6453a-8eb8-4682-ac1d-5ef5220d293d
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 12:06:40 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
[
    {
        "id": 1,
        "idBook": 1,
        "firstName": "First Name 1",
        "lastName": "Last Name 1"
    },
    {
        "id": 2,
        "idBook": 1,
        "firstName": "First Name 2",
        "lastName": "Last Name 2"
    },
```
### 29. Authors: получение данных авторов несуществующей книги (GET /api/v1/Authors/authors/books/{несуществующий idBook})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/authors/books/{{id_non-existent_Book}} 
- **Ожидаемый результат:** HTTP статус: 404 Not Found. Тело ответа в JSON-формате c описанием ошибки (запрашиваемые данные не найдены) возвращается от сервера.

- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: f10d41ac-9256-41da-97b2-b314c6f7d947
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 12:17:44 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** []

### 30. Authors: получение данных авторов книги запросом с невалидными данными(GET /api/v1/Authors/authors/books/{невалидный idBook})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/authors/books/{{id_invalid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и проблемы валидации в поле id возвращается от сервера. 

- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 1b89ed98-77c4-4909-8ce1-a641be208bd7
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 13:35:01 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-b5319e60a6367b4eb117ab6ac8be5fb7-b3b092b8a5990c45-00",
    "errors": {
        "idBook": [
            "The value '2147483648' is not valid."
        ]
    }
}
```
### 31. Authors: получение данных автора (GET /api/v1/Authors/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с данными автора (id 1) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 83eb1a40-9204-458c-bd0e-d0c7db9f5304
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 13:48:32 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 1,
    "idBook": 1,
    "firstName": "First Name 1",
    "lastName": "Last Name 1"
}
```
### 32. Authors: получение данных несуществующего автора (GET /api/v1/Authors/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_non-existent_Author}}
- **Ожидаемый результат:** HTTP статус: 404 Not Found. Тело ответа в JSON-формате c описанием ошибки (запрашиваемые данные не найдены) возвращается от сервера.

- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: cdbfaa62-2367-4b10-ba36-2d996aed6dee
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 13:55:34 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-6e7afbf60fd83b46ba111c9435be6470-6a3be80f01a90241-00"
}
```
### 33. Authors: получение данных автора запросом с невалидными данными (GET /api/v1/Authors/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_invalid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и проблемы валидации в поле id возвращается от сервера. 

- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: fbc88355-18f8-4bdd-823d-e85d3f01a287
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 14:03:45 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-53033a53bfba524488fff510b4af008a-95ccb037bb0a0c41-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ]
    }
}
```
### 34. Authors: обновление данных автора (PUT /api/v1/Authors/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с обновленными данными ("firstName": "1 First Name") возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 16fbbd32-c854-4833-ae16-d82f72ee7551
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 98
```
- **Тело запроса:** 
```
{
    "id": 1,
    "idBook": 1,
    "firstName": "1 First Name",
    "lastName": "Last Name 1"
  }
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 15:16:31 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 1,
    "idBook": 1,
    "firstName": "1 First Name",
    "lastName": "Last Name 1"
}
```
### 35. Authors: добавление данных автора (PUT /api/v1/Authors/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_non-existent_Author}}
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 621) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 3e741997-a17c-458d-9a3a-7145c1534026
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 79
```
- **Тело запроса:** 
```
{
  "id": {{id_non-existent_Author}},
  "idBook": 0,
  "firstName": "string",
  "lastName": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 16:56:05 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 621,
    "idBook": 0,
    "firstName": "string",
    "lastName": "string"
}
```
### 36. Authors: обновление/добавление данных автора запросом с невалидными данными(PUT /api/v1/Authors/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_invalid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и проблемы валидации в поле id возвращается от сервера. 

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 88f77a29-dffc-4ad8-91d5-2371c69b0b93
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 107
```
- **Тело запроса:** 
```
{
    "id": {{id_invalid}},
    "idBook": 1,
    "firstName": "First Name 1",
    "lastName": "Last Name 1"
  }
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 17:11:30 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-fa55f61e4c6ff24da77c1f53fca8d269-d17c13ee13e96d45-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ],
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 20."
        ]
    }
}
```
### 37. Authors: обновление данных автора запросом с некорректным JSON (PUT /api/v1/Authors/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Указана ошибка в синтаксисе JSON, не удалось преобразовать значение JSON.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 65eaddf6-9c82-4111-93cf-874fab1766dc
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 77
```
- **Тело запроса:** 
```
"id": 1,
"idBook": 1,
"firstName": "First Name 1",
"lastName": "Last Name 1"
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 17:21:33 GMT
Server: Kestrel
Transfer-Encoding: chunked
Response Body
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-3eed94b1ecbed941b0fc85327b8a0ba9-abd61d5b2649234f-00",
    "errors": {
        "$": [
            "The JSON value could not be converted to FakeRestAPI.Models.Author. Path: $ | LineNumber: 1 | BytePositionInLine: 4."
        ]
    }
}
```
### 38. Authors: обновление данных автора запросом с пустым значением id в теле запроса (PUT /api/v1/Authors/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 OK. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера.

- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: f17d277e-660a-4b0b-b20c-ca212d6bdd2e
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 76
```
- **Тело запроса:** 
```
{
  "id": ,
  "idBook": 0,
  "firstName": "string",
  "lastName": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 17:33:28 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-821e466b6b91fc47a42c7fc520906375-8047fe664bac0049-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```
### 39. Authors: обновление данных автора запросом с пустым телом (PUT /api/v1/Authors/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: ea355441-b851-4d33-b03a-75ff6611f1ee
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 02 Jul 2023 17:41:57 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:**
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-c3bb18851cd4ce468e86f82abfdadc1b-23dc4f44a9b1ab4f-00",
    "errors": {
        "": [
            "A non-empty request body is required."
        ]
    }
}
```
### 40. Authors: обновление данных автора запросом с пустым JSON-объектом (PUT /api/v1/Authors/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: e605bb5d-98c4-48ba-95f9-9f0c89d81fdc
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 2
```
- **Тело запроса:** { }
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 02 Jul 2023 17:48:56 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:**
```
{
    "id": 0,
    "idBook": 0,
    "firstName": null,
    "lastName": null
}
```
### 41. Authors: удаление автора (DELETE /api/v1/Authors/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Authors/{{id_valid}}
- **Ожидаемый результат:** HTTP статус: 204 No Content. Активность удалена.

- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 9e4d8f2a-3204-49b7-9195-aef083522285
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Length: 0
Date: Sun, 02 Jul 2023 17:56:18 GMT
Server: Kestrel
api-supported-versions: 1.0
```
- **Тело ответа:** -

## Раздел Books:

### 42. Books: получение списка книг (GET ​/api​/v1​/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с массивом данных (Books от 1 до 200-ста) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 14c12af5-ea73-406c-96de-562b44d74247
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 07 Jul 2023 00:55:03 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
[
    {
        "id": 1,
        "title": "Book 1",
        "description": "Lorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\n",
        "pageCount": 100,
        "excerpt": "Lorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\n",
        "publishDate": "2023-07-06T00:55:04.1463855+00:00"
    },
   .....
```

### 43. Books: добавление новой книги (POST ​/api​/v1​/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 201) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: bba6781a-fe13-469e-a5dd-e3b51cad7514
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alivee
```
- **Тело запроса:** 
'''
{
  "id": 201,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-05T02:14:57.450Z"
}
'''
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 07 Jul 2023 00:59:22 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 201,
    "title": "string",
    "description": "string",
    "pageCount": 0,
    "excerpt": "string",
    "publishDate": "2023-07-05T02:14:57.45Z"
}
```

### 44. Books: добавление уже существующей книги (POST /api/v1/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 409 Conflict. Тело ответа в JSON-формате c описанием ошибки и указанием конфликта отправленного значения с текущим состоянием ресурса возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 540d4e91-6fc8-4fb2-85f8-35ace0e67135
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
'''
{
  "id": 1,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-05T02:14:57.450Z"
}
'''
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 07 Jul 2023 22:20:31 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 1,
    "title": "string",
    "description": "string",
    "pageCount": 0,
    "excerpt": "string",
    "publishDate": "2023-07-05T02:14:57.45Z"
}
```

### 45. Books: добавление книги запросом с невалидными данными (POST /api/v1/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: a24d9ada-994e-48f9-b590-8e3c48995735
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
'''
{
  "id": {{invalid_id}},
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-05T02:14:57.450Z"
}
'''
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 07 Jul 2023 22:24:02 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-36eab8b592f8e240a8767d63a9187abb-7eec3bc2840d7340-00",
    "errors": {
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 18."
        ]
    }
}
```

### 46. Books: добавление книги запросом с невалидными данными (POST /api/v1/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (Bad Request) и указанием ошибки в синтаксисе JSON (не удалось преобразовать значение JSON) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 4d4ab58e-3cc8-4a3e-8530-a4e84f3be68b
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
'''
id": 1,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-05T02:14:57.450Z"
'''
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 07 Jul 2023 22:26:00 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-d74a991592f0be4d88275f8aaf874b7b-c1752e376d5bc844-00",
    "errors": {
        "$": [
            "'i' is an invalid start of a value. Path: $ | LineNumber: 0 | BytePositionInLine: 0."
        ]
    }
}
```

### 47. Books: добавление книги запросом с пустым значением id (POST /api/v1/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: fb53f26d-667f-4aeb-b79e-970b52261fac
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
'''
{
  "id": ,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-05T02:14:57.450Z"
}
'''
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 07 Jul 2023 22:28:50 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-fd1de96d4ea6564c9f0ea7aec4944784-360d22679420a14e-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```

### 48. Books: добавление книги запросом с пустым телом (POST /api/v1/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: d23fa9aa-821d-431a-adaa-2b427c8510ac
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** пустое тело запроса
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 07 Jul 2023 23:01:43 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-c4783bd9c352e14a94a5ca252c2f5702-8568f1b1238cce4f-00",
    "errors": {
        "$": [
            "The input does not contain any JSON tokens. Expected the input to start with a valid JSON token, when isFinalBlock is true. Path: $ | LineNumber: 1 | BytePositionInLine: 0."
        ]
    }
}
```

### 49. Books: добавление книги запросом с пустым JSON-объектом (POST /api/v1/Books)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 019776ca-c7dc-483a-9234-c0f1931fc7b2
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** { }
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 07 Jul 2023 23:04:49 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 0,
    "title": null,
    "description": null,
    "pageCount": 0,
    "excerpt": null,
    "publishDate": "0001-01-01T00:00:00"
}
```

### 50. Books: получение данных книги (GET ​/api​/v1​/Books​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/1
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с данными (Book 1) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 8f07a48c-76f5-47ef-a4da-f7757ed7472d
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 07 Jul 2023 23:21:05 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 1,
    "title": "Book 1",
    "description": "Lorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\n",
    "pageCount": 100,
    "excerpt": "Lorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\nLorem lorem lorem. Lorem lorem lorem. Lorem lorem lorem.\n",
    "publishDate": "2023-07-06T23:21:05.6063484+00:00"
}
```

### 51. Books: получение данных несуществующей книги (GET ​/api​/v1​/Books​/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/201
- **Ожидаемый результат:** HTTP статус: 404 Not Found. Тело ответа в JSON-формате c описанием ошибки (запрашиваемые данные не найдены) возвращается от сервера. 
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 11b1b367-ac3e-4f61-98d8-ca5382fd7064
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8; v=1.0
Date: Fri, 07 Jul 2023 23:30:17 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-d9e1a89f02db60499d32b72011f2269e-ca398c4ba4732745-00"
}
```

### 52.Books: получение данных книги запросом с невалидными данными(GET /api/v1/Books/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/2147483648
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера. 
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 999c1bfa-f9b3-4d66-bb2c-894fc9284de3
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Fri, 07 Jul 2023 23:38:01 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-30089b3dea020942b5b776dc60e9dd33-2b5322f342aa424a-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ]
    }
}
```

### 53. Books: обновление данных книги (PUT ​/api​/v1​/Books​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/1
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с обновленными данными ("title": "string1") возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: e4984fe7-5c16-4f1f-8d1a-1b8ff9353a72
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 1,
  "title": "string 1",
  "description": "string 1",
  "pageCount": 0,
  "excerpt": "string 1",
  "publishDate": "2023-07-07T23:41:35.300Z"
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Fri, 07 Jul 2023 23:45:28 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 1,
    "title": "string 1",
    "description": "string 1",
    "pageCount": 0,
    "excerpt": "string 1",
    "publishDate": "2023-07-07T23:41:35.3Z"
}
```

### 54. Books: добавление данных книги (PUT /api/v1/Books/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/201 
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 201) возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 73693a30-06c2-4553-88e4-23a3a62333c7
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 201,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-08T01:54:34.621Z"
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:59:03 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 201,
    "title": "string",
    "description": "string",
    "pageCount": 0,
    "excerpt": "string",
    "publishDate": "2023-07-08T01:54:34.621Z"
}
```

### 55. Books: обновление/добавление книги запросом с невалидными данными(PUT /api/v1/Books/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/2147483648 
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: bc6efd20-decf-4a24-a3cb-af0003fd3089
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 2147483648,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-08T01:54:34.621Z"
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 02:01:25 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-470e073a264ba342a19f65b39a15155d-fc722136c9d4c94a-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ],
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 18."
        ]
    }
}
```

### 56. Books: обновление книги запросом с некорректным JSON (PUT /api/v1/Books/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/1  
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (Bad Request) и указанием ошибки в синтаксисе JSON (не удалось преобразовать значение JSON) возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 18fd1c64-41d2-49aa-8810-79f41ff70804
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
  {
    "id": 1,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-08T02:02:30.973Z"
  }
```
- **Заголовки ответа:**
```
content-type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 02:03:22 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-c31e459ad2c94a49b4bd8f7c5fd796e7-e23fb02c52d7c44c-00",
    "errors": {
        "$": [
            "The JSON value could not be converted to FakeRestAPI.Models.Book. Path: $ | LineNumber: 0 | BytePositionInLine: 4."
        ]
    }
}
```
### 57. Books: обновление книги запросом с пустым значением id в теле запроса (PUT /api/v1/Books/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/1  
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 3c34bd4b-3233-40b2-820a-ec1930cca0d6
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
  {
  "id": ,
  "title": "string",
  "description": "string",
  "pageCount": 0,
  "excerpt": "string",
  "publishDate": "2023-07-08T02:02:30.973Z"
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 02:04:33 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-ef30027b8f211d409a81f651bf7b3164-18fc804ea4b4e24a-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```

### 58. Books: обновление книги запросом с пустым телом (PUT /api/v1/Books/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/1  
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: fa60c9e1-45b8-47da-b00f-695a0a2f913c
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 00:17:31 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-844aea273898af46a69e3e95b8d85c0c-99ca0dcc6cc95541-00",
    "errors": {
        "$": [
            "The input does not contain any JSON tokens. Expected the input to start with a valid JSON token, when isFinalBlock is true. Path: $ | LineNumber: 0 | BytePositionInLine: 1."
        ]
    }
}
```

### 59. Books: обновление книги запросом с пустым JSON-объектом (PUT /api/v1/Books/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/1  
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 46a2c2ba-2ca3-4d5e-af3c-1920175503af
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
    
} 
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 00:20:53 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 0,
    "title": null,
    "description": null,
    "pageCount": 0,
    "excerpt": null,
    "publishDate": "0001-01-01T00:00:00"
}
```

### 60. Books: удаление книги (DELETE /api/v1/Books/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Books/1  
- **Ожидаемый результат:** HTTP статус: 204 No Content. Тело ответа в JSON-формате (с описанием состояния объекта — удален) возвращается от сервера. 
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: e220594b-f025-4450-be1e-4a8dec4fc3b5
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Length: 0
Date: Sat, 08 Jul 2023 00:33:03 GMT
Server: Kestrel
api-supported-versions: 1.0
```
- **Тело ответа:** - 

## Раздел CoverPhotos:

### 61. CoverPhotos: получение списка фото на обложке (GET /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с массивом данных (Authors от 1 до ~200-ста) возвращается от сервера. 
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 031fc6e3-f6c0-4992-bfa2-aafc1908420a
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 00:52:56 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
   [ 
    {
        "id": 1,
        "idBook": 1,
        "url": "https://placeholdit.imgix.net/~text?txtsize=33&txt=Book 1&w=250&h=350"
    },
...]
```

### 62. CoverPhotos: добавление нового фото на обложке (POST /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 201) возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 202df8d9-680e-435f-a1c9-0ec3f4ba6e38
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 201,
  "idBook": 0,
  "url": "string"
} 
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:01:19 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
  "id": 201,
  "idBook": 0,
  "url": "string"
}
```
### 63. CoverPhotos: добавление уже существующее фото на обложке (POST /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 409 Conflict. Тело ответа в JSON-формате c описанием ошибки и указанием конфликта отправленного значения с текущим состоянием ресурса возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 6c8c7527-7e20-4d7c-bcf6-e56d76ce5827
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 1,
  "idBook": 1,
  "url": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:05:26 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
  {
    "id": 1,
    "idBook": 1,
    "url": "string"
}
```

### 64. CoverPhotos: добавление фото на обложке запросом с невалидными данными (POST /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 67614c1b-95b5-490f-babc-906bfa0bd4c3
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 2147483648,
  "idBook": 2147483648,
  "url": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 01:10:10 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-2563e3a5e3512b4087274cb94f1c8d62-4740d2af4b3bc344-00",
    "errors": {
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 18."
        ]
    }
}
```

### 65. CoverPhotos: добавление фото на обложке запросом с некорректным JSON (POST /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (Bad Request) и указанием ошибки в синтаксисе JSON (не удалось преобразовать значение JSON) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 89c0a096-84e2-460c-8cb2-a6be5d93d07f
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{ 
    "id": 1,
  "idBook": 1,
  "url": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 01:14:00 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-4d87011f722d7f4591243748ea16d92c-20e3b594a212a54c-00",
    "errors": {
        "$": [
            "The JSON value could not be converted to FakeRestAPI.Models.CoverPhoto. Path: $ | LineNumber: 0 | BytePositionInLine: 4."
        ]
    }
}
```

### 66. CoverPhotos: добавление фото на обложке запросом с пустым значением id (POST /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: c9c505cc-1c86-4e2e-8083-397d54716b4d
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": ,
  "idBook": 1,
  "url": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 01:17:01 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-63d3e6a63dd11640828a74043d7b41ca-d93c7b3815f1f74e-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```

### 67. CoverPhotos: добавление фото на обложке запросом с пустым телом (POST /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 070cf2e9-d815-4d55-953e-1ebdf147d47a
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 01:19:47 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-41ac1919c5966343829ab1db96331919-a6d22d63f16bb840-00",
    "errors": {
        "$": [
            "The input does not contain any JSON tokens. Expected the input to start with a valid JSON token, when isFinalBlock is true. Path: $ | LineNumber: 0 | BytePositionInLine: 1."
        ]
    }
}
```

### 68. CoverPhotos: добавление фото на обложке запросом с пустым JSON-объектом (POST /api/v1/CoverPhotos)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos 
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 738e4f2f-5cd2-4ec5-89ab-d0e8fb422a80
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:23:16 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 0,
    "idBook": 0,
    "url": null
}
```
### 69. CoverPhotos: получение данных фото на обложке конкретной книги (GET ​/api​/v1​/CoverPhotos​/books​/covers​/{существующий idBook})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/books/covers/1 
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с массивом данных авторов книги (idBook 1) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: a0a24be8-4647-4cb6-95cb-5efd491285a5
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:30:45 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
        "id": 1,
        "idBook": 1,
        "url": "https://placeholdit.imgix.net/~text?txtsize=33&txt=Book 1&w=250&h=350"
    }
```
### 70. CoverPhotos: получение данных фото на обложке несуществующей книги(GET ​/api​/v1​/CoverPhotos​/books​/covers​/{несуществующий idBook})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/books/covers/201 
- **Ожидаемый результат:** HTTP статус: 404 Not Found. Тело ответа в JSON-формате c описанием ошибки (запрашиваемые данные не найдены) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 06407e70-1b40-44b0-8a65-7f99a5e24101
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:34:42 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
   "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
  "title": "Not Found",
  "status": 404,
  "traceId": "00-47fa730285508340b38b55a89e006d6d-ab7bafce81896149-00"
} 
```
### 71. CoverPhotos: получение данных фото на обложке книги запросом с невалидными данными (GET ​/api​/v1​/CoverPhotos​/books​/covers​/{невалидный idBook})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/books/covers/2147483648
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 761e4df2-f8eb-4e26-a904-b75060213a94
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 01:38:25 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-579ad5bb4906fb4596a7c6ab749220d4-15a06b825047334f-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ]
    }
}
```
### 72. CoverPhotos: получение данных фото на обложке(GET ​/api​/v1​/CoverPhotos​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/1
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с данными фото на обложке (id 1) возвращается от сервера. 
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 3a02d33e-beb3-48d1-894a-136f82aa8320
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:43:17 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 1,
    "idBook": 1,
    "url": "https://placeholdit.imgix.net/~text?txtsize=33&txt=Book 1&w=250&h=350"
}
```
### 73. CoverPhotos: получение данных несуществующей фото на обложке (GET ​/api​/v1​/CoverPhotos​/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/201
- **Ожидаемый результат:** HTTP статус: 404 Not Found. Тело ответа в JSON-формате c описанием ошибки (запрашиваемые данные не найдены) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 56edd927-497a-4c5d-9711-9f5c7a9438f3
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:46:44 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-37bf7c57569d85449b2f0f92d3dd9239-ac9fcb1777a1b445-00"
}
```
### 74. CoverPhotos: получение данных фото на обложке запросом с невалидными данными (GET ​/api​/v1​/CoverPhotos​/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/2147483648
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: d1b48cae-a05c-4eac-8f96-47b2b741c6ef
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 01:49:13 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-e0b87fd28c41274fa3a55afbfbb3a710-2f82e42a550af244-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ]
    }
}
```
### 75. CoverPhotos: обновление данных фото на обложке (PUT ​/api​/v1​/CoverPhotos/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/1
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с обновленными данными ("idBook": "idBook": 1) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 9f656de4-88d8-48da-b331-f8ede4d20777
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 1,
  "idBook": 1,
  "url": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 02:09:37 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
  "id": 1,
  "idBook": 1,
  "url": "string"
}
```
### 76. CoverPhotos: добавление данных фото на обложке (PUT ​/api​/v1​/CoverPhotos​/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/201
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 201) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 8a16608b-c3be-4959-a978-8aabbb720539
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 201,
  "idBook": 0,
  "url": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 02:15:13 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 201,
    "idBook": 0,
    "url": "string"
}
```
### 77. CoverPhotos: обновление/добавление данных фото на обложке запросом с невалидными данными(PUT ​/api​/v1​/CoverPhotos​/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/2147483648
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: ceb931ea-fd85-4e80-b138-9c6526e4f6ef
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 2147483648,
  "idBook": 2147483648,
  "url": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 02:18:26 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-fe0196ce63627d4f971e95cae1b876aa-def112dbdd3daf42-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ],
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 18."
        ]
    }
}
```
### 78. CoverPhotos: обновление данных фото на обложке запросом с некорректным JSON (PUT /api/v1/CoverPhotos/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/1
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (Bad Request) и указанием ошибки в синтаксисе JSON (не удалось преобразовать значение JSON) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 5c2f24bd-fbf1-43c1-81bf-8ba1fadf6189
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
 { 
    "id": 1,
  "idBook": 1,
  "url": "string"
 }
``` 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 02:21:59 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-9fa0ba2b14b59a46b5cbdf5bf2da2888-006ba15b6a9dfe44-00",
    "errors": {
        "$": [
            "'i' is an invalid start of a value. Path: $ | LineNumber: 0 | BytePositionInLine: 0."
        ]
    }
}
```
### 79. CoverPhotos: обновление данных фото на обложке запросом с пустым значением id в теле запроса (PUT /api/v1/CoverPhotos/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/1
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера..
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: e3b563c5-dc4f-47ec-bd59-32ffecf5e2d7
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": ,
  "idBook": 1,
  "url": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 02:30:08 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-4a4a73996bc7004ea6f85b9bcb0069b8-2e959736ba1cc14c-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```
### 80. CoverPhotos: обновление данных фото на обложке запросом с пустым телом (PUT /api/v1/CoverPhotos/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/1
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 5280ecc4-a614-4124-99cd-8bb99e0fced0
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sat, 08 Jul 2023 02:32:54 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-92251751b70fac4d9b423844c36ad071-78c7504af1c00f4f-00",
    "errors": {
        "$": [
            "The input does not contain any JSON tokens. Expected the input to start with a valid JSON token, when isFinalBlock is true. Path: $ | LineNumber: 0 | BytePositionInLine: 1."
        ]
    }
}
```
### 81. CoverPhotos: обновление фото на обложке запросом с пустым JSON-объектом (PUT /api/v1/CoverPhotos/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/1
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 32842d28-3768-4cb6-a69d-af7ad69dcee3
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 02:35:26 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 0,
    "idBook": 0,
    "url": null
}
```
### 82. CoverPhotos: удаление фото на обложке (DELETE /api/v1/CoverPhotos/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/CoverPhotos/1
- **Ожидаемый результат:** HTTP статус: 204 No Content. Тело ответа в JSON-формате (с описанием состояния объекта - удален) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: f7d80135-4da6-4503-a126-1a64e79d607a
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Length: 0
Date: Sat, 08 Jul 2023 02:39:04 GMT
Server: Kestrel
api-supported-versions: 1.0
```
- **Тело ответа:** -

## Раздел Users:

### 83. Users: получение списка пользователей (GET /api/v1/Users)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users 
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с массивом данных (Users от 1 до 10-ти) возвращается от сервера. 
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: cdc20c40-ec16-4989-bd13-c321c50522d5
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Length: 0
Date: Sun, 09 Jul 2023 12:42:09 GMT
Server: Kestrel
```
- **Тело ответа:** 
```
   [ {
        "id": 1,
        "userName": "User 1",
        "password": "Password1"
    },
    {
        "id": 2,
        "userName": "User 2",
        "password": "Password2"
    },
   ]
```

### 84. Users: добавление нового пользователя (POST /api/v1/Users)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users 
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 201) возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 202df8d9-680e-435f-a1c9-0ec3f4ba6e38
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 1,
  "userName": "string",
  "password": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sat, 08 Jul 2023 01:01:19 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
  "id": 1,
  "userName": "string",
  "password": "string"
}
```
### 85. Users: добавление уже существующего пользователя (POST /api/v1/Users)

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users 
- **Ожидаемый результат:** HTTP статус: 409 Conflict. Тело ответа в JSON-формате c описанием ошибки и указанием конфликта отправленного значения с текущим состоянием ресурса возвращается от сервера. 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 399595a9-d218-468e-be54-b6f879424688
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 61
```
- **Тело запроса:** 
```
{
  "id": 1,
  "userName": "string",
  "password": "string"
}
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 09 Jul 2023 13:47:42 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
  {
  "id": 1,
  "userName": "string",
  "password": "string"
}
```
### 86. Users: получение данных существующего пользователя (GET ​/api​/v1​/Users​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/1 
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с данными (User 1) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: f946ebb6-bc0d-495b-a0fb-f682780fd72b
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 09 Jul 2023 13:53:25 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 1,
    "userName": "User 1",
    "password": "Password1"
}
```
### 87. Users: получение данных несуществующего пользователя (GET ​/api​/v1​/Users​/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/11 
- **Ожидаемый результат:** HTTP статус: 404 Not Found. Тело ответа в JSON-формате c описанием ошибки (запрашиваемые данные не найдены) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 0ca9b81f-99c4-4bd5-903a-4a31e6de91cc
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, def
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8; v=1.0
Date: Sun, 09 Jul 2023 14:13:46 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-f3f31b1f2865554db854f866e43506c7-027d2a67d1baef4c-00"
}
```
### 88. Users: получение данных пользователя запросом с невалидными данными (GET ​/api​/v1​/Users​/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/2147483648
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: b548c5c0-57d5-4003-9691-9c2b26250cfa
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** -  
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 09 Jul 2023 14:16:12 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-0ae17902a4b20446bee6f71827d00a8e-289d4379b3f2f043-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ]
    }
}
```

### 89. Users: обновление данных пользователя (PUT ​/api​/v1​/Users​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/1 
- **Ожидаемый результат:** HTTP статус: 200 OK. Тело ответа в JSON-формате с обновленными данными ("username": "string1"). 
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: e7d3e353-3853-460d-b79d-e62f7c0fc940
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 1,
  "userName": "string 1",
  "password": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 09 Jul 2023 14:08:28 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
  "id": 1,
  "userName": "string 1",
  "password": "string"
}
```
### 90. Users: добавление данных пользователя (PUT ​/api​/v1​/Users​/{несуществующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/11
- **Ожидаемый результат:** HTTP статус: 201 Created. Тело ответа в JSON-формате с созданными данными ("id": 11) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: b72bfce9-e07e-4e29-9ae7-54c4a8889d13
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 11,
  "userName": "string",
  "password": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 09 Jul 2023 14:02:53 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.09 Jul 2023
```
- **Тело ответа:** 
```
{
  "id": 11,
  "userName": "string",
  "password": "string"
}
```
### 91. Users: обновление/добавление пользователя запросом с невалидными данными (PUT /api/v1/Users/{невалидный id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/2147483648
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки и указанием проблемы валидации в поле id возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: a4ba7157-882e-48d6-b26a-2bab798225d2
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": 2147483648,
  "userName": "string",
  "password": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 09 Jul 2023 13:59:09 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-33225822e42c8744a3f9fb1846edfeeb-217c62ddfc9c3c49-00",
    "errors": {
        "id": [
            "The value '2147483648' is not valid."
        ],
        "$.id": [
            "The JSON value could not be converted to System.Int32. Path: $.id | LineNumber: 1 | BytePositionInLine: 18."
        ]
    }
}
```
### 92. Users: обновление данных пользователя запросом с некорректным JSON (PUT ​/api​/v1​/Users​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/1 (заполнив id в поле ввода и в теле значением 1)
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (Bad Request) и указанием ошибки в синтаксисе JSON (не удалось преобразовать значение JSON) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: da55976b-1d9f-4e15-be6c-20ddfd3ca213
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
  "id": ,
  "userName": "string",
  "password": "string"
``` 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 09 Jul 2023 13:55:23 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-02cfb093e762cd47b4e5e8367f212ffc-d32453f8b577524b-00",
    "errors": {
        "$": [
            "The JSON value could not be converted to FakeRestAPI.Models.User. Path: $ | LineNumber: 0 | BytePositionInLine: 4."
        ]
    }
}
```
### 93. Users: обновление данных пользователя запросом с пустым значением id в теле запроса (PUT /api/v1/Users/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/1
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (недопустимо пустое значение id) возвращается от сервера..
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 94e2fdf3-cf81-4437-9c3b-14286f9a69c7
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
{
  "id": ,
  "userName": "string",
  "password": "string"
}
``` 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 09 Jul 2023 13:52:42 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-7c6da2906bb7d9449127d58cccdcc3a7-f23bdb14da607c4f-00",
    "errors": {
        "$.id": [
            "',' is an invalid start of a value. Path: $.id | LineNumber: 1 | BytePositionInLine: 8."
        ]
    }
}
```
### 94. Users: обновление данных пользователя запросом с пустым телом (PUT ​/api​/v1​/Users​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/1
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: 002699d1-31de-4d93-be80-7f424a95fa55
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Type: application/problem+json; charset=utf-8
Date: Sun, 09 Jul 2023 13:43:49 GMT
Server: Kestrel
Transfer-Encoding: chunked
```
- **Тело ответа:** 
```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-b5908cff878665408d3a5fda198312d6-3ec4774c26aabd4c-00",
    "errors": {
        "$": [
            "The input does not contain any JSON tokens. Expected the input to start with a valid JSON token, when isFinalBlock is true. Path: $ | LineNumber: 0 | BytePositionInLine: 1."
        ]
    }
}
```
### 95. Users: обновление данных пользователя запросом с пустым JSON-объектом (PUT ​/api​/v1​/Users​/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/1 
- **Ожидаемый результат:** HTTP статус: 400 Bad Request. Тело ответа в JSON-формате c описанием ошибки (требуется непустое тело запроса) возвращается от сервера.
- **Заголовки запроса:**
```
Content-Type: application/json
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: fc64ff8b-f56c-4fe0-a886-667a122240ff
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** 
```
 {
     
 }
```
- **Заголовки ответа:**
```
Content-Type: application/json; charset=utf-8; v=1.0
Date: Sun, 09 Jul 2023 13:37:09 GMT
Server: Kestrel
Transfer-Encoding: chunked
api-supported-versions: 1.0
```
- **Тело ответа:** 
```
{
    "id": 0,
    "userName": null,
    "password": null
}
```
### 96. Users: удаление данных пользователя (DELETE /api/v1/Users/{существующий id})

- **URL:** https://fakerestapi.azurewebsites.net/api/v1/Users/1 
- **Ожидаемый результат:** HTTP статус: 204 No Content. Тело ответа в JSON-формате (с описанием состояния объекта - удален) возвращается от сервера.
- **Заголовки запроса:**
```
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Cache-Control: no-cache
Postman-Token: aa0b78f7-7d72-4ad4-8c39-48ae186082d3
Host: fakerestapi.azurewebsites.net
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
- **Тело запроса:** - 
- **Заголовки ответа:**
```
Content-Length: 0
Date: Sun, 09 Jul 2023 13:33:52 GMT
Server: Kestrel
api-supported-versions: 1.0
```
- **Тело ответа:** -