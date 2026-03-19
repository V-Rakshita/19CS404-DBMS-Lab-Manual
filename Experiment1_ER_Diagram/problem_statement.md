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
<img width="625" height="382" alt="image" src="https://github.com/user-attachments/assets/105d491c-823b-42b8-84ff-cdde77e9a7f6" />



### Entities and Attributes

| Entity     | Attributes                          | Notes (PK, FK, etc.)                                                                 |
|------------|-------------------------------------|--------------------------------------------------------------------------------------|
| Member     | Name, Start Date, Membership Type*  | PK: MemberID (Implied).   |
| Program    | PID, Name                           | PK: PID.                                                                            |
| Trainer    | Name, Program*                      | PK: TrainerID (Implied).                    |
| Session    | SID, Session Type                   | PK: SID.                                                                            |
| Payment    | Amount                              | PK: PaymentID (Implied).                                                            |
| Attendance | Date, Pres/Ab                       | PK: AttendanceID (Implied).                  |

### Relationships and Constraints

| Relationship       | Entities Involved     | Cardinality | Participation        | Notes                                                                 |
|--------------------|----------------------|-------------|----------------------|------------------------------------------------------------------------|
| JOIN              | Member - Program     | M:N         | Total (Member)       | A member can join many programs; programs have many members.          |
| BOOK              | Member - Session     | M:N         | Partial              | Members can book many sessions; sessions can have many members.       |
| Assigned          | Program - Trainer    | M:N         | Total (Trainer)      | Programs can have multiple trainers; trainers are assigned to many.   |
| Type of Session   | Session - Trainer    | M:N         | Partial              | A trainer leads many sessions; sessions involve many trainers (N:M).  |
| P/A               | Session - Attendance | 1:1         | Total (Attendance)   | One attendance record is generated per session.                       |
| Membership Pmt    | Member - Payment     | 1:N         | Partial              | One member makes many membership payments.                            |
| Session Pmt       | Session - Payment    | 1:N         | Partial              | One session can have multiple associated payments.                    |

### Assumptions
- **Implicit Primary Keys**  
  Several entities (Member, Trainer, Payment) lack explicit primary keys. It is assumed unique IDs (e.g., MemberID) will be created in the physical schema.

- **Missing Attributes**  
  "Membership Type" is required but not shown in the Member entity. This is important for billing logic.

- **Type of Session Relationship**  
  The M:N relationship between Trainer and Session suggests multiple trainers can conduct a single session.

- **Payment Structure**  
  The separation of Membership Payment and Session Payment implies a hybrid pricing model (subscription + pay-per-session).

- **Attendance Tracking**  
  The 1:1 Session–Attendance relationship suggests attendance is tracked per session as a whole, not per individual member.

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
  
<img width="628" height="471" alt="image" src="https://github.com/user-attachments/assets/4323c525-f1e4-4444-902a-ee041deaa7dc" />


### Entities and Attributes

| Entity   | Attributes                     | Notes (PK, FK)                          |
|----------|--------------------------------|------------------------------------------|
| Members  | Name, MemberID*               | PK: MemberID (Implied).                 |
| Books    | Title, Author, Category       | PK: ISBN/BookID (Implied).              |
| Event    | EventName*, Date*             | PK: EventID (Implied).                  |
| Speaker  | SpeakerName*                  | PK: SpeakerID (Implied).                |
| Room     | RoomNumber*                   | PK: RoomID (Implied).                   |
| Loan     | Begin, Due                    | PK: LoanID (Implied).                   |
| Fine     | Amount*                       | PK: FineID (Implied).                   |

### Relationships and Constraints

| Relationship   | Entities Involved   | Cardinality | Participation     | Notes                                                                 |
|----------------|--------------------|-------------|------------------|------------------------------------------------------------------------|
| Initiates      | Members - Loan     | 1:N         | Total (Loan)     | One member can have many loans.                                       |
| has            | Loan - Books       | N:N         | Total (Loan)     | A loan transaction can involve multiple books.                        |
| Reserves       | Members - Books    | M:N         | Partial          | Members can place many reservations; books can have many reservations.|
| Registers for  | Members - Event    | N:M         | Partial          | Multiple members register for multiple events.                        |
| Conduct        | Speaker - Event    | M:N         | Total (Event)    | Events require at least one speaker.                                  |
| Held in        | Event - Room       | N:1         | Total (Event)    | Many events can be scheduled in one room (at different times).        |
| Generate       | Loan - Fine        | 1:1         | Partial          | A specific loan generates one fine if overdue.                        |
| Includes       | Books - Fine       | N:1         | Partial          | Fines are linked to the specific books involved.                      |

### Assumptions
- **Loan vs. Reserve**  
  The system distinguishes between a **Loan** (active borrowing of books) and a **Reserve** (placing a hold for future use).

- **Speaker Roles**  
  The **Conduct** relationship is M:N, meaning an event can have multiple speakers (e.g., panels), and a speaker can participate in multiple events.

- **Fine Generation**  
  The 1:1 relationship between Loan and Fine implies each fine is uniquely associated with a specific loan instance.

- **Room Usage**  
  Although rooms are mentioned for "study" in requirements, the diagram only links rooms to events. Study room booking would likely follow a similar structure to event scheduling.

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
<img width="628" height="518" alt="image" src="https://github.com/user-attachments/assets/96f9a214-aa0b-4da8-9591-967eda751d0e" />
 


### Entities and Attributes

| Entity      | Attributes                          | Notes (PK, FK)        |
|-------------|-------------------------------------|------------------------|
| Customer    | Customer ID, Customer Name, Ph no   | PK: Customer ID        |
| Reservation | Reservation ID, Date, Time, Guests* | PK: Reservation ID     |
| Orders      | OrderID, Dishes*, Categories*       | PK: OrderID            |
| Table       | TableID, Capacity                   | PK: TableID            |
| Waiters     | Waiter ID, Name                     | PK: Waiter ID          |
| Bill        | BillID, Amount                      | PK: BillID             |

### Relationships and Constraints

| Relationship | Entities Involved       | Cardinality | Participation     | Notes                                                                 |
|--------------|------------------------|-------------|------------------|------------------------------------------------------------------------|
| makes        | Customer - Reservation | 1:N         | Partial          | One customer can make many reservations over time.                    |
| places       | Customer - Orders      | 1:N         | Partial          | Customers place orders (often linked via reservation).                |
| reserves     | Reservation - Table    | 1:1         | Total            | Each reservation is assigned to exactly one specific table.           |
| serves       | Waiters - Reservation  | 1:N         | Total            | A waiter can serve multiple reservations/tables during a shift.       |
| generates    | Reservation - Bill     | 1:1         | Total (Bill)     | One reservation results in exactly one final bill.                    |

### Assumptions
- **Walk-ins**  
  Walk-in customers can be modeled as "instant" reservations so that a table and waiter can still be assigned within the system.

- **Order Linking**  
  Although the diagram shows Customer placing Orders, in practice orders are tied to reservations. Therefore, `ReservationID` should be included as a foreign key in the Orders table.

- **Dish Details**  
  The Orders entity is simplified. In a real system, an `Order_Items` associative table would be required to support multiple dishes per order.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
