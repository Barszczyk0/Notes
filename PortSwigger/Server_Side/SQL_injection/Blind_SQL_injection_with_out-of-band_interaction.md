# Blind SQL injection with out-of-band interaction
# Objective
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.\
\
The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain.\
\
To solve the lab, exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator.
# Solution
This lab requires Professional edition of Burp Suite.


