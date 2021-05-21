 Запрос на получениe списка дебитов 

{api_address}/debit/list

Method: POST

Request
```
{
  "date_from":"2020-01-02T15:04:05Z",
    "date_to":"2022-01-02T15:04:05Z",
  "external_ref": "",
  "id": 0,
  "sender_pan": "",
  "rows_limit": 20,
  "rows_offset": 0,
  "service_name": "",
  "status": ""
}

```
Примичиание! rows_limit должен быть в интервале: от 0 до 1000

Success Response 

```
external_ref": "",
    "code": 1000,
    "message": "Успешно",
    "payload": {
        "count": 27,
        "result": [
            {
                "id": 29,
                "service_name": "test",
                "external_ref": "23",
                "pan": "860011******1111",
                "pan2": "",
                "amount": "1000",
                "response_id": "",
                "response": "{\"jsonrpc\":\"2.0\",\"id\":29,\"error\":{\"code\":-207,\"message\":\"Transaction with such ext=29 (refNum=13) already exist in the database!\"}}",
                "regdate": "2021-04-30T18:37:33.199535+05:00",
                "stsdate": "2021-04-30T18:37:44.142549+05:00",
                "status": "failed",
                "err_code": 926,
                "err": "Transaction with such ext=29 (refNum=13) already exist in the database!"
            }
        ]
    },
    "status": "approved"
}
```
Failed Response

```
{
    "external_ref": "",
    "code": 910,
    "message": "Wrong page size",
    "status": "failed"
}

```
