# Transaction
    метод состоит из нескольких роутов 

### api/Transaction/GetTransactionsInfo
    возвращает список транзакций с даты начала по определенной дате

    Request :
        string SourceCardNumber     => карта с которой сняты деньги  
        string TargetCardNumber     => карта получателя для методов (credit, p2p)     
        int Offset                  => количество элеметов для offset (default 0)     
        int? Quantity               => количество элементов для пагинации (default 15)
        DateTime DateFrom           => с какой даты взять транзакции  (required)
        DateTime DateTo             => по какую дату взять транзакции (required)
        States? Status              => указывайтся если хотите получить транзакции с определенными статусами
        TransactionType? Type       => указывается если хотите получить транзакции с определенным типом (credit, debit, p2p)
        string ServiceName          => service name имя сервиса с которого была осуществлена транзакция (required)
        decimal? AmountFrom         => указывается если хотите получить транзакции с суммой больше 
        decimal? AmountTo           => указывается если хотите получить транзакции  до какой то суммы     
        string TerminalID           => не используется (не нужно указывать) 

    --------------------------------------------------------------------------------
    Response : 

        class InfoResponse
        {
            int Count                       => общее количество записей (использутся для пагинации)
            decimal AmountSum               => общее количетсво оборота денег
            List<TransactionInfo> Data      => подробная информация о каждой транзакции
        }

        class TransactionInfo
        {  
            int ID                           
            string GatewayOrderID 
            string ExternalRef       
            string SourceCardNumber 
            string TargetCardNumber 
            decimal Amount 
            int Currency 
            decimal Fee 
            string Country
            string ServiceName 
            string Phone 
            TransactionType Type 
            string TypeDesc
            States State 
            string StateDesc
            DateTime DateCreated 
            DateTime DateCanceled 
            DateTime DateConfirmed 
            DateTime DateReturnPayment 
            Errors ErrorCode 
            string ErrorMessage 
        }