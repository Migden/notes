2025-05-12 08:06

##### Learning Covered:
- What is UNION?
- What is UNION Based SQLi
--------------------------
Tags: [[SQL]], 


### UNION-Based Payloads
--------------------------------
Whenever your dealing with in-band SQLi and the results of the query are displayed in some way, we should test for UNION-Based SQLi

The UNION keyword aids exploitation because it enables the execution of an extra SELECT statement and provides the results in the same query, thus practically combining two queries into one statement and result.

In order for UNION-based payloads to work, we need to satisfy two conditions:

- The UNION query has to include the same number of columns as the original query would return
- The data types need to be compatible between each column

We can test for the first criteria utilising the `ORDER BY` command, injecting the command `ORDER BY 1;-- ` will return results if the amount of data being return in 1 column. So just repeat this feature until it is successful.
### References:




