1. Запрос на токенизацию карты

{api_address}/token/create

nats subject: {service}.token

Method: POST

Request

```

{
    "service_name":"alif.moliya",
    "external_ref":"130444",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312",
        "phone":"998900111111"
    },
    "description":"test",
    "country":"uz"
}

```

Success Response

 Если номер телефона привязанной карты равен номеру телефону в запросе,   
 в этом случае токенизация происходит моментально и возвращает токен 
 
```
{
    "external_ref": "128",
    "code": 1000,
    "message": "успешно",
    "payload": {
        "token": "f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e",
        "bank_name": "Agrobank",
        "pan": "8600*****1111",
        "full_name": "SOME NAME",
        "pan_hash": "9bf9c57f7b0a0c1c98164b8307309d7f2380d890b508a73f8dcf821d9de31fd6",
        "phone":"998900111111"
    },
    "status": "approved"
}

```

Pending Response

В этом случае, отправлятся сообщение с OTP на номер к привязанной карте в банке. 

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

Confirm Request

Для подтверждения токенизации необходимо отправить запрос  
При этом, отправляетя тот же cамый запрос с тем же самым external_ref.  
Также в запросе должен находиться OTP пришедший на номер держателя карты. 

```

{
    "service_name":"alif.moliya",
    "external_ref":"130444",
    "sender":{
        "pan":"8600111111111111",
        "yymm":"2312",
        "phone":"998900111111"
    },
    "otp": "123456",
    "description":"test",
    "country":"uz"
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
