# طراحی پایگاه‌داده — سامانه رزرو نیروی خدماتی خانه‌داری

## جداول اصلی
- **Customer**: اطلاعات مشتری (نام، تلفن، ایمیل، آدرس)  
- **Worker**: اطلاعات نیروی خدماتی (نام، مهارت‌ها، امتیاز، وضعیت دسترس‌پذیری)  
- **ServiceType**: نوع خدمت (عنوان، توضیح، قیمت پایه، مدت استاندارد)  
- **Booking**: رزروها (مشتری، خدمت، نیرو، تاریخ، وضعیت، قیمت کل)  
- **Payment**: پرداخت‌ها (رزرو، مبلغ، روش، وضعیت)  
- **Rating**: امتیازدهی (رزرو، مشتری، نیرو، امتیاز، نظر)

---

## دیاگرام ERD با Mermaid

```mermaid
erDiagram
    CUSTOMER ||--o{ BOOKING : "ایجاد می‌کند"
    WORKER ||--o{ BOOKING : "انجام می‌دهد"
    SERVICETYPE ||--o{ BOOKING : "شامل می‌شود"
    BOOKING ||--|| PAYMENT : "پرداخت دارد"
    BOOKING ||--o{ RATING : "امتیازدهی می‌شود"
    CUSTOMER ||--o{ RATING : "ثبت می‌کند"
    WORKER ||--o{ RATING : "دریافت می‌کند"

    CUSTOMER {
        int id PK
        string name
        string phone
        string email
        string address
    }

    WORKER {
        int id PK
        string name
        string phone
        string skills
        float rating
        string availability
    }

    SERVICETYPE {
        int id PK
        string title
        string description
        float base_price
        int duration
    }

    BOOKING {
        int id PK
        int customer_id FK
        int service_type_id FK
        int worker_id FK
        date booking_date
        time start_time
        time end_time
        string status
        float total_price
    }

    PAYMENT {
        int id PK
        int booking_id FK
        float amount
        string method
        string status
        string transaction_id
    }

    RATING {
        int id PK
        int booking_id FK
        int customer_id FK
        int worker_id FK
        int score
        string comment
    }
