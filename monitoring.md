Запрос на мониторинг карты

{api_address}/card/monitoring

Method: POST

Request
```
{
    "service_name": "alif.moliya",
    "page_size":20,
    "external_ref":"ext 1",
    "page_number":0,
    "date_from":"2021-04-30T15:04:05+05:00",
    "date_to":"2021-05-02T15:04:05+05:00",
    "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    
}
```

Success Response
```
{
    "external_ref": "",
    "code": 1000,
    "message": "Успешно",
    "payload": {
        "total_pages": 0,
        "total_elements": 0,
        "page_size": 3,
        "page_number": 0,
        "content": [
            {
                "amount": 0,
                "merchant_name": "",
                "pan": "",
                "terminal_id": "",
                "merchant_id": "",
                "date": "0001-01-01T00:00:00Z",
                "type": "",
                "merchant_category_code": 0,
                "reversal": false
            }
        ]
    },
    "status": "approved"
}

```

Failed Response 

```
{
    "external_ref": "",
    "code": 914,
    "message": "Недействительная карта",
    "payload": null,
    "status": "failed"
}
```
