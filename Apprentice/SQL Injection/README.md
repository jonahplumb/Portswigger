# SQL Injection Apprentice All Labs

# Lab 1: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
This lab contains an SQL injection vulnerability in the product category filter. <br>
When the user selects a category, the application carries out an SQL query like the following: <br>
`SELECT * FROM products WHERE category = 'Gifts' AND released = 1` <br>
To solve the lab, perform an SQL injection attack that causes the application to display details of all products in any category, 
both released and unreleased.

## Solution
Want to intercept applying the product category filter within burp. Send the request to the repeater.
![repeater-get](./Lab1/repeater-get.PNG) <br>
In the repeater change the category parameter to `'+OR+1=1--`, originally 12 results, after our injection,
this reveals 20 total, 8 unreleased products. Will also see your sql injection command as the pages title.
![flag](./Lab1/command-solve.PNG) <br>

<br />
<br />
<br />
<br />

# Lab 2: SQL injection vulnerability allowing login bypass
This lab contains an SQL injection vulnerability in the login function. <br>
To solve the lab, perform an SQL injection attack that logs in to the application as the `administrator` user. <br>

## Solution
The goal is to login as the user `administrator` so the initial target is the login request. Intercepting the login request
looks like this. <br>
![get-request.PNG](./Lab2/get-request.PNG) <br>
The value we want to feed the `username` parameter is `administrator'--`. <br>
![username-value.PNG](./Lab2/username-value.PNG) <br>
This is a very simple SQL injection attack where we are specifying our username as `administrator`, then a single quote 
to specify the end of the string, and the `--` to comment out everything after the username to bypass the system checking our password. Send the modified request through and the login as `administrator` was successful. <br>
![solved.PNG](./Lab2/solved.PNG) <br>













