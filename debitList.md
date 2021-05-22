 Запрос на получениe списка дебитов 

{api_address}/debit/list

Method: POST

Request

```
{
  "service_name": "alif.moliya",
  "date_from":"2020-01-02T15:04:05Z",
  "date_to":"2022-01-02T15:04:05Z",
  "rows_limit": 20,
  "rows_offset": 0,
  "status": ""
}

```
Примичиание! rows_limit должен быть в интервале: от 0 до 1000

Success Response 

```

{
	"code": 1000,
	"message": "Успешно",
	"payload": {
		"count": 27,
		"result": [{
			"id": 29,
			"external_ref": "23",
			"pan": "860011******1111",
			"amount": "1000.00",
			"regdate": "2021-04-30T18:37:33.199535+05:00",
			"stsdate": "2021-04-30T18:37:44.142549+05:00",
			"status": "failed",
			"err_code": 926,
			"err": "Transaction with such ext=29 (refNum=13) already exist in the database!"
		}]
	},
	"status": "approved",
	"external_ref": ""
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
