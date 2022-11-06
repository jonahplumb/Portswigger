# Information Disclosure Apprentice All Labs

## Lab 1: Information disclosure in error messages
This lab's verbose error messages reveal that it is using a vulnerable version of a third-party framework. <br>
To solve the lab, obtain and submit the version number of this framework. <br>

## Solution
When we naviagte the the lab website `https://0a570011035dfb07c0de9d22003000e8.web-security-academy.net/` <br>
we find no ways for an end user to input data and force an error. I intially turned analyzing the url. <br>
If we click on a product we can see the url changes to `https://0a570011035dfb07c0de9d22003000e8.web-security-academy.net/product?productId=2` <br>
From here if we change the product id to an id that can't be found like 200 or 2000, we still don't recieve a verbose error message 
like the labs description, so we need to try feeding the product id other data types, if we feed the product id a string, we get the following error message. <br>
`https://0a570011035dfb07c0de9d22003000e8.web-security-academy.net/product?productId='string'` <br>
![error](./Lab1/lab-1-error-message.PNG) <br>

At the bottom of the error message we can see `Apache Struts 2 2.3.31`, if you do some quick research you'll find <br>
that this is the vulnerable version that the lab is looking for, and is also our flag. 
<br />
<br />
<br />
<br />

## Lab 2: Information disclosure on debug page
This lab contains a debug page that discloses sensitive information about the application. To solve the lab, obtain and submit the `SECRET_KEY` environment variable.

## Solution
Navigate to the lab site `https://0a620043046fcbe1c018e19c0028005c.web-security-academy.net/` <br>
and you want to capture your traffic using Burp, after capturing going to the homepage in Burp. <br>
Go to the target tab, and you'll notice a file called `phpinfo.php`, click on this file and send it to the repeater <br> within Burp. <br>
![target](./Lab2/target.PNG) <br>

If we send the request in the response we can search the files code using the search bar <br>
in the bottom of the repeater tab in Burp. If we search for `secret` this will reveal the `SECRET_KEY` value that we are looking for. <br>
![burp-flag](./Lab2/burp-flag.PNG) <br>

Alternatively you could navigate to the url `https://0a620043046fcbe1c018e19c0028005c.web-security-academy.net/cgi-bin/phpinfo.php` and CTRL + F and search for `secret` on the page to find the `SECRET_KEY`. <br>
![source-code](./Lab2/source-code-flag.PNG)
`SECRET_KEY` = `bafphsvrjifqvyp7gtpryo5zh6qj1xsk`
<br />
<br />
<br />
<br />

## Lab 3: Source code disclosure via backup files
This lab leaks its source code via backup files in a hidden directory. To solve the lab, identify and submit the database password, which is hard-coded in the leaked source code.

## Solution
Add `/robots.txt` to the url, this will reveal a new directory backup, which is exactly what we're looking for. <br>
Replace `/robots.txt` with `/backup` revealing a productemplate file. <br>
![template](./Lab3/template.PNG) <br>
Click the hyperlink to the product template taking you to `/backup/ProductTemplate.java.bak`
In this file we're looking for a database password, which is hardcoded in the `readObject` method. <br>
![password](./Lab3/password.PNG)
