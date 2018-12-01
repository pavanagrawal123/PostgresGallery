---
title: "Averaging using Pivot Tables"
Date: "2018-11-20"
---


### Description
Sometimes, companies need to average multiple pieces of data together in a meaningful way. Enter the pivot table - this allows one to summarise an extensive database in a simple, grouped way. When creating averages, companies may deal with many, many pieces of data in a database; hence, a pivot table can allow one to continuously calculate statistics and averages as data enters, making it a flexible solution. Here's how it works: 

### Code
Here we have an existing SQL table called `DailyTransactions`, which displays all transactions and the day they occurred:

```
TransacID  AMOUNT      DAY    
---------- ----------- ----------- 
CARL       100         MON


ANNA       100         TUE


CARL       1200        MON


ANNA       900         MON


BOB        400         TUE  


CARL       500         TUE


BOB        200         MON
```

After several pieces of data have been inputted, we can make a pivot table from it, which calculates the sums of each person's transaction:

{{< highlight sql  >}}
SELECT
  mon.transacid as TransacId,
  MON,
  TUE
FROM (
  SELECT
    transacid,
    SUM(amount) AS MON
  FROM dailytransactions
  WHERE day='MON' GROUP BY transacid
) as mon,
(
  SELECT
    transacid,
    SUM(amount) AS TUE
  FROM dailytransactions
  WHERE day='TUE' GROUP BY transacid
) as tue
WHERE mon.transacid = tue.transacid;
{{< / highlight >}}

### Code Breakdown and Explanation
Here, the user would select all the information from the daily transactions table. Then, they would be able to organise it into a pivot table which clearly displays the sum of transactions per day to the user, by organising per person. The sample output would look something like this:

```
 transacid | mon  | tue 
-----------+------+-----
 ANNA      |  900 | 100
 BOB       |  200 | 400
 CARL      | 1300 | 500
```

In conclusion, using Pivot Tables in SQL queries makes them far more efficient, especially when using them in organising income/monetary data.

