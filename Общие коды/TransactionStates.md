# Статусы: 
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