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
<img width="907" height="730" alt="Screenshot 2026-07-28 180148" src="https://github.com/user-attachments/assets/df1e4910-d71a-4353-bcc4-7a7e4b000476" />


### Entities and Attributes

| Entity                        | Attributes (PK, FK)                                                           | Notes                                          |
| ----------------------------- | ----------------------------------------------------------------------------- | ---------------------------------------------- |
| **MEMBER**                    | **PK:** member_id; membership_type, start_date, email                         | Stores gym member details                      |
| **PROGRAM**                   | **PK:** program_id; program_name, duration, fee                               | Stores fitness program details                 |
| **TRAINER**                   | **PK:** trainer_id; trainer_name, specialization, phone, email                | Stores trainer information                     |
| **MEMBER_PROGRAM**            | **PK/FK:** member_id, program_id; join_date                                   | Associative entity between Member and Program  |
| **TRAINER_PROGRAM**           | **PK/FK1:** trainer_id; **PK/FK2:** program_id                                | Associative entity between Trainer and Program |
| **PAYMENT**                   | **PK:** payment_id; **FK:** member_id; amount, payment_type                   | Stores member payment details                  |
| **PERSONAL_TRAINING_SESSION** | **PK:** session_id; **FK:** member_id, trainer_id; session_date, session_time | Stores personal training sessions              |
| **ATTENDANCE**                | **PK:** attendance_id; **FK:** session_id, member_id; status                  | Stores member attendance for sessions          |


### Relationships and Constraints

| Relationship                           | Cardinality | Participation                      | Notes                                                 |
| -------------------------------------- | ----------- | ---------------------------------- | ----------------------------------------------------- |
| MEMBER – MEMBER_PROGRAM                | 1 : M       | Member Program depends on Member   | One member can join many programs                     |
| PROGRAM – MEMBER_PROGRAM               | 1 : M       | Member Program depends on Program  | One program can have many members                     |
| TRAINER – TRAINER_PROGRAM              | 1 : M       | Trainer Program depends on Trainer | One trainer can conduct multiple programs             |
| PROGRAM – TRAINER_PROGRAM              | 1 : M       | Trainer Program depends on Program | A program can have multiple trainers                  |
| MEMBER – PAYMENT                       | 1 : M       | Payment depends on Member          | One member can make many payments                     |
| MEMBER – PERSONAL_TRAINING_SESSION     | 1 : M       | Session depends on Member          | One member can attend many personal training sessions |
| TRAINER – PERSONAL_TRAINING_SESSION    | 1 : M       | Session depends on Trainer         | One trainer can conduct many sessions                 |
| PERSONAL_TRAINING_SESSION – ATTENDANCE | 1 : M       | Attendance depends on Session      | A session can have multiple attendance records        |
| MEMBER – ATTENDANCE                    | 1 : M       | Attendance depends on Member       | A member can have many attendance records             |


### Assumptions
1. A member can enroll in multiple fitness programs, and each program can have multiple members.
2. A trainer can be assigned to multiple programs, and a program may have multiple trainers.
3. Each personal training session is conducted by one trainer for a member.
4. A member can make multiple payments.
5. The attendance status is recorded as present or absent for each session.

---

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
<img width="1177" height="698" alt="Screenshot 2026-07-23 083238" src="https://github.com/user-attachments/assets/7fb29372-c188-499a-a0f9-620204610006" />


### Entities and Attributes

| Entity            | Attributes (PK, FK)                                                                                                      | Notes                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------- |
| **MEMBER**        | **PK:** member_id; first_name, last_name, membership_date, date_of_birth, phone, email, address, membership_type, status | Stores library member details                |
| **BOOK**          | **PK:** book_id; isbn, title, author, category_id, publisher, publication_year, availability, total_copies, status       | Stores book information                      |
| **CATEGORY**      | **PK:** category_id; category_name, description                                                                          | Stores book categories                       |
| **AUTHOR**        | **PK:** author_id; author_name, bio                                                                                      | Stores author details                        |
| **BOOK_LOAN**     | **PK:** loan_id; **FK:** member_id, book_id; loan_date, due_date, return_date, status                                    | Stores book borrowing transactions           |
| **BOOK_AUTHOR**   | **PK/FK1:** book_id; **PK/FK2:** author_id                                                                               | Associative entity between Book and Author   |
| **EVENT**         | **PK:** event_id; event_title, event_description, event_date, start_time, end_time, event_type, capacity, status         | Stores library event details                 |
| **MEMBER_EVENT**  | **PK/FK1:** member_id; **PK/FK2:** event_id; registration_date, status                                                   | Stores member registration for events        |
| **FINE**          | **PK:** fine_id; **FK:** member_id; fine_amount, fine_date, payment_status, payment_date                                 | Stores fines issued to members               |
| **SPEAKER**       | **PK:** speaker_id; speaker_name, bio, phone, email                                                                      | Stores speaker details                       |
| **EVENT_SPEAKER** | **PK/FK1:** event_id; **PK/FK2:** speaker_id; role                                                                       | Associative entity between Event and Speaker |
| **ROOM**          | **PK:** room_id; room_name, room_type, capacity, location, status                                                        | Stores library room details                  |
| **EVENT_ROOM**    | **PK:** event_room_id; **FK:** event_id, room_id; start_time, end_time                                                   | Stores room allocation for events            |
| **ROOM_BOOKING**  | **PK:** booking_id; **FK:** room_id, booked_by; purpose, booking_date, start_time, end_time, status                      | Stores room booking details                  |

### Relationships and Constraints

| Relationship            | Cardinality | Participation                    | Notes                                                  |
| ----------------------- | ----------- | -------------------------------- | ------------------------------------------------------ |
| MEMBER – BOOK_LOAN      | 1 : M       | Book Loan depends on Member      | One member can borrow many books                       |
| BOOK – BOOK_LOAN        | 1 : M       | Book Loan depends on Book        | One book can have many loan records over time          |
| CATEGORY – BOOK         | 1 : M       | Book belongs to one Category     | One category contains many books                       |
| BOOK – BOOK_AUTHOR      | 1 : M       | Book Author depends on Book      | Supports multiple authors per book                     |
| AUTHOR – BOOK_AUTHOR    | 1 : M       | Book Author depends on Author    | Supports multiple books per author                     |
| MEMBER – MEMBER_EVENT   | 1 : M       | Member Event depends on Member   | A member can register for many events                  |
| EVENT – MEMBER_EVENT    | 1 : M       | Member Event depends on Event    | An event can have many members                         |
| MEMBER – FINE           | 1 : M       | Fine depends on Member           | A member can receive multiple fines                    |
| EVENT – EVENT_SPEAKER   | 1 : M       | Event Speaker depends on Event   | An event can have multiple speakers                    |
| SPEAKER – EVENT_SPEAKER | 1 : M       | Event Speaker depends on Speaker | A speaker can participate in multiple events           |
| EVENT – EVENT_ROOM      | 1 : M       | Event Room depends on Event      | An event can use rooms                                 |
| ROOM – EVENT_ROOM       | 1 : M       | Event Room depends on Room       | A room can host multiple events over time              |
| ROOM – ROOM_BOOKING     | 1 : M       | Room Booking depends on Room     | A room can have many bookings                          |
| MEMBER – ROOM_BOOKING   | 1 : M       | Room Booking linked to Member    | The `booked_by` field is assumed to refer to member_id |


### Assumptions
1. A book may have multiple authors, and an author may write multiple books.
2. A member may borrow the same book multiple times on different dates.
3. Members can register for multiple events, and each event can have many members.
4. A room cannot have overlapping confirmed bookings or event allocations for the same time slot.
5. The booked_by attribute in ROOM_BOOKING is assumed to be a foreign key referencing MEMBER.member_id.

---

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
<img width="1402" height="1122" alt="image" src="https://github.com/user-attachments/assets/c211ecac-4036-4954-b632-6bc232ae7bfd" />


### Entities and Attributes

| Entity          | Attributes (PK, FK)                                                                                                                | Notes                                     |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| **CUSTOMER**    | **PK:** customer_id; first_name, last_name, phone, email, address, member_status                                                   | Stores customer details                   |
| **RESERVATION** | **PK:** reservation_id; **FK:** customer_id; reservation_date, reservation_time, no_of_guests, reservation_type, status            | Stores advance or walk-in reservations    |
| **TABLE**       | **PK:** table_id; table_number, capacity, location, status                                                                         | Stores restaurant table details           |
| **WAITER**      | **PK:** waiter_id; waiter_name, phone, section                                                                                     | Stores waiter information                 |
| **ORDER**       | **PK:** order_id; **FK:** reservation_id, waiter_id; order_time, status                                                            | Stores customer orders                    |
| **ORDER_ITEM**  | **PK/FK1:** order_id; **PK/FK2:** dish_id; quantity, unit_price, subtotal                                                          | Associative entity between Order and Dish |
| **DISH**        | **PK:** dish_id; **FK:** category_id; dish_name, description, price, status                                                        | Stores menu dish details                  |
| **CATEGORY**    | **PK:** category_id; category_name, description                                                                                    | Stores dish categories                    |
| **BILL**        | **PK:** bill_id; **FK:** reservation_id; bill_date, food_total, service_charge, tax_amount, discount, total_amount, payment_status | Stores billing details                    |
| **PAYMENT**     | **PK:** payment_id; **FK:** bill_id; payment_date, payment_method, amount_paid, payment_status                                     | Stores payment information                |


### Relationships and Constraints

| Relationship           | Cardinality | Participation                     | Notes                                                          |
| ---------------------- | ----------- | --------------------------------- | -------------------------------------------------------------- |
| CUSTOMER – RESERVATION | 1 : M       | Reservation depends on Customer   | One customer can make many reservations                        |
| RESERVATION – TABLE    | M : 1       | Reservation assigned to one Table | A table can be associated with multiple reservations over time |
| RESERVATION – ORDER    | 1 : M       | Order depends on Reservation      | One reservation can have multiple orders                       |
| WAITER – ORDER         | 1 : M       | Order assigned to one Waiter      | One waiter can handle many orders                              |
| ORDER – ORDER_ITEM     | 1 : M       | Order Item depends on Order       | One order contains many order items                            |
| DISH – ORDER_ITEM      | 1 : M       | Order Item depends on Dish        | One dish can appear in many order items                        |
| CATEGORY – DISH        | 1 : M       | Dish belongs to one Category      | One category contains many dishes                              |
| RESERVATION – BILL     | 1 : 1       | Bill associated with Reservation  | Each reservation generates one bill                            |
| BILL – PAYMENT         | 1 : M       | Payment depends on Bill           | A bill may have multiple payment records                       |


### Assumptions
1. A reservation is made by exactly one customer and is assigned to one table.
2. A table may be used for many reservations at different times.
3. An order must be linked to one reservation and one waiter.
4. An order can contain multiple dishes, and a dish can appear in multiple orders.
5. The displayed RESERVATION–ORDER–WAITER connections indicate waiter assignment through the Order entity.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
