Запрос на получение транзакций за последний год

rest {api_address}/card/monitoring

Method: POST

Request


Типы транизакций Debit:
 "DEBIT"
 "DEBIT_REVERSAL"
 "CREDIT"
 "CREDIT_REVERSAL"
 "P2P_DEBIT"
 "P2P_CREDIT"


```
{
    "service_name":"alif.moliya",
    "external_ref":"12",
    "sender":{
    "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "txn_type":""
}
```

Success Response

```
"external_ref": "12",
    "code": 1000,
    "message": "Успешно",
    "payload": [
        {
            "tran_num": "17",
            "tran_type": "DEBIT",
            "date": "2021-07-19T14:29:01.452128Z",
            "amount": 200,
            "merchant": "somename",
            "city": "somename",
            "street": "somename",
            "mcc": "122"
        },
        {
            "tran_num": "2",
            "tran_type": "DEBIT",
            "date": "2021-07-19T14:29:01.452128Z",
            "amount": 200,
            "merchant": "somename",
            "city": "somename",
            "street": "somename",
            "mcc": "122"
        },
        {
            "tran_num": "1",
            "tran_type": "DEBIT",
            "date": "2021-07-19T14:29:01.452128Z",
            "amount": 200,
            "merchant": "somename",
            "city": "somename",
            "street": "somename",
            "mcc": "122"
        }
    ],
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


