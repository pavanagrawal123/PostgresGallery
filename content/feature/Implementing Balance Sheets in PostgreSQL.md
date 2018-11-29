|Implementing Balance Sheets in PostgreSQL|November 28, 2018  |
|--|--|

### Example
| Date | Title | Credit (+) | Debit (-) | Balance | 
|--|--|--|--|--|
| 2018-10-31 | Halloween Candy |  | 30 | -30 |
| 2018-11-30 | Salary and Tax | 4000 | 200 | 3770 |
| 2018-12-01 | Christmas Tree |  | 200 | 3570 |

### Description
Using balance sheets is a great way to keep track of assets and liabilities for both personal and business reasons. Spreadsheet software may be a good choice since it is simpler to access previous rows; however, this document entails the process of building a balance sheet in PostgreSQL in a simple manner. In this real-life example shown above, it is easy to interpret what the person has bought or where they have lost money and where they have gained money.

### Code
```sql
CREATE TABLE public."BalanceSheet"
             (
                          "Date"       Date,
				 		  "Title"      Text,
                          "Credit (+)" NUMERIC,
                          "Debit (-)"  NUMERIC,
                          "Balance"    NUMERIC
             );
INSERT INTO "BalanceSheet"
            (
                        "Date",
                        "Title",
                        "Credit (+)",
                        "Debit (-)",
                        "Balance"
            )
            VALUES
            (
                        '2018-10-31',
                        'Halloween Candy',
                        0,
                        30,
                        0
            )
            ,
            (
                        '2018-11-30',
                        'Salary and Tax',
                        4000,
                        200,
                        0
            )
            ,
            (
                        '2018-12-02',
                        'Christmas Tree',
                        0,
                        200,
                        0
            );

WITH tt
     AS (SELECT a."Date",
                Sum(b."Credit (+)" - b."Debit (-)") Running_Total
         FROM   "BalanceSheet" a,
                "BalanceSheet" b
         WHERE  ( b."Date" <= a."Date" )
         GROUP  BY 1
         ORDER  BY 1)
UPDATE "BalanceSheet"
SET    "Balance" = tt.running_total
FROM   tt
WHERE  tt."Date" = "BalanceSheet"."Date";

SELECT *
FROM   PUBLIC."BalanceSheet"
ORDER  BY "Date" ASC; 
```
### Code Breakdown and Explanation
*BalanceSheet* contains columns for date, title, credit, debit, and balance. This makes it easy to view and understand the table's contents.

*tt* is a temporary table used to calculate *running_total* of all of the previous entries' separate balances until the current entry.
>`Sum` is used to calculate this by subtracting the *Debits (-)* (money owed) from the *Credit (+)* (money gained) each month.

>`GROUP BY` selects the data for aggregation (*running_total*).

>`ORDER BY` sorts the data by *Date* so an accurate balance is calculated.

>`WHERE` makes sure the *Balance* is only updated for the correct entry.

Finally, the table is sorted by *Date* for easier interpretation using `ORDER BY`.
