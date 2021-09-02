 Метод P2P перевод денег с карты на карту
 
nats subject {service}.p2p

Method: POST

P2P pan2pan Перевод денег по пану и сроку действия карты отправителя и пану получателя
 
Request: 

```
{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312"
    },
    "receiver":{
        "pan":"8600111111111121"
    },
    "terminal": "p2p_0",
    "fee": 0.00,
    "amount":1000.50,
    "description":"test",
    "country":"uz",
    "lang":"ru"
}

```

отправлятся сообщение с OTP на номер к привязанной карте в банке. 


```

{
    "external_ref": "130444",
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
    "receiver":{
        "pan":"8600111111111121"
    },
    "terminal": "p2p_0",
    "fee": 0.00,
    "otp":"123456",
    "amount":1000.50,
    "description":"test",
    "country":"uz",
    "lang":"ru"
}

```

P2P token2pan перевод денег по токену отправителя, пану карты получателя

Credit by sender token request

```
{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e",
    },
    "receiver":{
        "pan":"8600111111111121"
    },
    "terminal": "p2p_0",
    "fee": 0.00,
    "amount":1000.50,
    "description":"test",
    "country":"uz",
    "lang":"ru"
}

```

Success Response

Если транзакция прошла успешно, в ответ возвращаются хэш пана и номер телефона получателя.
```
{
    "external_ref": "131",
    "code": 1000,
    "message": "успешно",
    "payload": {
        "id": 160,
        "pan_hash": "9bf9c57f7b0a0c1c98164b8307309d7f2380d890b508a73f8dcf821d9de31fd6",
        "phone":"998900111111"
    },
    "status": "approved"
}

```

Failed Response

```
{
    "external_ref": "131",
    "code": 926,
    "message": "Повторяющаяся транзакция,
    "status": "failed"
}

```

