```mermaid

stateDiagram-v2
    [*] --> PendingPayment : ایجاد درخواست رزرو (UC3)
    PendingPayment --> PaymentFailed : پرداخت ناموفق (UC4)
    PendingPayment --> Processing : پرداخت موفق (UC4)
    
    Processing --> Confirmed : تخصیص نیرو (UC13)
    Processing --> Cancelled : لغو توسط مشتری (UC6)
    
    Confirmed --> InProgress : شروع کار
    Confirmed --> Cancelled : لغو توسط مشتری/مدیر (UC6)
    
    InProgress --> Completed : ثبت وضعیت انجام (UC9)
    InProgress --> Cancelled : لغو حین کار
    
    Completed --> Rated : امتیازدهی توسط مشتری (UC7)
    
    PaymentFailed --> Cancelled : انقضای زمان/لغو
    
    Rated --> [*]
    Cancelled --> [*]

