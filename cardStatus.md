1. Получение статуса карты по пану

rest {api_address}/card/status

nats subject: {service}.card.status

Method: POST

Request

```
{
    "service_name":"alif.moliya",
    "external_ref":"12",
    "sender":{
    "pan":"8600111111111111"
    }
    
}

```

Success Response

```
{
    "external_ref": "",
    "code": 1000,
    "message": "Успешно",
    "payload": {
        "pan": "860011******1111",
        "bank": "Orient Finans Bank",
        "full_name": "VASYA PUPKIN"
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


