Метод позволяет получить список всех партнеров, к которым
привязана данная карта.
В ответ выдает названия предприятий, к
которым привязана карта

nats subject: uzcard.card.session.list

Method: POST

Request

```
{
    "service_name": "alif.mobi",
    "external_ref": "18",
    "sender": {
        "token": "f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    }
}

```

Success Response 

```
{
    "external_ref": "",
    "code": 1000,
    "message": "Успешно",
    "payload": [
        "testservicename1",
        "testservicename2",
        "testservicename3",
        "testservicename4"
    ],
    "status": "approved"
}
```
Failed Response

```
{
    "external_ref": "18",
    "code": 910,
    "message": "Неверные данные запроса",
    "status": "failed"
}


```
