|Date|Profit ($)|Loss ($)|Monthly Earnings ($)|Total ($)|
|----|----------|--------|--------------------|---------|
|"2018-01-28"|576|543|33|33|
|"2018-02-28"|675|521|154|187|
|"2018-03-28"|432|653|-221|-34|
|"2018-04-28"|765|321|444|410|


### Description
Creating a table on a SQL server can help you in a variety of sectors.
Let’s say we wanna create and share our financial conditions depicted through a table to someone far away from us, but don’t want to fuss over the work of making a copy of the file and sending it through an e-mail. We can just create the same table in Postgresql which will automatically update the data on it to a public server, which can be accessed easily by anyone with the server name and password.
It also makes it easier for people to add the values and then have them automatically calculated through a press of a button
It can even help us to share our server with a large group of people. This makes our work even more clean and quick.

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

The `Lag` function then creates a new column from the values of the “Monthly Earnings ($)” column just placing them row before.

It finally `SETS` the value of the “Total” column by adding the previous row values (Calculated through `LAG` function) with the `“Monthly Earnings ($)”` column.
