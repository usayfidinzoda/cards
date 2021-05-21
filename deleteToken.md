
1. Удаление токена

{api_address}/token/delete

Method: POST

Request

```

{
    "service_name":"alif.moliya",
    "external_ref":"128",
    "sender":{
        "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "description":"reason: card is expired, user: Joh Doe" 
    "country":"uz"
}

```

Success Response

```
{
    "external_ref": "128",
    "code": 1000,
    "message": "успешно",
    "status": "approved"
}

```

Failed Response

```
{
    "external_ref": "128",
    "code": 924,
    "message": "Внутренняя ошибка сервера",
    "status": "failed"
}

```


