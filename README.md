# WCCI BWAPP Exercise 1

[BWAPP](http://www.itsecgames.com/index.htm) is an intentionally buggy web application that helps students learn about web vulnerabilites. While these vulnerabilities are quite old this application is a great way to discover common web vulnerabilites. 

## Requirements

- Docker
- Docker Compose

## Instructions (Local)

1. Clone this Repo: `git clone `
2. Navigate into this folder: `cd BWAPP-Exercise`
3. Start the Docker Container: `docker compose up -d'
4. Open a web browser and navigate to http://localhost:80/install.php.
5. Click the "here" link to instapp bWAPP
6. Once the installation is complete, click the "Login" button.
7. Login with the following credentials:
    - Username: `bee`
    - Passsword: `bug`
8. Select the vulnerability you'd like to exploit and click "Hack"

## In-Class Exercise

Let's exploit an SQL Injection Vulnerability.
1. From the bWAPP Bug Selection page, please select "SQL Injection (GET/Search)" and then click "Hack".
2. Once the page loads we can begin to perform the exploit. 
3. Let's first examine the behavior of the page. Input "Iron Man" into the test field and click "Search".
4. One way to detect a SQL Injection vulnerability is to input a single quote into the the text field. Type "'" into the text field and examine the output. Notice the error message! The output is an error message directly from the backend.
**Note**: The SQL Commannd that was performed "SELECT * FROM movies WHERE title LIKE ‘%’%’"
5. One thing we can do to bypass this error is add a " #" to the end of our query to ignore everything after. In the search field type the following: "' #". Notice the behavior now? It outputs everything in the Movies table. 
6. Let's begin to exploit the db. First let's determine how many rows are in the table. We can do this by using the Order By clause. The Order By clause will sort the table by the selected row. We should see an error, when we get the the max number of rows.
    1. Run the following command and find the maximum number of rows: "iron' order by `insert_row-number_here` #"
    2. How many rows are in this table? 
7. Next we need to figure out which columns are shown on the page. We can do this using the union clause. Run the following command and examine the output: "iron' union select 1,2,3,4,5,6,7 #"
8. Now let's get some additional information about the database. Input the following command and examine the output: "iron' union select 1,user(),database(),version(),5,6,7 #"
    1. What is the SQL User?
    2. What is the Version of SQL that is running?
    3. What is the name of the DB?
9. Let's see if there's a user table that we can extract some data from: "iron' union select 1,login,password,email,5,6,7 from users #"
    1. What users exist?
    2. Notice the passwords are stored as hashes? Can you crack the hashes and provide the plain-text passwords?

## Independent Exercise: 
- Select one of the vulnerabilities from the [bWAPP tutorial page](https://wooly6bear.wordpress.com/wp-content/uploads/2016/01/bwapp-tutorial.pdf) and perform the exploit. After you have performed it, research the vulnerability and the steps you performed and answer the following questions:
    1. What was the vulnerability?
    2. Can you please explain how the vulnerability works and provide the OWASP Information Page?
    3. Please walk us through the steps of the exploit and explain what is happening.
    4. What steps can you take to avoid this vulnerability?

## Resources
[bWAPP Main Page](http://www.itsecgames.com/index.htm)
[bWAPP Tutorials](https://wooly6bear.wordpress.com/wp-content/uploads/2016/01/bwapp-tutorial.pdf)
[SQL Union Clause](https://www.w3schools.com/sql/sql_union.asp)
[SQL Order By Clause](https://www.w3schools.com/sql/sql_orderby.asp)