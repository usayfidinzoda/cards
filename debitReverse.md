Запрос Запрос на отмену транзакции
{api_address}/debit/reverse

Method: POST

Request

```


{
    "service_name":"alif.moliya",
    "external_ref":"130444",
    "description":"reverse reason"
}

```

Success Response

```
{
    "external_ref": "130444",
    "code": 992,
    "message": "Транзакция успешно отменена",
    "status": "reversed"
}

```

Failed Response

```
{
    "external_ref": "130444",
    "code": 919,
    "message": "Not found",
    "status": "failed"
}

```
