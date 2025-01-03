# Intro to SQL - Key Notes

- **Databases** store data in tables organized into rows and columns.
- Tables in databases can include data such as:
  - **Patrons**: library card number, name, membership year, fines owed.
  - **Books**: book details.
  - **Checkouts**: records of borrowed books.

- **Relational databases** link data between tables, enabling questions like:
  - "Which books did James check out in 2022?"
  - "Which books are checked out most often?"

- **Advantages of databases** include:
  - Greater power and storage capacity than spreadsheets.
  - Enhanced security with encryption.
  - Ability for multiple users to query data simultaneously.

- **SQL (Structured Query Language)** is a powerful tool for:
  - Creating databases.
  - Querying data.
  - Updating data while leaving the original information unchanged.
 
# Tables - Key Notes

- **Tables** are the main building block of databases, organized into rows (records) and columns (fields).

- **Records** (rows) hold data for an individual observation. Example: In the patrons table, each row represents one patron, including details like membership year and fines owed.

- **Fields** (columns) hold one piece of information for all records in a table. Example: The "name" field in the patrons table lists the names of all library patrons.

- **Table Naming**:
  - Use **lowercase**.
  - Avoid spaces; use **underscores** instead.
  - Prefer collective or plural names (e.g., "inventory" or "products").

- **Field Naming**:
  - Use **lowercase** and avoid spaces.
  - Use **singular names** for fields (e.g., "card_num" instead of "card_nums").
  - Field names must be unique and should not match the table name.

- **Unique Identifiers**:
  - A unique value, called a "key," distinguishes records in a table.
  - Example: Use the "card_num" field as a unique identifier for patrons, not "name," since names may repeat.

- **Table Separation**:
  - Separate information into distinct tables for clarity and to avoid duplicate data.
  - Example: Keep patrons and checkouts in separate tables and use SQL to connect them when needed.
 
# Data - Key Notes

- **SQL Data Types**:
  - Each field in a table must have a **data type** that specifies the type of data it will hold (e.g., number, text, date).
  - **Why data types matter**:
    - Different types of data take up different storage space.
    - Certain operations only apply to specific data types (e.g., numbers can be multiplied, but text cannot).

- **Strings**:
  - A "string" is a sequence of characters (e.g., names like "Maham" or "James").
  - SQL has data types for strings:
    - **Short strings** save storage space (e.g., `CHAR`).
    - **VARCHAR** is flexible, storing short or long strings (up to tens of thousands of characters).

- **Integers**:
  - Used for whole numbers (e.g., the `member_year` field in the patrons table).
  - The `INT` data type is commonly used and can store values from ~ -2 billion to +2 billion.

- **Floats**:
  - Used for numbers with fractional parts (e.g., 2.05 dollars in fines).
  - The `NUMERIC` data type can store floats with up to 38 total digits.

- **Schemas**:
  - A **schema** is the "blueprint" of a database, showing:
    - Tables included.
    - Relationships between tables.
    - Data types for each field.
  - Example: In the library database, `VARCHAR` is used for strings like book title, author, and genre.

- **Database Storage**:
  - Data is physically stored on the hard disk of a **server**.
  - **Servers**:
    - Centralized computers that perform services (e.g., data access, websites).
    - Typically powerful machines that handle high volumes of requests.

# Introducing Queries - Key Notes

- **SQL Queries**:  
  - SQL is used to answer questions both within and across relational database tables.
  - Example: Find which books James checked out in 2022 or compare salaries across departments.

- **Best for Large Datasets**:  
  - SQL complements tools like spreadsheets but excels with large, complex datasets.
  - Example: Use SQL for data related to website traffic, customer reviews, or product sales where relationships between data are critical.

- **Keywords**:  
  - **SELECT**: Specifies the fields to retrieve (e.g., `name`).
  - **FROM**: Specifies the table containing the data (e.g., `patrons`).

- **Writing a Query**:  
  - Queries consist of a **SELECT** statement followed by a **FROM** statement.
  - Best practices:
    - Capitalize keywords (e.g., SELECT, FROM).
    - Use lowercase for table and field names.
    - End queries with a **semicolon** (`;`).

- **Result Set**:  
  - The result set is the output of a query (e.g., a list of patron names).
  - Writing a query does not modify the database itself.

- **Selecting Multiple Fields**:  
  - List field names after the **SELECT** keyword, separated by commas (e.g., `SELECT card_num, name`).
  - The order of fields in the result set does not need to match the table.

- **Selecting All Fields**:  
  - Use an asterisk (`*`) to select all fields in a table (e.g., `SELECT * FROM patrons`).


# Writing Queries - Key Notes

- **Aliasing**:  
  - Rename columns in the result set using the **AS** keyword for clarity or brevity.  
  - Example:  
    ```sql
    SELECT name AS first_name, hire_year FROM employees;
    ```
  - The alias only affects the query result, not the original table.

- **Selecting Distinct Records**:  
  - Use the **DISTINCT** keyword to return unique values.  
  - Example: Get unique years employees were hired:  
    ```sql
    SELECT DISTINCT year_hired FROM employees;
    ```

- **DISTINCT with Multiple Fields**:  
  - Return unique combinations of multiple fields by using DISTINCT with multiple columns.  
  - Example:  
    ```sql
    SELECT DISTINCT dept_id, year_hired FROM employees;
    ```

- **Views**:  
  - A **view** is a virtual table created by saving a SQL query.  
  - Views automatically update results when the underlying data changes.  
  - To create a view:  
    ```sql
    CREATE VIEW employee_hire_years AS
    SELECT name, hire_year FROM employees;
    ```
  - Query a view just like a table:  
    ```sql
    SELECT * FROM employee_hire_years;
    ```

# SQL Flavors - Key Notes

- **SQL Flavors**:  
  - SQL flavors are different versions of SQL, often designed to complement major relational database systems (e.g., Microsoft SQL Server, Oracle Database).  
  - All SQL flavors follow universal standards set by ISO and ANSI. Differences come from additional features built on top of these standards.

- **Two Popular SQL Flavors**:  
  - **PostgreSQL**:  
    - Free and open-source relational database system.  
    - Originally developed at the University of California, Berkeley.  
    - Sponsored by DARPA, the agency behind innovations like the internet, GPS, and the computer mouse.  
    - Uses `PostgreSQL SQL` flavor.  
  - **SQL Server**:  
    - Developed by Microsoft.  
    - Available in free and enterprise versions.  
    - Uses **T-SQL**, Microsoft's proprietary SQL flavor.  

- **Comparing PostgreSQL and SQL Server**:  
  - SQL flavors are like dialects of the same language (e.g., American vs. British English).  
  - Example: Limiting results:  
    - PostgreSQL: Use `LIMIT`.  
      ```sql
      SELECT name, id FROM employees LIMIT 2;
      ```
    - SQL Server: Use `TOP`.  
      ```sql
      SELECT TOP 2 name, id FROM employees;
      ```
  - Differences are small, and queries often look similar.

- **Choosing a Flavor**:  
  - Learn the flavor your employer or project requires (e.g., SQL Server for Microsoft-based systems).  
  - Don’t worry too much—learning one flavor makes it easy to switch to another with minor adjustments.  



