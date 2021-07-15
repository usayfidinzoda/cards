Запрос на кеширования транзакций

nats subject: {service}.monitoring

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
        "pan": "9bf9c57f7b0a0c1c98164b8307309d7f2380d890b508a73f8dcf821d9de31fd6"
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


