Метод позволяет блокировать карту

nats subject: uzcard.card.block

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
    "external_ref": "131",
    "code": 1000,
    "message": "успешно",
    "status": "approved"
}
```
Failed Response

```
{
    "external_ref": "",
    "code": 926,
    "message": "Дублированный запрос",
    "payload": null,
    "status": "failed"
}
```
