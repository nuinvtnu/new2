```mermaid
classDiagram
direction LR

class UserAccount {
  +userId: UUID
  +fullName: String
  +email: String
  +phone: String
  +status: String
  +createdAt: DateTime
}

class Restaurant {
  +restaurantId: UUID
  +name: String
  +description: String
  +hotline: String
  +priceRange: String
  +status: String
}

class Branch {
  +branchId: UUID
  +name: String
  +address: String
  +openHours: String
}

class Table {
  +tableId: UUID
  +tableCode: String
  +capacity: int
  +locationNote: String
  +status: String
}

class Reservation {
  +reservationId: UUID
  +reservationCode: String
  +date: Date
  +timeStart: Time
  +timeEnd: Time
  +guestCount: int
  +status: String
  +specialRequest: String
  +createdAt: DateTime
}

class ReservationItem {
  +id: UUID
  +assignedCapacity: int
}

class Payment {
  +paymentId: UUID
  +amount: Decimal
  +method: String
  +status: String
  +paidAt: DateTime
  +transactionRef: String
}

class Promotion {
  +promoId: UUID
  +code: String
  +type: String
  +value: Decimal
  +validFrom: Date
  +validTo: Date
}

class AppliedPromotion {
  +id: UUID
  +discountAmount: Decimal
}

class Review {
  +reviewId: UUID
  +rating: int
  +content: String
  +createdAt: DateTime
  +status: String
}

%% Associations + Multiplicity
Restaurant "1" --> "1..*" Branch : has
Branch "1" --> "1..*" Table : contains

UserAccount "1" --> "0..*" Reservation : makes
Reservation "0..*" --> "1" Branch : for

%% Table assignment (optional but common)
Reservation "1" --> "0..*" ReservationItem : includes
ReservationItem "0..*" --> "1" Table : assigns

%% Deposit/payment
Reservation "1" --> "0..*" Payment : paidBy

%% Promotion (optional)
Reservation "0..1" --> "0..*" AppliedPromotion : uses
AppliedPromotion "0..*" --> "1" Promotion : from

%% Review (optional)
UserAccount "1" --> "0..*" Review : writes
Review "0..*" --> "1" Restaurant : about
