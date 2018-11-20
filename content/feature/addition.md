---
title: "Transaction Management/Processing"
Date: "2018-11-20"
---


### Description
Sometimes, companies need to manage several thousands of inputs per second, using a database - we usually wouldn't consider that a normal use of SQL. However, banks often use the latter to handle transaction management efficiently.

SQL is the perfect language to use for such a task, as it combines both Data Integrity with the ability to directly support transaction processing - this means that data is safe, secure and validated, but multiple safety measures are in place as well, should an operation fail. Transaction processing ensures that if one process in a banking system should fail, the whole operation will stop, preventing the company/user from incurring losses. Here is how it works:

### Code
{{< highlight sql  >}}
DELETE FROM money WHERE COST = 20000;
COMMIT;
ROLLBACK;
{{< / highlight >}}

### Code Breakdown and Explanation
Transaction management works on the key principle that actions can be rolled back. The first line, DELETE FROM money WHERE COST = 20000; , simply means that records where the cost is equal to 20000 will be deleted from the database - however, the ROLLBACK command that follows it ensures that if an error is encountered during such a process, the query can be undone. This prevents disastrous consequences in terms of bank management. 
