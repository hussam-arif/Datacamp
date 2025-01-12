# Intermediate SQL Notes

# Querying a Database - Key Notes

- **Course Focus**:  
  - Using SQL to query databases and turn raw data into actionable insights.  
  - Topics include filtering data, aggregate functions, sorting, grouping, and understanding query execution order.  

- **Films Database**:  
  - Contains four tables: `films`, `reviews`, `people`, and `roles`.  
  - The schema includes table names, field names, and data types.

- **COUNT()**:  
  - Counts the number of records with a value in a field.  
  - Example: Count the number of `birthdate` values in the `people` table:  
    ```sql
    SELECT COUNT(birthdate) AS count_birthdates FROM people;
    ```
    Result: 6152 birthdates.

- **COUNT() Multiple Fields**:  
  - Use COUNT separately for each field.  
  - Example: Count the number of `name` and `birthdate` values in the `people` table.

- **Using * with COUNT()**:  
  - Use `COUNT(*)` to count the total number of records in a table.  
  - Example:  
    ```sql
    SELECT COUNT(*) AS total_records FROM people;
    ```

- **DISTINCT**:  
  - Retrieves unique values from a field, removing duplicates.  
  - Example: Get all unique languages in the `films` table:  
    ```sql
    SELECT DISTINCT(language) FROM films;
    ```

- **COUNT() with DISTINCT**:  
  - Counts the number of unique values in a field.  
  - Example: Count distinct birth dates:  
    ```sql
    SELECT COUNT(DISTINCT birthdate) AS unique_birthdates FROM people;
    ```
  - Note: The count of distinct values may differ from the total count due to duplicates.
 

# Query Execution - Key Notes

- **Order of Execution**:  
  - SQL code is processed in a specific order, not as it is written:  
    1. **FROM**: Identify the table containing the data.  
    2. **SELECT**: Choose the fields to retrieve.  
    3. **Other clauses**: Refine results (e.g., `LIMIT`, `WHERE`).  
  - Example: Limit results to the first ten names from the `people` table:  
    ```sql
    SELECT name FROM people LIMIT 10;
    ```
  - Understanding execution order is crucial for debugging and using aliases effectively.

- **Debugging SQL**:  
  - **Helpful Error Messages**:  
    - SQL often pinpoints the issue, such as misspelling a field name or missing a keyword.  
  - **Comma Errors**:  
    - Missing commas are common. Check for commas between fields in the `SELECT` statement.  
    - Example: Missing comma between `country` and `duration` in:  
      ```sql
      SELECT title, country duration FROM films;
      ```  
      Correct version:  
      ```sql
      SELECT title, country, duration FROM films;
      ```
  - **Keyword Errors**:  
    - Misspelled keywords result in precise error messages with caret indicators pointing to the issue.  

- **Common Errors**:  
  - Misspelled fields or keywords.  
  - Missing commas or punctuation.  
  - Incorrect capitalization.  

- **Final Note**:  
  - Debugging is an essential skill, and the best way to master it is by making and learning from mistakes.  


