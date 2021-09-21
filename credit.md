Запрос на пополнение карты

nats subject: {service}.credit

Method: POST

Request: пополнение карты по пану и сроку действия

```

{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "receiver":{
        "pan":"8600111111111111"
    },
    "terminal": "credit",
    "amount":1000.50,
    "description":"test",
    "country":"uz",
    "lang":"ru"
}

```

Пополнение карты по токену

Credit By Token Request

```
{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "receiver":{
        "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "terminal": "credit_0",
    "amount":1000.50,
    "description":"test",
    "country":"uz"
}

```


Success Response

Если транзакция прошла успешно, в ответ возвращаются хэш пана и номер телефона получателя.
```
{
    "external_ref": "131",
    "code": 1000,
    "message": "успешно",
    "payload": {
        "id": 160,
        "pan_hash": "9bf9c57f7b0a0c1c98164b8307309d7f2380d890b508a73f8dcf821d9de31fd6",
        "phone":"998900111111"
    },
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

