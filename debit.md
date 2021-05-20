1. Метод Debit списание с карты

{api_address}/debit/create

Method: POST

Request: списание с карты по пану и сроку действия

```

{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312"
    },
    "amount":1000.50,
    "description":"test",
    "country":"uz"
}

```

Response

