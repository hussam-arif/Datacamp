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


