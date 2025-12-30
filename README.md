```mermaid
classDiagram
direction LR

class UserAccount {
  +userId: UUID
  +fullName: String
  +email: String
}

class Restaurant {
  +restaurantId: UUID
  +name: String
}

UserAccount "1" --> "0..*" Restaurant : books
