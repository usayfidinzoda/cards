1. Получение пана и срока действия карт по токену

{api_address}/card/pan

Method: POST

Request

```
{
    "service_name":"alif.moliya",
    "external_ref":"12",
    "sender":{
    "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    }
    
}

```

Success Response

```
{
    "external_ref": "12",
    "code": 1000,
    "message": "Успешно",
    "payload": {
        "pan": "8600111111111111",
        "expiry": "2312"
    },
    "status": "approved"
}

```

Failed Response

```
{
    "external_ref": "12",
    "code": 910,
    "message": "Неверные данные запроса",
    "status": "failed"
}

```


