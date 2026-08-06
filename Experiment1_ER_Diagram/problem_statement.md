# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

![ER Diagram](er_diagram_fitness.png)

### Entities and Attributes:

| Entity               | Attributes (PK, FK)                                                                                | Notes                                   |
| -------------------- | -------------------------------------------------------------------------------------------------- | --------------------------------------- |
| **Member**           | **Member_ID (PK)**, Name, Membership_Type, Start_Date                                              | Stores gym members                      |
| **Program**          | **Program_ID (PK)**, Program_Name, Duration, Fee                                                   | Stores fitness programs                 |
| **Trainer**          | **Trainer_ID (PK)**, Name, Specialization, Phone                                                   | Stores trainer information              |
| **Member_Program**   | **Member_ID (PK, FK)**, **Program_ID (PK, FK)**, Join_Date                                         | Resolves many-to-many relationship      |
| **Program_Trainer**  | **Program_ID (PK, FK)**, **Trainer_ID (PK, FK)**                                                   | Assigns trainers to programs            |
| **Personal_Session** | **Session_ID (PK)**, Member_ID (FK), Trainer_ID (FK), Session_Date, Session_Time, Duration         | Records personal training bookings      |
| **Attendance**       | **Attendance_ID (PK)**, Session_ID (FK), Attendance_Date, Status                                   | Tracks attendance for each session      |
| **Payment**          | **Payment_ID (PK)**, Member_ID (FK), Session_ID (FK, Nullable), Payment_Date, Amount, Payment_Type | Records membership and session payments |





### Relationships and Constraints:

| Relationship                  | Cardinality    | Participation    | Notes                                                                                     |
| ----------------------------- | -------------- | ---------------- | ----------------------------------------------------------------------------------------- |
| Member – Program              | M:N            | Partial          | Members can join multiple programs, and each program has many members.                    |
| Program – Trainer             | M:N            | Partial          | A program may have multiple trainers, and a trainer can teach multiple programs.          |
| Member – Personal Session     | 1:M            | Partial          | A member may book many personal sessions.                                                 |
| Trainer – Personal Session    | 1:M            | Partial          | A trainer conducts multiple sessions.                                                     |
| Personal Session – Attendance | 1:1            | Total            | Every session has one attendance record.                                                  |
| Member – Payment              | 1:M            | Total on Payment | Each payment belongs to one member; members may have many payments.                       |
| Personal Session – Payment    | 1:M (Optional) | Partial          | Session payments are linked to sessions; membership payments may not reference a session. |


### Assumptions
1.Every member has a unique Member_ID.


2.Every trainer has a unique Trainer_ID.


3.Members can enroll in multiple fitness programs.


# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

![ER Diagram](er_diagram_library.png)

### Entities and Attributes:

| Entity                 | Attributes (PK, FK)                                                              | Notes                              |
| ---------------------- | -------------------------------------------------------------------------------- | ---------------------------------- |
| **Member**             | **Member_ID (PK)**, Name, Phone, Email, Membership_Date                          | Stores library member details      |
| **Book**               | **Book_ID (PK)**, Title, Author, Category, Publisher                             | Stores book information            |
| **Loan**               | **Loan_ID (PK)**, Member_ID (FK), Book_ID (FK), Loan_Date, Due_Date, Return_Date | Tracks borrowed books              |
| **Event**              | **Event_ID (PK)**, Event_Name, Event_Date, Event_Time, Room_ID (FK)              | Stores library event details       |
| **Speaker**            | **Speaker_ID (PK)**, Name, Profession, Contact                                   | Stores guest speakers/authors      |
| **Event_Speaker**      | **Event_ID (PK, FK)**, **Speaker_ID (PK, FK)**                                   | Resolves many-to-many relationship |
| **Event_Registration** | **Member_ID (PK, FK)**, **Event_ID (PK, FK)**, Registration_Date                 | Members registering for events     |
| **Room**               | **Room_ID (PK)**, Room_Name, Capacity, Room_Type                                 | Rooms used for events and study    |
| **Fine**               | **Fine_ID (PK)**, Loan_ID (FK), Member_ID (FK), Amount, Paid_Status              | Stores overdue fines               |






Relationships and Constraints:

| Relationship    | Cardinality | Participation  | Notes                                                                           |
| --------------- | ----------- | -------------- | ------------------------------------------------------------------------------- |
| Member – Loan   | 1:M         | Partial        | A member may borrow many books.                                                 |
| Book – Loan     | 1:M         | Partial        | A book can be borrowed multiple times over time.                                |
| Member – Event  | M:N         | Partial        | Members can register for multiple events; each event can have many members.     |
| Event – Speaker | M:N         | Total on Event | Every event has at least one speaker; a speaker may participate in many events. |
| Room – Event    | 1:M         | Partial        | One room can host many events, but each event uses one room.                    |
| Loan – Fine     | 1:0..1      | Partial        | A loan may generate one fine if the book is returned late.                      |
| Member – Fine   | 1:M         | Partial        | A member can have multiple overdue fines.                                       |




### Assumptions
1.Every member has a unique Member_ID.


2.Every book has a unique Book_ID.


3.A member can borrow multiple books simultaneously.



# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

![ER Diagram](er_diagram_restaurant.png)

### Entities and Attributes:

| Entity          | Attributes (PK, FK)                                                                                                                          | Notes                                                        |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| **Customer**    | **Customer_ID (PK)**, Name, Phone, Email                                                                                                     | Stores customer details                                      |
| **Reservation** | **Reservation_ID (PK)**, Customer_ID (FK), Table_ID (FK), Waiter_ID (FK), Reservation_Date, Reservation_Time, No_of_Guests, Reservation_Type | Stores table reservations and walk-ins                       |
| **Table**       | **Table_ID (PK)**, Table_No, Capacity, Status                                                                                                | Stores restaurant table details                              |
| **Waiter**      | **Waiter_ID (PK)**, Name, Phone                                                                                                              | Stores waiter information                                    |
| **Order**       | **Order_ID (PK)**, Reservation_ID (FK), Order_Time                                                                                           | Stores customer orders                                       |
| **Dish**        | **Dish_ID (PK)**, Dish_Name, Price, Category_ID (FK)                                                                                         | Stores menu items                                            |
| **Category**    | **Category_ID (PK)**, Category_Name                                                                                                          | Categories such as Starter, Main Course, Dessert             |
| **Order_Item**  | **Order_ID (PK, FK)**, **Dish_ID (PK, FK)**, Quantity                                                                                        | Resolves many-to-many relationship between orders and dishes |
| **Bill**        | **Bill_ID (PK)**, Reservation_ID (FK), Food_Amount, Service_Charge, Total_Amount, Bill_Date                                                  | Stores billing details                                       |







### Relationships and Constraints

| Relationship           | Cardinality | Participation | Notes                                                                      |
| ---------------------- | ----------- | ------------- | -------------------------------------------------------------------------- |
| Customer – Reservation | 1:M         | Partial       | A customer can make multiple reservations or walk-ins.                     |
| Table – Reservation    | 1:M         | Partial       | A table can be reserved many times on different dates/times.               |
| Waiter – Reservation   | 1:M         | Partial       | One waiter can serve multiple reservations.                                |
| Reservation – Order    | 1:M         | Total         | Each reservation may have one or more food orders.                         |
| Order – Dish           | M:N         | Total         | Each order contains multiple dishes, and a dish can appear in many orders. |
| Category – Dish        | 1:M         | Total on Dish | Every dish belongs to exactly one category.                                |
| Reservation – Bill     | 1:1         | Total         | Each completed reservation generates one bill.                             |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
