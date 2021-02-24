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
                "client_id": "98765432", -> id клиетна в системе Хумо
                "bank_code": "10", -> код банка эмитета
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
| Название | Тип | Описание |
|---|---|---|
| client_id  |  string |  идентификатор для запросов. В основном используется для транзакционных операций |
| bank_code  | int  |  Код ответа. Включает в себя код ошибки |
| payload  | struct |  Тело ответа, хранящая в себе информацию. Для каждого запроса, структуры(объекты) разные |
| message  | string | Описание кода(code) ответа в виде строки. |
| status | string | Используется для описания статуса транзакции. |

    2. Метод Check Sms banking [GET]:        
        Проверка на подключения смс информирования банком. Операции по платежам не могут проводится если клиент не подключен к смс информированию.

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
            "card_number": "987654*****1234",
            "card_holder_name": "TEST TEST",
            "currency": "UZS",
            "currency_desc": "UZS",
            "available_amount": 8888888
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
        "include_declined": true -> включить ли отмененные(Отменены по причине нехватки денег или же других причин) тразакции
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
                "state": 3,
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
                "state": 3,
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
            "external_ref": "1612357300058500100", -> уникальный номер
            "sender": { -> структура отправки, при котором sender считается как клиент.
                "pan": "9876543211234567", -> номер карты
                "yymm": "2301", -> срок истечения карты клиента
                "phone": "+998111111111" -> номер клиента
            },
            "service_name": "testExternalServiceName",
            "country": "testCountryName"
            "lang" : "string"                           -> язык сообщения для оповещения (uz, en, ru).
        }
        Ответ может быть в двух видах. 
            1. Если номер телефона привязанной карты равен номеру телефону в запросе, в этом случае токенизация происходит моментально и возвращает желанный токен 
            {
                "external_ref": "1612357300058500100",
                "code": 900,
                "payload": {
                    "token": "add19f8779730110bd3d92c781fcebc0c25e42c41661bd0b59174140",
                    "masked_pan":"987654****4567"
                },
                "message": "Accepted for further process",
                "status": null
            }

            2. Иначе, приходит ответ: 
            {
                "external_ref": "1612357300058500100",
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
                    "token": "add19f8779730110bd3d92c781fcebc0c25e42c41661bd0b59174140",
                    "masked_pan":"987654****4567"
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
    
    Термины: 
        sender       -> отправитель, c кого будет взыматься указанная сумма
        receiver     -> получатель, для кого будет отправлятся, переводиться сумма
        servicе_name -> имя сервиса который пользуется предоставленной услугой (alif.mobi, alif.shopuz, aliftech и тд)
        external_ref -> уникальный id для данной транзакции 
        token        -> уникальный номер для зарегистрированной карты


    1. Метод Debit From Registered Card [POST]:
        Снятие с карты по предоставленному токену. 
        Процес происходит по протоколу request-reply. Отправляетя запрос с token-ом зарегистрированной карты, 
        в объекте-e sender. В объект-e sender больше ничего не нужно указывать так как необходимая информация уже имеется.
        Кроме этого понадобится, external_ref, amount, service_name, country. Другие, указаны
        как optional. 
        POST запрос для снятия:
        {
            "external_ref": "1612357300058500100", : mandatory
            "sender": {
                "account": "string",
                "pan": "string",
                "yymm": "string",
                "cvv2": "string",
                "holder_name": "string",
                "token": "tokenforsomecard",    
                "phone": "string"
            },
            "amount": 9999,                          -> указывается в UZS, Например: 1234.50 : mandatory 
            "service_name": "string",                -> сервис отправитель (consumer name): пример alif.mobi, alif.shopuz и тд. : mandatory 
            "country": "string"                      -> Страна(UZ, RU, TJ) : mandatory
            "instant": true,                         -> true указывает на синхронность платяжа, false -> за ассинхроность (not implemented) : optional 
            "life_time": "2021-02-23T06:22:05.215Z", -> timeout платяжа (under construction, not implemented) : optional
            "description": "string",                 -> описание к оплате : optional
            "otp": "string",                         -> otp код, не используется для данного метода
            "fee": 0,                                -> если взымается коммисия с клиента за оплату, указывается коммисия в UZS : optional
            "lang" : "string"                        -> язык сообщения для оповещения (uz, en, ru).
        }
        Ответ:
        {
            "external_ref": "1612357300058500100",
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
            "code": 0,                      
            "payload": {            
                "external_ref": "string",   :       уникальный номер транзакции от пользователя услуг
                "state": 0,                 :       код статуса (таблицу общих кодов можно посмотреть внизу)
                "state_desc": "string",     :       описание к статусу
                "amount": 0,                :       сумма транзакции
                "error_code": 0,            :       код ошибки (таблицу общих кодов можно посмотреть внизу)    
                "error_message": "Success", :       описание к ошибке
                "type": 0,                  :       тип транзакции (таблицу общих кодов можно посмотреть внизу)
                "typ_desc": "string",       :       описание к транзакции
                "service_name": "string"    :       имя сервиса
            },
            "message": "string",
            "status": "string"
        }
    3. Метод ReturnTransaction [POST]
        Используется для возврата денег на карту. 
        POST запрос:
        {
            "external_ref" : "1612357300058500100",
            "service_name" : "testServiceName"
        } 
        Ответ: 
        {
            "external_ref": "1612357300058500100",
            "code": 900,
            "payload": {
                "state": 3,
                "state_desc": "Refunded"
            },
            "message": "Accepted for further process",
            "status": "Refunded"
        }

### Общие коды
    Статусы платяжа: 

        [Description("Платеж создан / В очереде на прохождение")]
        New = 0,
        
        [Description("Ошибка")]
        Error = 1,

        [Description("Операциия отменена")]
        Calceled = 2,
        
        [Description("Возврат средств")]
        Refunded = 3,
        
        [Description("Транзакция ожидает подтверждения клиента")]
        TransactionVerified = 4,
        
        [Description("Транзакция завершена")]
        TransactionConfirmed = 5

    -----------------------------------------
    Типы транзакций:
        [Description("Снятие с карты")]
        Debit = 0, 

        [Description("Перевод с карты на карту")]
        P2P = 1,

        [Description("Пополнение карты")]
        Credit = 2

    --------------------------------------------

    Коды ошибок:

        [Description("Accepted for further process")]
        Accepted = 900,
        
        [Description("Approved with partial amount")]
        ApprovedWithPartialAmount = 901,
        
        [Description("Accepted, need confirmation code")]
        NeedForConfirmationCode = 902,

        [Description("Invalid confirmation code")]
        InvalidConfirmationCode = 903,

        [Description("Bad request")]
        BadRequest = 910,  
        
        [Description("Bad gateway")]
        BadGateway = 911,
        
        [Description("Upstream service unavailable")]
        ServiceUnavailable = 912,
        
        [Description("Limit exceeded")]
        LimitExceeded = 913,
        
        [Description("Invalid card (expired or not found)")]
        InvalidCard = 914, 
        
        [Description("Insufficient funds")]
        InsufficientFunds = 915,
        
        [Description("Invalid amount")]
        InvalidAmount = 916,
        
        [Description("Invalid transaction")]
        InvalidTransaction = 917,
        
        [Description("Can not finalize transaction")]
        CanNotFinalizeTransaction = 918,
        
        [Description("Not found")]
        NotFound = 919,
        
        [Description("Sender card/account blocked or temporarily unavailable")]
        SenderCardBlockedOrUnavailable = 920,
        
        [Description("Receiver card/account blocked or temporarily unavailable")]
        ReceiverCardBlockedOrUnavaulable = 921,
        
        [Description("Unauthorized client")]
        UnAuthorized = 922,
        
        [Description("Forbidden transaction")]
        ForbiddenTransaction = 923,
        
        [Description("Internal server error")]
        InternalError = 924,
        
        [Description("Gateway timeout")]
        GatewayTimeout = 925,
        
        [Description("Duplicate transaction")]
        DublicateTransaction = 926,
        
        [Description("Transaction declined by host")]
        TransactionDeclinedByHost = 927,

        [Description("Apporoved")]
        Approved = 1000
