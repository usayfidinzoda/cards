# Humouz
Docs of Humo UZ API - uz.alif.mobi/humo/swagger

### Содержание:
    1. Общая информация 
    2. Card
    3. Money Transfer

## Общая информация
    > Соединение осуществляется по протоколу REST и имеет формат (request-response) - JSON. При каждом запросе сервис поставщика услуг (провайдера) обрабатывает запрос и выдает соответствующий результат 

    > Запрос на транзакции: P2P, Debit, Credit со стороны потребителя услуг должен включать уникальный идентификатор (“external_ref”). В качестве примера можно использовать guid или uuid. Этот идентификатор, будет необходим при сверках и  для решения спорных вопросов. 

    > Авторизация происходит с использованием api ключа(“Api-Key”) в заголовке (header) каждого запроса, который предоставляется поставщиком услуг.

    > Если услуга не предоставлена провайдером потребителю, ответом будет ошибка с кодом 401 (UnAuthorized).

    > Предоставляемые услуги делятся на 2 типа: 
        - Card Operation: карточные операции, такие как card info, card balance, tokenization, и тд. 
        - Money transfer : платежные операции нацеленные на снятие, пополнение, p2p. Также есть статус платежа по external_ref.
    
    - Структура результата следующая:
        {
            “external_ref”:”string”,
            “code” : int,
            “payload”: struct,
            “message” : “string”
            “status” : “string”
        }

| Название | Тип | Описание |
|---|---|---|
| external_ref  |  string |  идентификатор для запросов. В основном используется для транзакционных операций |
| code  | int  |  Код ответа. Включает в себя код ошибки |
| payload  | struct |  Тело ответа, хранящая в себе информацию. Для каждого запроса, структуры(объекты) разные |
| message  | string | Описание кода(code) ответа в виде строки. |
| status | string | Используется для описания статуса транзакции. |

<br/>
<br/>

### Card
    Карточные операции состоят из нескольких операций, по которым можно узнать ту или иную информацию. Например, в ClientInfoByCardNumber предоставляется информация о клиенте по номеру(pan) карты. 
    
    1. Метод Client Info [GET]:
        Возвращает информацию о клиенте по номеру карты. 
        
        GET запрос с номером карты “9876543217654321”
        Ответ:
	    {
            "external_ref": null,
            "code": 0,
            "payload": {
                "client_id": "98765432",
                "bank_code": "10",
                "second_name": "TEST",
                "first_name": "TEST",
                "birthday": "1992-09-12T00:00:00",
                "email": "",
                "phone": "+998987654321",
                "country": "UZB",
                "card_number": “9876543217654321”,
                "registered_street": "TOSHKENT SHAHAR TEST TEST",
                "id_card": "2345678",
                "doc_type": "Passport",
                "issued_by": "DIA IN KHUDAND",
                "doc_name": "Passport",
                "doc_since": "2015-04-02T00:00:00",
                "doc_serial": "P"
            },
            "message": "Success",
            "status": null
        }

    2. Метод Check Sms banking [GET]:        
        Проверка на подключения смс информирования банком. Операции по платежам не могут проводится если клиент не подключен к смс информированию. Если смс информирование подключено, в теле ответа(payload) будет информация о номере телефона привязанной к карте. 

        GET запрос по номеру карты
        Ответ:
        {
            "external_ref": null,
            "code": 900,
            "payload": {
                "card_holder_id": "client_id-bank_code",
                "card_holder_name": "TEST TEST",
                "is_sms_on": true
            },
            "message": "Accepted for further process",
            "status": null
        }

    3. Метод GetCardBalance [GET]
       Возвращается информация о доступной сумме на карте. 
       GET запрос но номеру карты
       Ответ:
       {
        "external_ref": null,
        "code": 900,
        "payload": {
            "card_number": "986010*****7451",
            "card_holder_name": "A ABDURASHIDOV",
            "currency": "UZS",
            "currency_desc": "UZS",
            "available_amount": 8888888 -> возвращается в копейках
        },
        "message": "Accepted for further process",
        "status": null
        }

    4. Метод Get Card Transaction History [POST]
        Возвращает информацию о транзакциях карты. 
        POST запрос:
        {
        "card_number": "string", -> номер карты
        "begin_date": "2021-02-08T08:30:46.377Z", -> с какой даты
        "end_date": "2021-02-08T08:30:46.377Z", -> по какую
        "include_declined": true -> включить ли отмененные тразакции
        }
        Ответ:
        {
            "external_ref": null,
            "code": 900,
            "payload": {
                "card_number": "9860100124167451",
                "begin_date": "2020-02-08T00:00:00Z",
                "end_date": "2021-02-08T23:59:59",
                "transactions": [
                    {
                        "card_number": "987654*****1234",
                        "client_id": "098765",
                        "code": "",
                        "fee": 0,
                        "type": "11V",
                        "currency": "UZS",
                        "amount": 10000,
                        "date_created": "2021-01-25T12:54:23",
                        "reconciled_on": "2021-01-26T00:00:00",
                        "date_confirmed": "2021-01-26T00:00:00",
                        "account_currency": "UZS",
                        "amount_in_account_currency": 10000,
                        "bank_name": "Kapital",
                        "merchant_title": "",
                        "city": "",
                        "country": "",
                        "declined": false
                    }, 3
                ]
            },
            "message": "Accepted for further process",
            "status": null
        }

    5. Метод Get Transaction By External Id [GET]:
        Возвращает информацию о тразакции по external_ref. 
        GET запрос с external_ref
        Ответ:
        {
            "external_ref": "testexternalref123",
            "code": 900,
            "payload": {
                "source_card_number": "987654*****1234",
                "target_card_number": null,
                "amount": 1000,
                "currency": 860, -> (Currency code: UZS, etc)
                "conversion_rate": 1,
                "state": "Refunded",
                "state_desc": "returned",
                "refunded_amount": 100000
            },
            "message": "Accepted for further process",
            "status": null
        }

    6. Метод Get Transaction Info List [GET]
        Возвращает лист информаций о транзакциях.
        GET запрос с желаемым периодом dateFrom и dateTo
        Ответ:
        {
            "external_ref": null,
            "code": 900,
            "payload": [
                {
                "source_card_number": "986010*****7451",
                "target_card_number": null,
                "amount": 1000,
                "currency": 860,
                "conversion_rate": 1,
                "state": "Refunded",
                "state_desc": "returned",
                "refunded_amount": 100000
                },
                {
                "source_card_number": "986010*****7451",
                "target_card_number": "986027*****3923",
                "amount": 1000,
                "currency": 860,
                "conversion_rate": 1,
                "state": "finished",
                "refunded_amount": 0
                },
            ],
            "message": "Accepted for further process",
            "status": null
        }

    7. Метод GetCardInfo [GET]:
        Возвращает информацию о карте.
        GET запрос с номером карты
        Ответ:
        {
            "external_ref": null,
            "code": 0,
            "payload": {
                "card_number": "987654*****1234",
                "card_bin": "98601001",
                "card_type": "Debit", -> тип карты
                "card_level": "Visa Gold", 
                "card_status": "active", -> статус карты
                "cardholder_name": "TEST TEST", имя указанное на карте
                "bank_code": "10",
                "bank_name": "Kapital",
                "card_stop_cause": "active", -> если карта закрыта или же отключена здесь указывется прична
                "message_to_card_holder": "",
                "card_holder_first_name": "TEST",
                "card_holder_surname": "TEST"
            },
            "message": "Success",
            "status": null
        }

    8. Метод Tokenize [POST]:
        Регистрирует карту и возвращает токен по которым проводятся транзакции (DEBIT, CREDIT, P2P)

        POST запрос:
        {
            "external_ref": "1612357300058500100",
            "sender": {
                "pan": "9876543211234567",
                "yymm": "2301",
                "phone": "+998111111111"
            },
            "service_name": "testExternalServiceName",
            "country": "testCountryName"
        }
        Ответ может быть в двух видах. 
            1. Если номер телефона привязанной карты равен номеру телефону в запросе, в этом случае токенизация происходит моментально и возвращает желанный токен 
            {
                "external_ref": "1612357300058500100",
                "code": 900,
                "payload": {
                    "token": "987654****4567",
                    "masked_pan": "add19f8779730110bd3d92c781fcebc0c25e42c41661bd0b59174140"
                },
                "message": "Accepted for further process",
                "status": null
            }

            2. Иначе, приходит ответ: 
            {
                "external_ref": "test",
                "code": 902,
                "payload": null,
                "message": "Accepted, need confirmation code",
                "status": "Accepted, need confirmation code"
            }
            В этом случае, отправлятся сообщение с OTP на номер к привязанной карте. 
            При этом, отправляетя тот же cамый запрос с тем же самым external_ref. Также в запросе должен находиться OTP пришедший на номер держателя карты. 
            Запрос:
            {
                "external_ref": "1612357300058500100",
                "sender": {
                    "pan": "9876543211234567",
                    "yymm": "2301",
                    "phone": "+998111111111"
                },
                "service_name": "testExternalServiceName",
                "country": "testCountryName",
                "otp" = "123456" -> код пришедший на номер телефон держателя карты. 
            }
            Ответ:
            {
                "external_ref": "1612357300058500100",
                "code": 900,
                "payload": {
                    "token": "987654****4567",
                    "masked_pan": "add19f8779730110bd3d92c781fcebc0c25e42c41661bd0b59174140"
                },
                "message": "Accepted for further process",
                "status": null
            }
    9. Метод UnTokenize [DELETE]:
        Метод для удаления карты по токену
        DELETE запрос с токеном карты
        Ответ:
        {
            "external_ref": null,
            "code": 1000,
            "payload": true, -> означает что токен успешно удален
            "message": "Apporoved",
            "status": null
        }
### Money Transfer
    Услуга money trasfer занивается снятием, пополнением и p2p для предоставленных карт.

    1. Метод Debit From Registered Card [POST]:
        Снятие с карты по предоставленному токену. 
        POST запрос для снятия:
        {
            "external_ref": "testexternalref",
            "sender": {
                "token": "tokenforsomecard"
            "amount": 9999, -> указывается в UZS, Например: 1234.50 
            "service_name": "testServiceName"
        }
        Ответ:
        {
        "external_ref": "testexternalref",
        "code": 1000,
        "payload": {
            "state": "5",
            "state_desc": "TransactionConfirmed"
        },
        "message": "Approved",
        "status": "TransactionConfirmed"
        }
    2. Метод TransactionInfo [GET]:
        Возвращает информацию о транзакции по external_ref
        GET запрос с external_ref
        Ответ:
        {
            "external_ref": "string",
            "code": 0,
            "payload": {
                "external_ref": "string",
                "state": "New",
                "state_desc": "string",
                "amount": 0,
                "error_message": "string",
                "error_code": "Success",
                "type": 0, тип тран
                "typ_desc": "string",
                "service_name": "string"
            },
            "message": "string",
            "status": "string"
        }
    3. Метод ReturnTransaction [POST]
        Используется для возврата денег на карту. 
        POST запрос:
        {
            "external_ref" : "string",
            "service_name" : "testServiceName"
        } 
        Ответ: 
        {
            "external_ref": "string",
            "code": 900,
            "payload": {
                "state": 3,
                "state_desc": "Refunded"
            },
            "message": "Accepted for further process",
            "status": "Refunded"
        }