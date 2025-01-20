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
 
  # SQL Style - Key Notes

- **SQL Formatting**:  
  - SQL does not require strict formatting like other programming languages.  
  - Example: Queries without capitalization or new lines will still run but are harder to read.  

- **Best Practices**:  
  - Capitalize SQL keywords (e.g., `SELECT`, `FROM`).  
  - Use new lines and indentation to improve readability.  
  - Example of well-formatted SQL:  
    ```sql
    SELECT
        title,
        release_year,
        country
    FROM films
    LIMIT 3;
    ```

- **Style Guides**:  
  - Follow a SQL style guide for consistency (e.g., Holywell's guide).  
  - Common practices:  
    - Capitalize keywords.  
    - Indent selected fields when listing multiple fields.  
    - Use clear naming conventions for tables, fields, and aliases.  

- **Semicolon (`;`)**:  
  - Optional in PostgreSQL but considered best practice for:  
    - Compatibility with other SQL flavors.  
    - Clearly indicating the end of a query, especially in files with multiple queries.

- **Non-Standard Field Names**:  
  - Fields with spaces in their names must be enclosed in double quotes.  
  - Example:  
    ```sql
    SELECT "release year" FROM films;
    ```

- **Why Format?**:  
  - Readable and clean SQL code improves collaboration and debugging.  
  - Following SQL style guides is valued in professional environments.


# Filtering Numbers - Key Notes

- **WHERE Clause**:  
  - Filters data to focus on records relevant to specific business questions.  
  - Example: Select coats **where** the color is green.

- **Filtering Numbers with Comparison Operators**:  
  - Common operators used with `WHERE`:
    - **Greater than** (`>`) – Films released after 1960:  
      ```sql
      SELECT title FROM films WHERE release_year > 1960;
      ```
    - **Less than** (`<`) – Films released before 1960.  
    - **Less than or equal to** (`<=`) – Films released during or before 1960.  
    - **Equal to** (`=`) – Films released in a specific year.  
    - **Not equal to** (`<>`) – Films released in all years except 1960:  
      ```sql
      SELECT title FROM films WHERE release_year <> 1960;
      ```

- **WHERE with Strings**:  
  - Filter strings using `=` with single quotes around the value.  
  - Example: Filter films where the country is Japan:  
    ```sql
    SELECT title FROM films WHERE country = 'Japan';
    ```

- **Order of Execution**:  
  - Query written order:  
    ```sql
    SELECT title FROM films WHERE release_year > 1960 LIMIT 5;
    ```
  - Execution order:  
    - **FROM**: Identify the table.  
    - **WHERE**: Filter the records.  
    - **SELECT**: Retrieve specified fields.  
    - **LIMIT**: Limit the result set.


# Filtering with Multiple Criteria - Key Notes

- **Multiple Criteria**:  
  - Use additional keywords to filter data based on multiple conditions:  
    - **OR**: At least one condition must be true.  
    - **AND**: All conditions must be true.  
    - **BETWEEN**: Filter values within a range (inclusive).

- **OR Operator**:  
  - Filters records where at least one condition is satisfied.  
  - Example: Films released in 1994 **or** 2000:  
    ```sql
    SELECT title FROM films WHERE release_year = 1994 OR release_year = 2000;
    ```

- **AND Operator**:  
  - Filters records where all conditions are satisfied.  
  - Example: Films released between 1994 **and** 2000:  
    ```sql
    SELECT title FROM films WHERE release_year >= 1994 AND release_year <= 2000;
    ```

- **Combining AND and OR**:  
  - Use parentheses to ensure the correct execution order when combining multiple conditions.  
  - Example: Films released in 1994 **or** 1995, and with a certification of PG **or** R:  
    ```sql
    SELECT title 
    FROM films 
    WHERE (release_year = 1994 OR release_year = 1995) 
      AND (certification = 'PG' OR certification = 'R');
    ```

- **BETWEEN Keyword**:  
  - Shorthand for filtering a range of values.  
  - Example: Films released **between** 1994 and 2000:  
    ```sql
    SELECT title FROM films WHERE release_year BETWEEN 1994 AND 2000;
    ```

- **Combining BETWEEN with AND and OR**:  
  - Example: Films released between 1994 and 2000 from the UK:  
    ```sql
    SELECT title 
    FROM films 
    WHERE release_year BETWEEN 1994 AND 2000 
      AND country = 'United Kingdom';
    ```

# Filtering Text - Key Notes

- **Text Filtering with WHERE**:  
  - Use the `WHERE` clause to filter text data by exact matches or patterns.

- **LIKE Operator**:  
  - Searches for patterns in a field using wildcards:  
    - `%` matches zero, one, or many characters.  
      - Example: Names starting with "Ad":  
        ```sql
        SELECT name FROM people WHERE name LIKE 'Ad%';
        ```
    - `_` matches a single character.  
      - Example: Three-letter names starting with "E":  
        ```sql
        SELECT name FROM people WHERE name LIKE 'E__';
        ```

- **NOT LIKE Operator**:  
  - Finds records that **don’t match** a specific pattern.  
    - Example: Names without "A.":  
      ```sql
      SELECT name FROM people WHERE name NOT LIKE 'A._%';
      ```
  - Note: `LIKE` and `NOT LIKE` are case-sensitive.

- **Wildcard Positioning**:  
  - Wildcards can be used flexibly to match patterns at the start, end, or middle of text:  
    - Names ending in "r":  
      ```sql
      SELECT name FROM people WHERE name LIKE '%r';
      ```
    - Names with "t" as the third character:  
      ```sql
      SELECT name FROM people WHERE name LIKE '__t%';
      ```

- **IN Operator**:  
  - Simplifies filtering with multiple conditions.  
    - Example: Films released in 1920, 1930, or 1940:  
      ```sql
      SELECT title FROM films WHERE release_year IN (1920, 1930, 1940);
      ```
    - Example with text: Titles where the country is Germany or France:  
      ```sql
      SELECT title FROM films WHERE country IN ('Germany', 'France');
      ```
