Метод позволяет удалить токен партнера по названию.

nats subject: uzcard.card.unbind

Method: POST

Request

```
{
    "service_name": "alif.mobi",
    "external_ref": "18",
    "sender": {
        "token": "f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "description": "testservicename"
}

```

Success Response 

```
{
    "external_ref": "",
    "code": 1000,
    "message": "Успешно",
    "status": "approved"
}
```
Failed Response

```
{
    "external_ref": "",
    "code": 910,
    "message": "Неверные данные запроса",
    "status": "failed"
}

```
