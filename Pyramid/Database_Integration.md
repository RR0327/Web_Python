# Database Integration: Learn how to integrate a database with Pyramid for persistence (স্থায়িত্ব).

This means:

```text
Pyramid app + Database = Data can be saved permanently
```

> Without database:

```text
User writes data → App closes → Data lost
```

> With database:

```text
User writes data → Data saved in database → Can be used later
```

---

## 1. Why Database is Needed in Pyramid?

A real web app needs to store data like:

```text
Users
Login information
Blog posts
Products
Orders
Comments
Messages
Student records
```

Example:

```text
A user creates a blog post.
The post should still exist tomorrow.
So we need a database.
```

That is called **persistence**.

---

## 2. What Pyramid Uses for Database?

Pyramid itself does **not force one database system**.

This is one big difference from Django.

Means :

> In **Django**:

```bash
Django has its own built-in ORM style.
```

In Pyramid:

```text
Pyramid gives flexibility.
You choose your database tool.
```

The Pyramid community strongly supports **SQLAlchemy** as the common ORM/database tool for Pyramid applications. ([Pylons Project Documentation][1])

---

## 3. What is SQLAlchemy?

SQLAlchemy is a Python library used to connect Python code with a database.

Simple meaning:

```text
SQLAlchemy = bridge between Python and database
```

Instead of writing raw SQL every time:

```sql
SELECT * FROM users;
```

You can work with Python objects like:

```text
User
Post
Product
Student
```

This style is called **ORM**.

For more understanding about SQLAlchemy:

([SQLAlchemy - The Database Toolkit for Python][5])

([SQLAlchemy - Wikipedia][6])

([SQLAlchemy-Introduction - Geeksforgeeks][7])

([SQLAlchemy - EDX][8])

([What is SQLAlchemy][9])

---

## 4. What is ORM?

ORM means:

```text
Object Relational Mapper
```

Simple explanation:

```text
Python class  →  Database table
Python object →  Database row
Class field   →  Database column
```

Example:

```text
Student class       → students table
student.name        → name column
student.email       → email column
one student object  → one row in database
```

So ORM helps you think in Python instead of only SQL.

For more understanding about ORM:

([Object Relational Mappers (ORMS) - FullStackPython][10])

([ORMS For Python][11])

([What is an ORM – The Meaning of Object Relational Mapping Database Tools][12])

([ORM Explained: SQLAlchemy Fundamentals for Beginners (Python 2026)][13])

---

## 5. Pyramid Database Flow

![Pyramid Request/Response Flow](Pyramid_request_response_flow.png)

Here is the main working flow:

```text
User sends request
        ↓
Pyramid route matches URL
        ↓
View function runs
        ↓
View asks SQLAlchemy for data
        ↓
SQLAlchemy talks to database
        ↓
Database returns data
        ↓
View creates response
        ↓
User sees result
```

More simply:

```text
Browser → Route → View → SQLAlchemy → Database
Database → SQLAlchemy → View → Response → Browser
```

> Explanation:

That’s the **request/response flow** in a web app.

## Forward path

**Browser → Route → View → SQLAlchemy → Database**

- **Browser**: user sends a request
- **Route**: URL is matched to a handler
- **View**: code runs for that page/action
- **SQLAlchemy**: ORM layer talks to the database
- **Database**: stores or returns data

## Return path

**Database → SQLAlchemy → View → Response → Browser**

- data comes back from the **Database**
- **SQLAlchemy** converts it into Python objects
- **View** prepares the result
- **Response** is built
- **Browser** displays it

## In short

It means: **a user request goes from browser to database and then the result goes back to the browser**.

---

## 6. Main Parts of Database Integration

To connect a database with Pyramid, you mainly need these parts:

### A. Database

This is where data is stored.

Examples:

```text
SQLite
PostgreSQL
MySQL
MariaDB
```

For learning, we usually start with:

```text
SQLite
```

Because it is simple and does not need a separate database server.

---

### B. Model

A **model** represents your data structure.

Example:

```text
User model
Post model
Product model
Student model
```

In a SQLAlchemy-based Pyramid app, model objects usually come from querying SQL database tables. ([Pylons Project Documentation][2])

Example thinking:

```text
Student model
--------------
id
name
email
department
```

This model becomes a table in the database.

---

### C. Engine

The **engine** is the connection system between SQLAlchemy and the database.

Simple meaning:

```text
Engine = database connection manager
```

Example:

```text
Pyramid app wants data
        ↓
SQLAlchemy engine connects to database
        ↓
Data is read or written
```

---

### D. Session

A **session** is used to perform database operations.

Simple meaning:

```text
Session = temporary working area for database actions
```

Example operations:

```text
Add data
Read data
Update data
Delete data
```

Think of it like a shopping cart:

```text
You add changes to session
Then save/commit them to database
```

---

### E. Transaction

A **transaction** means a safe group of database operations.

Example:

```text
Add user
Add profile
Add login record
```

If all operations are successful:

```text
Save everything
```

If one operation fails:

```text
Cancel everything
```

Pyramid has transaction-management support, which is useful when coordinating database commits safely. ([Pylons Project Documentation][3])

---

## 7. Database Integration Architecture

```text
              User / Browser
                    ↓
              HTTP Request
                    ↓
              Pyramid Route
                    ↓
              Pyramid View
                    ↓
              SQLAlchemy Session
                    ↓
              SQLAlchemy Model
                    ↓
              Database Table
                    ↓
              Saved Data
```

Response comes back like this:

```text
Database Table
      ↓
SQLAlchemy Model
      ↓
SQLAlchemy Session
      ↓
Pyramid View
      ↓
HTTP Response
      ↓
Browser
```

---

## 8. Example Scenario: Student Management App

Suppose we build a small student app.

User visits:

```text
/students
```

Pyramid route catches it:

```text
Route name: students
```

Then Pyramid calls the view:

```text
students_view()
```

The view asks the database:

```text
Give me all students
```

SQLAlchemy gets data from database:

```text
id | name  | department
1  | Rakib | CSE
2  | Hasan | BBA
```

Then Pyramid sends response:

```text
Student list page
```

Full flow:

```text
/students URL
      ↓
students route
      ↓
students_view()
      ↓
Student model
      ↓
students table
      ↓
HTML response
```

---

## 9. CRUD Operations

Most database apps use CRUD.

CRUD means:

```text
C = Create
R = Read
U = Update
D = Delete
```

Example with student data:

```text
Create → Add a new student
Read   → Show student list
Update → Edit student information
Delete → Remove student record
```

Almost every web app uses CRUD.

Examples:

```text
Facebook post CRUD
E-commerce product CRUD
University student CRUD
Blog post CRUD
Task management CRUD
```

---

## 10. Pyramid + Database Folder Idea

A Pyramid project with database may look like this:

```text
myproject/
│
├── views/
│   └── student_views.py
│
├── models/
│   ├── meta.py
│   └── student.py
│
├── templates/
│   └── students.jinja2
│
├── __init__.py
└── development.ini
```

Meaning:

```text
views/      → request handling logic
models/     → database structure
templates/  → HTML pages
.ini file   → project/database settings
```

---

## 11. Important Pyramid Style

Pyramid is flexible.

It does not say:

```text
“You must use this database only.”
```

Instead it says:

```text
“You can use SQLAlchemy, SQLite, PostgreSQL, MySQL, or other tools.”
```

This is why Pyramid is good for both small and large projects.

---

## 12. Modern Note About Project Generator

Some older Pyramid tutorials mention older cookiecutter templates like `pyramid-cookiecutter-alchemy`, but Pyramid’s latest glossary notes those older alchemy/ZODB cookiecutters are deprecated and recommends `pyramid-cookiecutter-starter` going forward. ([Pylons Project Documentation][4])

So for our learning, we should focus on the modern structure:

```text
Pyramid + SQLAlchemy + SQLite first
```

Then later we can move to:

```text
Pyramid + SQLAlchemy + PostgreSQL
```

---

## 13. Super Simple Summary

```text
Pyramid handles the web request.
SQLAlchemy handles the database.
Model defines the table structure.
Session performs database actions.
Database stores the data permanently.
```

One-line memory:

```text
In Pyramid, the view talks to the model through SQLAlchemy, and SQLAlchemy talks to the database.
```

---

### Best Flow to Remember

```text
Request
   ↓
Route
   ↓
View
   ↓
Model
   ↓
Session
   ↓
Database
   ↓
Response
```

For your learning path, the next practical step should be:

```text
Build a tiny Pyramid app with SQLite database:
Student Management App
- Add student
- Show students
- Edit student
- Delete student
```

[1]: https://docs.pylonsproject.org/projects/pyramid/en/latest/quick_tutorial/databases.html?utm_source=chatgpt.com "19: Databases Using SQLAlchemy — The Pyramid Web ..."
[2]: https://docs.pylonsproject.org/projects/pyramid/en/latest/tutorials/wiki2/basiclayout.html?utm_source=chatgpt.com "Basic Layout — The Pyramid Web Framework v2.1"
[3]: https://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/introduction.html?utm_source=chatgpt.com "Pyramid Introduction"
[4]: https://docs.pylonsproject.org/projects/pyramid/en/latest/glossary.html?utm_source=chatgpt.com "Glossary — The Pyramid Web Framework v2.1"
[5]: https://share.google/cbsLDjZ4AtB40uRCH "SQLAlchemy - The Database Toolkit for Python"
[6]: https://en.wikipedia.org/wiki/SQLAlchemy "SQLAlchemy - Wikipedia"
[7]: https://www.geeksforgeeks.org/python/sqlalchemy-introduction/ "SQLAlchemy-Introduction - Geeksforgeeks"
[8]: https://www.edx.org/learn/sqlalchemy "SQLAlchemy - EDX"
[9]: https://www.youtube.com/shorts/1kO0v-jvjgg "What is SQLAlchemy"
[10]: https://www.fullstackpython.com/object-relational-mappers-orms.html "Object-Relational-Mappers-ORMS - fullstackpython"
[11]: https://github.com/vajol/python-data-engineering-resources/blob/main/resources/orms-for-python.md "ORMS-For-Python"
[12]: https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/ "What is an ORM – The Meaning of Object Relational Mapping Database Tools"
[13]: https://www.youtube.com/watch?v=eeluKtkDjJw "ORM Explained: SQLAlchemy Fundamentals for Beginners (Python 2026)"
