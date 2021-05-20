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
    "country":"uz",
    "lang":"ru",
}

```


При совершении снятия по пану и сроку действия карты, требуется смс подтверждения 

Pending Response

```

{
    "external_ref": "131",
    "code": 902,
    "message": "Принято, нужен код подтверждения",
    "payload": {
        "phone": "998*****1112"
    },
    "status": "pending"
}

```

Для подтверждения транзакции необходимо отправить запрос  
При этом, отправляетя тот же cамый запрос с тем же самым external_ref.  
Также в запросе должен находиться OTP пришедший на номер держателя карты. 

Confirm Request

```

{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312"
    },
    "amount":1000.50,
    "otp":"123456",
    "description":"test",
    "country":"uz",
    "lang":"ru",
}

```

Снятия по токену

Debit By Token Request

```
{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "amount":1000.50,
    "description":"test",
    "country":"uz",
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
    "external_ref": "131",
    "code": 926,
    "message": "Повторяющаяся транзакция,
    "payload": null,
    "status": "failed"
}

```

