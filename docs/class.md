```mermaid
classDiagram
    direction LR

    class Customer {
        +customerID: String
        +name: String
        +contactInfo: String
        +viewServices()
        +createReservation()
    }

    class ServiceProvider {
        +providerID: String
        +name: String
        +specialty: String
        +availability: List~TimeSlot~
        +acceptReservation()
        +updateStatus()
    }

    class Reservation {
        +reservationID: String
        +dateTime: DateTime
        +status: ReservationStatus
        +estimatedDuration: Integer
        +calculateCost()
    }

    class Service {
        +serviceID: String
        +name: String
        +description: String
        +basePrice: Currency
        +specifications: String
    }

    class Payment {
        +paymentID: String
        +amount: Currency
        +paymentMethod: String
        +transactionDate: DateTime
        +status: PaymentStatus
    }

    Customer "1" -- "*" Reservation : creates
    ServiceProvider "1" -- "*" Reservation : assignedTo
    Service "1" -- "*" Reservation : relatesTo
    Reservation "1" -- "1" Payment : involves
    
    Reservation ..> ReservationStatus: uses
    Payment ..> PaymentStatus: uses

    note for ReservationStatus "Enum: PendingPayment, Confirmed, InProgress, Completed, Cancelled"
    note for PaymentStatus "Enum: Pending, Success, Failed"
