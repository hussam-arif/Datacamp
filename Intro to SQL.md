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
