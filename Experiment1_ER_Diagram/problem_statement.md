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

<img width="1092" height="578" alt="image" src="https://github.com/user-attachments/assets/812ec466-80e3-4e07-82fb-2f6beb0ba11b" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|MEMBER |Member_ID (PK), Name, Membership_Type, Start_Date |Tracks all gym members |
|PROGRAM |Program_ID (PK), Program_Name, Type |Yoga, Zumba, Weight Training |
|TRAINER |Trainer_ID (PK), Name, Specialization |A trainer may take multiple programs|
|SESSION |Session_ID (PK), Member_ID (FK), Trainer_ID (FK), Date, Time |For personal training sessions |
|ATTENDANCE|Attendance_ID (PK), Session_ID (FK), Status (Present/Absent)|Records session attendance |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|Member–Program (Joins) |M:N |Partial|A member can join many programs |
|Program–Trainer (Assigned) |M:N |Total |Programs can have multiple trainers |
|Session–Attendance |1:M |Partial|Each session must have attendance record |

### Assumptions
Membership type determines allowed programs but not restricted in ER model. -Personal training sessions are optional. -Payments cover both membership fees and session fees.

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

<img width="1092" height="578" alt="image" src="https://github.com/user-attachments/assets/11a4d587-d105-4126-b904-5725d8f885ed" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | MemberID (PK), Name, Address, Phone, Email | Library members |
| Book | BookID (PK), Title, Author, Category, ISBN, PubYear | Books in collection |
| Loan | LoanID (PK), LoanDate, DueDate, ReturnDate, FineAmount, MemberID (FK), BookID (FK) | Tracks book borrowing |
| Event | EventID (PK), Name, Description, EventDate, StartTime, EndTime, RoomID (FK) | Library cultural events |
| Speaker | SpeakerID (PK), Name, Bio, ContactInfo | Event speakers/authors |
| Booking | BookingID (PK), BookingDate, StartTime, EndTime, RoomID (FK), MemberID (FK) | Study room reservations |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member–Book | M:N | Mandatory for Loan, Optional for Member/Book | Members borrow books |
| Member–Event | M:N | Mandatory for Registration, Optional for Member/Event | Members register for events |
| Event–Speaker | M:N | Mandatory for EventSpeaker, Optional for Event/Speaker | Events may have multiple speakers |
| Event–Room | 1:N | Mandatory for Event, Optional for Room | Each event in one room |
| Room–Booking | 1:N | Mandatory for Booking, Optional for Room | Rooms booked for study by members |

### Assumptions
- Overdue fines are stored per Loan record.
- BookCopy not modeled
- Rooms serve both events and study bookings.

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

<img width="1092" height="578" alt="image" src="https://github.com/user-attachments/assets/4954bf09-e7f3-4875-bd74-478ef9c7f1ad" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|CHEF| Chef_id (PK), Chef_name, Chef_salary|Each chef is uniquely identified by Chef_id. Prepares meals.|
|MEAL|meal_name (PK), meal_price|A meal is prepared by chefs, ordered by customers, and consists of ingredients.|
|INGREDIENTS| ing_name (PK), description|Each ingredient has a unique name and is linked to meals.|
|CUSTOMERS| cust_phone (PK), cust_name, cust_address |Customers place orders for meals.|
|SUPPLIER| S_id (PK), S_name, S_city |Suppliers attend to customers.|

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|prepares (CHEF–MEAL) |1:N|CHEF (total), MEAL (partial)|One chef can prepare many meals, but a meal is prepared by one chef.|
|orders (CUSTOMERS–MEAL)|M:N|Both partial|A customer can order many meals, and a meal can be ordered by many customers |
|consists of (MEAL–INGREDIENTS)|M:N|Both total| Each meal consists of multiple ingredients, and each ingredient can be part of many meals.|

### Assumptions
Each chef can prepare multiple meals, but a meal is prepared by only one chef. A customer can place multiple orders, and each order may include one or more meals. Each meal consists of one or more ingredients, and an ingredient may be used in multiple meals.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).
2. Identify entities, relationships, and attributes for each.
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.
4. Fill in all tables and assumptions for each scenario.
5. Export the completed Markdown (with diagrams) as **a single PDF**
