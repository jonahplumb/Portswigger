# SQL Injection Practitioner All Labs

# Lab 1: SQL injection UNION attack, determining the number of columns returned by the query
This lab contains an SQL injection vulnerability in the product category filter. <br>
The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. <br>
The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack. <br>
To solve the lab, determine the number of columns returned by the query by performing an SQL injection UNION attack that returns an additional row containing null values. <br>

## Solution
The description gives the clue to use UNION to determine the number of columns, and that will display the flag. <br>
Intercept a request on burp with the product category filter. Change the category to `'+union+select+NULL--`. <br>
This will return an internal server error.

![request](./Lab1/request.PNG) <br>
![error](./Lab1/error.PNG) <br>

To solve, continue adding NULL values to the end of `'+union+select+NULL,NULL......--` until there is no error returned. <br>
The total amount is 3, `'+union+select+NULL,NULL,NULL--`. <br>
Returned you will see your command used as the header and the lab is solved. <br>
![solved](./Lab1/solved.PNG) <br>

<br />
<br />
<br />
<br />

# Lab 2:


