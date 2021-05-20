Запрос на получении скоринга карты
{api_address}/card/history

Method: POST

Request

```

{
    "service_name":"alif.moliya",
    "external_ref":"130444",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312"
    },
}

```


Success Response

```
{
    "external_ref": "",
    "code": 1000,
    "message": "Успешно",
    "payload": {
        "full_name": "HOLDER NAME",
        "phone": "998900111111",
        "card_number": "860057******1862",
        "bank_name": "Orient Finans Bank",
        "begin_date": "20210501",
        "end_date": "20210430",
        "history": [
            {
                "date": "20210401",
                "debits_amount": "300",
                "debits_count": 3,
                "credits_amount": "0",
                "credits_count": 0,
                "p2p_debits_amount": "0",
                "p2p_debits_count": 0,
                "p2p_credits_amount": "0",
                "p2p_credit_count": 0,
                "reversal_debits_amount": "0",
                "reversal_debits_count": 0,
                "reversal_credits_amount": "0",
                "reversal_credits_count": 0
            }
        ]
    },
    "status": "approved"
}
```

Failed Response

```
{
    "external_ref": "128",
    "code": 914,
    "message": "Недействительная карта",
    "payload": null,
    "status": "failed"
}

```
