---
title: "Averaging using Pivot Tables"
Date: "2018-11-20"
---


### Description
Sometimes, companies need to average multiple pieces of data together in a meaningful way. Enter the pivot table - this allows one to summarise an extensive database in a simple, grouped way. When creating averages, companies may deal with many, many pieces of data in a database; hence, a pivot table can allow one to continuously calculate statistics and averages as data enters, making it a flexible solution. Here's how it works: 

### Code
We could input some data for a transaction ID along with some dates:

{{< highlight sql  >}}
insert into DailyTransactions values ('CARL', 'MON', 100)
insert into DailyTransactions values ('ANNA', 'MON', 100)
insert into DailyTransactions values ('CARL', 'MON', 1200)
insert into DailyTransactions values ('ANNA', 'MON', 900)
insert into DailyTransactions values ('BOB', 'MON', 400)
insert into DailyTransactions values ('CARL', 'MON', 500)
insert into DailyTransactions values ('BOB', 'MON', 200)
{{< / highlight >}}

After several pieces of data have been inputted, we can make a pivot table from it:

{{< highlight sql  >}}
SELECT * FROM DailyTransactions
pivot (avg (TransactionAmount) for Day in ([MON])) as AvgTransactionsPerDay
{{< / highlight >}}

### Code Breakdown and Explanation
Here, the user would select all the information from the daily transactions table. Then, by using the pivot function, they would be able to organise it into a pivot table which clearly displays only the average transactions per day to the user, by organising per day.
The sample output would look something like this:

```
TransacID  MON         
---------- ----------- 
ANNA       500         


BOB        300          


CARL       600          
```

In conclusion, using Pivot Tables in SQL queries makes them far more efficient, especially when using them in organising income/monetary data.

