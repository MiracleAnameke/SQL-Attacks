#  Web Security
## SQL Attacks

### Lab Requirements
- Internet connectivity & VMware Workstation version 14.0.0 or above
- Windows 10 VM and Ubuntu Server, and Kali

### Lab Overview
focuses on exploiting SQL injection vulnerabilities in web applications. Students will perform a series of tasks that demonstrate how SQL injection can be used to bypass authentication, access sensitive data, and manipulate database content.

### Lab Tasks and Screenshots

### Part 01: Bypassing Authentication
**Task**: Bypass the authentication mechanism of a vulnerable login page using SQL injection.
- **Steps**:
    1. Open Firefox in W10 VM and navigate to the Mutillidae page on the Ubuntu Server VM.
    2. Reset the Database and navigate to the Login/Register page.
    3. Examine error messages by injecting a single quote into the login field.
    4. Bypass authentication with the SQL statement: `' OR 1 = 1 -- `.
    5. Include the output of `net config workstation` in the screenshot.
- **Slide 01**: Screenshot of the successful admin login and command output.
    <img src="https://i.imgur.com/7b2NF4V.png" height="400px" width="auto" alt="Bypassing Authentication"/>

### Part 02: Altering Login Mechanics with SQL Injection
**Task**: Use SQL injection to manipulate the login mechanism and log in as a specific user.
- **Steps**:
    1. Create a new user with username `FOLusername` and password `Windows1`.
    2. Attempt to log in with the username `FOLusername` and a tampered password field using Firefox Developer Tools.
    3. Use `' OR 1 = 1 -- ` in the password field to bypass authentication.
    4. Modify the SQL statement to log in as `FOLusername`.
- **Slide 02**: Screenshot showing the login page with altered SQL injection and successful login as `FOLusername`.
    <img src="https://i.imgur.com/2cHjXoV.png" height="400px" width="auto" alt="Altering Login Mechanics"/>

### Part 03: Capturing Authentication with Burp Suite
**Task**: Capture the authentication request using Burp Suite and prepare it for SQL injection testing with SQLmap.
- **Steps**:
    1. Set up Burp Suite to intercept the login request in the Kali Linux VM.
    2. Attempt to log in as `FOLusername` with the captured details.
    3. Save the POST request from the intercepted data for use with SQLmap.
- **Slide 03**: Screenshot of the Burp Suite intercepting the login request and the captured POST data.
    <img src="https://i.imgur.com/44or2Es.png" height="400px" width="auto" alt="Capturing Authentication"/>

### Part 04: Preparing SQLmap with Captured Data
**Task**: Use the captured login data to configure SQLmap and identify the back-end Database Management System (DBMS).
- **Steps**:
    1. Save the entire contents of the captured POST packet to a file named `login.post.request`.
    2. Run SQLmap with the saved request file to enumerate the database and detect the DBMS.
    3. Note the additional information provided by SQLmap about potential vulnerabilities.
- **Slide 04**: A screenshot showing the terminal with the content of the login.post.request file using the cat command.
    <img src="https://i.imgur.com/1Tizrtx.png" height="400px" width="auto" alt="Preparing SQLmap"/>

### Part 05: Enumerating Databases and Tables with SQLmap
**Task**: Use SQLmap to enumerate databases, tables, and dump sensitive data from the targeted tables.
- **Steps**:
    1. Use SQLmap to enumerate all databases on the server using the saved request file.
    2. Focus on extracting data from specific tables, such as credit card information.
- **Slide 05**: Screenshot showing SQLmap output with enumerated databases, tables, and extracted data.
    <img src="https://i.imgur.com/tCC6BSd.png" height="400px" width="auto" alt="Enumerating Databases with SQLmap"/>

### Part 06: Advanced Data Extraction and Verification
**Objective**: Execute advanced data extraction using `sqlmap` to retrieve sensitive information such as credit card details from the database, and then verify the content using the `cat` command in the terminal.

- **Steps**:
    1. Use `sqlmap` with the previously created `login.post.request` file to enumerate databases and tables, focusing on extracting data from the `credit_cards` table.
    2. Execute the command `sqlmap -r /login.post.request -D [database_name] -T credit_cards --dump` to dump the contents of the targeted table.
    3. After extraction, the data will be typically stored in a CSV file or similar format within the sqlmap output directory. Use the `cat` command or an equivalent command to display the contents of this file.
    4. Capture the entire terminal session showing the `sqlmap` command execution, its output, and the subsequent use of the `cat` command displaying the sensitive data.

- **Expected Outcome**: 
    - A screenshot capturing the terminal window with the complete `sqlmap` process, commands used, and the output, especially showing the use of the `cat` command to display extracted sensitive data such as credit card details. This should include the enumeration of the `credit_cards` table and the display of its contents, focusing on the sensitive data.

**Slide 06**: Screenshot showing the use of cat command showing the details of the credit card in the terminal

<img src="https://i.imgur.com/b5TzUbF.png" height="400px" width="auto" alt="Advanced Enumeration with SQLmap"/>

### Part 07: Challenge - Finding Hidden Products in OWASP Juice Shop
**Task**: Find and order hidden products using SQL injection in the OWASP Juice Shop.
- **Steps**:
    1. Navigate to OWASP Juice Shop and manipulate the search query to reveal hidden products.
    2. Place an order for one of the revealed products, such as the Christmas Super-Surprise-Box.
- **Slide 07**: Screenshot showing the order confirmation for a hidden product.
    <img src="https://i.imgur.com/lbx3P2T.png" height="400px" width="auto" alt="Finding Hidden Products in OWASP Juice Shop"/>


**Conclusion**: LAB 07 equips students with an understanding of SQL injection attacks and hands-on experience in exploiting these vulnerabilities. Through a series of tasks, students learn to identify, exploit, and mitigate such vulnerabilities, emphasizing the importance of secure coding practices and database security measures.
