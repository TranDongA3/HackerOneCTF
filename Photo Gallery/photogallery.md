# Photo Gallery Challenge Writeup

## Introduction

This challenge involves SQL injection and command injection vulnerabilities.

![alt text](image.png)

## Flag 1: SQL Injection

1. Navigate to the view page.

![alt text](image-1.png)

The app fetches data from the backend.

2. Use BurpSuite to intercept requests.

![alt text](image-2.png)

3. Test for SQL injection and observe responses.

![alt text](image-3.png)

4. Use sqlmap to dump the database.

![alt text](image-4.png)
![alt text](image-5.png)

## Flag 2: Union-Based SQL Injection

1. Unable to find exploitation method initially, so check the hint.

![alt text](image-6.png)

Hint: "This is the third hint."

2. Search online for similar structures.

![alt text](image-7.png)

Resembles Docker image structure.

3. Modify the query accordingly.

![alt text](image-8.png)

## Flag 3: Command Injection

1. Review the code.

![alt text](image-9.png)

Uses `subprocess.check_output` to join files/filenames for usage calculation – vulnerable to OS command injection.

2. Inject stacked queries:

   ```
   fetch?id=3; UPDATE photos SET filename=";echo $(ls)" WHERE id=3; commit;
   ```

3. No flag visible.

![alt text](image-10.png)

4. Hint: "Be aware of your environment."
   - Search for Linux environment variables: https://www.cyberciti.biz/faq/linux-list-all-environment-variables-env-command/
   - `printenv` shows all environment variables.

5. Updated payload:
   ```
   fetch?id=3; UPDATE photos SET filename=";echo $(printenv)" WHERE id=3; commit;
   ```

![alt text](image-11.png)
