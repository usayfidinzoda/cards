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

 Если номер телефона привязанной карты равен номеру телефону в запросе,   
 в этом случае транзакция проходит

Success Response

```
{
    "external_ref": "131",
    "code": 1000,
    "message": "успешно",
    "status": "approved"
}

```

В противном случае, отправлятся сообщение с OTP на номер к привязанной карте в банке. 

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

