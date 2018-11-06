|BALANCE SHEET IMPLEMENTATION|Date|
|----------------------------|----|

|Profit ($)| Loss ($)|Monthly Earnings ($)|Total ($)||
|-------|---------|---------|--------|----|
|576|543|33|33|2018-01-28|
|675|521|154|187|2018-02-28|
|432|653|-221|-34|2018-03-28|
|765|321|444|410|2018-04-28|


### Description
PostgreSQL offers many a ways to help people communicate through their work to a large scale of people. It provides quick editing and sharing on a large scale.
The following code scripted in SQL can help create a dynamic workflow table for users who want to depict their financial conditions as different as it may through a table. It helps calculate a monthly earning or perhaps the gain in the share market. Combined with PostgreSQL, it reduces the effort of making the work public. 

### Code
CREATE TABLE table1 (“Date” date, “Profit ($)” integer, “Loss ($)” integer, “Monthly Earnings ($)” integer);

INSERT INTO public.table1 (
	"Date", "Profit ($)", "Loss ($)", "Monthly Earnings ($)", "Total")
	VALUES ('2018-01-28', 576, 543, 0, 0),
     ('2018-02-28', 675, 521, 0, 0),
     ('2018-03-28', 432, 653, 0, 0), 
     ('2018-04-28', 765, 321, 0, 0);

UPDATE public.table1
	SET "Monthly Earnings ($)"="Profit ($)"-"Loss ($)", 
"Total"= (SELECT LAG ("Monthly Earnings ($)”, 1, 0) OVER (ORDER BY "Monthly Earnings ($)")) +"Monthly Earnings ($)";


### Code Breakdown and Explanation
The `UPDATE` statement updates the values of the “Monthly Earnings ($)” column by subtracting the values of the “Loss ($)” column from the “Profit ($)” one.

The `LAG()` function has the ability to access data from the coresponding previous rows, it uses it's functionality to create a new column from that data and fills it into the "Total" column.

It finally `UPDATES` the value of the “Total” column by adding the previous row values (Calculated through `LAG` function) with the “Monthly Earnings ($)” column. So as to total up all the previous values for each row.
