Запрос Запрос на отмену транзакции

rest {api_address}/transaction/reverse

nats subject: {service}.transaction.reverse

Method: POST

Request

```


{
    "service_name":"alif.moliya",
    "external_ref":"130444",
    "description":"reverse reason",
    "txn_type":"debit"        //transaction type: debit, credit, p2p
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
