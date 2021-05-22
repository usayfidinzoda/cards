Запрос на мониторинг карты

{api_address}/card/monitoring

Method: POST

Request
```
{

    "service_name": "servicename",
    "external_ref":"ext 1",
    "rows_limit":20,
    "rows_offset":0,
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
    "payload":  [{
                "amount": 100050.50,
                "merchant_name": "Bozori Korvon, 23",
                "pan": "8934******1234",
                "date": "2021-01-01T10:40:30Z",
                "type": "debit",
                "merchant_category": "Supermarket",
                "reversal": false
            }],
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
