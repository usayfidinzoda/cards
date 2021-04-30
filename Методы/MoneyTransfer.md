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
