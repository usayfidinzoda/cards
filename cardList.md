Метод вызова списка карт, связанных с основной картой. В
случае успеха возвращает массив активных карт, связанных с
основной картой.

rest {api_address}/card/list

Method: POST

Request

```
{
    "service_name": "alif.mobi",
    "external_ref": "18",
    "sender": {
        "pan": "8600111111111111"
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
        "cards": [
            {
                "pan": "8600111111111111",
                "yymm": "2312",
                "full_name": "Cardholder Full Name",
                "status": 1000
            },
            {
                "pan": "8600111111111121",
                "yymm": "2311",
                "full_name": "Cardholder Full Name,
                "status": 1000
            }
        ]
    },
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
