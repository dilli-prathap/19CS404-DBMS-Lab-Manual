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
<img width="1855" height="926" alt="502671917-d474307b-16a9-4382-a0df-0f8e3dd781c5" src="https://github.com/user-attachments/assets/24a27776-8d19-4c3a-848d-d560e2419caa" />


### Entities and Attributes
| **Entity**           | **Attributes (PK, FK)**                                                                  | **Notes**                                    |
| -------------------- | ---------------------------------------------------------------------------------------- | -------------------------------------------- |
| **Member**           | Member ID **(PK)**, Member Name, Membership Type, Start Date                             | Each member has a unique Member ID           |
| **Program**          | Program ID **(PK)**, Program Name                                                        | Each fitness program has a unique Program ID |
| **Trainer**          | Trainer ID **(PK)**, Trainer Name, Trainer Duty Time                                     | Each trainer has a unique Trainer ID         |
| **Training Session** | Session ID **(PK)**, Session Date, Session Time, Trainer ID **(FK)**, Member ID **(FK)** | Links members and trainers for each session  |
| **Attendance**       | Attendance ID **(PK)**, Member ID **(FK)**, Status                                       | Tracks attendance for members                |
| **Payment**          | Payment ID **(PK)**, Member ID **(FK)**, Amount                                          | Tracks each payment transaction              |


### Relationships and Constraints

| **Relationship**               | **Cardinality**                  | **Participation** | **Notes**                              |
| ------------------------------ | -------------------------------- | ----------------- | -------------------------------------- |
| **Attends**                    | Member : N, Program : N          | Total (mandatory) | Members may attend multiple programs   |
| **Teach Programs**             | Trainer : N, Program : N         | Partial           | Trainers may teach multiple programs   |
| **Attend Sessions**            | Member : N, Training Session : N | Partial           | Members may attend several sessions    |
| **Allotted to (Trainer)**      | Member : 1, Trainer : N          | Partial           | Trainers allotted to several members   |
| **Mark Attendance**            | Member : 1, Attendance : N       | Total             | Attendance is tracked per member       |
| **Pay for Membership**         | Member : 1, Payment : N          | Partial           | Members can have multiple payments     |
| **Training Session - Trainer** | Trainer : 1, Session : N         | Total             | Each session supervised by one trainer |
| **Training Session - Member**  | Member : 1, Session : N          | Total             | Each session attended by one member    |


### Assumptions
- Each entity’s primary key is unique and referenced by their respective foreign key.
- A Training Session is assumed to involve one member and one trainer, but can be extended for group sessions.
- Attendance marking is performed per session or per day for each member.
- Payment details are linked directly to individual members.
- Trainers may be allotted multiple members and can teach multiple programs.

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
<img width="1728" height="828" alt="502669694-7bf4e1ec-249a-498a-bca6-a061632027da" src="https://github.com/user-attachments/assets/024456dc-f478-4e76-ac06-746bfbeb19c6" />


### Entities and Attributes

| **Entity**  | **Attributes (PK, FK)**                                                                       | **Notes**                        |
| ----------- | --------------------------------------------------------------------------------------------- | -------------------------------- |
| **MEMBER**  | member id **(PK)**, name, phone no., membership type                                          | Each member has a unique ID      |
| **BOOK**    | book id **(PK)**, book title, category, availability                                          | Each book has a unique ID        |
| **BORROW**  | borrow id **(PK)**, member id **(FK)**, book id **(FK)**, loan date, return date, fine amount | Links members and borrowed books |
| **EVENT**   | event id **(PK)**, event name, event date, event type                                         | Each event has a unique ID       |
| **ROOM**    | room id **(PK)**, room name, location, capacity                                               | Each room has a unique ID        |
| **SPEAKER** | speaker id **(PK)**, name, expertise, contact number                                          | Each speaker has a unique ID     |


### Relationships and Constraints

| **Relationship**                | **Cardinality**        | **Participation** | **Notes**                                                      |
| ------------------------------- | ---------------------- | ----------------- | -------------------------------------------------------------- |
| **Members have borrow records** | MEMBER : 1, BORROW : N | Total             | Each member can have multiple borrow records                   |
| **Book is borrowed**            | BOOK : 1, BORROW : N   | Partial           | Books can be borrowed multiple times                           |
| **Member register event**       | MEMBER : N, EVENT : N  | Optional          | Members can register for multiple events                       |
| **Participate**                 | EVENT : N, SPEAKER : N | Optional          | Events may feature multiple speakers                           |
| **Event held in room**          | EVENT : 1, ROOM : 1    | Total             | Events are held in exactly one room; each room may host events |


### Assumptions
- Each primary key is unique in its entity and properly referenced by foreign keys.
- One borrow event links one member and one book; multiple borrow events per member or book are allowed.
- Event registration by members can be many-to-many.
- Multiple speakers can participate in a single event.
- Each event is held in exactly one room, though rooms may host many events.
- Book availability is managed by the system and updated upon each borrow/return.
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

### ER Diagram
<img width="1850" height="875" alt="502669986-4c9ca114-cbdc-4414-a4c0-ecbf7870193d" src="https://github.com/user-attachments/assets/2876ea1b-b5ba-4eb2-a64f-a932949de81f" />

### Entities and Attributes

| **Entity**      | **Attributes (PK, FK)**                                                              | **Notes**                                              |
| --------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------ |
| **CUSTOMER**    | customer id **(PK)**, name, email, phone no.                                         | Each customer has a unique ID                          |
| **RESERVATION** | reservation id **(PK)**, customer id **(FK)**, time, no. of guests, date             | Each reservation links to a customer                   |
| **BILL**        | bill id **(PK)**, reservation id **(FK)**, waiter id **(FK)**, bill amount, bill tax | Each bill refers to a reservation, handled by a waiter |
| **WAITER**      | waiter id **(PK)**, name, duty time                                                  | Each waiter has a unique ID                            |
| **ORDER**       | order id **(PK)**, reservation id **(FK)**, order date, order amount                 | Each order is linked to a reservation                  |
| **DISH**        | dish id **(PK)**, name, category, price                                              | Each dish has a unique ID                              |


### Relationships and Constraints

| **Relationship**      | **Cardinality**                       | **Participation** | **Notes**                                                                |
| --------------------- | ------------------------------------- | ----------------- | ------------------------------------------------------------------------ |
| **Makes reservation** | CUSTOMER : 1, RESERVATION : N         | Mandatory         | Each customer can make multiple reservations                             |
| **Generates bill**    | RESERVATION : 1, BILL : 1, WAITER : 1 | Mandatory         | For every reservation, there is exactly one bill, handled by one waiter  |
| **Served by**         | RESERVATION : 1, WAITER : N           | Mandatory         | Multiple reservations can be handled by the same waiter                  |
| **Places order**      | RESERVATION : 1, ORDER : N            | Optional          | Each reservation can have multiple orders                                |
| **Includes**          | ORDER : N, DISH : N                   | Optional          | Orders can include multiple dishes, and dishes may appear in many orders |


### Assumptions
- Each primary key is unique and referenced as foreign keys where applicable.
- A reservation is associated with exactly one customer, and may be handled by one or more waiters.
- Orders are associated with reservations; each order can include multiple dishes.
- A bill is generated per reservation, and handled by a specific waiter.
- Cardinality is mostly one-to-many from customer to reservation/orders, and many-to-many from orders to dishes.
- All data entities and relationships reflect the diagram structure and relational schema.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
