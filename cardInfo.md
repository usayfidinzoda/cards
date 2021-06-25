1. Реквизиты карты по токену

rest {api_address}/card/info
nats {service}.card.info

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
    "external_ref": "",
    "code": 1000,
    "message": "Успешно",
    "payload": {
        "full_name": "VASYA PUPKIN",
        "bank_name": "Agrobank",
        "account_number": "11111111111111111111",
        "card_type": "private",
        "inn": "",
        "bik": ""
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


