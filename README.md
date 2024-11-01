## REG.NO:212222110050
## NAME:SWETHA N
# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/user-attachments/assets/a3a8cc58-5694-4a97-b372-9de946b2ec38)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/user-attachments/assets/ab3b60ee-e7be-4796-9efc-d6029cf1461a)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/user-attachments/assets/96765630-9946-4443-b752-516af04bbf51)

Click on the menu Login/Register and register for an account

![image](https://github.com/user-attachments/assets/834af271-54bb-4ed7-ba91-d1c47530677e)

Click on the link “Please register here”

![image](https://github.com/user-attachments/assets/5400a7a8-13d7-4582-957b-eb9fff5665f8)

Click on “Create Account” to display the following page:

![image](https://github.com/user-attachments/assets/3bc08e6f-b73c-4ca3-8703-beaa17f260b1)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/user-attachments/assets/76731fe3-de06-4ddb-9bfc-0e56d7f9d871)

Click “Login”. The logged in page will show as below:

![image](https://github.com/user-attachments/assets/f263292e-f65a-4e34-9e2e-6c3161d02241)

##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.


![image](https://github.com/user-attachments/assets/472f91dd-4c26-4f17-8417-bf42ec450713)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/user-attachments/assets/194841d3-ca6e-445d-bef5-ac8bc0555e20)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/user-attachments/assets/d4157047-f8e9-4d78-9a70-d5449a3f55f6)

## Union-based SQL injection:

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
![image](https://github.com/user-attachments/assets/69b0d5a8-9800-46d0-a28f-dc895cabeaeb)

![image](https://github.com/user-attachments/assets/48f1ea3c-75e2-4acb-ad5c-f4e82b815c23)

![image](https://github.com/user-attachments/assets/dd8511d4-99a9-4182-bf9a-999c31f53f45)

![image](https://github.com/user-attachments/assets/33d6cdc0-4f8e-4da3-a4e3-9eb1ffdc7f4d)

![image](https://github.com/user-attachments/assets/60f4c3f2-12eb-46db-9050-b65d7ce29825)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/user-attachments/assets/9ba8620d-3900-441b-9991-43e08b234227)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

![image](https://github.com/user-attachments/assets/368bdd83-ec61-47d6-a6f1-b22dbd3044c5)

After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/user-attachments/assets/aa78ace8-cb59-4672-ac6d-874fb0423e87)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/user-attachments/assets/9acf5784-ac88-4bf0-ab2e-f55818c17bb4)

![image](https://github.com/user-attachments/assets/faebb70e-2fc8-4082-9cdf-d41c290fb91f)

As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/user-attachments/assets/66b3be07-78a9-49e2-b843-bf628ab3b1db)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![image](https://github.com/user-attachments/assets/fb8b65cc-4523-40b5-932b-e8563d0ec77e)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/user-attachments/assets/93311949-0285-4971-8ff6-5af2e1212ab5)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

![image](https://github.com/user-attachments/assets/774f6934-a3eb-44c3-b1ad-074add5e3b28)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

![image](https://github.com/user-attachments/assets/5754c8c2-f671-4b95-8365-e56d14b740bb)


![image](https://github.com/user-attachments/assets/87593e04-ce99-4d4a-ad72-e0cff7880fee)

Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

![image](https://github.com/user-attachments/assets/7ac115ad-0762-4767-90d4-90f283f8e421)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
