# Balance

1. Получите баланс по пану и сроку действия

{api_address}/card/balance

Method: POST

Request

```

{
    "service_name":"alif.moliya",
    "external_ref":"128",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312"
    },
    "country":"uz"
}

```

Success Response

```
{
    "external_ref": "128",
    "code": 1000,
    "message": "успешно",
    "payload": {
        "balance": "49282.69",
        "full_name": "Test Testov",
        "bank_name": "Agrobank",
        "pan": "8600*****1111"
    },
    "status": "approved"
}

```

Failed Response

```
{
    "external_ref": "128",
    "code": 914,
    "message": "Недействительная карта",
    "payload": null,
    "status": "failed"
}

```


2. Получите баланс по token

{api_address}/card/balance

Method: POST

Request

```

{
    "service_name":"alif.moliya",
    "external_ref":"128",
    "sender":{
        "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "country":"uz"
}

```

Success Response

```
{
    "external_ref": "128",
    "code": 1000,
    "message": "успешно",
    "payload": {
        "balance": "49282.69",
        "full_name": "Test Testov",
        "bank_name": "Agrobank",
        "pan": "8600*****1111"
    },
    "status": "approved"
}

```

Failed Response

```
{
    "external_ref": "128",
    "code": 914,
    "message": "Недействительная карта",
    "payload": null,
    "status": "failed"
}

```

