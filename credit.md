Запрос на пополниние карты

{api_address}/credit/create

Method: POST

Request: пополнение карты по пану и сроку действия

```

{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312"
    },
    "amount":1000.50,
    "description":"test",
    "country":"uz",
    "lang":"ru",
}

```

Пополнение карты по токену

Credit By Token Request

```
{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "amount":1000.50,
    "description":"test",
    "country":"uz",
}

```


Success Response

```
{
    "external_ref": "131",
    "code": 1000,
    "message": "успешно",
    "status": "approved"
}

```

Failed Response

```
{
    "external_ref": "131",
    "code": 926,
    "message": "Повторяющаяся транзакция,
    "status": "failed"
}

```

