# 📚 Library Management System using SQL  

## 📌 Project Overview  

The **Library Management System** is a structured database project built using SQL to efficiently manage a library's operations. It helps in organizing books, tracking issued and returned books, calculating overdue fines, and analyzing library usage patterns. The project involves advanced SQL techniques such as **CRUD operations, CTAS (Create Table As Select), joins, aggregation, and constraints** to ensure data integrity and efficient retrieval.  

## 📷 Entity-Relationship Diagram
![Library ERD](https://raw.githubusercontent.com/Imadmirza/Library-Management-System-using-SQL/master/library.jpg)

## 🎯 Objectives  

📖 **Database Design & Implementation**: Create a relational database with an optimized structure.  
🛠 **CRUD Operations**: Manage books, members, and employees with Insert, Update, Delete, and Select queries.  
📊 **CTAS (Create Table As Select)**: Generate new tables dynamically from existing data for reporting and analysis.  
🔍 **Advanced SQL Queries**: Perform data analytics such as overdue books, fine calculations, and frequent book issuers.  
📥 **Data Import & Export**: Support importing books and members' records from external Excel files.  
⚡ **Performance Optimization**: Ensure efficient indexing and query execution for better performance.  

---

## 🏛️ Database Schema  

The **Library Management System** consists of the following tables:  

### 📚 **1. Books Table (`books`)**  
Stores information about the books available in the library.  
- 🔑 `isbn` (Primary Key)  
- 📖 `book_title`  
- ✍️ `author`  
- 🎭 `genre`  
- 🔄 `status` (Available, Issued, Damaged, Lost)  

### 👤 **2. Members Table (`members`)**  
Stores details about the library members.  
- 🔑 `member_id` (Primary Key)  
- 🏷️ `member_name`  
- 📧 `email`  
- 📞 `phone_number`  
- 📅 `membership_date`  

### 📑 **3. Issued Books (`issued_status`)**  
Records books issued to members.  
- 🔑 `issued_id` (Primary Key)  
- 🆔 `issued_member_id` (Foreign Key → `members.member_id`)  
- 📚 `issued_book_isbn` (Foreign Key → `books.isbn`)  
- 🗓️ `issued_date`  
- ⏳ `due_date`  

### 🔄 **4. Return Status (`return_status`)**  
Tracks the return status of issued books.  
- 🔑 `return_id` (Primary Key)  
- 📑 `issued_id` (Foreign Key → `issued_status.issued_id`)  
- 📆 `return_date`  

### ⚠️ **5. Overdue Fines (`overdue_fines`)**  
Calculates fines for books returned late.  
- 🆔 `member_id` (Foreign Key → `members.member_id`)  
- ⏳ `overdue_books` (Total overdue books)  
- 💲 `total_fines` (Fine calculated at **$0.50 per day overdue**)  
 

---

## 📊 Key SQL Features Implemented  

### ✅ **CTAS Query for Overdue Books & Fine Calculation**  
```sql
CREATE TABLE overdue_fines AS  
SELECT ist.issued_member_id AS member_id,  
       COUNT(*) AS overdue_books,  
       SUM((CURRENT_DATE - ist.issued_date - 30) * 0.50) AS total_fines  
FROM issued_status AS ist  
LEFT JOIN return_status AS rs ON ist.issued_id = rs.issued_id  
WHERE rs.return_id IS NULL AND (CURRENT_DATE - ist.issued_date) > 30  
GROUP BY ist.issued_member_id;


## 📁 Project Structure
📂 Library-Management-System-SQL/
┣ 📜 app_library.sql – Database schema and table definitions
┣ 📜 insert_queries.sql – SQL queries for inserting initial data
┣ 📜 insert_queries2.sql – Additional data insertions
┣ 📜 lms_project_advanced_solution_2.sql – Advanced queries & reports
┣ 📜 SQL_complete_code_lib_management.sql – Complete SQL scripts
┣ 🖼️ library.jpg – Entity Relationship Diagram (ERD)
┣ 🖼️ library_erd.png – Graphical representation of the database schema
┗ 📜 README.md – Project documentation


