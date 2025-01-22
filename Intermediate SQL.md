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

  # NULL Values - Key Notes

- **What is NULL?**:  
  - In SQL, `NULL` represents a missing or unknown value.  
  - Databases often contain `NULL` values due to human error, unavailable data, or unknown information.  
  - Handling `NULL` values is crucial to ensure accurate analysis.

- **Filtering NULL Values**:  
  - Use `IS NULL` to identify missing values.  
    - Example: Find names with missing birthdates:  
      ```sql
      SELECT name FROM people WHERE birthdate IS NULL;
      ```
  - Use `IS NOT NULL` to exclude missing values.  
    - Example: Count people with non-missing birthdates:  
      ```sql
      SELECT COUNT(*) FROM people WHERE birthdate IS NOT NULL;
      ```

- **COUNT() and NULL Values**:  
  - `COUNT(*)` includes all records, including `NULL` values.  
  - `COUNT(field_name)` excludes `NULL` values.  
    - Example:  
      ```sql
      SELECT COUNT(birthdate) FROM people;
      ```
    - Equivalent to:  
      ```sql
      SELECT COUNT(*) FROM people WHERE birthdate IS NOT NULL;
      ```

- **Practical Example**:  
  - Analyzing the `deathdate` field in the `people` table:  
    - Without filtering, we might assume all records have a `deathdate`.  
    - Checking for `NULL` values reveals that half the records are missing this information, which could lead to inaccurate conclusions if ignored.

- **Best Practices**:  
  - Always check for `NULL` values using `IS NULL` or `IS NOT NULL`.  
  - Filtering `NULL` values is a common task and becomes second nature with practice.


# Summarizing Data - Key Notes

- **What are Aggregate Functions?**:  
  - Aggregate functions perform calculations on multiple values in a field and return a single value.  
  - Useful for understanding datasets as a whole, not just individual records.

- **Key Aggregate Functions**:  
  - **COUNT()**: Counts non-NULL records in a field.  
  - **AVG()**: Calculates the average value of a numeric field.  
    ```sql
    SELECT AVG(budget) FROM films;
    ```
  - **SUM()**: Adds up all values in a numeric field.  
    ```sql
    SELECT SUM(budget) FROM films;
    ```
  - **MIN()**: Returns the lowest value in a field.  
    ```sql
    SELECT MIN(budget) FROM films;
    ```
  - **MAX()**: Returns the highest value in a field.  
    ```sql
    SELECT MAX(budget) FROM films;
    ```

- **Using Aggregate Functions on Non-Numerical Data**:  
  - **COUNT()**: Works on any field type to count non-NULL values.  
  - **MIN()** and **MAX()**: Can be used with:
    - **Strings**: Returns the alphabetically first (`MIN`) or last (`MAX`) value.  
      Example:  
      ```sql
      SELECT MIN(country), MAX(country) FROM films;
      ```
    - **Dates**: Finds the earliest (`MIN`) or latest (`MAX`) date.  

- **Example with Non-Numerical Data**:  
  - Find the alphabetically first and last countries in the `films` database:  
    ```sql
    SELECT MIN(country) AS first_country, MAX(country) AS last_country FROM films;
    ```
    Result: Afghanistan (first), West Germany (last).

- **Aliasing in Aggregate Functions**:  
  - Use aliases to make query results easier to read.  
  - Example:  
    ```sql
    SELECT AVG(budget) AS avg_budget FROM films;
    ```

  # Summarizing Subsets - Key Notes

- **Combining WHERE with Aggregate Functions**:  
  - Use the `WHERE` clause to filter subsets of data before applying aggregate functions.  
  - Example: Average budget of movies made in 2010 or later:  
    ```sql
    SELECT AVG(budget) 
    FROM films 
    WHERE release_year >= 2010;
    ```
  - Other examples:
    - Total budget for 2010:  
      ```sql
      SELECT SUM(budget) 
      FROM films 
      WHERE release_year = 2010;
      ```
    - Smallest budget in 2010:  
      ```sql
      SELECT MIN(budget) 
      FROM films 
      WHERE release_year = 2010;
      ```
    - Count of budgets recorded in 2010:  
      ```sql
      SELECT COUNT(budget) 
      FROM films 
      WHERE release_year = 2010;
      ```

- **ROUND() Function**:  
  - Cleans up decimals by rounding to a specified number of places.  
  - Syntax: `ROUND(number, decimal_places)`  
    - Example: Average budget rounded to 2 decimals:  
      ```sql
      SELECT ROUND(AVG(budget), 2) 
      FROM films 
      WHERE release_year >= 2010;
      ```
  - **Default Rounding**:  
    - Omitting the second parameter rounds to the nearest whole number (or pass `0`).  

- **ROUND() with Negative Parameters**:  
  - Rounds to the left of the decimal point.  
  - Example: Round to the nearest hundred thousand:  
    ```sql
    SELECT ROUND(budget, -5) 
    FROM films;
    ```

---

**Key Takeaways**:
- Combine `WHERE` with aggregate functions to analyze subsets of data.  
- Use `ROUND()` to improve readability of numerical results.


# Aliasing and Arithmetic - Key Notes

- **Arithmetic in SQL**:  
  - Perform basic arithmetic using `+`, `-`, `*`, and `/`.  
  - Use parentheses for clarity and to control execution order.  
  - Example:  
    ```sql
    SELECT (gross - budget) AS profit FROM films;
    ```
  - Be cautious with division: dividing integers returns an integer.  
    - To get a precise result, use decimals:  
      ```sql
      SELECT 4.0 / 3.0 AS precise_result;
      ```

- **Aggregate Functions vs. Arithmetic**:  
  - **Aggregate Functions**: Operate vertically on columns (e.g., `SUM(budget)`).  
  - **Arithmetic**: Operates horizontally on rows (e.g., `gross - budget`).

- **Aliasing with AS**:  
  - Use `AS` to name calculated fields for clarity.  
  - Example:  
    ```sql
    SELECT (gross - budget) AS profit FROM films;
    ```
  - Avoid ambiguous field names, especially when using multiple functions:  
    ```sql
    SELECT MAX(budget) AS max_budget, MAX(gross) AS max_gross FROM films;
    ```

- **SQL Execution Order and Aliasing**:  
  - SQL processes in this order:  
    1. `FROM`: Identify the table.  
    2. `WHERE`: Filter the data.  
    3. `SELECT`: Calculate and alias fields.  
    4. `LIMIT`: Restrict the result set.  
  - **Aliases cannot be used in `WHERE`**, as they are created in the `SELECT` step.


# Sorting Results - Key Notes

- **Sorting in SQL**:  
  - Sorting results helps organize data in a specific order for better understanding.  
  - Example: Find the three longest coats by sorting by garment type and length.

- **ORDER BY Clause**:  
  - Use `ORDER BY` to sort results based on one or more fields.  
  - By default, `ORDER BY` sorts in ascending order (smallest to largest, A to Z).  
    ```sql
    SELECT title FROM films ORDER BY budget;
    ```
  - **ASC (Ascending)**: Explicitly sorts results in ascending order (optional).  
    ```sql
    SELECT title FROM films ORDER BY budget ASC;
    ```
  - **DESC (Descending)**: Sorts results in descending order.  
    ```sql
    SELECT title FROM films ORDER BY budget DESC;
    ```

- **Filtering Null Values**:  
  - Use `WHERE` before `ORDER BY` to exclude null values for better sorting:  
    ```sql
    SELECT title FROM films WHERE budget IS NOT NULL ORDER BY budget DESC;
    ```

- **Sorting on Non-Selected Fields**:  
  - It’s possible to sort by fields not included in the `SELECT` clause, but it’s good practice to include them for clarity.  
    ```sql
    SELECT title FROM films ORDER BY release_year;
    ```

- **Sorting by Multiple Fields**:  
  - Specify multiple fields, separated by commas. The second field acts as a tie-breaker.  
    Example: Sort films by number of Oscar wins and then by IMDb score:  
    ```sql
    SELECT title, oscar_wins, imdb_score 
    FROM films 
    ORDER BY oscar_wins DESC, imdb_score DESC;
    ```

- **Different Sorting Orders for Multiple Fields**:  
  - Use different orders for each field:  
    ```sql
    SELECT name, birthdate 
    FROM people 
    ORDER BY birthdate ASC, name DESC;
    ```

- **Order of Execution**:  
  - `ORDER BY` is executed after `FROM`, `WHERE`, and `SELECT`, but before `LIMIT`:  
    ```sql
    SELECT title 
    FROM films 
    WHERE budget > 1000000 
    ORDER BY imdb_score DESC 
    LIMIT 10;
    ```


# Grouping Data - Key Notes

- **Why Group Data?**:  
  - Grouping allows us to summarize data for specific categories.  
  - Example: Calculate the average film duration grouped by certification.

- **GROUP BY Clause**:  
  - Used to group data by one or more fields, often with aggregate functions.  
  - Example: Group films by certification and calculate average duration:  
    ```sql
    SELECT certification, AVG(duration) AS avg_duration 
    FROM films 
    GROUP BY certification;
    ```

- **Error Handling**:  
  - Fields in the `SELECT` clause must either:
    - Be included in the `GROUP BY` clause, or  
    - Use an aggregate function.  
  - Incorrect query:  
    ```sql
    SELECT certification, title 
    FROM films 
    GROUP BY certification;
    ```  
    - Fix: Add an aggregate function:  
      ```sql
      SELECT certification, COUNT(title) AS title_count 
      FROM films 
      GROUP BY certification;
      ```

- **GROUP BY Multiple Fields**:  
  - Similar to `ORDER BY`, multiple fields can be grouped in sequence.  
  - Example: Group by certification and language:  
    ```sql
    SELECT certification, language, COUNT(title) AS title_count 
    FROM films 
    GROUP BY certification, language;
    ```

- **Combining GROUP BY and ORDER BY**:  
  - Sort grouped results using `ORDER BY`.  
  - Example: Sort by the number of titles in descending order:  
    ```sql
    SELECT certification, COUNT(title) AS title_count 
    FROM films 
    GROUP BY certification 
    ORDER BY title_count DESC;
    ```

- **Order of Execution**:  
  - `GROUP BY` executes after `FROM` but before `SELECT`, `ORDER BY`, and `LIMIT`.  
  - Execution flow:  
    - `FROM`: Identify the data source.  
    - `GROUP BY`: Group the data.  
    - `SELECT`: Calculate aggregates and define aliases.  
    - `ORDER BY`: Sort the results.  
    - `LIMIT`: Restrict the result set.


# Filtering Grouped Data - Key Notes

- **HAVING Clause**:  
  - Used to filter grouped records based on aggregate functions.  
  - Example: Show years where more than 10 films were released:  
    ```sql
    SELECT release_year, COUNT(title) AS title_count 
    FROM films 
    GROUP BY release_year 
    HAVING COUNT(title) > 10;
    ```

- **Order of Execution**:  
  - `HAVING` executes **after** `GROUP BY` and **before** `SELECT`.  
  - Written order:  
    ```sql
    SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY, LIMIT
    ```
  - Execution order:  
    ```sql
    FROM, WHERE, GROUP BY, HAVING, SELECT, ORDER BY, LIMIT
    ```
  - **Why HAVING Exists**:  
    - `WHERE` filters individual records **before** aggregation.  
    - `HAVING` filters aggregated (grouped) records.

- **HAVING vs WHERE**:  
  - Use `WHERE` for individual record filtering:  
    Example: Films released in 2000:  
    ```sql
    SELECT title 
    FROM films 
    WHERE release_year = 2000;
    ```
  - Use `HAVING` for grouped record filtering:  
    Example: Years where the average film duration is over 2 hours:  
    ```sql
    SELECT release_year, AVG(duration) AS avg_duration 
    FROM films 
    GROUP BY release_year 
    HAVING AVG(duration) > 120;
    ```

- **Steps for Filtering with HAVING**:  
  1. **Select the grouped field** (e.g., `release_year`).  
  2. **Aggregate the target field** (e.g., `AVG(duration)`).  
  3. **Filter using HAVING** for the aggregated value.  
  4. **Group by the relevant field** (e.g., `release_year`).  

- **Example Query**:  
  - Find the release years with an average film duration over 2 hours:  
    ```sql
    SELECT release_year, AVG(duration) AS avg_duration 
    FROM films 
    GROUP BY release_year 
    HAVING AVG(duration) > 120;
    ```
