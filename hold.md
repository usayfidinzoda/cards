# Холдирование транзакции

{api_address}/debit/hold

Method: POST

Холдирование по токену

### Hold By Token Request

```
{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "sender":{
        "token":"f535e2a13abbf2bc2738afe93494fk43efa06a6a167bd84718fed39e"
    },
    "life_time" : "2021-06-20" до какого числа холдировать
    "amount":1000.50,
    "description":"test",
    "country":"uz"
}


```

### Подтверждения холдирования


```
{
    "service_name":"alif.moliya",
    "external_ref":"131",
    "country":"uz"
}

```

### Удаление холдирования

> Method Delete

    ```
    {
        "service_name":"alif.moliya",
        "external_ref":"131",
        "country":"uz"
    }

    ```



> Success Response

```
{
    "external_ref": "131",
    "code": 1000,
    "message": "успешно",
    "status": "approved"
}

```

> Failed Response

```
{
    "external_ref": "131",
    "code": 926,
    "message": "Повторяющаяся транзакция,
    "status": "failed"
}

```

