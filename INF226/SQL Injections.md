[[SQL]] Injection is a common security vulnerability that occurs when untrusted data is improperly concatenated into SQL queries, allowing an attacker to manipulate the query's logic and potentially gain unauthorised access to a database or modify its contents. It is considered one of the most critical security risks for web applications that interact with a database.

Here's how SQL Injection typically occurs:
1. User Input: Web applications often accept user input, such as form fields, search queries, or URL parameters, which are used to construct SQL queries.
2. Unsanitized Input: If the application does not properly validate, sanitize, or parameterize the user input, it may directly concatenate it into SQL statements without proper handling.
3. Malicious Payload: An attacker can then submit crafted input containing SQL commands or special characters that alter the intended behavior of the SQL query.
4. Manipulated Query: When the application concatenates the user input into the SQL query without proper precautions, the injected SQL commands become part of the query and are executed by the database server.
5. Impact: Depending on the severity of the vulnerability, SQL Injection attacks can lead to unauthorized data disclosure, data manipulation, privilege escalation, or even the complete compromise of the underlying system.

To mitigate SQL Injection attacks, the following best practices should be followed:
1. Parameterized Queries: Use prepared statements or parameterized queries with placeholders instead of concatenating user input directly into SQL statements. This ensures that user input is treated as data, separate from the SQL logic, preventing attackers from altering the query structure.
2. Input Validation and Sanitization: Implement strict input validation to ensure that user input adheres to expected formats and limits. Use proper data sanitization techniques, such as escaping special characters or using safe encoding functions, to prevent SQL injection through user-supplied data.
3. Principle of Least Privilege: Apply the principle of least privilege to database access permissions. Use separate database accounts with minimal privileges for different application functionalities to limit the potential impact of a successful SQL Injection attack.
4. Secure Coding Practices: Follow secure coding practices, such as using secure APIs, prepared statements, and safe ORM (Object-Relational Mapping) frameworks that handle SQL parameterization automatically. Avoid dynamic query generation using string concatenation.
5. Regular Security Updates and Patching: Keep your database management system and associated libraries up to date with the latest security patches and updates. Vulnerabilities that could lead to SQL Injection attacks are often discovered and patched over time.
6. Security Audits and Penetration Testing: Regularly conduct security audits and penetration testing to identify and address SQL Injection vulnerabilities in your application. Automated tools and manual code reviews can help identify potential weaknesses.
7. Input Validation on Client and Server Side: Implement input validation on both the client and server sides to detect and reject malicious input early. Client-side validation is important for usability and providing immediate feedback, but server-side validation is essential for security as client-side validation can be bypassed.

By implementing these preventive measures, you can significantly reduce the risk of SQL Injection vulnerabilities and enhance the overall security of your web applications. Regular security assessments and ongoing monitoring are also critical to stay vigilant against emerging threats.

## Example
- A regular SQL Example:
```SQL
SELECT * FROM items WHERE owner='paul' AND itemname='crysknife'
```
- Result:
![[Pasted image 20230523031929.png]]
- Now lets inject:
```SQL
01 String userName = ctx.getAuthenticatedUserName();  
02 String query = "SELECT * FROM items WHERE owner = '"  
		+ userName + "' AND itemname = '" + ItemName.Text + "'";  
03 sda = new SqlDataAdapter(query, conn);  
04 DataTable dt = new DataTable();  
05 sda.Fill(dt);
```

```SQL  
02 string query = "SELECT * FROM items WHERE owner = '"  
+ userName + "' AND itemname = '" + ItemName.Text + "'";
```
- What happens if ``ItemName.Text`` comes from user input, and the user inputs the following string? 
```SQL
name' OR 'a'='a
```
- The full SQL query would then be:
```SQL
SELECT * FROM items WHERE owner='paul' AND itemname='name' OR 'a'='a'
```
- The intention of the attacker's input is to manipulate the SQL query's logic by injecting additional conditions. The injected portion, `'a'='a'`, is always true, which effectively bypasses the original condition. As a result, the query will return all items owned by 'paul' regardless of the actual item name.
- Result:
![[Pasted image 20230523032231.png]]
- This is a classic example of an SQL Injection vulnerability, where the user input is not properly validated or sanitized before being concatenated into the SQL query. The malicious input alters the query's structure, allowing the attacker to control its behavior and potentially gain unauthorized access to sensitive data or perform unauthorized operations.
- To mitigate this vulnerability, it is crucial to use parameterized queries or prepared statements instead of directly concatenating user input into SQL statements. Parameterized queries separate the SQL logic from the user input and handle proper encoding or escaping of special characters, preventing SQL Injection attacks.
- What if the input was the following?
```SQL
name'; DELETE FROM items; --
```
- If the user input for `ItemName.Text` is `name'; DELETE FROM items; --`, and the code constructs the query as shown:
```SQL
String query = "SELECT * FROM items WHERE owner = '"  
        + userName + "' AND itemname = '" + ItemName.Text + "'";
```
- The resulting query becomes:
```SQL
SELECT * FROM items WHERE owner='paul' AND itemname='name'; DELETE FROM items; --'
```
- In this case, the user input includes a malicious payload that attempts to execute an additional SQL statement to delete all the rows from the `items` table. The semicolon (`;`) is used to separate the original query from the malicious statement, and the double hyphen (`--`) is used to comment out the rest of the original query, preventing any syntax errors.
- If the code does not have proper security measures in place, and the SQL engine does not prevent multiple statements execution, this can lead to the deletion of all the items in the `items` table.
- To prevent [[SQL]] Injection attacks and mitigate this vulnerability, it is essential to use parameterized queries or prepared statements, as mentioned earlier. Parameterized queries handle user input separately and automatically handle proper escaping or encoding of special characters, ensuring the integrity and security of the SQL statements executed.

## Prepared Statements
Prepared Statements, also known as parameterized queries, are a way to execute SQL queries safely and securely by separating the query logic from the user input. They provide a mechanism to handle user input as parameters rather than directly concatenating them into the SQL query string.

The process of using Prepared Statements involves two steps: preparation and execution.
-   Preparation:
    - The SQL query is defined with placeholders or parameter markers (e.g., `?` or `:param`) in place of the actual values.
    - The query is sent to the database server, which performs a syntax check and compiles an execution plan for the query.
    - The compiled query, along with the placeholders, is stored in memory on the server side.

-   Execution:
    - User input values are provided as separate parameters, corresponding to the placeholders in the prepared statement.
    - The database server uses the compiled execution plan from the preparation step and binds the provided values to the placeholders.
    - The query is executed with the bound parameters, and the result is returned.

Benefits of using Prepared Statements:
1. Security: Prepared Statements help prevent SQL Injection attacks by separating the query structure from the user input. The input values are treated as data rather than executable code, reducing the risk of unauthorized database access.
2. Performance: Prepared Statements can improve performance as the database server can reuse the compiled execution plan for subsequent executions of the same query with different parameter values. This reduces the overhead of query parsing and optimization.
3. Maintainability: By separating the query logic from the data values, code readability and maintainability are improved. Changes to the query structure can be made without modifying the parameter handling code.

Example in Java using JDBC:
```Java
String query = "SELECT * FROM users WHERE username = ? AND password = ?";
PreparedStatement statement = connection.prepareStatement(query);
statement.setString(1, username);
statement.setString(2, password);
ResultSet result = statement.executeQuery();
```

In the above example, the query uses `?` as placeholders for the username and password values. The `setString` method is used to bind the actual values to the prepared statement parameters. This way, the user input is treated as data and not interpreted as part of the SQL query, reducing the risk of SQL Injection.

By using Prepared Statements, developers can enhance the security and robustness of their applications when interacting with databases.

- Without Prepared Statements:
- ![[Pasted image 20230523033150.png]]
- With Prepared Statements:
- ![[Pasted image 20230523033218.png]]

## Resources
- https://github.com/Gallopsled/pwntools-tutorial#readme
- https://www.youtube.com/watch?v=ciNHn38EyRc
- 