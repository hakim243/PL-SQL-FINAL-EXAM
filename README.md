
NAMES: NDJIBU KADIOBO JUGE
GROUP: WEDNESDAY 6PM
ID:25273
                                                PROBLEME STATEMENT: LIBRARY MANAGEMENT SYSTEM



PHASE II

📘 Business Process Modeling Explanation – Library Management System
1. Define the Scope
Business Process Modeled:
The Book Borrowing and Return Workflow within a Library Management System.
Relevance to MIS:
This process integrates inventory management, user services, and reporting to support operational decision-making. By leveraging MIS, the system can manage resources (books), track user behavior (borrow/return trends), and optimize staff workflows.
Objectives and Expected Outcomes:
•	Automate the manual process of borrowing and returning books.
•	Reduce errors and delays caused by paper-based systems.
•	Provide real-time access to inventory status.
•	Enable librarians to make informed decisions on procurement and overdue handling.
________________________________________
2. Identify Key Entities
Entity	Role
Library Member	Initiates borrow or return request; receives system notifications.
Librarian	Approves transactions, manages inventory, handles overdue penalties.
Library System (Database & Interface)	Central system that handles transactions, inventory, and reports.
Admin	Manages system settings, adds/removes books, oversees user permissions.
MIS Reporting System	Analyzes system logs and usage patterns to generate decision-support reports.
________________________________________
3. Use of Swimlanes
•	Swimlane 1: Library Member
o	Searches for books
o	Requests to borrow/return
o	Receives due-date alerts and return confirmations
•	Swimlane 2: Librarian
o	Checks request validity
o	Updates inventory and confirms transaction
o	Applies overdue penalties
•	Swimlane 3: System/Database
o	Validates member status and book availability
o	Updates inventory status automatically
o	Logs transactions for MIS
•	Swimlane 4: Admin
o	Adds/removes books from inventory
o	Updates user permissions
o	Runs system health checks
________________________________________
4. UML/BPMN Notation Key Features in Diagram
•	Start Point: User logs in
•	Activities/Tasks: Search book, verify user, approve request, update inventory
•	Decision Gateway: Book available? Overdue? User eligible?
•	Data Objects: Book records, user info, system logs
•	End Point: Transaction completed or failed due to unavailability/violation
•	System Interactions: Inventory updated, reports generated
________________________________________
5. Logical Flow of the Process
1.	Member Login & Book Search → System fetches records
2.	Borrow Request Initiation → System checks availability
3.	Librarian Review & Approval → If approved → System logs transaction
4.	Return Process → System verifies return and checks for delay
5.	Penalty Applied if Overdue → System updates member status
6.	MIS Reporting Tool → Generates usage reports for Admin
________________________________________
6. Explanation of Diagram and MIS Support
Main Components & Interactions:
The flowchart showcases how different users interact with the system:
•	Members request book loans.
•	Librarians and admins control and validate these requests.
•	The system updates data and generates reports.
How the Process Supports MIS Functions:
•	Improves Decision-Making: By providing real-time reports on popular books, late returns, and stock levels.
•	Streamlines Operations: Automates repetitive tasks like inventory updates and alerts.
•	Enables Forecasting: Insights from MIS help librarians prepare for demand surges and optimize procurement.
Importance for Organizational Efficiency:
•	Reduces dependency on manual records.
•	Enhances reliability, consistency, and transparency.
•	Supports data-driven planning and user satisfaction.
•	Reduces book misplacement, lost data, and delays.
________________________________________
7. Tools Used
•	Diagram was created using Draw.io.
•	Notations followed BPMN standards, with swimlanes for role clarity

Diagram



![ChatGPT Image May 24, 2025, 10_16_38 AM](https://github.com/user-attachments/assets/8b542a3a-b9bb-4188-99a9-55ab59295c6d)



PHASE III

1. 🔷 Entity-Relationship (ER) Model
2. 
✅ Entities and Attributes
Entity	Attributes	PK / FK	Data Type / Constraints
User	User_ID, Name, Email, Phone, Address, Role (Member/Librarian/Admin), Status	PK: User_ID	INT (PK), VARCHAR, ENUM, NOT NULL
Book	Book_ID, Title, Author, ISBN, Category, Status (Available/Borrowed), Shelf_No	PK: Book_ID	INT (PK), VARCHAR, NOT NULL, UNIQUE (ISBN)
Transaction	Transaction_ID, User_ID, Book_ID, Date_Borrowed, Due_Date, Date_Returned, Status	PK: Transaction_ID
FK: User_ID, Book_ID	INT (PK, FK), DATE, ENUM, NOT NULL
Penalty	Penalty_ID, Transaction_ID, Amount, Reason, Status (Paid/Unpaid)	PK: Penalty_ID
FK: Transaction_ID	INT (PK), DECIMAL, VARCHAR, ENUM, NOT NULL
Admin_Log	Log_ID, Admin_ID, Action, Timestamp	PK: Log_ID
FK: Admin_ID	INT (PK), TEXT, TIMESTAMP
________________________________________
2. 🔗 Relationships & Constraints
🔄 Relationships
Relationship	Cardinality	Explanation
User → Transaction	1 to Many	A user can have many transactions.
Book → Transaction	1 to Many	A book can appear in multiple transactions (borrowed/returned multiple times).
Transaction → Penalty	1 to 0 or 1	A transaction may result in one penalty, or none.
Admin (User with Role) → Admin_Log	1 to Many	An admin can perform multiple system actions, logged in Admin_Log.
⚙️ Constraints
Table	Constraint Type	Constraint Details
User	NOT NULL, UNIQUE	Email must be unique, Role must be ENUM (Member/Admin)
Book	NOT NULL, UNIQUE	ISBN must be unique, Status default is 'Available'
Transaction	CHECK, NOT NULL	Status must be ('Borrowed', 'Returned', 'Overdue')
Penalty	CHECK, DEFAULT	Status default is 'Unpaid'
Admin_Log	NOT NULL	Timestamp is auto-generated
________________________________________
3. 🧩 Normalization (Up to 3NF)
✅ First Normal Form (1NF)
•	All attributes are atomic (e.g., no multiple authors or emails in one field).
•	Each entity has a unique primary key.
✅ Second Normal Form (2NF)
•	All non-key attributes are fully functionally dependent on the entire primary key (especially in Transaction and Penalty).
✅ Third Normal Form (3NF)
•	No transitive dependency (e.g., Penalty details depend directly on Transaction, not on User or Book indirectly).
•	Log actions are stored separately in Admin_Log instead of embedded in User.
________________________________________
4. 🔍 Handling Data Scenarios
Scenario	Handled By
User borrows multiple books	One-to-many relationship in Transaction table
Overdue return leads to penalty	Penalty table linked to Transaction
Book status updates upon borrow/return	Status field in Book updated via Transaction logic
Admin deletes a book	Cascading or restricted based on Transaction FK rules
System generates usage reports	Admin views logs and transactions using joins/queries
________________________________________
5. 📝 Presentation & Feedback Preparation
Your ER model is now:
•	Fully normalized (3NF)
•	Mapped clearly to business processes from Phase II
•	Documented with relationships, constraints, and data types
•	Capable of supporting MIS reporting, inventory updates, and penalties


![ChatGPT Image May 24, 2025, 01_30_56 PM](https://github.com/user-attachments/assets/e664ff95-cd28-47d3-b4e1-626fd9907fa3)



PHASE:IV. 

PLUGGABLE DATABASE CREATION

![Screenshot 2025-05-25 081548](https://github.com/user-attachments/assets/a4b3839b-e519-4a68-90b9-f3781f18af64)

OEM PERFROMANCE:

![Screenshot 2025-05-25 081854](https://github.com/user-attachments/assets/96d5fbdf-1d8c-401b-a869-26791a15020a)
![Screenshot 2025-05-25 080459](https://github.com/user-attachments/assets/daefa1b9-ffd0-47ea-bc69-86e7083d2d84)
![Screenshot 2025-05-25 080507](https://github.com/user-attachments/assets/0a6d1478-b8a6-4b21-bd6e-334bdfea8c45)


V. PHASE: TABLE IMPLEMENTATION AND DATA INSERTION

![Screenshot 2025-05-25 061509](https://github.com/user-attachments/assets/e3958e1d-3ef0-4003-956a-133950b4928a)
![Screenshot 2025-05-25 061546](https://github.com/user-attachments/assets/25b480a6-3688-4d37-adeb-67a5419c43b2)
![Screenshot 2025-05-25 061615](https://github.com/user-attachments/assets/87ecda35-d3b2-4b4b-aec7-9580c53413b8)
![Screenshot 2025-05-25 061652](https://github.com/user-attachments/assets/6890dc7d-1233-4a11-8407-145518a1f927)
![Screenshot 2025-05-25 061628](https://github.com/user-attachments/assets/017ec87a-f29d-452d-8ce0-475f7b8d67e2)


✅ PHASE VI: Database Interaction and Transactions
________________________________________
1.	INSERT INTO BOOK VALUES (
  106, 
  'Python for Data Science', 
  'Jake VanderPlas', 
  'O''Reilly', 
  2018, 
  5, 
  5
);
UPDATE BOOK SET copies_available = 4 WHERE book_id = 106;
SELECT * FROM BOOK WHERE book_id = 106;


Add column and update things which are inside


SQL> SELECT column_name
  2  FROM all_tab_columns
  3  WHERE table_name = 'LIBRARIAN'
  4    AND column_name = 'PHONE';

COLUMN_NAME
--------------------------------------------------------------------------------
PHONE

SQL> UPDATE LIBRARIAN
  2  SET phone = '0788123456'
  3  WHERE librarian_id = 501;

1 row updated.

SQL>
SQL> UPDATE LIBRARIAN
  2  SET phone = '0788001122'
  3  WHERE librarian_id = 502;

1 row updated.

SQL> SELECT librarian_id, full_name, phone
  2  FROM LIBRARIAN;

LIBRARIAN_ID
------------
FULL_NAME
--------------------------------------------------------------------------------
PHONE
--------------------
         501
Patrick Ndjibu
0788123456

         502
Grace Uwimana
0788001122

LIBRARIAN_ID
------------
FULL_NAME
--------------------------------------------------------------------------------
PHONE
--------------------


SQL>



2. Problem Statement Using Window Functions
Problem: "Analyze student borrowing frequency and rank students based on how many books they’ve borrowed."
SELECT 
    s.student_id,
    s.first_name || ' ' || s.last_name AS student_name,
    COUNT(br.book_id) AS total_books_borrowed,
    RANK() OVER (ORDER BY COUNT(br.book_id) DESC) AS borrow_rank
FROM 
    STUDENT s
JOIN 
    BORROW_RECORD br ON s.student_id = br.student_id
GROUP BY 
    s.student_id, s.first_name, s.last_name;
   
![Screenshot 2025-05-25 063251](https://github.com/user-attachments/assets/82573f81-b0d8-4e23-996a-b078890355b2)
![Screenshot 2025-05-25 063339](https://github.com/user-attachments/assets/a2031806-c376-494b-8d66-203db42d52b4)
![Screenshot 2025-05-25 064217](https://github.com/user-attachments/assets/b5648b29-2c88-4e68-a1a9-6d5ea94eeda9)
![Screenshot 2025-05-25 064628](https://github.com/user-attachments/assets/ad281641-5478-4e66-8379-389651f84a25)
![Screenshot 2025-05-25 064637](https://github.com/user-attachments/assets/6f0d07ea-d08f-4f68-a6bd-790e9017fcd3)





