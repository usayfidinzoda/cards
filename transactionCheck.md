Запрос на проверку статуса транзакции
{api_address}/transaction/check

Method: POST

Request

```

{
    "service_name":"alif.moliya",
    "external_ref":"130444"
    "tran_type":"debit"        //transaction type: debit, credit, p2p
}

```

Статус транзакции будет хранится в response.status а код в response.code

Success Response

```
{
    "external_ref": "130444",
    "code": 1000,
    "message": "успешно",
    "status": "approved"
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
